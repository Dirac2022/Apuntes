# Despliegue de una Aplicación Web Simple en AWS

**Mitchel Soto Cuya**

## Parte 1: Configuración de Seguridad y Acceso (IAM) 

**1. Crear un Grupo IAM**

- Se creó un nuevo **User group** llamado `AdminsWeb`

![[Pasted image 20250929101853.png]]

**2. Crear Políticas IAM**

Se creó una **Política IAM** con las siguientes especificaciones:
- **Permissions**: EC2 (todo), VPC Endpoints (TODO)
	- VPC service tenía 3 opciones: `Endpoints`, `Lattice` y `Lattice Services`. Solo seleccioné `Endpoints`

![[Pasted image 20250929102856.png]]

![[Pasted image 20250929102937.png]]


**3. Adjuntar políticas al grupo**

- En **Policies** busqué la política recientemente creada `EC2AndVPCAccessPolicy`
- Seleccioné la política y en el menú **Actions** seleccioné **Attach**
- Seleccioné `AdminsWeb` el grupo al cual adjuntar la política

![[Pasted image 20250929103505.png]]

De la misma manera, se adjuntó la política `AmazonS3ReadOnlyAccess` al grupo `AdminsWeb` aunque fuera *opcional*

![[Pasted image 20250929103722.png]]


**4. Crear un usuario IAM**

- En **Users** seleccioné el botón **Create user**
- Definí **User name** como  `dev-web-admin`
- Seleccioné la casilla  **Provide user access to the AWS Management Console - optional**
- Seleccioné el *radio button* **I wan to create an IAM user** para tener acceso programático 

![[Pasted image 20250929104126.png]]

- Adjunté el usuario al grupo `AdminsWeb`

![[Pasted image 20250929104151.png]]

- Se guardaron las credenciales de acceso

![[Pasted image 20250929104616.png]]


## Parte 2: Configuración de Red (VPC, Subredes, Grupos de Seguridad) 

**1. Crear una VPC Personalizada**

- Se creo una VPC con nombre: `MiVPCWeb` y bloque CIDR: `10.0.0.0/16`

![[Pasted image 20250929111803.png]]


**2. Crear Subredes**

- Se creó una subnet pública
	- nombre: `PublicSubnet-AZ1`
	- bloque CIDR: `10.0.1.0/24`
	- Zona de disponibilidad: `us-east-1a`
![[Pasted image 20250929112040.png]]

- Se creo una subnet privada:
	- nombre: `PrivateSubnet-AZ1`
	- bloque CIDR: `10.0.2.0/24`
	- Zona de disponibilidad: `us-east-1a`

![[Pasted image 20250929112310.png]]

**3. Crear Internet Gateway (IGW)**

- Se creo el IGW con nombre: `My-Internet-Gateway`

![[Pasted image 20250929112508.png]]

- Se adjunto al VPC `MiVPCWeb`

![[Pasted image 20250929112534.png]]


**4. Configurar Tablas de Rutas**

- En **Route tables** seleccioné la correspondiente a `MiVPCWeb`
- En la pestaña **Routes** seleccioné el botón **Edit routes**
![[Pasted image 20250929113245.png]]

- Procedí a añadir una **ruta**
	- **Destination** `0.0.0.0/0`
	- **Target**: `Internet Gateway` (el que acabo de crear)

![[Pasted image 20250929113514.png]]

**5. Crear Grupo de Seguridad (Security Group)**

- Se creó un nuevo **Security Group** con nombre: `WebSG`
- Descripción: `Security group para Web Server PC1`
- Se creó dentro del VPC: `MiVPCWeb`
- Para las **Inbound rules**
	- SSH 
	- HTTP
	- HTTPS
- Para las **Outbound rules**
	- Todo el tráfico saliente

![[Pasted image 20250929114114.png]]

## Parte 3: Despliegue de Instancia EC2 y Almacenamiento EBS

**1. Lanzar instancia EC2**

Lancé la instancia EC2 con las siguientes específicaciones

- Nombre: `Mi-EC2-Web`
- AMI: Por efecto `Amazon Linux`
- Tipo de instancia: Por defecto `t3.micro`. (ya no se encuentra habilitada t2.micro)
- Configuraciones de red
	- Red: `MiVPCWeb`
	- Subred: `PublicSubnet-AZ1`
	- Habilite la asignación automática de IP

![[Pasted image 20250929115006.png]]

- Se creo el **key pair (logging): `web-key-pair`
- Se creó el nuevo volumen EBS con 2 GB y topo `gp2`

![[Pasted image 20250929115725.png]]


**2. Conectarse a la instancia EC2**

Me conecte mediante SSH. Consideraciones
- Use una IP publica, ya que con la privada tuve problemas

![[Pasted image 20250929121226.png]]

**3. Configurar el Servidor Web y Montar EBS**

Ejecuté los comandos de la guía para:
- Actualizar paquetes
- Instalar Apache

![[Pasted image 20250929121534.png]]

- Iniciar y habilitar Apache

![[Pasted image 20250929121653.png]]

- Cree una página web simple

![[Pasted image 20250929122039.png]]

- Monté el volumen EBS adicional
	- Identifique el nuevo volumen, nombre: `nvme1n1`
	- Cree el sistema de archivos
	- Cree un directorio para montarlo
	- Monte el volumen
	- Hice que el montaje sea permanente
	- Probe que funcionará

El nuevo volumen se llama `nvme1n1` asi que los comandos se usan con ese nombre

![[Pasted image 20250929122709.png]]


**4. Verificar la Aplicación Web**

Vemos si se creo la app web exitosamente

![[Pasted image 20250929122923.png]]


## Parte 4: Limpieza de Recursos 

**1. Terminar la instancia EC2**

![[Pasted image 20250929123031.png]]


**2. Eliminar Volúmenes EBS**

Se eliminó EBS secundario:

![[Pasted image 20250929123225.png]]


**3. Eliminar Grupos de Seguridad**

![[Pasted image 20250929123307.png]]


**4. Eliminar Internet Gateway**

![[Pasted image 20250929123336.png]]
![[Pasted image 20250929123353.png]]


**5. Eliminar Subredes**

Se elimino la sub red pública

![[Pasted image 20250929123433.png]]

Se elimino la sub red privada:

![[Pasted image 20250929123450.png]]




**6. Eliminar VPC**

![[Pasted image 20250929123510.png]]


**7. Eliminar Usuario y Grupo IAM**

- Eliminé usuario `dev-web-admin`

![[Pasted image 20250929123619.png]]

- Elimine grupo `AdminsWeb`

![[Pasted image 20250929123645.png]]

- Elimine política `EC2AndVPCAccessPolicy`

![[Pasted image 20250929123718.png]]