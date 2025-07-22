> **Tarea teórica:**  
> - Investigar una herramienta de IaC (p. ejemplo. Terraform) y describir cómo organiza sus módulos.  
> - Proponer la estructura de archivos y directorios para un proyecto hipotético que incluya tres módulos: `network`, `database` y `application`. Justificar la jerarquía elegida.



Es una herramienta IaC que permite definir y administrar recursos de infraestructura a través de archivos de configuración. Terraform permite gestionar de manera declarativa una variedad de servicios y automatizar cambios en ellos, reduciendo el riesgo de errores producidos por operaciones manuales.

# HCP Terraform

**HCP Terraform** amplía estas funcionalidades al gestionar las ejecuciones de Terraform en un entorno seguro, en lugar de hacerlo en tu máquina local. Almacena de forma segura el estado y los datos sensibles y puede conectarse a sistemas de control de versiones para que puedas desarrollar tu infraestructura con un flujo de trabajo similar al del desarrollo de aplicaciones. La interfaz de usuario de HCP Terraform proporciona una vista detallada de los recursos gestionados por un proyecto de Terraform y ofrece una mayor visibilidad de cada operación realizada.

HCP Terraform también incluye un registro privado para compartir módulos y proveedores de Terraform dentro de tu organización. HCP Terraform facilita la colaboración en cada etapa del desarrollo de infraestructura.

**Resumen**
- **Ejecución gestionada**: Corre Terraform en un entorno controlado en lugar de en máquinas locales.
- **Almacenamiento seguro**: Guarda de forma segura el estado de la infraestructura y datos sensibles.
- **Integración con control de versiones**: Permite trabajar con flujos similares al desarrollo de aplicaciones.
- **Interfaz de usuario**: Proporciona visibilidad detallada de los recursos y operaciones de Terraform.
- **Registro privado**: Facilita compartir módulos y proveedores dentro de una organización.
- **Funciones avanzadas (de pago)**: Incluye control de acceso, políticas de gobernanza, estimaciones de costos y más.
- **Colaboración segura**: Permite revisión y aprobación de cambios antes de aplicarlos.
- **Prevención de conflictos**: Bloquea automáticamente el estado para evitar modificaciones simultáneas.


# Workflows
En HCP Terraform, los recursos se organizan en *workspaces*, que contienen las definiciones de los recursos, variables de entorno, variables de entrada y archivos de estado. Cada operación de Terraform ocurre dentro de un *workspace* y Terraform usa su configuración y estado para modificar la infraestructura.

HCP Terraform admite tres flujos de trabajo para ejecutar Terraform:
1. **Flujo basado en CLI**: Usa las herramientas estándar de la línea de comandos de Terraform para ejecutar operaciones en HCP Terraform.
2. **Flujo basado en UI/Sistema de Control de Versiones (VCS)**: Los cambios en repositorios de control de versiones activan ejecuciones en el *workspace* asociado.
3. **Flujo basado en API**: Permite interactuar programáticamente con la API de HCP Terraform para crear herramientas personalizadas.


# Instalación Manual


