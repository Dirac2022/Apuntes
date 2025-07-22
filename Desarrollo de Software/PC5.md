**Proyecto 16: Adaptador de invocación de comandos entre contenedores y host**

- **Cubierto:** `docker exec`, `kubectl exec`, espacios de nombres, adaptadores, E2E .
    
- **Faltan:**
    
    - **Autenticación** de usuario en contenedores (exec como un usuario específico)
    - **TLS** y conexiones seguras
    - **Logging** centralizado de outputs
    - **Integración** con CI para pruebas automáticas
    - **Gestión de permisos** (RBAC en K8s)

* Integración con CI para pruebas automáticas (1 Yoel)
* Autenticación de usuario en contenedores (exec como un usuario específico) (2 Mitchel)
* Logging centralizado de outputs (3 Mitchel)
* Gestión de permisos (RBAC en K8s) (4 Yoel)
* TLS y conexiones seguras (5 Mitchel)

---

### **Autenticación** de usuario en contenedores (exec como un usuario específico)

El Dockerfile debe quedar así:

```Dockerfile
FROM ubuntu:22.04

RUN apt-get update && apt-get install -y iputils-ping
# Aqui estamsos creando un usuario llamado dirac he incluimos un directorio home y con -s /bin/bash/bah estamos especificando el shell que se usara cuando el usuario inice sesión
RUN useradd -ms /bin/bash dirac

# Ahora cambiamos el usuario actual del contenedor a dirac
USER dirac

CMD ["tail", "-f", "/dev/null"]
```

Construir la imagen

```sh
docker build -t dirac/simple-app:1.6.0 ./simple-app
```

Correr un contenedor a partir de la imagen:

```sh
docker run -d --name <nombre-conteneodr> <imagen>
```


Para ejecutar comandos dentro del contenedor y ver el usuario:

```sh
docker exec -it <contenedor> sh
```

Dentro podemos escribir

```sh
whoami
```

Y nos saldrá el usuario `dirac`. Si por ejemplo queremos crear un archivo en una carpeta restringida como `/etc`

```sh
touch etc/test.txt
```

Saldrá permiso denegado.


### **Logging** centralizado de outputs

El archivo `container_exec.py` debe quedar así:

