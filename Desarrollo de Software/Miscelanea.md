# Pull Request
**PR** es una solicitud para fusionar cambios de código en un repositorio de control de versiones. Su propósito es permitir que otros miembros del equipo revisen y aprueben los cambios antes de integrarlos en la rama principal del proyecto.

**Ejemplo**
Supongamos que estás trabajando en una nueva configuración de infraestructura usando **Terraform**. Creas una nueva rama en tu repositorio:
```sh
git checkout -b nueva-configuracion
```

Haces cambios en los archivos de configuración y los subes al repositorio
```sh
git add .
git commit -m "Agregada configuración para balanceador de carga"
git push origin nueva-configuracion
```

Luego, en GitHub, creas un **Pull Request** para que tu equipo revise los cambios antes de fusionarlos en la rama principal.

# Entorno preproductivo

Un **entorno preproductivo** es un entorno de pruebas que simula la infraestructura de producción pero sin afectar a los usuarios finales. Se utiliza para validar cambios antes de su despliegue final.

**Ejemplo de entorno preproductivo**

Si tienes una aplicación web, podrías tener tres entornos distintos:

- **Desarrollo (dev):** Aquí los programadores prueban nuevas funcionalidades.
- **Preproducción (staging):** Simula el entorno real y permite probar cambios antes de que los usuarios los vean.
- **Producción (prod):** Donde los usuarios acceden a la aplicación real.

Cuando usas IaC, puedes desplegar una infraestructura idéntica en un entorno preproductivo para validar cambios antes de implementarlos en producción.


# Linting

El **linting** es el proceso de analizar código para detectar errores de sintaxis, estilos inconsistentes y malas prácticas.

#### **Ejemplo de linting en Ansible con `ansible-lint`:**

Si tienes un `playbook.yml` mal escrito:

```yaml
- hosts: all
  tasks:
    - name: Instalar nginx
      apt:
       name: nginx
       state: present

```

Ejecutar 
```sh
ansible-lint playbook.yml
```
detectará errores como mala indentación y sugerirá correcciones.

Otros ejemplos de herramientas de linting:

- `terraform validate` (para Terraform)
- `pylint` (para Python)
- `eslint` (para JavaScript)

# HashiCorp Vault

**HashiCorp Vault** es una herramienta diseñada para **almacenar, gestionar y proteger secretos y credenciales** de manera segura.

Un "secreto" en este contexto puede ser:
- Contraseñas
- Claves API
- Tokens de acceso
- Credenciales de bases de datos

Muchas aplicaciones almacenan secretos en **archivos de configuración en texto plano**, lo cual es un grave riesgo de seguridad.  
Con **Vault**, los secretos se almacenan en una base de datos cifrada, con **control de acceso** y **auditoría**.

### Principales características de HashiCorp Vault


**1. Almacenamiento seguro de secretos**
Vault **cifra** automáticamente los secretos antes de almacenarlos en su backend de datos.
Podemos almacenar una clave API de manera segura en Vault con el siguiente comando:
```sh
vault kv put secret/api-key value="1234567890"
```

Esto almacena `1234567890` bajo la clave `api-key` en la ruta `secret/`. Para recuperarla:
```sh
vault kv get secret/api-key
```

Salida esperada:
```
Key       Value
---       -----
value     1234567890
```

Esto evita que las claves API queden expuestas en archivos de configuración.

**2. Acceso basado en permisos (ACLs)**
Vault permite definir **políticas de acceso**.  
Por ejemplo, podríamos dar acceso de solo lectura a un servicio específico:

```hcl
path "secret/api-key" {
  capabilities = ["read"]
}
```

Así, solo ciertos usuarios o aplicaciones pueden acceder a los secretos.

**3. Expiración y renovación de credenciales**
Vault puede **generar credenciales temporales** que se eliminan después de un tiempo.  
Ejemplo:  
Un usuario solicita credenciales para una base de datos MySQL:

