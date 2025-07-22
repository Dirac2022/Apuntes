
# Infraestructura para AWS


Creamos una carpeta llamada `Terraform`  con un archivo llamado  `terraform.tf`

Luego de aplicar `terraform init` se crea:

- El archivo `.terraform.locl.hcl`:
  - Contiene información sobre el proveedor. Guarda metadata importante
- La carpeta `.terraform/` con los archivos
  - `LICENTE.txt`
  - `terraform-provider-aws_v6.0.0-beta2_x5`
    - Contiene el binario que se ejecuta al momento de aplicar algun cambio


```python
terraform {
    # Especificamos la version de terraform que se va a usar
    required_version = ">=1.10"

    # Especificamos el provedor que terraform usara
    required_providers {
      aws = { # En este caso sera aws
        source = "hashicorp/aws" # Se detalla la fuente
        version = "6.0.0-beta2" # Y la version
      } # Esto se puede ver desde la propia documentacion de terraform
    } # En la parte de Providers: https://registry.terraform.io/browse/providers
}

# Se recomienda ver la documentacion de cada proveedor en la pagina de Terraform
provider "aws" {
    region = "us-east-1"
    version = "~> 5.0"
}
```

> [!warning] Por qué necesito especificar version en `required_providers` y luego también en `providers`


---

En AWS, un **CIDR block** (Classless Inter-Domain Routing block) es un rango de direcciones IP definido para asignar a recursos de red, como **VPCs (Virtual Private Clouds)**, subredes o grupos de seguridad.  

### 📌 **¿Qué es un CIDR?**  
CIDR es una notación que especifica un bloque de direcciones IP en formato:  
```
<dirección IP>/<prefijo>
```  
- **Ejemplo:** `10.0.0.0/16`  
  - `10.0.0.0` → Dirección de red base.  
  - `/16` → Máscara de subred (indica cuántos bits están reservados para la red).  

### 🔹 **CIDR en AWS**  
En AWS, los **CIDR blocks** se usan principalmente para:  
1. **Definir una VPC**:  
   - Al crear una VPC, debes asignarle un bloque CIDR (ej. `10.0.0.0/16`).  
   - Esto determina el rango de direcciones IP privadas disponibles dentro de la VPC.  

2. **Crear subredes (Subnets)**:  
   - Dentro de una VPC, puedes dividir el CIDR en subredes más pequeñas (ej. `10.0.1.0/24`).  
   - AWS permite subredes públicas (con acceso a Internet) y privadas (sin acceso directo).  

3. **Grupos de Seguridad (Security Groups) y ACLs de Red**:  
   - Puedes permitir/denegar tráfico basado en CIDR blocks (ej. `192.168.1.0/24`).  

### 📏 **Rangos comunes en AWS**  
- **VPC típica:** `10.0.0.0/16` (65,536 direcciones IP).  
- **Subred típica:** `10.0.1.0/24` (256 direcciones IP).  
- **AWS recomienda usar rangos RFC 1918** (privados):  
  - `10.0.0.0/8`  
  - `172.16.0.0/12`  
  - `192.168.0.0/16`  

### ⚠️ **Restricciones importantes**  
- El tamaño mínimo de un CIDR en una VPC es `/28` (16 IPs).  
- No puedes superponer CIDR blocks entre VPCs o con redes on-premise.  
- AWS reserva 5 IPs en cada subred (la primera y última + 3 para AWS).  

### 🔍 **Ejemplo práctico**  
Si defines una VPC con `10.0.0.0/16` y creas dos subredes:  
- **Subred pública:** `10.0.1.0/24` (IPs del `10.0.1.1` al `10.0.1.254`).  
- **Subred privada:** `10.0.2.0/24` (IPs del `10.0.2.1` al `10.0.2.254`).  

Esto permite organizar recursos (EC2, RDS, etc.) en redes lógicas dentro de AWS.  

---

## Creando nuestro primer recurso

Creamos un archivo m̀ain.tf` en la raíz del proyecto
```go
# Un recurso en terraform representa un recurso dentro
# del proveedor de nube, provedor SaaS, etc.

