
<h5>Mitchel Soto Cuya</h5>

## Task 1: Create a Security Group for the RDS DB Instance

- Busqué el servicio **VPC** en la caja de búsqueda
- Seleccioné **Security groups** en el panel lateral izquierdo
- Seleccioné el botón **Create security group**

![[Pasted image 20250927103329.png]]

Detallo las configuraciones que definí:
- **Security group name**: `DB security Group`
- **Description**: `Permit access from Web Security Group`
- **VPC**: `Lab VPC`
- **Inbound rules**
	- **Type**: `MySQL/Aurora`
	- **Source**: `Custom` / `Web Security Group sg ...`


![[Pasted image 20250927104043.png]]

## Task 2: Create a DB Subnet Group

- Busqué el servicio **RDS** en la caja de búsqueda
- Seleccioné **Security groups** en el panel lateral izquierdo
- Seleccioné el botón **Create DB Subnet Group**


![[Pasted image 20250927104536.png]]



Detallo las configuraciones que definí:
- **Name**: `DB-Subnet-Group`
- **Description**: `DB Subnet Group`
- **VPC**: `Lab VPC`
- **Add subnets**
	- `us-east-1a`
	- `us-east-1b`
	- **Subnets**
		- Private Subnet 1 `10.0.1.0/24`
		- Private Subnet 2 `10.0.3.0/24`

Procedí a crear el  **DB Subnet Group**

![[Pasted image 20250927105055.png]]

## Task 3: Create an Amazon RDS DB Instance


Para la creación de una instancia **Amazon RDS DB**

- Elegí el servicio **Aurora and RDS** en el cuadro de búsqueda
- Seleccioné **Databases** en el panel lateral izquierdo
- Seleccioné el botón **Create database**

![[Pasted image 20250927112926.png]]


Detallo las configuraciones que definí
- **Engine Options**: MySQL
- **Templates**: Dev/Test
- **Availability and durability**: Multi-AZ DB instance deployment (2 instances)


- **Settings**
	- **DB instance identifier**: `lab-db`
	- **Master username**: `main`
	- En **Credential management** seleccioné *Self managed* para activar el *Master password* y *Confirm password*
	- **Master password**: `lab-password`
	- **Confirm password**: `lab-password`

![[Pasted image 20250927120606.png]]


- En **Instance configuration** (según la guía es *DB instance class*)
	- Seleccioné `Burstable classes (includes t classes)`
	- Seleccioné `db.t3.micro`
- En **Storage**
	- **Storage type**: `General Purpose SSD (gp3)`
	- **Allocated storage** `20`
- En **Connectivity**
	- En **Virtual Private Cloud (VPC)**: `Lab VPC (vpc-...)`
	- En **Existing VPC security groups**
		- Seleccioné `DB Security Group`
		- Deseleccioné `default`

![[Pasted image 20250927115022.png]]

- En **Monitoring/Additional monitoring settings**
	- Deseleccioné **Enable Enhanced monitoring**

- En **Additional configuration** (debajo de la sección *Monitoring*)
	- **Initial database name**: `lab`
	- Deseleccioné **Enable automatic backups**
	- Deseleccioné **Enable encryption**

Finalmente, seleccioné el botón **Create database**

La base de datos se creó exitosamente:

![[Pasted image 20250927120709.png]]

- Después de esperar  a que la Base de Datos este habilitada la seleccioné y fui a la sección **Connectivity & Security** para copiar el campo **Endpoint**


![[Pasted image 20250927121220.png]]

## Task 4: Interact with Your Database


Siguiendo la guía en **AWS Details**, copie el **WebServer IP** y lo copié en una nueva pestaña del navegador:

- Me situé en la pestaña **RDS**

![[Pasted image 20250927121612.png]]

Apliqué las siguientes configuraciones
- **Endpoint**: `lab-db.c1i8kyqs6fmv.us-east-1.rds.amazonaws.com`
- **Database**: `lab`
- **Username**: `main`
- **Password**: `lab-password`

Luego seleccioné el botón **Submit**

Mensaje de salida: 

![[Pasted image 20250927121832.png]]

Para testear la aplicación web y que los datos persistan, ingrese mis datos en el **Address Book**:

![[Pasted image 20250927122345.png]]

**Laboratorio finalizado**