```python
import subprocess
import sys
import argparse
import configparser
from pathlib import Path # Agrega esto
import logging # Agrega esto


log_path = Path("logs-centralizado.log") # Agrega esto

logging.basicConfig(filename=log_path, encoding='utf-8', level=logging.DEBUG)

def cargar_aliases(config_file="config.ini") -> dict:
    """
    Carga los alias desde un archivo de configuracion .ini.
    Devuelve un diccionario con los alias.
    """
    config = configparser.ConfigParser()
    if not config.read(config_file):
        return {}

    return dict(config.items('aliases'))


def listar_contenedores() -> list[str]:
    """
    Lista los contenedores docker en ejecucion usando docker ps
    retorna el id imagen por cada contenedor
    """
    comando = ["docker", "ps", "--format", "{{.ID}}: {{.Image}} - {{.Names}}"]
    resultado = subprocess.run(comando, stdout=subprocess.PIPE, stderr=subprocess.PIPE, text=True) # Agrega stderr=subprocess.PIPE
    contenedores: list[str] = resultado.stdout.strip().split("\n")

    if not contenedores or contenedores == ['']:
        print("No hay contenedores en ejecucion.")
        sys.exit(0)
    # AGERGA DESDE AQUI
    logging.info("Listando contenedores:")
    if resultado.stdout:
        logging.debug(f"std:\n{resultado.stdout}")
    if resultado.stderr:
        logging.error(f"stderr:\n{resultado.stderr}")
    # HASTA AQUI
    return contenedores
    # print("\nContenedores activos:")
    # for i, cont in enumerate(contenedores):
    #     print(f"{i + 1}. {cont}")
    # return contenedores


def listar_pods(namespace: str | None) -> list[str]:
    """
    Lista pods en Kubernetes
    en ejecucion y los imprime
    """
    comando = ["kubectl", "get", "pods", "-o", "custom-columns=NAME:.metadata.name"]
    if namespace:
        comando.extend(["-n", namespace])
    resultado = subprocess.run(comando, stdout=subprocess.PIPE, stderr=subprocess.PIPE, text=True, check=True) # AGREGA stderr=subprocess.PIPE
    pods = resultado.stdout.strip().splitlines()[1:]
    if not pods:
        print("No hay pods en el namespace actual.")
        sys.exit(0)
    # AGREGA DESDE AQUI
    logging.info("Listando pods:")
    if resultado.stdout:
        logging.debug(f"std:\n{resultado.stdout}")
    if resultado.stderr:
        logging.error(f"std:\n{resultado.stderr}")
    # HASTA AQUI
    return pods


def ejecutar_comando_docker(contenedor_id: str, comando: list[str]) -> None:
    """
    Ejecuta comando arbitrario dentro del contenedor docker.
    Se toma el id o nombre del contenedor del docker, y el comando
    a ejecutar.
    """
    resultado = subprocess.run(
        ["docker", "exec", contenedor_id] + comando,
        stdout=subprocess.PIPE,
        stderr=subprocess.PIPE,
        text=True
    )
    print("\nSalida estandar:")
    print(resultado.stdout)
    print("Errores:")
    print(resultado.stderr)
    # AGREGA DESDE AQUI
    logging.info(f"Ejecución Comando dentro de Docker. Contenedor: {contenedor_id}. Comando: {' '.join(comando)}")
    if resultado.stdout:
        logging.debug(f"std:\n{resultado.stdout}")
    if resultado.stderr:
        logging.error(f"stderr:\n{resultado.stderr}")
    # HASTA AQUI


def seleccionar_pod(pods: list[str]) -> str:
    """
    Solicita al usuario que seleccione un pod por número.
    Devuelve el nombre del pod.
    """
    while True:
        entrada = input("\nSelecciona un pod (numero): ").strip()
        if entrada.isdigit():
            idx = int(entrada) - 1
            if 0 <= idx < len(pods):
                return pods[idx]
        print(f"'{entrada}' no es un numero valido, intentarlo de nuevo")


def ejecutar_comando_k8s(pod: str, namespace: str | None, comando: list[str]) -> None:
    """
    Ejecuta comando arbitrario dentro de un pod de Kubernetes.
    usando flags para interactuar en bash
    """
    cmd_base = ["kubectl", "exec"]
    if namespace:
        cmd_base.extend(["-n", namespace])
    flags = ["-i", "-t"] if comando and comando[0] in ("bash", "sh") else []
    cmd = cmd_base + flags + [pod, "--"] + comando
    resultado = subprocess.run(
        cmd, 
        # stdin=sys.stdin, 
        stdout=subprocess.PIPE, 
        stderr=subprocess.PIPE,
        text=True) # ELIMINA stdin=sys, AGREGA stdout=subprocess.PIPE, stderr=subprocess.PIPE y text=TRUE
    print("\nSalida estandar:")
    print(resultado.stdout)
    print("Errores:")
    print(resultado.stderr)
    # AGREGA DESDE AQUI
    logging.info(f"Ejecución Comando dentro de Minikube. Pod: {pod}. Comando: {' '.join(comando)}")
    if resultado.stdout:
        logging.debug(f"std:\n{resultado.stdout}")
    if resultado.stderr:
        logging.error(f"stderr:\n{resultado.stderr}")
    # HASTA AQUI



def seleccionar_recurso(recursos: list[str], tipo_recurso: str) -> str:
    """
    Mostarmos una lista numerada de recursos (contenedores en docker o pods en kubernetes).
    Y devolvemos el nombre del recurso seleccionado por el usuario.
    """
    print(f"Recursos '{tipo_recurso}' disponibles:")
    for i, recurso in enumerate(recursos, 1):
        print(f"{i}. {recurso}")

    while True:
        try:
            indice = int(input(f"Selecciona un {tipo_recurso} por número: ")) - 1
            if 0 <= indice < len(recursos):
                if tipo_recurso == "contenedor":
                    return recursos[indice].split(":")[0] # Para contenedores
                return recursos[indice] # Para pods
        except ValueError:
            print("Entrada inválida. Introduce un número") 


def manejar_docker(aliases: dict):
    """
    Para manejar ejecucion de comandos en Docker.
    Soporte para alias
    """
    recursos = listar_contenedores()
    if not recursos:
        return # Termina ejecución si no hay recursos
    recurso_id = seleccionar_recurso(recursos, "contenedor")
    comando_str = input(f"\nComando o alias a ejecutar en el contenedor {recurso_id}: ").strip()
    if not comando_str:
        print("No se ingreso ningun comando")
        return
    comando_final_str = aliases.get(comando_str, comando_str)
    if comando_final_str != comando_str:
        print(f"Ejecutando alias: '{comando_str}': '{comando_final_str}'\n")
    ejecutar_comando_docker(recurso_id, comando_final_str.split())


def manejar_kubernetes(namespace: str | None, aliases: dict):
    """
    Para manejar ejecucion de comandos en Kubernetes.
    Soporte para alias
    """
    recursos = listar_pods(namespace)
    if not recursos:
        return
    recurso = seleccionar_recurso(recursos, "pod")
    comando_str = input(f"\nComando o alias a ejecutar en el pod {recurso}: ")
    if not comando_str:
        print("No se ingreso ningun comando")
        return
    comando_final_str = aliases.get(comando_str, comando_str)
    if comando_final_str != comando_str:
        print(f"Ejecutando alias: '{comando_str}': '{comando_final_str}'\n")
    ejecutar_comando_k8s(recurso, namespace, comando_final_str.split())


def main():
    """
    Funcion principal que parsea los argumentos y dirige el flujo del programa.
    """
    pars = argparse.ArgumentParser(
        description="Ejecuta comandos en Docker o Kubernetes"
    )
    pars.add_argument(
        "--platform", "-p",
        choices=["docker", "k8s"],
        default="docker",
        help="Plataforma: docker (por defecto) o k8s"
    )

    pars.add_argument(
        "--namespace", "-n",
        help="Especifica el namespace de Kubernetes a utilizar. (Solo para la plataforma k8s)"
    )

    args = pars.parse_args()

    aliases = cargar_aliases()

    if args.platform == "docker":
        # conts = listar_contenedores()
        # cid = seleccionar_contenedor(conts)
        # cmd = input("\nEscribe el comando a ejecutar dentro del contenedor: ").strip().split()
        # ejecutar_comando_docker(cid, cmd)
        manejar_docker(aliases)
    elif args.platform == "k8s":
        manejar_kubernetes(args.namespace, aliases)
    # else:
    #     pods = listar_pods(args.na)
    #     pod = seleccionar_pod(pods)
    #     cmd = input("\nEscribe el comando a ejecutar dentro del pod: ").strip().split()
    #     ejecutar_comando_k8s(pod, cmd)
    

if __name__ == "__main__":
    main()
```