```sh
vault read database/creds/read-only
```
Vault devuelve credenciales temporales, que expiran automáticamente después de cierto tiempo, reduciendo riesgos.

**4. Autenticación flexible**
Vault permite autenticarse con varios métodos:

- Tokens (`vault login -method=token`) 
- GitHub OAuth
- AWS IAM
- Kubernetes Service Accounts

Esto facilita la integración con aplicaciones y servicios en la nube.


# Vagrant
**Vagrant** es una herramienta de código abierto que permite crear, configurar y gestionar máquinas virtuales de manera automatizada, usando un archivo de configuración llamado `Vagrantfile`

**Ventajas**
- Creación rápida de entornos de desarrollo.
- Facilita la colaboración al definir entornos idénticos.
- Compatible con VirtualBox, VMware, Hyper-V, entre otros.
- Permite ejecutar scripts de aprovisionamiento automáticamente

>[!Note] Entorno de desarrollo
>Conjunto de herramientas, configuraciones y software que permiten a los programadores escribir, probar y ejecutar código en un ambiente controlado antes de desplegarlo en producción. También existe entorno de pruebas o testing y preproducción o staging.

Verificar instalación
```bash
vagrant --version
```

## Vagrantfile
Es un archivo de configuración en **Ruby** que define la infraestructura de la máquina virtual.
```ruby
Vagrant.configure("2") do |config|
	config.vm.box = "ubuntu/bionic64"
```


**Comandos básicos**
```bash
# Inicia la máquina virtual
vagrant up

# Apaga la máquina virtual
vagrant halt

# Elimina la máquina virtual
vagrant destroy

# Muestra el estado actual de la máquina virtual
vagran status
```


### Configuración Avanzada del Vagrantfile

El **Vagrantfile** permite configurar máquinas virtuales con opciones más avanzadas para mejorar el rendimiento, la seguridad y la automatización del entorno de desarrollo. Aquí veremos varias configuraciones clave:

#### Personalización de Recursos (CPU, RAM, VirtualBox)

Puedes ajustar la cantidad de CPU y RAM asignada a la máquina virtual para optimizar el rendimiento. Esto es útil si tu proyecto requiere más recursos.

#### Configuración de Redes (Red Privada, Pública y NAT)

- **Red privada:** Permite la comunicación entre la máquina anfitriona y la máquina virtual sin exponerla a Internet.
- **Red pública:** Hace que la máquina sea accesible desde la red local.
- **NAT (Network Address Translation):** La máquina virtual se conecta a Internet usando la red del anfitrión.


#### Sincronización de Carpetas entre Host y Máquina Virtual
Esto permite compartir archivos entre el sistema operativo anfitrión y la máquina virtual.

#### Aprovisionamiento Automático con Shell y Ansible
Vagrant permite ejecutar scripts para configurar automáticamente la máquina virtual después de su creación.

#### Ejemplos

**Configurar CPU, RAM y VirtualBox en Vagrantfile**
Este código ajusta la memoria RAM a **2 GB** y asigna **2 núcleos de CPU** a la máquina virtual.

```ruby
Vagrant.configure("2") do |config|

  # Usar la imagen base de Ubuntu 20.04
  config.vm.box = "ubuntu/focal64"

  # Configurar recursos de la máquina virtual en VirtualBox
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"   # 2 GB de RAM
    vb.cpus = 2          # 2 Núcleos de CPU
  end

end
```

📌 **¿Para qué sirve esto?**

- Se asegura de que la máquina virtual tenga suficiente RAM y CPU para correr aplicaciones sin ralentizarse.
    

---

**Configurar Redes en Vagrantfile**

```ruby
Vagrant.configure("2") do |config|

  # Usar la imagen de Ubuntu 22.04
  config.vm.box = "ubuntu/jammy64"

  # Configuración de red privada (IP estática)
  config.vm.network "private_network", ip: "192.168.33.10"

  # Configuración de red pública (Se asigna IP automáticamente)
  config.vm.network "public_network"

end
```