# Crea una vcp dentro de la cuenta de AWS
resource "aws_vpc" "example" {
  cidr_block = "10.0.0.0/16"
}
```

Ejecutamos `terraform plan`
Si obtenemos el error: `Planning failed. Terraform encountered an error while generating this plan` necesitamos autenticación.

```go
provider "aws" {
  region     = "us-west-2"
  access_key = "my-access-key"
  secret_key = "my-secret-key"
}
```

A continuación los pasos: [[Crear Credenciales]]

Luego, ejecutamos nuevamente `terraform plan`
Ahora deberíamos tener una salida similar: 

```sh
dirac@ubuntu:~/Documents/Self-Learning/Terraform/Terraform$ terraform plan

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # aws_vpc.example will be created
  + resource "aws_vpc" "example" {
      + arn                                  = (known after apply)
      + cidr_block                           = "10.0.0.0/16"
      + default_network_acl_id               = (known after apply)
      + default_route_table_id               = (known after apply)
      + default_security_group_id            = (known after apply)
      + dhcp_options_id                      = (known after apply)
      + enable_dns_hostnames                 = (known after apply)
      + enable_dns_support                   = true
      + enable_network_address_usage_metrics = (known after apply)
      + id                                   = (known after apply)
      + instance_tenancy                     = "default"
      + ipv6_association_id                  = (known after apply)
      + ipv6_cidr_block                      = (known after apply)
      + ipv6_cidr_block_network_border_group = (known after apply)
      + main_route_table_id                  = (known after apply)
      + owner_id                             = (known after apply)
      + region                               = "us-east-1"
      + tags_all                             = (known after apply)
    }

Plan: 1 to add, 0 to change, 0 to destroy.

──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.
dirac@ubuntu:~/Documents/Self-Learning/Terraform/Terraform$ 
```

Posteriormente ejecutamos `terraform apply` o `terraform apply -auto-approve`
- Se inicia un proceso de creación del recurso en el proveedor de la nube.
- Si nos vamos a nuestra cuenta de AWS se observar el recurso creado.
- Para ver la `vpc` creada debemos asegurarnos de estar en la región correcta. En nuestro caso `us-east-1`.


![[Pasted image 20250603215248.png]]


---

## Creando variables y outputs

- Las variables son parámetros de entrada, nos permiten configurar los recursos que tenemos. 
- Los outputs son parametros de salida. Nos permite obtener una salida de algun estado o información útil.

Creamos dos archivos: `variables.tf` y `outputs.tf`. 

```sh
dirac@ubuntu:~/Documents/Self-Learning/Terraform/Terraform$ terraform plan
var.cidr_block
  AWS VPC CIDR block

  Enter a value: 

```

Luego Terraform nos genera este plan:

```sh
  Enter a value: 20.0.0.0/16

aws_vpc.example: Refreshing state... [id=vpc-024cd98890eda02bb]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
-/+ destroy and then create replacement

Terraform will perform the following actions:

  # aws_vpc.example must be replaced
-/+ resource "aws_vpc" "example" {
      ~ arn                                  = "arn:aws:ec2:us-east-1:211125751902:vpc/vpc-024cd98890eda02bb" -> (known after apply)
      - assign_generated_ipv6_cidr_block     = false -> null
      ~ cidr_block                           = "10.0.0.0/16" -> "20.0.0.0/16" # forces replacement
      ~ default_network_acl_id               = "acl-02be4b6197d194ce7" -> (known after apply)
      ~ default_route_table_id               = "rtb-0aec5a9fbce0644dd" -> (known after apply)
      ~ default_security_group_id            = "sg-01fee1b92cf37dee0" -> (known after apply)
      ~ dhcp_options_id                      = "dopt-06472b8e4dd13983a" -> (known after apply)
      ~ enable_dns_hostnames                 = false -> (known after apply)
      ~ enable_network_address_usage_metrics = false -> (known after apply)
      ~ id                                   = "vpc-024cd98890eda02bb" -> (known after apply)
      + ipv6_association_id                  = (known after apply)
      + ipv6_cidr_block                      = (known after apply)
      + ipv6_cidr_block_network_border_group = (known after apply)
      - ipv6_netmask_length                  = 0 -> null
      ~ main_route_table_id                  = "rtb-0aec5a9fbce0644dd" -> (known after apply)
      ~ owner_id                             = "211125751902" -> (known after apply)
      - tags                                 = {} -> null
      ~ tags_all                             = {} -> (known after apply)
        # (4 unchanged attributes hidden)
    }

