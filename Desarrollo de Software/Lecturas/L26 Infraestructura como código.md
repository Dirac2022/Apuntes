

En un entorno DevOps moderno, el **Infrastructure as Code** (IaC) se ha consolidado como la práctica clave para automatizar y versionar la provisión y configuración de infraestructuras. 

## ¿Qué es "infraestructura"?

En su sentido más amplio, ==la **infraestructura** engloba todos los componentes necesarios para ejecutar aplicaciones y servicios==:

* **Cómputo** (servidores físicos o máquinas virtuales)
* **Red** (VPC, subredes, [[Miscelánea#Balanceadores de carga|balanceadores]])
* **Almacenamiento** (volúmenes, [[Miscelánea#Buckets|buckets]])
* **Seguridad** (grupos de seguridad, [[Miscelánea#🔐 Políticas de IAM|políticas de IAM]])
* **Servicios complementarios** (bases de datos gestionadas, colas, DNS, etc.)

Tradicionalmente, ==la infraestructura se gestionaba de forma manual==: un operador ingresaba a consolas web, ejecutaba comandos de CLI o editaba configuraciones en servidores. Este enfoque, además de ser lento, está sujeto a errores humanos, ==falta de trazabilidad y divergencias entre entornos== (desarrollo, pruebas, producción).


## ¿Qué es IaC?

### Configuración manual vs IaC

* **Configuración manual** implica ejecutar pasos ad-hoc ("click aquí", `ssh server && yum install nginx`) sin un registro completo de lo hecho. ==Cada despliegue puede diferir ligeramente, y reproducir un entorno exacto puede convertirse en un reto==.
* **Infrastructure as Code** traslada la definición de infraestructura a **archivos de texto**, p. ej., HCL o JSON en Terraform, YAML en Ansible—que ==describen de forma declarativa **qué** recursos queremos, no **cómo** crearlos paso a paso==. Al almacenar esos archivos en un repositorio Git, logramos:

   - **Versionar** cambios en infraestructura
   - **Revisar** propuestas (pull requests) antes de aplicar modificaciones
   - **Automatizar** despliegues con pipelines de CI/CD

## ¿Qué *no* es IaC?

* Ejecutar scripts imperativos (`bash setup.sh`) sin declaratividad ni idempotencia.
* Usar paneles de consola web sin respaldo en código.
* Configurar servidores manualmente y luego "exportar" imágenes sin un proceso reproducible.

Aunque automatizar scripts ya es un paso adelante, carece de los principios de reproducibilidad y trazabilidad que sí aporta IaC.


## Principios de IaC

### 1. Reproducibilidad

> [!note] Un archivo de IaC debe permitir recrear un entorno idéntico cada vez que se aplique.

**Ejemplo Terraform (local):**
Versionamos en Git estos tres archivos:

* **`network.tf.json`** (variables para red y nombre)
* **`main.tf.json`** (definición de `null_resource`)
* **`terraform.tfstate`** (estado actual, pero no se versiona)

Cualquier colaborador clona el repo y hace:

```bash
git checkout v1.0.0             # etiqueta de la versión estable
terraform init                  # descarga los proveedores (null)
terraform apply -auto-approve   # crea la misma "infraestructura" local
```

Cada vez que ejecuten ese flujo, verán exactamente el mismo resultado en consola:

```
null_resource.hello-server: Creating...
null_resource.hello-server (local-exec): Arrancando servidor hello-world en red local-network
null_resource.hello-server: Creation complete!
```

Si otro colaborador cambia a la rama `feature/X` y modifica `network.tf.json` para usar `"network": "red-pruebas"`, al aplicar verá el nuevo mensaje:

```
null_resource.hello-server (local-exec): Arrancando servidor hello-world en red red-pruebas
```

De este modo, **el repositorio y sus versiones etiquetadas garantizan entornos reproducibles**.

### 2. Idempotencia

> [!note] Aplicar varias veces el mismo código no debe cambiar el estado si ya está en el resultado deseado.

#### Terraform

Después del primer `apply`, el estado local (`terraform.tfstate`) guarda que el recurso existe. Si vuelves a ejecutar:

```bash
terraform apply
```

Terraform detecta que no hay diferencias entre el archivo JSON y el estado real, y responderá:

```
No changes. Infrastructure is up-to-date.
```

No volverá a ejecutar el `local-exec`, ni recreará el recurso.

#### Ansible

Imagina un playbook que instala y arranca Nginx:

```yaml
# playbook.yml
hosts: web        # Apunta a los host definidos en el inventario bajo el grupo 'web'
become: true      # Permite que las tareas se ejecuten con privilegios de                                 # superusuario (sudo)
tasks:      # Comienza la lista de tareas que se ejecutarán en los host definidos
  - name: Instalar nginx
    apt:       # Usa el modulo 'apt', que es el gestor de paquetes en Debian/Ubuntu 
      name: nginx       # Nombre del paquete a instalar
      state: present    # Asegura que esté instalado; si ya lo está, no hace nada

  - name: Asegurarse de que nginx esté en marcha
      service:  # Módulo que gestiona servicios del sistema (como systemctl)
        name: nginx     # Nombre del servicio
        state: started  # Se asegura de que el servicio esté corriendo
        enabled: true   # Se asegura de que se inicie automáticamente al arrancar el                            # sistema
```

Si lo ejecutas varias veces:

```bash
ansible-playbook -i hosts playbook.yml
```

* La primera vez instalará y arrancará Nginx.
* Las siguientes marcarán las tareas como "ok" (sin cambios), porque `state: present` y `state: started` ya están satisfechos.

Este comportamiento **evita efectos secundarios** y hace confiable la re-ejecución en entornos en drift.


### 3. Composabilidad

> [!note] Definir módulos o bloques reutilizables que puedan combinarse para construir infraestructuras complejas.

#### Terraform Modules

Imagina un directorio:

```
modules/
├── network/         ← Módulo de red
│   └── main.tf
└── compute/         ← Módulo de cómputo (servidores)
    └── main.tf
main.tf              ← Archivo principal que orquesta los módulos
variables.tf         ← Variables globales que se pasan a los módulos
```


#### `modules/network/main.tf`

```hcl
variable "network_name" { type = string }
resource "null_resource" "network" {
  triggers = { name = var.network_name }
  provisioner "local-exec" {
    command = "echo 'Configurando red ${var.network_name}'"
  }
}
```


- `variable "network_name" { type = string }`
	- Se declara una variable de entrada llamada `network_name` de tipo `string`.
	- Esta variable será usada para nombrar la red.

```hcl
resource "null_resource" "network" {
  triggers = { name = var.network_name }
  provisioner "local-exec" {
    command = "echo 'Configurando red ${var.network_name}'"
  }
}
```

- **`null_resource`** es un recurso ficticio (no crea nada real en la nube). Se usa para demostrar o probar algo (aquí, solo imprime un mensaje).
    
- **`triggers`**: asegura que si cambia el valor de `network_name`, se reprovisiona el recurso.
    
- **`local-exec`**: ejecuta un comando local. Aquí, simplemente imprime por consola algo como:
    
    ```
    Configurando red red-de-prueba
    ```


#### `modules/compute/main.tf`

```hcl
variable "server_name" { type = string }
resource "null_resource" "server" {
  triggers = {
    name    = var.server_name
    network = var.network_network_name
  }
  provisioner "local-exec" {
    command = "echo 'Arrancando servidor ${var.server_name} en red ${var.network_network_name}'"
  }
}
```


### `modules/compute/main.tf`

```hcl
variable "server_name" { type = string }
```

- Declara una variable de entrada `server_name` para nombrar el servidor.
    

```hcl
resource "null_resource" "server" {
  triggers = {
    name    = var.server_name
    network = var.network_network_name
  }
  provisioner "local-exec" {
    command = "echo 'Arrancando servidor ${var.server_name} en red ${var.network_network_name}'"
  }
}
```

- Otro recurso ficticio que se activa si cambia el nombre del servidor o la red.
    
- Imprime por consola un mensaje con el nombre del servidor y la red asociada.
    

> ⚠️ Aquí hay un pequeño error en el código original: falta declarar la variable `network_network_name`. Debería haber algo como:

```hcl
variable "network_network_name" { type = string }
```

---


#### `main.tf`

```hcl
module "red" {
  source       = "./modules/network" # Usa el modulo de red  
  network_name = var.network         # Le pasa la variable 'network' como nombre de red
}

module "servidor" {                   
  source      = "./modules/compute"                # Usa el modulo de computo
  server_name = var.name                           # Le passa un nombre de servidor
  # Pasamos salida del módulo de red:
  network_network_name = module.red.network_name   # Intenta pasar la salida del modulo                                                    # de red
}
```

Cada módulo encapsula una pieza de infraestructura —red o cómputo— y se combinan sin duplicar código.


---

- `module "red" {}`
	- Se instancia el módulo `network`, le pasa el valor `var.network` como nombre.
- `module "servidor {}`: Instancia el módulo `compute` y le pasa el valor de:
	- `var.name`: nombre del servidor.
    - `module.red.network_name`: intenta pasar como variable el nombre de la red creada por el módulo anterior.

---

> ⚠️ Este código asumirá que `module.red` expone una **salida** llamada `network_name`, pero eso no está definido. Para que funcione, dentro del módulo `network` debe añadirse:

```hcl
output "network_name" {
  value = var.network_name
}
```

---



### 4. Evolvibilidad

> [!note] Facilitar la extensión y adaptación de la configuración a medida que cambian los requisitos.

#### Uso de variables en Terraform

En lugar de hard-codear:

```json
"command": "echo 'Arrancando servidor hello-world en red local-network'"
```

defínelo con variables:

```hcl
variable "name"    { type = string }
variable "network" { type = string }

resource "null_resource" "hello" {
  triggers = {
    name    = var.name
    network = var.network
  }
  provisioner "local-exec" {
    command = "echo 'Arrancando servidor ${var.name} en red ${var.network}'"
  }
}
```

Y en `terraform.tfvars`:

```hcl
name    = "hello-world"
network = "local-network"
```

Cuando necesites crear un entorno de staging:

```hcl
# staging.tfvars
name    = "staging-server"
network = "staging-network"
```

Basta con:

```bash
terraform apply -var-file=staging.tfvars
```

Sin tocar código ni copiar y pegar.

#### Versionado de cambios breaking

Cuando cambies la sintaxis de un módulo (p. ej., cambies el nombre de una variable), crea un **CHANGELOG.md** o un documento de migración en tu repo, indicando paso a paso cómo actualizar de la versión anterior a la nueva.


### 5. Aplicación de los principios

1. **Separación de responsabilidades**

   * Variables (`network.tf.json`) vs cómputo (`main.tf.json`) vs lógica de generación (`main.py`).

2. **Parametrización**

   * `main.py` recibe argumentos:

     ```python
     hello_server_local(name="app1", network="net1")
     hello_server_local(name="app2", network="net2")
     ```
   * Genera distintos JSON sin duplicar lógica.

3. **Portabilidad con Docker**

   * El `Dockerfile` multi-stage y el `docker-compose.yml` garantizan que cualquier máquina (Windows, Linux, macOS) con Docker pueda reproducir exactamente el mismo flujo:

     ```bash
     docker-compose up --build
     ```
   * Internamente, siempre se usa la misma versión de Terraform, Python y de tus scripts.


## ¿Por qué usar Infrastructure as Code?

Adoptar IaC no es solo una moda: aporta ==beneficios== concretos en ==control, velocidad, colaboración y seguridad==. A continuación profundizamos en cada uno de estos aspectos, con ejemplos prácticos que ilustran su impacto en un flujo DevOps.

#### 1. Gestión de cambios

* **Rastro de auditoría (Audit trail)**
  Cada modificación en tu infraestructura queda registrada como un commit en Git. Por ejemplo, si cambias `instance_type` de `t2.micro` a `t3.small` en tu `main.tf.json`, el diff de Git mostrará exactamente qué atributo cambió y cuándo. Esto facilita responder a "¿quién cambió esto?" y "¿por qué?", gracias a mensajes de commit descriptivos y al historial de pull requests.

* **Revisión por pares**
  Antes de aplicar un cambio, se abre un *pull request* que incluye un `terraform plan`. En la pipeline, un job ejecuta:

  ```bash
  terraform init
  terraform plan -var-file=staging.tfvars
  ```

  Si al revisar el plan los compañeros detectan que vas a eliminar sin querer un recurso de producción, pueden comentar directamente en la línea del plan. Solo cuando todos aprueban, el job de `apply` se dispara, garantizando un control de calidad colaborativo.

* **Rollback instantáneo**
  ==Si un despliegue automático introduce un error, basta con revertir el commit en Git (`git revert <SHA>`) y volver a ejecutar la pipeline. Terraform detectará que el archivo ha vuelto a la versión anterior y deshará cualquier cambio no deseado. Este proceso toma minutos, en lugar de horas de reconstrucción manual==.

#### 2. Retorno de inversión (ROI) de tiempo

* **Despliegues exprés**
  Un entorno completo, una red local simulada con `null_resource`, servidor de pruebas, balanceador se crea en segundos con:

  ```bash
  terraform apply -auto-approve
  ```

  Frente a ello, configurar manualmente implicaría decenas de clicks en consolas web, SSHs y validaciones de estado.

* **Pipelines automatizados**
  Integrar IaC en GitHub Actions, GitLab CI o Jenkins permite que, al hacer merge a `main`, se ejecute automáticamente:

  1. `terraform fmt && tflint` (asegura estilo y buenas prácticas)
  2. `terraform plan` y generación de artefacto JSON con el plan
  3. `terraform apply -auto-approve` si el plan pasa todas las validaciones

  De este modo, el equipo dedica menos tiempo a tareas repetitivas y puede enfocarse en diseñar arquitecturas más eficientes.

* **Escalado horizontal instantáneo**
  ¿Necesitas 5 instancias nuevas para un pico de tráfico? Solo modifica una variable (`count = 5`) y reaplica. Terraform crea exactamente las instancias adicionales necesarias, sin intervención manual.


#### 3. Compartir conocimiento

* **Documentación viva en el código**
  Las variables con nombres claros (`var.network_name`, `var.server_count`), los comentarios en módulos y los ejemplos en `README.md` actúan como guía para nuevos miembros. No hay que leer manuales externos: la propia definición de `module "compute"` o los ejemplos de uso de `main.py` muestran cómo parametrizar y extender la infraestructura.

* **Onboarding acelerado**
  Al clonar el repositorio y ejecutar `docker-compose up --build`, un desarrollador novato levanta un entorno de pruebas idéntico al de producción local. Esto reduce drásticamente la curva de aprendizaje y evita "works on my machine" gracias a la contenerización de todo el flujo.

* **Bibliotecas de módulos reutilizables**
  Almacenando módulos genéricos (por ejemplo, un módulo `security_group` que acepte puertos y descripciones), el equipo crea un **catálogo interno** de bloques IaC. Esto fomenta la consistencia entre proyectos y evita reinventar la rueda.


#### 4. Seguridad

* **Gestión centralizada de secretos**
  Nunca hardcodees credenciales. En lugar de ello, integra Vault, AWS SSM o Azure Key Vault. Por ejemplo, tu pipeline podría inyectar un token con:

  ```yaml
  - name: Login to Vault
    run: vault login -method=github token=${{ secrets.VAULT_TOKEN }}

  - name: Fetch DB password
    run: vault kv get -field=password secret/databases/prod > db_pass.txt

  - name: Apply Terraform
    run: terraform apply -var="db_password=$(cat db_pass.txt)" -auto-approve
  ```

* **Revisión de políticas**
  Al definir roles y permisos de IAM como código, puedes usar herramientas como `terraform-compliance` o `checkov` para escanear malas configuraciones (por ejemplo, "¡no 0.0.0.0/0 en reglas de SSH!") antes de aplicar. Esto introduce validaciones de seguridad en cada *merge request*.

* **Principio de menor privilegio**
  Al versionar los `aws_iam_policy` o sus equivalentes locales, documentas qué permisos exactos necesita cada componente. Si mañana una función lambda reclama permisos excesivos, el diff del código muestra exactamente qué añadió y por qué, evitando que un servicio tenga más privilegios de los necesarios.


En conjunto, estos beneficios transforman la forma de operar de los equipos DevOps, convirtiendo tareas manuales y propensas a errores en flujos reproducibles, veloces y auditables. Infrastructure as Code es, hoy en día, la base indiscutible de cualquier estrategia de despliegue automatizado y resiliente.

## Herramientas

A continuación profundizamos en las tres grandes categorías de herramientas en un flujo DevOps: ==**Aprovisionamiento**, **Gestión de configuración** e **Construcción de imágene==s**, mostrando cómo se encajan entre sí y ejemplos concretos.

#### 1. Aprovisionamiento

El **aprovisionamiento** es la etapa de "orquestar" o crear los recursos de infraestructura (VMs, redes, balanceadores, bases de datos). En DevOps:

* **Herramientas declarativas** definidas en archivos de texto, versionadas y revisables.
* **Idempotencia**: ejecutar varias veces no genera duplicados.
* **Multi-proveedor**: mismo lenguaje para AWS, GCP, Azure o incluso entornos on-premises.

#### Ejemplos

#### Terraform

```go
# variables.tf
variable "region" { type = string, default = "us-east-1" }
variable "vm_count" { type = number, default = 2 }

# main.tf
provider "aws" {
  region = var.region
}

resource "aws_vpc" "main" {
  cidr_block = "10.0.0.0/16"
}

resource "aws_instance" "app" {
  count         = var.vm_count
  ami           = "ami-0abcdef1234567890"
  instance_type = "t3.micro"
  subnet_id     = aws_subnet.main.id
  tags = {
    Name = "app-${count.index}"
  }
}
```

* `terraform init`
* `terraform plan`
* `terraform apply`

#### Pulumi (IaC con código)

```
import * as aws from "@pulumi/aws";

const vpc = new aws.ec2.Vpc("main", { cidrBlock: "10.0.0.0/16" });
const subnet = new aws.ec2.Subnet("app-subnet", {
    vpcId: vpc.id,
    cidrBlock: "10.0.1.0/24",
});

for (let i = 0; i < 2; i++) {
  new aws.ec2.Instance(`app-${i}`, {
    ami: "ami-0abcdef1234567890",
    instanceType: "t3.micro",
    subnetId: subnet.id,
  });
}
```

* `pulumi up` crea o actualiza los recursos.
* Ideal si tu equipo prefiere TypeScript/Python/Go sobre HCL.

#### 2. Gestión de configuración

Mientras el aprovisionamiento crea la máquina, la **gestión de configuración** se encarga de dejarla en el estado deseado: ==instalar paquetes==, ==copiar archivos de configuración==, ==gestionar servicios==.

#### Características clave

* **Estado deseado**: cada "playbook" o "recipe" describe el estado final.
* **Agentes vs "agentless"**: Chef/Puppet usan agentes; Ansible y SaltStack suelen funcionar por SSH.
* **Idempotencia**: aplicable tanto en la máquina recién creada como en aquellas recreadas tras un reprovisioning.

#### Ejemplos

#### Ansible (agentless, YAML)

```yaml
# playbook.yml
- hosts: all
  become: true
  vars:
    app_user: deploy
  tasks:
    - name: Crear usuario de la aplicación
      user:
        name: "{{ app_user }}"
        shell: /bin/bash

    - name: Instalar dependencias
      apt:
        name:
          - nginx
          - git
        state: present

    - name: Desplegar código
      git:
        repo: "https://github.com/mi-org/mi-app.git"
        dest: "/home/{{ app_user }}/app"
        version: "main"

    - name: Configurar servicio systemd
      template:
        src: service.j2
        dest: /etc/systemd/system/mi-app.service

    - name: Habilitar y arrancar servicio
      systemd:
        name: mi-app
        enabled: yes
        state: started
```

* `ansible-playbook -i inventory playbook.yml`
* Ideal para configurar tanto servidores nuevos como corregir drift en los ya existentes.

#### Chef (con agentes, Ruby DSL)

```ruby
# recipes/default.rb
package %w(nginx git) do
  action :install
end

user 'deploy' do
  shell '/bin/bash'
end

git '/home/deploy/app' do
  repository 'https://github.com/mi-org/mi-app.git'
  revision 'main'
  user 'deploy'
end

template '/etc/systemd/system/mi-app.service' do
  source 'mi-app.service.erb'
  mode '0644'
end

service 'mi-app' do
  action [:enable, :start]
end
```

* `chef-client` en cada nodo aplica el cookbook.

#### 3. Construcción de imágenes

La **construcción de imágenes** busca crear artefactos inmutables —==contenedores Docker o imágenes VM==, con todo preinstalado. Así minimizas pasos en tiempo de arranque y garantizas entornos idénticos.

#### Beneficios

* **Arranque rápido**: la máquina o contenedor ya incluye dependencias y configuraciones.
* **Reproducibilidad**: la imagen corresponde a un *snapshot* exacto de tu stack.
* **Inmutabilidad**: si falla un nodo, descartas la imagen y lanzas otra idéntica.

#### Ejemplos

#### Docker

```dockerfile
FROM python:3.10-slim

# 1. Instala dependencias del sistema
RUN apt-get update && apt-get install -y git

# 2. Crea usuario y directorio de trabajo
RUN useradd -ms /bin/bash deploy
WORKDIR /home/deploy

# 3. Copia código y dependencias de Python
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .

# 4. Define comando por defecto
CMD ["gunicorn", "app:app", "--bind", "0.0.0.0:8000"]
```

* `docker build -t mi-app:latest .`
* `docker run -d -p 8000:8000 mi-app:latest`

#### Packer (imágenes VM)

```json
{
  "builders": [
    {
      "type": "amazon-ebs",
      "region": "us-east-1",
      "source_ami": "ami-0abcdef1234567890",
      "instance_type": "t3.micro",
      "ssh_username": "ubuntu",
      "ami_name": "app-{{timestamp}}"
    }
  ],
  "provisioners": [
    {
      "type": "shell",
      "inline": [
        "sudo apt-get update",
        "sudo apt-get install -y nginx git python3-pip",
        "git clone https://github.com/mi-org/mi-app.git /opt/mi-app",
        "pip3 install -r /opt/mi-app/requirements.txt"
      ]
    }
  ]
}
```

* `packer build packer.json` crea una AMI (o imagen en GCP/Azure) ya configurada.
* Luego, Terraform o tu orquestador puede instanciar esa imagen rápidamente.


#### Cómo encajan estas capas en un pipeline DevOps

1. **Desarrollo y pruebas locales**

   * Construyes tu contenedor Docker o imagen Packer.
   * Ejecutas playbooks de Ansible sobre un entorno local (Vagrant, Docker Compose).

2. **Control de calidad**

   * En CI, cada *pull request* dispara:

     * Linting/formateo de Terraform (`terraform fmt`, `tflint`)
     * Validación de playbooks Ansible (`ansible-lint`)
     * Build de imagen Docker (`docker build --no-cache`)
     * Pruebas de integración contra un "entorno staging" provisiónado con Terraform local (`null_resource`) o real.

3. **Despliegue**

   * Terraform crea/redimensiona infraestructura en la nube.
   * Ansible aplica configuraciones de último milla (si no usas contenedores).
   * El orquestador (Kubernetes, ECS) arranca contenedores basados en la imagen construida.

4. **Monitoreo y feedback**

   * Herramientas de observabilidad (Prometheus, Grafana) validan que todo esté en "verde".
   * Cualquier cambio manual dispara drift, detectado por `terraform plan` o inventarios Ansible.


En un entorno DevOps estas herramientas forman un **flujo continuo** que va desde la definición de recursos hasta el despliegue de aplicaciones en un recorrido íntegramente versionado, revisado y automatizado. Cada capa aporta idempotencia, reproducibilidad y velocidad, pilares indispensables para escalar de forma ágil y fiable.


### Escribiendo IaC

Al escribir Infrastructure as Code (IaC) buscamos capturar en texto plano todo el ciclo de vida de nuestros recursos, desde su creación hasta su actualización o destrucción, de modo que cualquier cambio sea visible, revisable y reproducible. A continuación profundizamos de manera fluida en cómo expresar cambios, trabajar con entornos inmutables y, finalmente, compartir pautas para mantener el código IaC limpio y sostenible.

#### Expresando cambios en infraestructura

1. **Edición declarativa de archivos**
   Cada vez que quieres cambiar algo , por ejemplo el tipo de instancia o el número de servidores, modificas el `.tf` o `.tf.json`. No ejecutas comandos imperativos, sino que ajustas la **declaración** de lo que deseas.

   ```hcl
   # Antes: usábamos una sola instancia
   resource "null_resource" "app" {
     triggers = { count = "1" }
   }

   # Ahora: escalamos a tres instancias
   resource "null_resource" "app" {
     triggers = { count = "3" }
   }
   ```

2. **Flujo clásico: `init`, `plan`, `apply`**

   * `terraform init` descarga proveedores, inicializa el módulo local y prepara el estado.

   * `terraform plan` muestra un reporte línea a línea de lo que va a crear, modificar o destruir.

   * `terraform apply` ejecuta esos cambios solo si has validado el plan.

   > **Tip:** siempre ejecuta `plan` en tu CI antes de aprobar un merge. Así ves en tu pipeline exactamente qué va a pasar, y puedes bloquear cambios peligrosos (por ejemplo, destrucción accidental de datos).

3. **Plan como contrato**
   Piensa en `terraform plan` como un **contrato** entre tu equipo y la infraestructura: una vez aceptado, `apply` cumple con lo pactado. Si alguien cambia manualmente un recurso "por fuera" (un drift), el siguiente `plan` lo detectará:

   ```
   # Terraform detecta un cambio "out-of-band"
     ~ null_resource.app
         triggers.count: "3" => "1"
   ```

   De inmediato puedes decidir si remediar (revertir el cambio manual) o actualizar tu código.

#### Comprendiendo la inmutabilidad

La inmutabilidad es un paradigma clave para entornos de producción robustos:

1. **Nunca parchear en caliente**
   Evita `ssh` directo a producción para instalar parches. En su lugar, consolida todos los cambios en una **imagen nueva**.

2. **Construcción de imágenes como paso previo**
   Con herramientas como Docker o Packer:

   ```dockerfile
   FROM ubuntu:20.04
   RUN apt-get update && apt-get install -y nginx=1.18.*
   COPY ./app /srv/app
   CMD ["nginx", "-g", "daemon off;"]
   ```

   Cada vez que cambies la versión de Nginx o tu aplicación, produces una nueva etiqueta (tag) de imagen, por ejemplo `registry/myapp:20250515-v2`.

3. **Despliegue de blue/green o rolling**

   * **Blue/Green**: despliegas la versión nueva (`green`), pruebas salud, y rediriges el tráfico. Luego descartas la antigua (`blue`).
   * **Rolling**: reemplazas los nodos uno a uno, manteniendo siempre capacidad de servir.

4. **Remediación de drifts ("out-of-band" changes)**
   Cualquier cambio manual queda fuera del control de IaC. Al detectar drift con `terraform plan`, puedes:

   * **Revertir** el cambio manual en consola.
   * **Actualizar** tu código para que refleje la nueva configuración deseada.

5. **Migración desde entornos legados**

   * **Importación**: usa `terraform import null_resource.app <id>` para traer recursos existentes al estado.
   * **Definición**: codifica en `.tf` cada recurso importado, p. ej.:

     ```hcl
     resource "aws_s3_bucket" "logs" {
       bucket = "mi-bucket-logs"
       acl    = "private"
     }
     ```
   * **Verificación**: `terraform plan` debe reportar "no changes" cuando ya coincida el estado con el código.


#### Escribiendo código limpio de Infrastructure as Code

1. **Control de versiones como fuente de verdad**

   * Incluye un `README.md` que explique el flujo completo (`init`, `plan`, `apply`, `destroy`).
   * Trabaja con **ramas de feature** y usa pull requests para revisar cambios.
   * Etiqueta (tags) versiones estables de tu infraestructura, p. ej. `v1.0.0`.

2. **Linting y formateo automático**

   * Ejecuta en tu CI y local:

     ```bash
     terraform fmt -recursive   # da formato estándar
     tflint                     # detecta malas prácticas
     ```
   * Configura un hook de Git (`pre-commit`) que bloquee commits que no pasen estos chequeos.

3. **Convenciones de nombrado**
   Sigue un patrón uniforme que refleje proyecto, entorno y tipo de recurso:

   ```
   project-env-type-name
   └─ myapp-prod-sg-web
   └─ myapp-dev-nullserver
   ```

   Así, al listar recursos, sabes de un vistazo a qué entorno y componente pertenecen.

4. **Variables bien estructuradas**

   * Agrupa variables en archivos:

     * `variables.network.tf.json` para red
     * `variables.compute.tf.json` para cómputo
   * Define descripciones claras y valores por defecto:

     ```json
     {
       "variable": [
         {
           "name": [
             {
               "type": "string",
               "default": "hello-world",
               "description": "Nombre del servidor principal"
             }
           ]
         },
         {
           "network": [
             {
               "type": "string",
               "default": "local-network",
               "description": "Identificador de la red local"
             }
           ]
         }
       ]
     }
     ```

5. **Parametrizar dependencias con código**
   Si tienes un script Python (`main.py`) o un módulo de Terraform, hazlo genérico:

   ```python
   def hello_server(name, network, count=1):
       # Genera un bloque JSON que Terraform puede consumir
       ...
   ```

   Al cambiar `name` o `network`, no replicas plantillas, solo llamas a la función con distintos argumentos.

6. **Manejo seguro de secretos**

   * **Jamás** codifiques credenciales en texto plano.
   * En Docker Compose o tu pipeline, monta secretos:

     ```yaml
     services:
       infra:
         environment:
           VAULT_ADDR: https://vault.example.com
         secrets:
           - vault_token
     secrets:
       vault_token:
         file: ./vault_token.txt
     ```
   * Dentro de Terraform, usa providers como `vault` o `external` para recuperar valores en tiempo de ejecución.

Al dominar estos patrones, desde el simple `init/plan/apply` hasta la creación de imágenes inmutables y el linteo automático, conviertes IaC en un proceso confiable, colaborativo y seguro. Cada cambio queda documentado, revisado y probado antes de entrar en producción, asegurando la calidad y agilidad propia de una cultura DevOps madura.