- Permite que los servicios dentro de la VM sean accesibles desde la máquina anfitriona.
- Útil para simular entornos de producción sin exponerlos a Internet.

**Sincronización de Carpetas**

```ruby
Vagrant.configure("2") do |config|

  # Definir la imagen base
  config.vm.box = "ubuntu/focal64"

  # Configurar carpeta compartida entre host y VM
  config.vm.synced_folder "./proyecto", "/var/www/proyecto"

end
```


- Facilita el desarrollo porque los archivos creados en el host se reflejan en la VM sin necesidad de transferencias manuales.

**Aprovisionamiento con Script de Shell**

```ruby
Vagrant.configure("2") do |config|

  # Definir la imagen base
  config.vm.box = "ubuntu/bionic64"

  # Aprovisionamiento con script de Shell
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update                # Actualizar lista de paquetes
    sudo apt-get install -y apache2    # Instalar servidor Apache
    echo "Servidor Apache listo" > /var/www/html/index.html  # Crear página web
  SHELL

end
```

- Automatiza la instalación de paquetes en la VM sin necesidad de hacerlo manualmente.

**Aprovisionamiento con Ansible**
Si prefieres usar **Ansible** en lugar de un script de shell, puedes integrarlo con Vagrant.

```ruby
Vagrant.configure("2") do |config|

  # Usar una imagen de Ubuntu 22.04
  config.vm.box = "ubuntu/jammy64"

  # Configurar Ansible para instalar y configurar Nginx
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"  # Archivo de configuración de Ansible
  end

end
```
Permite definir configuraciones más complejas y reutilizables usando Ansible.

## Comandos útiles de Vagrant


| Comando           | Descripción                                    |
| ----------------- | ---------------------------------------------- |
| `vagrant init`    | crea un `Vagrantfile` inicial.                 |
| `vagrant up`      | Inicia la VM                                   |
| `vagran halt`     | Apaga la VM                                    |
| `vagrant destroy` | Borra la VM                                    |
| `vagrant ssh`     | Accede a la VM por ssh                         |
| `vagrant reload`  | Reinicia la VM con cambios en el `Vagrantfile` |


# Aprovisionamiento
Se refiere al proceso de configurar y suministrar los recursos necesarios para que un sistema o aplicación funcione correctamente. En el contexto de infraestructura de TI, significa la asignación y configuración de servidores, redes, almacenamiento y otros recursos ya sea de forma manual o automatizada.

# Pipeline
Es un flujo de trabajo automatizado que define una serie de pasos secuenciales para procesar y transformar datos o código. En **DevOps** y **CI/CD**, un pipeline se usa para automatizar la construcción, prueba y despliegue de aplicaciones.

# Escáneres de vulnerabilidades
Son herramientas automatizadas que analizan el código, las dependencias y los contenedores para identificar riesgos de seguridad conocidos.

Herramientas comunes
- **Trivy**
- **Anchore**
- **Snyk**
- **Clair**

¿Que buscan estos escáneres?
- **Dependencias inseguras**
- **Malas configuraciones**
- **Errores en contenedores**

# Análisis de código (SAST y DAST)
El **análisis de código** se divide en dos categorías principales:

**Análisis estático de código (SAST - Static Application Security Testing)**
Se usa para detectar problemas temprano en el desarrollo.
- Se ejecuta antes de ejecutar la aplicación.
- Examina el código fuente en busca de patrones inseguros, fallos de validación, inyecciones SQL, etc.
- No requiere ejecutar la aplicación.



**Análisis dinámico de código (DAST - Dynamic Application Security Testing)**
- Se ejecuta **mientras la aplicación está en ejecución**
- Detecta vulnerabilidades en **tiempo de ejecución**, como ataques de inyección o errores de permisos.
- Se usa para probar APIs y aplicaciones web.