1. Descargar zip: [Install | Terraform | HashiCorp Developer](https://developer.hashicorp.com/terraform/install)
2. Descomprimir y colocarlo en una ruta específica
3. Agregar esa ruta al Path de variables de entorno
4. ejecutar `terraform -help` en la terminal para comprobar la instalación.

# Terraform Workflow
[A Beginner’s Guide to Infrastructure Automation with Terraform | by Deepa Mathan | Medium](https://medium.com/@deepamathan/terraform-infrastructure-as-a-code-1dbf0f7ed3e1)
**Terraform Init**
- Terraform inicializa el directorio de trabajo que contiene los archivos de configuración de terraform.
- Descarga e instala el plugin del **proveedor** para que posteriormente pueda ser ejecutado.
- Crea un archivo de bloqueo `.terraform.locl.hcl` para registrar las selecciones de proveedores que realizó anteriormente. Y también, inicializa las configuración del backend.

**Terraform fmt**
- Se utiliza para reescribir los archivos de configuración de Terraform a un formato y estilo canónicos.

**Terraform Validate**
- El comando terraform `validate` valida los archivos de configuración en directorio.
- El comando `validate` valida si una configuración es sintácticamente válida y, por lo tanto, es principalmente útil para la verificación general de módulos reutilizables, incluida la exactitud de los nombres de atributos y los tipos de valor.

**Terraform Plan**
- Se utiliza para crear un plan de ejecución. No va a modificar las cosas en la infraestructura. Compara el estado deseado de terraform con el estado actual en la nube.
- Este comando es una forma cómoda de comprobar si el plan de ejecución de un conjunto de cambios coincide con sus expectativas sin realizar ningún cambio en el estado.

**Terraform Apply**
Aplica los cambios necesarios para alcanzar el estado deseado de la configuración. Este comando ejecuta el plan que ya está creado. Compara el estado correcto con el estado deseado.

**Terraform Destroy**
El comando `destroy` se utiliza para eliminar los recursos creados en la infraestructura administrada por Terraform


---- 

# ¿Como funciona Terraform?


[🔥🚀¡Terraform Zero to Hero Series! ¡Domine la infraestructura como código con demostraciones del mundo real! 🔥🚀 | por DevOps Guru | Medio](https://medium.com/@anilbidary/terraform-zero-to-hero-series-master-infrastructure-as-code-with-real-world-demos-25792b62e280)


Terraform crea y administra recursos en plataformas en la nube y otros servicios a través de sus interfaces de programación de aplicaciones (API). Los proveedores (providers) permiten que Terraform funcione con prácticamente cualquier plataforma o servicio con una API accesible. 

![](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*jbYes44NaqNPwa1iYHR2gQ.png)


### Provider
Los proveedores son los complementos que Terraform utiliza para administrar esos recursos. Cada plataforma de servicio o infraestructura compatible tiene un proveedor que define qué recursos están disponibles y realiza llamadas a la API para administrar esos recursos. Por lo tanto, el proveedor comprende las interacciones de la API y expone los recursos.

> - Registry .... directory of providers `https://registry.terraform.io`
> - Provider ... understant API interactions and expose resources
> - terraform init ... download provider


### Variables
Una variable en Terraform es un contenedor que contiene un valor. Se puede utilizar para representar diferentes valores en diferentes momentos durante la ejecución de un programa. Las variables en Terraform son una excelente manera de definir valores reutilizables controlados centralmente. Terraform admite 3 tipos diferentes de variables: 
- **Variables de entrada** como argumento de función
- **Variable de salida**, valor de retorno de la función similar.
- **Variables locales** como la variable local temporal de una función.

> [!note] Variable preferences
> Terraform loads variables in following order
> - Environment variable
> - Terraform.tfvars
> - Terraform.tfvars.json
> - \*.auto.tfvars or \*.auto.tfvars.json
> - Command line arguments (-var & -var-file)

# Workspaces
Los **workspaces** de Terraform están asociados a un directorio de trabajo específico y aíslan varios archivos de estado en el mismo directorio de trabajo, lo que le permite administrar varios grupos de recursos con un solo archivo de configuración.

Terraform comienza con un único espacio de trabajo denominado `default` que no se puede eliminar. Al ejecutar el plan de terraform en un nuevo **workspace**, Terraform no accede a los recursos existentes en otros **workspaces**. Estos recursos siguen existiendo físicamente, pero debe cambiar de espacio de trabajo para administrarlos.

Un uso común de varios **workspaces** es crear una copia paralela y distinta de la infraestructura para probar un conjunto de cambios antes de modificar la infraestructura de producción.

![](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*RV0DwjGcqUSWVwaavrqcJA.png)


# Terraform Module
Los módulos son el ingrediente clave para escribir código de Terraform reutilizable, mantenible y comprobable. Los módulos son contenedores para varios recursos que se utilizan juntos. Un módulo consiste en una colección de archivos `.tf` que se mantienen juntos en un directorio. 

Un módulo de terraform (generalmente un módulo raíz) puede llamar a otros módulos para incluir sus recursos en la configuración. Un módulo que ha sido llamado por otro módulo se denomina módulo secundario. El módulo secundario se puede definir dentro del módulo raíz mediante el bloque de módulo, que especifica la fuente del módulo y cualquier variable de entrada que deba establecerse.





# Miscelánea Terraform

## Comandos

### `terraform init`
Inicializa un directorio de trabajo que contiene los archivos de configuración de Terraform

- `-input=true` : Ask for input if necessary. If false, will error if input was required
- `-upgrade` : Option to upgrade modules and plugins as part of their respective installation steps.



### Switching Working Directory

You can run Terraform from another directory if the needs arises. Useful when you are using different automations and you don't want to change directory

```sh
terraform -chdir="../dev" apply
```

## 📌 `resource`

---

In Terraform, a resource represents a specific entity or component of infrastructure you want to manage, provision, or configure. These resources can range from virtual machines, networks, and storage accounts to more specialized services from cloud providers.

```python
resource "azurerm_windows_function_app" "monitor" {
	# Configuration settings for the resource
	attribute1 = value1
	attribute2 = value2
	# ...
}
```

The block above is a declaration for a resource that is a function app in Azure. When executed, it communicates with the remote resource provider (Azure) and creates an Azure Function App resource base on the specifications of its configurations.

[Terraform Null Resource - What It is & How to Use It](https://spacelift.io/blog/terraform-null-resource)

---



Un **`resource`** en Terraform representa un componente de infraestructura que deseas gestionar (como un servidor, una base de datos o incluso un archivo local). Cada recurso tiene:  
- **Tipo** (ejemploemplo: `aws_instance`, `local_file`).  
- **Nombre** (identificador único dentro del módulo).  
- **Argumentos** (configuraciones específicas).  


```hcl
resource "tipo_recurso" "nombre_logico" {
  argumento1 = valor1
  argumento2 = valor2
  ...
}
```



**🔍 Recursos Específicos**  
####  `null_resource`  


---

The `null_resource` in Terraform is similar to a standard resource. It adheres to the resource lifecycle model and servers as a placeholder for executing arbitrary actions withing Terraform configurations without actually provisioning any physical resources. However, it does not perform any further actions beyond initialization.

Below is the syntax for declaring a `null-resource`

```go
resource "null_resource" "example" {

	// Using triggers to force execution on every apply
	triggers = {
		always_run = timestamp()
	}
	provisioner "local-exec" {
		command = "echo This command will execute whenever the configuration changes"
	}
}
```

- `resource`: indicates the declaration of a Terraform resource 
- `null_resource`:  specifies the type of resource being declared
- `provisioner`: specifies the type of provisioner (example: local, remote, etc.) 
- `triggers`: specifies what triggers this `null_resource` to execute 

[Terraform Null Resource - What It is & How to Use It](https://spacelift.io/blog/terraform-null-resource)


>[!warning] Si no usamos `triggers` el `null_resource` solo se ejecutará la primera vez que se llame con  `terraform apply`.

---

- Es un recurso "vacío" que no crea nada por sí mismo, pero permite ejecutar `provisioners` (como scripts o comandos).  
- Útil para tareas que no están directamente soportadas por proveedores de Terraform.  

**📌 Casos de Uso**  
✅ ejecutar scripts locales (`local-exec`).  
✅ Disparar acciones manuales durante el despliegue.  

**⚡ ejemploemplo**  
```go
resource "null_resource" "ejemploemplo" {
  triggers = {
    siempre_ejecutar = timestamp() # Fuerza ejecución en cada 'apply'
  }

  provisioner "local-exec" {
    command = "echo 'Hola Terraform!' > saludo.txt"
  }
}
```

---

#### 📄 [[#`local_file`|`local-file`]]

- Crea, actualiza o elimina **archivos en la máquina local** donde se ejecuta Terraform.  

**📌 Casos de Uso**  
✅ Generar archivos de configuración (Ejemplo: scripts, JSON, YAML).  
✅ Guardar outputs de Terraform en un archivo.  

#### **⚡ ejemploemplo**  
```hcl
resource "local_file" "config" {
  filename = "configuracion.txt"
  content  = "Este archivo fue generado por Terraform 🚀"
}
```

---

#### 🎯 `random_id`  

**¿Qué hace?**  
- Genera **IDs o strings aleatorios** (útil para nombres únicos de recursos).  
- Usa algoritmos criptográficos para garantizar aleatoriedad.  

**📌 Casos de Uso**  
✅ Evitar colisiones de nombres en recursos (ejemploemplo: buckets de S3).  
✅ Generar contraseñas o tokens temporales.  

**⚡ ejemploemplo**  
```hcl
resource "random_id" "server" {
  byte_length = 8 # Genera un ID de 8 bytes (16 caracteres hex)
}

# Uso en otro recurso:
resource "aws_instance" "servidor" {
  tags = {
    Name = "servidor-${random_id.server.hex}"
  }
}
```


---

## `provisioners` 

Los **`provisioners`** son bloques de código dentro de un **`resource`** que permiten ejecutar acciones **antes o después** de crear, actualizar o destruir un recurso. Se usan para tareas como:  
- Instalar software en una VM recién creada.  
- Copiar archivos de configuración.  
- ejecutar scripts locales o remotos.  

👉 **Importante**: Terraform recomienda usarlos **solo cuando no hay otra alternativa** (prefiera herramientas como **Ansible, Packer o cloud-init**).  


```hcl
provisioner "tipo_provisioner" {
  argumento1 = valor1
  ...
}
```

---

**Tipos de provisioners

### 📍 `local-exec` (ejecución Local) 

ejemploecuta comandos o scripts **en la máquina donde se está ejemploecutando Terraform** (no en el recurso creado).  

**📌 Casos de Uso**  
✅ ejecutar scripts de post-provisionamiento (ejemplo: notificaciones Slack, backups).  
✅ Generar archivos locales basados en outputs de Terraform.  

#### **⚡ ejemploemplo**  
```hcl
resource "aws_instance" "mi_servidor" {
  ami           = "ami-123456"
  instance_type = "t2.micro"

  # ejemploecuta un comando local después de crear la instancia
  provisioner "local-exec" {
    command = "echo 'Servidor ${self.public_ip} creado' >> servidores.log"
  }
}
```

---

### 🌐 `remote-exec` (ejecución Remota vía SSH/WinRM)

ejemploecuta comandos **directamente en el recurso recién creado** (ejemplo: una VM en AWS, Azure o GCP). Usa **SSH (Linux) o WinRM (Windows)**.  

 **📌 Casos de Uso**  
✅ Instalar paquetes (ejemplo: `apt-get install nginx`).  
✅ Configurar servicios o aplicaciones.  

**⚡ ejemploemplo**  
```hcl
resource "aws_instance" "web" {
  ami           = "ami-123456"
  instance_type = "t2.micro"
  key_name      = "mi-key-ssh"

  # Configura conexión SSH
  connection {
    type        = "ssh"
    user        = "ubuntu"
    private_key = file("~/.ssh/id_rsa")
    host        = self.public_ip
  }

  # ejemploecuta comandos en la VM remota
  provisioner "remote-exec" {
    inline = [
      "sudo apt-get update",
      "sudo apt-get install -y nginx",
      "sudo systemctl start nginx"
    ]
  }
}
```

---

### 📂 `file` (Copia de Archivos)

**¿Qué hace?**  
Copia archivos **desde tu máquina local al recurso remoto** (útil para enviar configuraciones, scripts o certificados).  

**📌 Casos de Uso**  
✅ Subir archivos de configuración (ejemplo: `nginx.conf`).  
✅ Enviar scripts para su ejecución remota.  

**⚡ ejemploemplo**  

```hcl
resource "aws_instance" "app_server" {
  ami           = "ami-123456"
  instance_type = "t2.micro"

  connection {
    type     = "ssh"
    user     = "ubuntu"
    private_key = file("~/.ssh/id_rsa")
    host     = self.public_ip
  }

  # Copia un archivo local al servidor remoto
  provisioner "file" {
    source      = "config/app.conf"
    destination = "/home/ubuntu/app.conf"
  }
}
```

---

**⚠️ Consideraciones Clave**  
- **Fragilidad**: Si un `provisioner` falla, el recurso se marca como **`tainted`** (requiere reprovisionamiento).  
- **Alternativas recomendadas**:  
  - Usar **imágenes preconfiguradas** (Packer).  
  - Gestión de configuración **post-Terraform** (Ansible, Chef).  

---


## 📌 `outputs` 

Los **`outputs`** en Terraform son valores que se exponen al finalizar la ejecución de un plan o apply. Permiten:  
- **Mostrar información importante** (ejemploemplo: IPs, URLs, IDs de recursos).  
- **Compartir datos entre módulos**.  
- **Ser consumidos por otros proyectos o scripts externos**.  

👉 **Key Point**: No modifican la infraestructura, solo **exportan datos**.  


```hcl
output "nombre_output" {
  value       = expresion
  description = "Descripción opcional"
  sensitive   = true/false  # Opcional (oculta el valor en logs)
}
```

---

**🔍 Tipos de Outputs**  

1. **Outputs simples**: Valores directos (strings, números, listas).  
2. **Outputs sensibles**: Datos ocultos (contraseñas, tokens).  
3. **Outputs condicionales**: Valores que dependen de una condición.  

---

### ⚡ Ejemplos Prácticos

**1. Output Básico (IP Pública de una VM)**  

```hcl
resource "aws_instance" "web" {
  ami           = "ami-123456"
  instance_type = "t2.micro"
}

output "public_ip" {
  value       = aws_instance.web.public_ip
  description = "La IP pública del servidor web"
}
```

**Resultado al aplicar**:  
```bash
Apply complete! Outputs:
public_ip = "54.210.120.45"
```

---

**2. Output Sensible (Contraseña de una BD)**  

```hcl
resource "aws_db_instance" "database" {
  password = "supersecreto123"
}

output "db_password" {
  value       = aws_db_instance.database.password
  sensitive   = true  # Oculta el valor en logs/pantalla
  description = "Contraseña de la base de datos (sensible)"
}
```

**Resultado**:  

```bash
Apply complete! Outputs:
db_password = <sensitive>
```

---

**3. Output con Dependencia (URL de un Balanceador)**  

```hcl
resource "aws_lb" "app_lb" {
  name               = "app-load-balancer"
  internal           = false
  load_balancer_type = "application"
}

output "lb_url" {
  value       = "https://${aws_lb.app_lb.dns_name}"
  description = "URL pública del balanceador de carga"
}
```

**Resultado**:  

```bash
lb_url = "https://app-load-balancer-1234567890.us-east-1.elb.amazonaws.com"
```

---

**4. Output de Lista (IPs de Múltiples Servidores)**  

```hcl
resource "aws_instance" "servers" {
  count         = 3
  ami           = "ami-123456"
  instance_type = "t2.micro"
}

output "servers_ips" {
  value       = aws_instance.servers[*].public_ip
  description = "Lista de IPs de los servidores"
}
```

**Resultado**:  

```bash
servers_ips = ["54.210.120.45", "54.210.120.46", "54.210.120.47"]
```

---

### 🎯 Usos Avanzados de Outputs 

**📌 Consumir Outputs en Otros Módulos**  

```hcl
# Módulo padre (main.tf)
module "network" {
  source = "./modules/network"
}

output "vpc_id" {
  value = module.network.vpc_id
}
```

**📌 Guardar Outputs en un Archivo**  

```bash
terraform output -json > outputs.json
```

---

### Buenas Prácticas

- **Siempre añade `description`**: Documenta para qué sirve el output.  
- **Usa `sensitive = true`** para datos críticos.  
- **Evita exponer información confidencial**: Usa servicios como AWS Secrets Manager.  

---


## `triggers`

Los **`triggers`** son argumentos usados principalmente en el recurso `null_resource` para **controlar cuándo se debe volver a ejecutar** un [[#`provisioners`|provicionador]] o recurso. Definen una dependencia de valores que, al cambiar, fuerzan la recreación del recurso.  

**🔍 Estructura Básica**:

```hcl
resource "null_resource" "ejemploemplo" {
  triggers = {
    clave1 = valor1  # Puede ser cualquier valor (timestamp, ID, etc.)
    clave2 = valor2
  }

  provisioner "local-exec" {
    command = "echo 'Trigger activado'"
  }
}
```

**📌 Casos de Uso**:

✅ **Forzar la ejecución en cada `apply`**: 

```hcl
triggers = {
  siempre = timestamp()  # Cambia en cada ejecución
}
```  

✅ **Reaccionar a cambios en otros recursos**:  

```hcl
triggers = {
  instancia_id = aws_instance.servidor.id  # Si el ID cambia, se recrea
}
```  

**⚡ ejemploemplo Práctico**:

```hcl
resource "null_resource" "actualizar_script" {
  triggers = {
    hash = filemd5("${path.module}/script.sh")  # Si el hash del archivo cambia, se ejemploecuta
  }

  provisioner "local-exec" {
    command = "bash ${path.module}/script.sh"
  }
}
```

---


## `depends_on`

El argumento **`depends_on`** establece **dependencias explícitas** entre recursos, módulos o datos, incluso cuando no hay referencias directas entre ellos. Terraform lo usa para determinar el orden de creación/destrucción.  

**🔍 Estructura Básica**:

```hcl
resource "recurso_a" "ejemploemplo" {
  # Configuración...
}

resource "recurso_b" "ejemploemplo" {
  depends_on = [recurso_a.ejemploemplo]  # Espera a que recurso_a esté creado
}
```

**📌 Casos de Uso**:

✅ **Dependencias implícitas no detectadas**: 

```hcl
resource "aws_instance" "servidor" {
  depends_on = [aws_iam_role.ejemploemplo]  # Espera a que el rol IAM exista
}
```  

✅ **Órdenes complejemploos**:  

```hcl
module "red" {
  # ...
}

resource "aws_instance" "app" {
  depends_on = [module.red]  # Espera a que el módulo de red termine
}
```

**⚠️ Importante**:  
- Usa `depends_on` **solo cuando sea necesario** (Terraform detecta la mayoría de dependencias automáticamente).  
- Puede ralentizar el despliegue si se abusa.  


**⚡ ejemploemplo Práctico**:
```hcl
resource "aws_s3_bucket" "datos" {
  bucket = "mi-bucket-de-datos"
}

resource "aws_instance" "procesador" {
  ami           = "ami-123456"
  instance_type = "t2.micro"
  depends_on    = [aws_s3_bucket.datos]  # Asegura que el bucket exista primero
}
```



## 📚 `data`

En Terraform, los bloques **`data`** permiten **obtener información de recursos ya existentes** (en tu infraestructura o en proveedores externos) para usarla en tu configuración. A diferencia de los recursos (`resource`), que **crean** infraestructura, los `data` solo **leen** información existente.

---

 **📌 ¿Para qué sirve `data`?**
1. **Consultar recursos existentes** (ejemplo: una VPC, una imagen de máquina, un grupo de seguridad).
2. **Obtener información de APIs externas** (ejemplo: AWS, GitHub, Cloudflare).
3. **Leer archivos locales o información del sistema** (ejemplo: contenido de un archivo JSON, IP pública).
4. **Evitar hardcodear valores** (usar datos dinámicos en lugar de estáticos).


**📌 Tipos de `data`**  

1. **Data Sources de Proveedores** (AWS, Azure, GitHub, etc.).  
2. **Archivos Locales** (`local_file`, `templatefile`).  
3. **Programas Externos** (`external`). 
4. **APIs y Secrets** (Vault, Secrets Manager).  

---

**📌 Sintaxis Básica**
```go
data "tipo_de_dato" "nombre_logico" {
  # Argumentos de búsqueda/filtrado
  argumento1 = valor1
  argumento2 = valor2
}

# ejemploemplo de uso:
output "ejemploemplo" {
  value = data.tipo_de_dato.nombre_logico.atributo
}
```

---

 **📌 Ejemplos Prácticos**

**1. Consultar una AMI en AWS**

```go
data "aws_ami" "ubuntu" {
  most_recent = true
  owners      = ["099720109477"] # Canonical (dueño oficial de Ubuntu)

  filter {
    name   = "name"
    values = ["ubuntu/images/hvm-ssd/ubuntu-focal-20.04-amd64-server-*"]
  }
}

# Uso en un recurso:
resource "aws_instance" "servidor" {
  ami           = data.aws_ami.ubuntu.id  # Usa la AMI encontrada
  instance_type = "t2.micro"
}
```

**2. Leer un archivo local (JSON, YAML, texto)**

```go
data "local_file" "config" {
  filename = "${path.module}/config.json"
}

# Usar el contenido en otro recurso:
resource "aws_s3_bucket_object" "upload" {
  bucket = "mi-bucket"
  key    = "config.json"
  content = data.local_file.config.content
}
```

**3. Obtener información de GitHub (ejemplo: repositorios)**

```go
data "github_repository" "terraform" {
  full_name = "hashicorp/terraform"
}

output "repo_info" {
  value = {
    stars  = data.github_repository.terraform.stargazers_count
    url    = data.github_repository.terraform.html_url
  }
}
```

---

## **📌 Diferencia entre `data` y `resource`**
| **Característica**  | **`resource`** | **`data`** |
|---------------------|---------------|------------|
| **Propósito**       | Crear recursos | Leer recursos existentes |
| **Efecto en la infraestructura** | Hace cambios (create/update/delete) | Solo consulta (no modifica) |
| **ejecución** | Se aplica con `terraform apply` | Se resuelve en tiempo de plan/apply |
| **Recomendación** | Usar para gestionar infraestructura | Usar para obtener datos de referencia |

---

**📌 Atributos de los `data`**

Cada `data` devuelve atributos específicos según su tipo. Puedes consultarlos en la **documentación oficial del proveedor** (ejemplo: [AWS Data Sources](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources)).

**Ejemplo** (AMI de AWS)

```go
output "ami_details" {
  value = {
    id      = data.aws_ami.ubuntu.id
    name    = data.aws_ami.ubuntu.name
    owner   = data.aws_ami.ubuntu.owners
  }
}
```

---

### **📌 Casos de Uso Avanzados**

**1. Filtrar recursos con `tags`**

```go
data "aws_vpc" "prod" {
  tags = {
    Environment = "Production"
  }
}
```

**2. Generar datos dinámicos con `template_file` (heredado, ahora se usa `templatefile`)**

```go
data "template_file" "user_data" {
  template = file("${path.module}/user-data.sh")
  vars = {
    db_host = aws_db_instance.mydb.address
  }
}
```

**3. Leer secretos de AWS Secrets Manager**

```go
data "aws_secretsmanager_secret_version" "db_password" {
  secret_id = "prod/db/password"
}

# Uso en un recurso RDS:
resource "aws_db_instance" "mydb" {
  password = data.aws_secretsmanager_secret_version.db_password.secret_string
}
```

**📌 Buenas Prácticas**

1. Usa `data` para evitar hardcodear valores (ejemplo: AMIs, IDs de VPCs).
2. **Verifica errores**: Algunos `data` pueden fallar si el recurso no existe.
3. Combínalo con `depends_on` si hay dependencias implícitas:

```go
data "aws_subnet" "example" {
depends_on = [aws_vpc.main] # Espera a que la VPC exista
}
```

---

### **📌 `data "external"` (Programas Externos)**  

Permite **ejecutar un script o comando externo** (Python, Bash, etc.) y usar su salida (JSON) en Terraform.  

🔹 **Sintaxis Básica**  
```go
data "external" "nombre_logico" {
  program = ["python", "ruta/script.py"]  # Comando a ejecutar  
  query   = {                            # Datos de entrada (opcional)  
    parametro1 = "valor1"  
  }  
}  

# Uso:  
output "resultado" {  
  value = data.external.nombre_logico.result  
}  
```  


🔹 **Ejemplo Práctico**  

**Script Python (`get_metadata.py`)**  
```python
#!/usr/bin/env python  
import json, sys  

input_data = json.load(sys.stdin)  # Lee entrada de Terraform  
output = {  
    "ami_id": "ami-12345678",  
    "region": "us-east-1"  
}  
print(json.dumps(output))  # Devuelve JSON  
```  

**En Terraform** 

```go
data "external" "metadata" {  
  program = ["python", "get_metadata.py"]  
  query   = { environment = "production" }  # Opcional  
}  

resource "aws_instance" "servidor" {  
  ami           = data.external.metadata.result["ami_id"]  
  instance_type = "t2.micro"  
}  
```  

🔹 **Atributos Clave**  

| Atributo  | Descripción |  
|-----------|-------------|  
| `program` | Lista del comando + argumentos (ej: `["bash", "script.sh"]`). |  
| `query`   | Mapa de datos enviados al script (se convierte en JSON). |  
| `result`  | Salida JSON del script (accesible como mapa). |  

---  

**📌 Casos de Uso para `data "external"`**  
1. **Obtener metadatos dinámicos** (ej: última AMI desde una API personalizada).  
2. **Procesar datos complejos** (ej: generar configuraciones con Python).  
3. **Integrar herramientas sin proveedor oficial** (ej: scripts legacy).  

⚠️ **Buenas Prácticas**  
- **El script debe ser determinista** (misma entrada → misma salida).  
- **Evita usar para secrets**, ya que la salida se guarda en el estado.  
- **Prefiere datasources nativas** (ej: `aws_ami`) cuando sea posible.  

---  

**Ejemplo Avanzado (Bash):**  
```go
data "external" "current_ip" {  
  program = ["bash", "-c", "echo '{\"ip\": \"'$(curl -s ifconfig.me)'\"}'"]  
}  

output "mi_ip" {  
  value = data.external.current_ip.result.ip  
}  
```  


---

# `local-exec`


El `provisioner` `local-exec` es una herramienta poderosa en Terraform que permite **ejecutar comandos o scripts directamente en la máquina donde se está ejecutando Terraform** (no en los recursos creados). Es especialmente útil para:

- Automatizar tareas posteriores a la creación de recursos (post-provisioning).
- Ejecutar scripts de configuración, backups o validaciones.
- Integrar Terraform con otras herramientas CLI o APIs locales.

**¿Cuándo usarlo?**
- Cuando necesitas ejecutar acciones que Terraform no soporta nativamente.
- Para complementar la infraestructura con configuraciones personalizadas.
- En workflows donde necesitas interactuar con el sistema local (archivos, variables de entorno, etc.).

---

La sintaxis básica dentro de un recurso (usualmente `null_resource`) es:

```go
resource "null_resource" "ejemplo" {
  provisioner "local-exec" {
    command = "echo 'Hola Mundo'"  # Comando a ejecutar
  }
}
```

**Componentes Clave:**
1. **`null_resource`**: Recurso "vacío" que sirve como contenedor para los `provisioners`.
2. **`provisioner "local-exec"`**: Bloque que define la ejecución local.
3. **`command`**: Parámetro obligatorio con el comando a ejecutar.


---

### `command` (Obligatorio)
Define el comando o script que se ejecutará en el sistema local.

**Características:**
- Puede ser un comando simple (`"ls -la"`) o un script multilínea (usando heredoc).
- Soporta interpolación de variables de Terraform (`${var.nombre}`).
- Se ejecuta en el shell del sistema (Bash en Linux, CMD/PowerShell en Windows).

**Ejemplo Detallado:**
```go
provisioner "local-exec" {
  command = <<-EOT
    # Script Bash que usa variables de Terraform
    echo "Creando archivo en ${path.module}"
    touch "${path.module}/config.txt"
    echo "IP del servidor: ${aws_instance.web.private_ip}" >> config.txt
  EOT
}
```
> 📌 **Nota:** El heredoc (`<<-EOT`) permite escribir scripts multilínea con indentación.

---

### `working_dir` (Opcional)
Controla **el directorio de trabajo** desde donde se ejecuta el comando.

**Valores posibles:**

| Valor | Descripción | Ejemplo de Uso |
|-------|-------------|----------------|
| `path.cwd` | Directorio donde se ejecutó `terraform apply` | Acceder a archivos en el contexto de invocación |
| `path.root` | Raíz del proyecto Terraform | Usar configuraciones globales |
| `path.module` | Directorio del módulo actual | Scripts modulares |
| Ruta absoluta | Directorio específico | Integración con rutas fijas |

**Ejemplo Contextual:**

```go
provisioner "local-exec" {
  command     = "./init.sh"  # Busca init.sh en el working_dir
  working_dir = "${path.module}/scripts"  # Ejecuta desde /módulo/scripts/
}
```

---

### `environment` (Opcional)
Define **variables de entorno** temporales para el comando.

**Características:**
- Útiles para pasar información sensible o dinámica.
- Se combinan con las variables del sistema existentes.
- Pueden referenciar otros recursos de Terraform.

**Ejemplo Avanzado:**

```go
provisioner "local-exec" {
  command     = "echo $DB_HOST > connection.txt"
  environment = {
    DB_HOST = aws_db_instance.main.address  # Usa la IP de la BD
    ENV     = terraform.workspace           # Dev/Prod
  }
  sensitive = true  # Oculta valores en los logs
}
```

---

### `interpreter` (Opcional)
Especifica **cómo se interpreta el comando** (útil para lenguajes no Bash).

**Casos de Uso Comunes:**

| Intérprete | Configuración | Descripción |
|------------|---------------|-------------|
| Bash | `["/bin/bash", "-c"]` | Fuerza ejecución en Bash |
| Python | `["python3", "-c"]` | Ejecuta código Python inline |
| PowerShell | `["pwsh", "-Command"]` | Para scripts en Windows |

**Ejemplo con Python:**

```go
provisioner "local-exec" {
  interpreter = ["python3", "-c"]
  command     = "print('Desde Python:', ${var.region})"
}
```

---

### `when` (Opcional)
Controla **cuándo se ejecuta** el `provisioner`.

**Valores posibles:**
- `create` (default): Solo en `terraform apply`.
- `destroy`: Solo en `terraform destroy`.

**Ejemplo para Limpieza:**

```go
provisioner "local-exec" {
  when    = destroy
  command = "rm -rf ${path.module}/tmp/*"  # Limpia archivos al destruir
}
```

---

### Ejemplos Prácticos

**Ejemplo 1: Configuración Post-Instalación**

```go
resource "aws_instance" "web" {
  ami           = "ami-123456"
  instance_type = "t2.micro"
}

resource "null_resource" "setup" {
  # Espera a que la instancia esté activa
  depends_on = [aws_instance.web]

  provisioner "local-exec" {
    command = <<-EOT
      ssh -i ~/.ssh/key.pem ubuntu@${aws_instance.web.public_ip} '
        sudo apt update && sudo apt install -y nginx
      '
    EOT
  }
}
```

**Ejemplo 2: Backup en Destroy

```go
resource "null_resource" "backup" {
  provisioner "local-exec" {
    when    = destroy
    command = "tar -czf backup-$(date +%s).tar.gz ${path.module}/data"
  }
}
```

**Ejemplo 3: Validación con Variables**

```go
provisioner "local-exec" {
  command = <<-EOT
    if [ "${var.environment}" != "prod" ]; then
      echo "ERROR: Solo válido en producción" >&2
      exit 1
    fi
    ./deploy-prod.sh
  EOT
}
```

---


# Tipos de variables

## Variables (Input Variables)
- **Propósito**: Son parámetros de entrada para tu configuración de Terraform.
- **Definición**: Se declaran en archivos `.tf` con el bloque `variable`.
- **Características**:
  - Permiten personalizar la infraestructura sin modificar el código
  - Pueden tener valores por defecto o ser requeridas
  - Se pueden pasar mediante archivos `.tfvars`, variables de entorno o prompts

**Ejemplo**:
```python
variable "instance_type" {
  description = "Tipo de instancia EC2"
  type        = string
  default     = "t2.micro"
}
```

**Uso**: Se accede con `var.instance_type`

## Locals (Local Values)

- **Propósito**: Son valores intermedios para simplificar expresiones complejas.
- **Definición**: Se declaran con el bloque `locals` (puede contener múltiples valores).
- **Características**:
  - Sólo son visibles dentro del módulo donde se definen
  - Útiles para evitar repetición de código
  - Pueden depender de variables, recursos y otros locals

**Ejemplo**:
```python
locals {
  common_tags = {
    Owner       = "DevOps"
    Environment = var.environment
  }
  
  instance_name = "${var.project_name}-${var.environment}"
}
```

**Uso**: Se accede con `local.common_tags`

## Outputs

- **Propósito**: Exponer información sobre la infraestructura creada.
- **Definición**: Se declaran con el bloque `output`.
- **Características**:
  - Permiten mostrar información después de `terraform apply`
  - Útiles para pasar información entre módulos
  - Pueden ser consultados con `terraform output`

**Ejemplo**:

```python
output "instance_public_ip" {
  description = "IP pública de la instancia EC2"
  value       = aws_instance.server.public_ip
  sensitive   = false
}
```

## Comparativa

| Característica       | Variables (Input)       | Locals                  | Outputs                 |
|----------------------|-------------------------|-------------------------|-------------------------|
| **Dirección de flujo** | Entrada                | Interno                | Salida                 |
| **Alcance**          | Módulo o padre          | Sólo módulo actual     | Módulo o padre         |
| **Mutabilidad**      | Configurable           | Calculado una vez      | Resultado de recursos  |
| **Acceso**           | `var.nombre`           | `local.nombre`         | `module.nombre.output` |
| **Principal uso**    | Parametrización        | Simplificar código     | Mostrar resultados     |

## Ejemplo Integrado

```go
# variables.tf
variable "region" {
  type    = string
  default = "us-east-1"
}

variable "env" {
  type    = string
  default = "dev"
}

# main.tf
locals {
  bucket_name = "myapp-${var.env}-assets"
  standard_tags = {
    Environment = var.env
    ManagedBy   = "Terraform"
  }
}

resource "aws_s3_bucket" "assets" {
  bucket = local.bucket_name
  tags   = local.standard_tags
}

# outputs.tf
output "bucket_arn" {
  value = aws_s3_bucket.assets.arn
}

output "bucket_name" {
  value = local.bucket_name
}
```


# `local_file`


El recurso `local_file` es parte del **proveedor Local** de Terraform y permite gestionar archivos en el sistema de archivos local donde se ejecuta Terraform. Vamos a desglosarlo completamente:


**Proveedor Requerido**

Primero, necesitas declarar el proveedor (generalmente en `provider.tf` o `main.tf`):

```python
terraform {
  required_providers {
    local = {
      source = "hashicorp/local"
      version = "2.4.0" # Revisa la última versión disponible
    }
  }
}

provider "local" {
  # No requiere configuración especial
}
```

**Estructura Básica del Recurso**

```python
resource "local_file" "nombre_recurso" {
  filename             = "ruta/al/archivo.ext"
  content             = "Contenido del archivo"
  directory_permission = "0755"    # Opcional
  file_permission     = "0644"     # Opcional
  sensitive_content   = false      # Opcional
}
```

### `filename` (Obligatorio)

- **Tipo**: String (cadena de texto)
- **Descripción**: Ruta absoluta o relativa donde se creará el archivo.
- **Ejemplo**:
  ```python
  filename = "/home/usuario/config.ini"  # Ruta absoluta (Linux)
  filename = "C:\\Windows\\Temp\\config.ini"  # Ruta absoluta (Windows)
  filename = "configuracion.json"  # Ruta relativa (se creará en el directorio de trabajo)
  ```

### `content` (Obligatorio)

- **Tipo**: String
- **Descripción**: Contenido que tendrá el archivo. Puede ser texto plano, JSON, XML, etc.
- **Alternativas**: En lugar de `content`, puedes usar:
  - `source`: Para copiar un archivo existente
  - `content_base64`: Para contenido en formato base64
- **Ejemplo Complejo**:
  ```python
  content = <<-EOT
    # Configuración generada por Terraform
    [database]
    host = "${var.db_host}"
    port = ${var.db_port}
    user = "admin"
  EOT
  ```

###  `file_permission` (Opcional)
- **Tipo**: String en notación octal
- **Descripción**: Permisos del archivo (sistemas Unix-like). Por defecto es "0777" (sin máscara umask).
- **Ejemplo**:
  ```python
  file_permission = "0600"  # Solo el propietario puede leer/escribir
  ```

### 4. `directory_permission` (Opcional)
- **Tipo**: String en notación octal
- **Descripción**: Permisos para directorios creados automáticamente. Por defecto "0777".
- **Ejemplo**:
  ```python
  directory_permission = "0755"  # Propietario: rwx, Grupo/Others: rx
  ```

### 5. `sensitive_content` (Opcional)
- **Tipo**: Boolean
- **Descripción**: Si es `true`, el contenido no se mostrará en los logs de Terraform.
- **Ejemplo**:
  ```python
  sensitive_content = true  # Para contraseñas o datos sensibles
  ```

## Atributos de Salida (Outputs)

Después de crear el recurso, puedes acceder a:

- `id`: Ruta completa del archivo (igual que filename)
- `content`: Contenido del archivo (útil para outputs)
- `content_base64`: Contenido en base64

**Ejemplo de output**:
```python
output "file_content" {
  value = local_file.config.content
  sensitive = true  # Si contiene información sensible
}
```

## Ejemplos

**Ejemplo 1: Archivo de Configuración Dinámico**

```python
variable "db_config" {
  type = object({
    host = string
    port = number
    user = string
  })
  default = {
    host = "db.example.com"
    port = 5432
    user = "admin"
  }
}

resource "local_file" "db_config" {
  filename = "${path.module}/config/database.ini"  # path.module da la ruta del módulo actual
  content = <<-EOT
    [database]
    host = "${var.db_config.host}"
    port = ${var.db_config.port}
    username = "${var.db_config.user}"
    # Comentario generado el ${timestamp()}  # Función de timestamp
  EOT
  file_permission = "0600"
}
```

**Ejemplo 2: Archivo JSON Generado**

```python
resource "local_file" "app_config" {
  filename = "config.json"
  content = jsonencode({
    app_name = "My Terraform App"
    features = ["auth", "logging", "monitoring"]
    settings = {
      debug_mode = false
      timeout   = 30
    }
  })
}
```

### Ejemplo 3: Script Bash con Permisos Ejecutables

```python
resource "local_file" "setup_script" {
  filename        = "setup.sh"
  file_permission = "0755"  # Permisos de ejecución
  content = <<-EOT
    #!/bin/bash
    echo "Instalando aplicación..."
    apt-get update
    apt-get install -y ${join(" ", var.packages)}
    systemctl start ${var.service_name}
  EOT
}
```

## Consideraciones Importantes

1. **Idempotencia**: Terraform sobrescribirá el archivo si cambia el contenido o los permisos.

2. **Sensibilidad de Datos**:
   ```python
   resource "local_file" "secret" {
     filename           = "secret.txt"
     content            = var.sensitive_data
     sensitive_content  = true  # No se mostrará en logs
     file_permission    = "0400"  # Solo lectura para propietario
   }
   ```

3. **Dependencias Implícitas**: Puedes forzar dependencias con `depends_on`:
   ```python
   resource "local_file" "final_config" {
     filename = "final.config"
     content  = "IP: ${aws_instance.server.private_ip}"
     depends_on = [aws_instance.server]
   }
   ```

4. **Funciones Útiles**:
   - `file()`: Leer archivos existentes
   - `templatefile()`: Procesar plantillas
   - `jsonencode()`/`yamlencode()`: Generar formatos estructurados

