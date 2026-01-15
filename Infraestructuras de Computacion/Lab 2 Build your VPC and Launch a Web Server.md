

**Mitchel Soto Cuya**

## Task 1: Create Your VPC

Ingresé al servicio **VPC**

![[Pasted image 20250915215852.png]]

Validé que me encontraba en la región **N. Virginia (us-east-1)**

![[Pasted image 20250915220044.png]]

Luego procedí a **Crear la VPC**

- Cambié de `project` a `lab`
- Cambié la Zona de Disponibilidad a 1
- Mantuve el numero de subredes públicas y subredes privadas a 1
- Cambie los CIDR block para subredes publicas a `10.0.0.0/24` (esto me brinda 256-1 IP) y los CIDR block para subredes privadas a `10.0.1.0/24` (también me brinda 256-1 IP)
- Establecí NAT gateway a `1 AZ` y los VPC endpoints a `None` y mantuve los DNS hostaname y DNS resolution habilitados

![[Pasted image 20250915220847.png]]

Valide el **Preview panel** como me lo indicó la guía (todo conforme)

![[Pasted image 20250915221026.png]]

Todos los recursos fueron creados exitosamente

![[Pasted image 20250915221435.png]]

Finalmente:

![[Pasted image 20250915221809.png]]


## Task 2: Create Additional Subnets

Para crear subredes adicionales me fue a **Subnets** en el panel de la izquierda y le di click a **Create subnet**, el boton naranja de la derecha.

![[Pasted image 20250915222212.png]]

<h5>Para crear la segunda subred pública</h5>
- Ingresé el nombre de la subred como `lab-subnet-public2`
- Ingresé la segunda AZ como **us-east-1b**
- Definí el IPv4 subnet CIDR block como `10.0.2.0/24`

![[Pasted image 20250915222914.png]]

![[Pasted image 20250915223030.png]]


<h5>Para crear la segunda subred privada</h5>
Los pasos fueron similares a lo anterior

![[Pasted image 20250915223334.png]]

![[Pasted image 20250915223423.png]]


<h5>Configuración del Route Table</h5>
Primero voy a **Route tables** en el panel de la izquierda. Luego de actualizar las **route tables**

- Seleccione la **route table** `lab-rtb-private1-us-east-1a`

![[Pasted image 20250915224059.png]]

Para editar las **subnet associations**

- Mantuve `lab-subnet-private1-us-east-1a` seleccionado
- Seleccione adicionalmente `lab-subnet-private2`

![[Pasted image 20250915225305.png]]

Luego, al dar clic a **Save associations**:

![[Pasted image 20250915225443.png]]


**Para la configuración del Route Table en las subredes públicas**

- Seleccioné `lab-rtb-public` y deselecciono lo demás
- Validé que `Destination 0.0.0.0/0` se envía a `igw-07xxx`
- Seleccioné **Subnet associations**
- Fuí a **Edit subnet associations**
- Seleccioné `lab-subnet-public2`

![[Pasted image 20250915230056.png]]

Al dar clic a **Save associations**

![[Pasted image 20250915230204.png]]


## Task 3: Create a VPC Security Group

Para crear un **Grupo de seguridad**

- Fui a la opción **Security groups** en el panel izquierdo
- Di clic a **Create security group**

![[Pasted image 20250915230400.png]]

- Asigne el nombre a `Web Security Group`
- La descripción a: `Enable HTTP access`
- Elegí la VPC `lab-vpc`
- Definí las **Inbound rules** como indicaba la guía

![[Pasted image 20250915230743.png]]


Al dar clic a **Create security group**:

![[Pasted image 20250915230907.png]]

## Task 4: Launch a Web Server Instance

Para lanzar una instancia de servidor web

- Busqué **EC2** en **Services**
- Di clic a **Launch instance**

![[Pasted image 20250915231117.png]]

Seguí las indicaciones:

- Nombre: `Web Server 1`
- AMI: `Amazon Linux`
- Cree un **key pair name** llamado `labo-2`
- Configuré las **Network settings**

![[Pasted image 20250915232233.png]]

Para los **Advance details**, ingresé el siguiente script en bash

![[Pasted image 20250915232405.png]]

Al dar clic a **Launch instance**

![[Pasted image 20250915232508.png]]

Mi instancia EC2:

![[Pasted image 20250915232913.png]]


 Por ultimo, al copiar el **Public DNS** y pegarlo en una pestaña nueva:
 
![[Pasted image 20250915232840.png]]