# logs
Los **logs** (registros de eventos) son archivos o mensajes generados automáticamente por sistemas operativos, aplicaciones, servidores, bases de datos y dispositivos de red. Estos registros documentan eventos importantes, como errores, accesos de usuarios, cambios en la configuración y actividad del sistema.

Los logs son esenciales para:
1. **Monitoreo del sistema**
2. **Depuración y resolución de errores**
3. **Seguridad y auditoría**
4. **Optimización del rendimiento**


# Troubleshooting
Es el proceso sistemática de identificar, analizar y resolver problemas en sistemas de software, hardware, redes u otros entornos tecnológicos.

El troubleshooting sigue un enfoque estructurado para detectar y corregir errores, generalmente en estos pasos:
1. **Identificación del problema**
2. **Hipótesis y diagnóstico**
3. **Prueba de soluciones**
4. **Documentación y prevención**


# 🔄 **Flujo de trabajo en DevSecOps y herramientas asociadas**

1️⃣ **Infraestructura como Código (IaC)**

- **Terraform**: Se usa para definir y aprovisionar infraestructura en la nube (AWS, Azure, GCP) mediante código declarativo.
- **Vagrant**: Permite crear y configurar entornos virtuales localmente, útil para desarrollo y pruebas.


2️⃣ **Configuración y Automatización**

- **Ansible**: Automatiza la configuración de servidores y la instalación de software. Se usa después de Terraform para preparar el entorno.


3️⃣ **Contenedores y Orquestación**

- **Docker**: Permite empaquetar aplicaciones y sus dependencias en contenedores, facilitando su despliegue en diferentes entornos.
- **Kubernetes**: Orquesta y gestiona múltiples contenedores en un clúster, asegurando escalabilidad y alta disponibilidad.
    

4️⃣ **Monitoreo y Observabilidad**

- **Prometheus**: Recopila métricas de sistemas y aplicaciones en tiempo real para detectar problemas.
- **Grafana**: Se usa para visualizar datos de Prometheus y generar paneles de monitoreo.

---

### 📌 **Relación entre herramientas y cómo trabajan juntas**

1. **Terraform** crea la infraestructura necesaria en la nube.
2. **Ansible** configura los servidores y despliega software.
3. **Docker** empaqueta las aplicaciones en contenedores.
4. **Kubernetes** gestiona y escala estos contenedores en producción.
5. **Prometheus** recopila métricas del sistema y **Grafana** las visualiza.


# Proyecto DevSecOps: Implementación de una Aplicación Web con Infraestructura como Código

Este proyecto tiene como objetivo desplegar una aplicación web utilizando herramientas de **DevSecOps**, incluyendo **Terraform, Ansible, Docker, Kubernetes, Prometheus y Grafana**. Se explica el flujo de trabajo paso a paso con comentarios detallados en el código y una explicación adicional en cada sección.

---

## **1. Provisionamiento de Infraestructura con Terraform**

Terraform se usa para crear una instancia en AWS donde desplegaremos la aplicación.

### **Archivo: `main.tf`**

```hcl
# Especificamos el proveedor de cloud, en este caso AWS
provider "aws" {
  region = "us-east-1" # Define la región en la que se creará la instancia
}

# Creación de una instancia EC2 en AWS
resource "aws_instance" "devsecops_server" {
  ami           = "ami-0c55b159cbfafe1f0" # ID de una imagen Ubuntu
  instance_type = "t2.micro"  # Tipo de instancia (gratuita en AWS)

  tags = {
    Name = "DevSecOps-Instance" # Etiqueta de la instancia para identificarla
  }
}
```

### **Explicación**

1. Se declara AWS como proveedor de infraestructura.
    
2. Se define una máquina virtual con Ubuntu en la región `us-east-1`.
    
3. Se etiqueta la instancia con el nombre `DevSecOps-Instance`.
    

Ejecutar los siguientes comandos para aplicar la configuración:

```bash
terraform init  # Inicializa el proyecto Terraform
terraform apply -auto-approve  # Crea la infraestructura
```

---