Plan: 1 to add, 0 to change, 1 to destroy.
```

Podemos luego elegir ejecutar los cambios con `terraform apply` y luego ingresar el valor del `cidr block` o también ingresar el valor directamente con

```sh
terraform apply -var cidr_block=10.20.0.0/16
```

Un problema que se presenta es que no sabemos en que `VPC` se ha creado el recurso (si tenemos más de una). Podemos usar un `output` para que se muestre el identificador del `VPC`

```go
// example es el nombre del recurso que definimos anteriormente
output "vpc_id" {
    value = aws_vpc.example.id
    description = "AWS VPC ID"
}
```

Al ejecutar nuevamente `terraform apply` al final de la salida obtenemos:

```sh
Apply complete! Resources: 1 added, 0 changed, 1 destroyed.

Outputs:

vpc_id = "vpc-00d25914cda3a04ba"
```

![[Pasted image 20250603215127.png]]
Vemos el recurso creado/modificado

---

Al ver la página de `Sus VPC` notamos que el atributo `Name` está vacío. No lo hemos definido.
Si agregamos una etiqueta (generalmente cada proveedor soporta esto)

```go
resource "aws_vpc" "main_vpc" {
  cidr_block = var.cidr_block
  tags = {
    Name = "Main VPC"
  }
}
```

Y aplicamos cambios:

![[Pasted image 20250603215825.png]]


---
## Dependencias
Algunos recursos dependen de otros. Debemos tener en cuenta que cambios en la infraestructura afectaran a ciertos recursos.

Por ejemplo, ya que tenemos el recurso `VPC`, podemos crear `subnets`. 
- Definimos variables para los `cidr blocks` de los `subnets` que vamos a agregar.

```go
variable "vpc_cidr_block" {
    type = string
    description = "AWS VPC CIDR block"
    default = "10.0.0.0/16"
}


variable "subnet_a_cidr_block" {
    type = string
    description = "AWS Subnet A CIDR block"
    default = "10.0.10.0/24"
}


variable "subnet_b_cidr_block" {
    type = string
    description = "AWS Subnet B CIDR block"
    default = "10.0.20.0/24"
}
```


- Luego en `main.tf`:

```go
resource "aws_vpc" "main_vpc" {
  cidr_block = var.vpc_cidr_block
  tags = {
    Name = "Main VPC"
  }
}

resource "aws_subnet" "subnet-a" {
  vpc_id     = aws_vpc.main_vpc.id
  cidr_block = var.subnet_a_cidr_block
  availability_zone = "us-east-1a"
  tags = {
    Name = "Subnet A"
  }
}


resource "aws_subnet" "subnet-b" {
  vpc_id     = aws_vpc.main_vpc.id
  cidr_block = var.subnet_b_cidr_block
  availability_zone = "us-east-1b"
  tags = {
    Name = "Subnet B"
  }
}
```



Al aplicar los cambios, vemos:

![[Pasted image 20250603223412.png]]

![[Pasted image 20250603223443.png]]

Para este ejemplo, no fue necesario definir explícitamente dependencia entre recursos, pero hay otros casos en los que si será necesario. Por ello siempre es recomendable seguir esta forma:

```go
resource "aws_subnet" "subnet-a" {
  vpc_id     = aws_vpc.main_vpc.id
  cidr_block = var.subnet_a_cidr_block
  availability_zone = "us-east-1a"
  
  tags = {
    Name = "Subnet A"
  }
// Aqui definimos la dependencia
  depends_on = [ aws_vpc.main_vpc ]
}
```


## Data Sources

Hacen referencia a un recurso ya creado el cual no necesariamente configuraremos mediante Terraform, pero lo utilizaremos al momento de configurar otro recurso dentro de la configuración de Terraform.

Por ejemplo, AWS ya nos crea un `aws_vpc` por defecto.

![[Pasted image 20250603224551.png]]

Haciendo uso de un data source podemos hacer referencia a ese recurso:

En un archivo `data.tf` a nivel de proyecto:

```go
data "aws_vpc" "default_vpc" {
    id = "vpc-0a6d9ae66e6681172"
}
```


Al ejecutar `terraform plan` vemos que nos aparece el recurso no gestionado por Terraform:

```sh
dirac@ubuntu:~/Documents/Self-Learning/Terraform/Terraform$ terraform plan
data.aws_vpc.default_vpc: Reading...
aws_vpc.main_vpc: Refreshing state... [id=vpc-018cfbf22e265e719]
data.aws_vpc.default_vpc: Read complete after 1s [id=vpc-0a6d9ae66e6681172] // Aqui
aws_subnet.subnet-a: Refreshing state... [id=subnet-03cd22c08e8b9c5da]
aws_subnet.subnet-b: Refreshing state... [id=subnet-042f80e6b7bede9f6]

