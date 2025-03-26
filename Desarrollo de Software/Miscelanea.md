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