## **2. Configuración del Servidor con Ansible**

Ansible se usa para instalar Docker y Kubernetes en la instancia creada.

### **Archivo: `playbook.yml`**

```yaml
- name: Configurar Servidor para DevSecOps
  hosts: all
  become: yes  # Ejecuta comandos como superusuario (root)
  tasks:
    - name: Instalar Docker y Kubernetes
      apt:
        name: "{{ item }}"
        state: present
      with_items:
        - docker.io
        - kubectl
```

### **Explicación**

1. Se define un "playbook" de Ansible para configurar el servidor.
    
2. Se ejecuta en todos los hosts especificados en el inventario.
    
3. Se instalan Docker y Kubernetes con el gestor de paquetes `apt`.
    

Ejecutar:

```bash
ansible-playbook -i inventory playbook.yml
```

---

## **3. Creación de una Imagen Docker con la Aplicación Web**

Se empaqueta una aplicación Flask dentro de un contenedor Docker.

### **Archivo: `Dockerfile`**

```dockerfile
# Imagen base con Python 3.8
FROM python:3.8

# Define el directorio de trabajo dentro del contenedor
WORKDIR /app

# Copia el código de la aplicación al contenedor
COPY app.py .

# Instala Flask dentro del contenedor
RUN pip install flask

# Ejecuta la aplicación cuando el contenedor inicie
CMD ["python", "app.py"]
```

### **Archivo: `app.py`**

```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def home():
    return "\u00a1Aplicación en Kubernetes con DevSecOps!"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

Ejecutar:

```bash
docker build -t myapp .
docker run -d -p 5000:5000 myapp
```

---

## **4. Orquestación con Kubernetes**

Se define un `Deployment` y un `Service` en Kubernetes.

### **Archivo: `deployment.yaml`**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp
        image: myapp:latest
        ports:
        - containerPort: 5000
---
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  selector:
    app: myapp
  ports:
  - protocol: TCP
    port: 80
    targetPort: 5000
  type: LoadBalancer
```

Ejecutar:

```bash
kubectl apply -f deployment.yaml
```

---

## **5. Monitoreo con Prometheus y Grafana**

### **Archivo: `prometheus.yaml`**

```yaml
global:
  scrape_interval: 15s
scrape_configs:
  - job_name: 'kubernetes'
    static_configs:
      - targets: ['localhost:9090']
```

Ejecutar:

```bash
kubectl apply -f prometheus.yaml
kubectl create deployment grafana --image=grafana/grafana
kubectl expose deployment grafana --type=LoadBalancer --port=3000
```

---

## **Resumen del Flujo DevSecOps**

1. **Terraform** crea la infraestructura en AWS.
2. **Ansible** instala Docker y Kubernetes.
3. **Docker** empaqueta la aplicación en contenedores.
4. **Kubernetes** orquesta la aplicación en un clúster.
5. **Prometheus y Grafana** permiten el monitoreo y visualización de métricas.

Este proyecto te permite practicar un flujo completo de **DevSecOps** con herramientas modernas. 🚀


# Delta Compression
En Git, se usa en los **objetos pack** (`packfiles`) para optimizar el almacenamiento y transmisión de datos. En lugar de almacenar versiones completas de archivos, Git almacena las diferencias (deltas) entre versiones anteriores y posteriores, reduciendo el tamaño del repositorio.

> **Ejemplo**: Si tienes un archivo que ha cambiado ligeramente en varias confirmaciones (`commits`), Git puede almacenar solo las diferencias en lugar de varias copias completas.


# Blob (Binary Large Object)
- Un blob en Git representa el contenido binario de un archivo. Es el objeto más básico en Git y almacena únicamente los datos del archivo, sin información sobre su nombre o ubicación en el sistema de archivos.
- Cada blob se identifica mediante un hash **SHA-1**, que se genera a partir del contenido del archivo.

---
 **Ejemplo**: Imagina que tienes un archivo `index.html`