### **TLS** y conexiones seguras

Crear el directorio de trabajo

```sh
$ mkdir -p ~/docker-tls
$ ~/docker-tls
```

#### Crear la CA 
Creamos la Autoridad certificadora, aquí vamos a generar una clave privada RSA de 4096 bits cifrada mediante AES-256 longitud de 256
  

```sh
$ openssl genrsa -aes256 -out ca-key.pem 4096
```

Crear certificado publico para la CA
Creamos un certificado auto firmado valido para un año. Este certificado será usado para firmar certificados del servidor y del cliente.

```sh
$ openssl req -new -x509 -days 365 -key ca-key.pem -sha256 -out ca.pem
```

#### Generar certificado para el servidor

```sh
$ openssl genrsa -out server-key.pem 4096
```
  

Crear CSR `hostname=127.0.0.1`
Creamos una CSR (Solicitud de firma de Certificado) he indico la IP de mi máquina virtual Ubuntu. Esta IP es la que será accedida por mi maquina host que hará de cliente remoto.

```sh
$ openssl req -subj "/CN=192.168.81.9" -sha256 -new -key server-key.pem -out server.csr
```

Especificar extensiones
Aquí especificamos para qué IP es válido el certificado. Y declaramos que el certificado será usado por el servidor.

```sh
$ echo subjectAltName = IP:192.168.81.9 > extfile.cnf
$ echo extendedKeyUsage = serverAuth >> extfile.cnf
```

  
Firmar el certificado
Aquí se firma la solicitud `server.csr` usando la CA para emitir el certificado final del servidor.
  
```sh

$ openssl x509 -req -days 365 -sha256 -in server.csr -CA ca.pem -CAkey ca-key.pem \
-CAcreateserial -out server-cert.pem -extfile extfile.cnf
```
  
#### Generar el certificado para el cliente

  
Algo similar para el certificado para el cliente. En nuestro caso será mi maquina host Windows.

- Genero una clave privada de 4096 bit para el cliente usando RSA
- Creamos una CSR para el cliente
- Indicamos que este certificado se usará para la autenticación del cliente.

```sh
$ openssl genrsa -out key.pem 4096
$ openssl req -subj '/CN=client' -new -key key.pem -out client.csr
$ echo extendedKeyUsage = clientAuth > extfile-client.cnf

```

  Se firma la CSR del cliente

```sh
$ openssl x509 -req -days 365 -sha256 -in client.csr -CA ca.pem -CAkey ca-key.pem \
-CAcreateserial -out cert.pem -extfile extfile-client.cnf
```

#### Proteger los archivos

- Solo lectura para el propietario
- Solo lectura para todos

```sh
$ chmod 0400 ca-key.pem key.pem server-key.pem
$ chmod 0444 ca.pem server-cert.pem cert.pem
```

  
#### Iniciar Docker con TLS

Detenemos el servicio docker

```sh
sudo systemctl stop docker
```

  Iniciamos el daemon Docker de forma manual:

```sh
sudo dockerd \
--tlsverify \
--tlscacert=ca.pem \
--tlscert=server-cert.pem \
--tlskey=server-key.pem \
-H=0.0.0.0:2376
```

#### En la maquina cliente remota
  

```sh
$ docker --tlsverify \
--tlscacert=ca.pem \
--tlscert=cert.pem \
--tlskey=key.pem \
-H=tcp://192.168.81.9:2376 version
```

  

```sh
$ export DOCKER_HOST=tcp://192.168.81.9:2376
$ export DOCKER_TLS_VERIFY=1 

# En mi Windows:
$ export DOCKER_CERT_PATH="C:\Users\mitch\Documents\docker-tls"
```

#### Prueba en maquina cliente Windows

```sh
$ docker ps
$ docker ps -a
```



- **Integración** con CI para pruebas automáticas (**1 Yoel**)
- **Autenticación** de usuario en contenedores (exec como un usuario específico) (**2 Mitchel**)
- **Logging** centralizado de outputs (**3 Mitchel**)
- **Gestión de permisos** (RBAC en K8s) (**4 Yoel**)
- **TLS** y conexiones seguras (**5 Mitchel**)