No changes. Your infrastructure matches the configuration.

Terraform has compared your real infrastructure against your configuration and found no differences, so no changes are needed.
dirac@ubuntu:~/Documents/Self-Learning/Terraform/Terraform$ 
```

---

Podemos leer la información de un recurso, a través de otro identificador, por ejemplo, el `cidr_block`.

```go
data "aws_vpc" "default_vpc" {
    cidr_block = "172.31.0.0/16"
}
```

---

Ahora podemos crear una `subnet` usando este `vpc`

```go
resource "aws_subnet" "default_subnet" {
  vpc_id = data.aws_vpc.default_vpc.id
  cidr_block = "172.31.96.0/24" // No debe crear conflicto con otras subnets creadas
  tags = {
    Name = "Default Subnet"
  }
}
```

Al ejecutar `terraform apply` se crea el subnet:

```sh
Plan: 1 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

aws_subnet.default_subnet: Creating...
aws_subnet.default_subnet: Creation complete after 1s [id=subnet-05c284ae72938052d]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.

Outputs:

```

Vemos que el recurso se ha creado: 

![[Pasted image 20250603231041.png]]


## Modules

Los `modules` son contenedores para múltiples recursos que se usan juntos. Un modulo consisten que una colección de archivos `.tf` y `.tf.json` en un mismo directorio.

Generalmente los archivos que forman un módulo son:

- `main.tf`
- `variables.tf`
- `outputs.tf`
- `providers.tf`

### Creando un modulo

Crearemos un modulo para llamar a un recurso  `aws_instance`. 

En `main.tf

```go
resource "aws_instance" "module_instance" {
    ami = var.ami_id
    instance_type = "t2.micro"

    tags = {
        Name = var.instance_name
    }
}
```

En `variables.tf`

```go
variable "ami_id" {
    type = string
    description = "ID de la AMI para lanzar la instancia (por ejemplo, Amazon Linux 2)"
}

variable "instance_name" {
    type = string
    description = "Nombre que se asignará a la instancia"
    default = "Terraform-EC2"
}
```

En `outputs.tf`

```go
output "instance_id" {
    value = aws_instance.module_instance.id
}
```

Ahora para llamar a ese módulo en el `main.tf` principal

```go
module "my_instance" {
  source = "./ruta-al-modulo"
  // Al definir source nos saldra error porque debemos tambien definir las variables
  // que se encuentran en el modulo

  ami_id = "ami_0c02fb55956c7d316" # ami gratuita
  instance_name = "Mi instancia en AWS"
}
```


Una vez hecho esto, podemos ejecutar `terraform plan / terraform apply`. Sin embargo, es posible que obtengamos un error:

```sh
dirac@ubuntu:~/Documents/Self-Learning/Terraform/Terraform$ terraform plan
╷
│ Error: Module not installed
│ 
│   on main.tf line 42:
│   42: module "my_instance" {
│ 
│ This module is not yet installed. Run "terraform init" to install all modules required by this configuration.
╵
dirac@ubuntu:~/Documents/Self-Learning/Terraform/Terraform$ 

```

Esto se debe a que cada vez que usemos o llamemos a un modulo, este debe estar mapeado por Terraform, por lo que es posible que tenga que cargar algunas dependencias. Se soluciona ejecutando primero `terraform init`.