```
> <html>
> 	<head>
> 	</head>
> 	<body>
> 		<h1>Hola mundo</h1>
> 	</body>
> </html>
```

Cuando se ejecuta `git add index.html`, Git crea un blob para almacenar este contenido. Si cambias el archivo Git generará un nuevo blob para representar el nuevo contenido.

>[!note] Si el contenido de un archivo no cambia entre commits Git reutiliza el mismo blob en lugar de crear uno nuevo.



# Tree (Git)
- Actúa como un directorio virtual. Asocia blobs con sus nombres de archivo, rutas y permisos, permitiendo a Git organizar los archivos dentro de una estructura jerárquica.
- Cada tree contiene referencias a blobs (para archivos) y otros trees (para subdirectorios).

---
**Ejemplo**

Supongamos que tienes el proyecto
```
proyecto/
├── index.html
├── style.css

```
Cuando haces un commit, Git crea un tree que incluye referencias a los blobs correspondientes a `index.html` y `style.css`. Este tree almacena información como:
- Permisos de archivo
- Nombre del archivo
- Hash del blob asociado.
Si agregas una subcarpeta llamada `img/` Git creara otro tree para esa carpeta y lo referenciara desde el tree principal.


# Tag (Git)
En Git, un tag es una referencia que apunta a un commit específico en el historial del proyecto, Los tags se utilizan comúnmente para marcar versiones importantes del proyecto, como lanzamientos o releases. Hay dos tipos: **lightweight** (sin metadatos adicionales) y **annotated** (con metadatos como autor y fecha).


# Código de Propósito Único

El *código de propósito único* se refiere a un principio de diseño en el desarrollo de software donde cada componente o fragmento de código tiene una única responsabilidad o función específica. Este enfoque promueve la claridad, modularidad y facilidad de mantenimiento en el código fuente. Se alinea con las mejores prácticas de desarrollo ágil y DevOps al facilitar la adaptabilidad y la integración continua.

**Características principales:**
- **Responsabilidad única:** Cada componente realiza una tarea específica, evitando sobrecargas funcionales.
- **Modularidad:** Los componentes son independientes entre sí, lo que facilita su comprensión, modificación y prueba.
- **Facilidad en CI/CD:** La integración continua (CI) y el despliegue continuo (CD) son más eficientes porque los módulos independientes reducen las probabilidades de conflictos o errores inesperados durante las integraciones.

**Beneficios:**
1. **Depuración eficiente:** Es más sencillo identificar problemas en componentes con responsabilidades claras.
2. **Colaboración simplificada:** Los cambios en Git son más comprensibles, lo que mejora la revisión de código y la comunicación entre desarrolladores.
3. **Adaptabilidad:** Los componentes pueden ser modificados o reemplazados sin afectar significativamente otros módulos.

---

# Código Completo

El *código completo* es un principio que enfatiza que cualquier fragmento de código desarrollado debe estar terminado en términos de intención y ejecución antes de ser integrado al sistema. Esto implica que el código cumpla con su propósito específico, sea apto para revisión por pares y esté respaldado por pruebas adecuadas.

**Características principales:**
- **Integridad funcional:** El código debe cumplir completamente con los requisitos establecidos para su función.
- **Preparación para revisión:** Debe adherirse a los estándares del equipo o proyecto.
- **Pruebas incluidas:** El código debe estar acompañado por pruebas que validen su funcionamiento.

**Beneficios:**
1. **Calidad asegurada:** Garantiza que el código integrado no cause interrupciones ni problemas en los pipelines de CI/CD.
2. **Colaboración eficiente:** Facilita revisiones más profundas y productivas al eliminar problemas básicos antes de la integración.
3. **Iteración progresiva:** Aunque no busca la perfección inicial, fomenta mejoras continuas basadas en retroalimentación.

**Relación con DevOps:**
En entornos DevOps, el código completo es esencial para mantener flujos ágiles y eficientes en CI/CD, asegurando que el software entregado sea funcional y confiable.



