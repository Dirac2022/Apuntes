
### Fase 1: Preparación con IAM 
#### 1. Crear un Usuario IAM Administrativo (Opcional, si no tienes uno)
Ve a IAM > Usuarios > Añadir usuario. 

Dale un nombre (ej. admin-aws-lab). 

- **User name**: `admin-aws-lab`
![[Pasted image 20251018090503.png]]

Adjunta la política AdministratorAccess

![[Pasted image 20251018090702.png]]


Selecciona "Acceso mediante programación" y "Acceso a la consola de administración". 
Crea una contraseña segura. 


#### 2. Crear un Rol IAM para EC2:
Ve a IAM > Roles > Crear rol.
Tipo de entidad de confianza: "Servicio de AWS" > "EC2". 

![[Pasted image 20251018091203.png]]

Adjunta la política: AmazonS3ReadOnlyAccess (para que los servidores web puedan leer de S3). 

![[Pasted image 20251018091255.png]]

Nombra el rol: `ec2-web-role`. 

![[Pasted image 20251018091430.png]]



### Fase 2: Construcción de la Red con VPC 
#### 1. Crear una Nueva VPC:
Ve a VPC > Tus VPCs > Crear VPC.
- Nombre: `WebAppVPC`. 
- Bloque CIDR de IPv4: `10.0.0.0/16`.
- Tenancy: "Default". 

![[Pasted image 20251018091949.png]]

#### 2. Crear Subredes:
Ve a Subredes > Crear subred. 
Selecciona tu WebAppVPC. 
##### Subred Pública 1:
- Nombre: `WebApp-Public-Subnet-1`.
- Zona de disponibilidad: `us-east-1a`
- Bloque CIDR: `10.0.1.0/24`. 

![[Pasted image 20251018092219.png]]

##### Subred Privada 1:
- Nombre: `WebApp-Private-Subnet-1.`
- Zona de disponibilidad: `us-east-1a`
- Bloque CIDR: `10.0.10.0/24`

![[Pasted image 20251018093014.png]]



(Opcional pero recomendado para alta disponibilidad): Crea una segunda subred pública y privada en una zona de disponibilidad diferente (ej. us-east-1b) para futura expansión con un Balanceador de Carga y Auto Scaling Group. Por simplicidad, este ejercicio se centrará en una sola AZ. 

#### 3. Crear Internet Gateway (IGW):
Ve a Internet Gateways > Crear Internet Gateway.
Nombre: WebApp-IGW. Adjúntalo a tu WebAppVPC. 

![[Pasted image 20251018093222.png]]

![[Pasted image 20251018093430.png]]


#### 4. Crear Tablas de Rutas:
Ve a Tablas de Route > Crear tabla de rutes.
Tabla de Rutas Pública:
- Nombre: `WebApp-Public-RT`.
- VPC: WebAppVPC.

![[Pasted image 20251018093532.png]]

- Asocia WebApp-Public-Subnet-1 a esta tabla.

![[Pasted image 20251018093652.png]]

- Añade una ruta: 0.0.0.0/0 -> WebApp-IGW. 

![[Pasted image 20251018093812.png]]



Tabla de Rutas Privada (sin ruta a Internet):

- Nombre: `WebApp-Private-RT`.
- VPC: `WebAppVPC`.

![[Pasted image 20251018093900.png]]

- Asocia WebApp-Private-Subnet-1 a esta tabla.

![[Pasted image 20251018093936.png]]

#### 5. Crear NAT Gateway (para la subred privada):
Ve a NAT Gateways > Crear NAT Gateway.
- **Name**: `Nat-Gateway-EP`
- Subred: `WebApp-Private-Subnet-1`. 

> [!info] Según la guía decía:  Subred: `WebApp-Public-Subnet-1`. Asumo que es un error, y lo configuré para `WebApp-Private-Subnet-1`

- **Elastic IP**: Elastic IP address 44.219.30.207 (eipalloc-047c0db5175a75674)
- Crea el NAT Gateway. Espera a que el estado sea "Available".

![[Pasted image 20251018094646.png]]



Una vez creado, edita la WebApp-Private-RT y añade una ruta: 0.0.0.0/0 -> (ID de tu NAT Gateway). 

![[Pasted image 20251018094756.png]]


Esto permitirá que los recursos en la subred privada accedan a Internet para actualizaciones, pero Internet no podrá iniciarse desde la subred privada. 

### Fase 3: Despliegue de EC2 y EBS 

#### 1. Crear Grupos de Seguridad (Security Groups):
Ve a Grupos de Seguridad > Crear grupo de seguridad (asegúrate de que sea en tu WebAppVPC). 

**sg-webserver:**
- Nombre: `webserver-sg`.

>[!warning] Al ingresar el nombre `sg-webserver`, me salió este error: A security group name cannot begin with sg-. Por tanto el nombre que elegí fue: `webserver-sg`

- Descripción: Permite trafico HTTP/S.
- Reglas de entrada: Tipo: HTTP (80), Origen: 0.0.0.0/0 (Para acceso público).
- Tipo: HTTPS (443), Origen: 0.0.0.0/0 (Para acceso público).
- Tipo: SSH (22), Origen: (Tu IP pública) (Solo tú para administración).
- Reglas de salida: Todo el tráfico (All traffic), Destino: 0.0.0.0/0.

![[Pasted image 20251018101000.png]]

**sg-database**:
- Nombre: sg-database.
- Descripción: Permite trafico de base de datos solo desde los servidores web.
- Reglas de entrada: Tipo: MySQL/Aurora (3306) o PostgreSQL (5432) - según tu elección de RDS.
- Origen: (ID de tu sg-webserver) (¡Muy importante! Restringe el acceso solo a los servidores web).
- Reglas de salida: Todo el tráfico (All traffic), Destino: 0.0.0.0/0. 

![[Pasted image 20251018101320.png]]


#### 2. Lanzar Instancia EC2 (Simulación de Servidor Web):
Ve a EC2 > Instancias > Lanzar instancias.

- **Name**: `MyEC2-EP`
- AMI: Amazon Linux 2 AMI (Gratuita y ligera).
- Tipo de instancia: `t3.micro`.

>[!info] `t2.micro` no habilitada, se eligió por defecto a `t3.micro`

- Se creó una **key pair**:
![[Pasted image 20251018101748.png]]


Detalles de instancia:
- Red: WebAppVPC.
- Subred: WebApp-Public-Subnet-1.
- Asignar IP pública automáticamente: "Habilitar".

> [!info] Se agrego también el **Security Group**:  `webserver-sg`

![[Pasted image 20251018102029.png]]


- Rol de IAM: ec2-web-role (el que creaste antes). 

![[Pasted image 20251018102133.png]]

- Datos de usuario (User data): Pega el siguiente script para instalar Apache y una página web simple: 

```sh
#!/bin/bash

yum update -y 
yum install -y httpd 
systemctl start httpd 
systemctl enable httpd 
echo "<h1>Hola desde mi Web Server en AWS!</h1>" > /var/www/html/index.html 
echo "<p>Contenido desde S3 (simulado): <img src='https://s3.amazonaws.com/TU
NOMBRE-DE-BUCKET-S3/imagen_test.png' alt='Imagen de S3'></p>" >> 
/var/www/html/index.html 
```


![[Pasted image 20251018102305.png]]


Importante: Reemplaza TU-NOMBRE-DE-BUCKET-S3 con el nombre de tu bucket de S3 real (lo crearemos después).
- Almacenamiento: Deja el predeterminado (8GB EBS gp2). Esto ya es un volumen EBS. (Hecho)
- Grupos de seguridad: Selecciona sg-webserver. (Hecho)
- Par de claves: Elige uno existente o crea uno nuevo para SSH. (Hecho)
- Lanza la instancia. Nómbrala: `WebServer-1`. (Hecho)


#### 3. Verificar EC2:
Una vez que la instancia esté en estado "running", copia su IP pública.
Pégala en un navegador web. Deberías ver la página "Hola desde mi Web Server en AWS!".

![[Pasted image 20251018102557.png]]


### Fase 4: Configuración de RDS
#### 1. Crear Subnet Group de Base de Datos:
Ve a RDS > Subnet Groups > Crear grupo de subredes de base de datos.
Nombre: `webapp-db-subnet-group`.
VPC: `WebAppVPC`.
Añade WebApp-Private-Subnet-1 (y cualquier otra subred privada que hayas creado). Esto es crucial para que la DB resida solo en subredes privadas.

![[Pasted image 20251018104417.png]]

> [!important]
> Tuve que crear otra subred privada adicional para crear el grupo de subredes para bases de datos:
> - **Name**: WebApp-Private-Subnet-2
> - CIDR block: `10.0.11.0/24`
> - AZ: `us-east-1b`


![[Pasted image 20251018104044.png]]


#### 2. Lanzar Instancia RDS:
Ve a RDS > Bases de datos > Crear base de datos.

- Método de creación: "Standard create".
- Motor: Elige MySQL o PostgreSQL.
- Plantilla: "Free tier" (para el ejercicio).
- Identificador de instancia de DB: `webapp-db-instance`.
- Credenciales: Crea un nombre de usuario maestro (admin) y una contraseña segura. (Exxx9$)

![[Pasted image 20251018104853.png]]

Clase de instancia de DB: db.t2.micro (Capa Gratuita).

> [!info] `db.t2.micro` no habilitada. Se eligió `db.t4.micro` por defecto


Almacenamiento: 20 GiB (predeterminado para Free Tier).
Conectividad:
- VPC: `WebAppVPC`.
- Grupo de subredes de DB: `webapp-db-subnet-group`.
- Acceso público: "No" (¡muy importante para seguridad!).
- Grupo de seguridad de VPC existente: `database-sg`

![[Pasted image 20251018105347.png]]

Configuración adicional (Desactivar en un entorno real si no es necesario): Desactiva "Enable deletion protection" para poder borrar fácilmente la DB al finalizar el ejercicio.

![[Pasted image 20251018105536.png]]


Crea la base de datos. Esto tomará varios minutos.

![[Pasted image 20251018110038.png]]


#### 3. Verificar RDS:
Una vez que la DB esté "Available", copia su "Endpoint".
Intenta conectarte desde tu WebServer-1 vía SSH (usando el cliente MySQL/PostgreSQL si lo instalas allí). No debería ser accesible desde tu máquina local directamente, solo desde el EC2.

![[Pasted image 20251018110242.png]]


#### Fase 5: Configuración de S3

#### 1. Crear un Bucket S3:

 Ve a S3 > Crear bucket.
 Nombre del bucket: mi-aplicacion-web-imagenes-XYZ (Debe ser globalmente único, usa tu nombre o iniciales y un número).
 Región de AWS: La misma que tu VPC.
 Bloquear todo el acceso público: Desactiva esta opción por ahora, ya que el sitio web necesita leer imágenes directamente. En un entorno de producción, configurarías un CloudFront con un OAI para S3.
 Reconoce que al desactivarlo, el bucket es público (para este ejercicio). Crea el bucket. 

- nombre: `mi-aplicacion-web-imagenes-192422`

![[Pasted image 20251018110838.png]]

 
#### 2. Subir un Objeto a S3:

Entra en tu nuevo bucket.
Crea una imagen de prueba simple (un PNG o JPG) en tu computadora. Puedes usar Paint o cualquier editor. Nómbrala imagen_test.png.
Súbela a tu bucket S3. 

![[Pasted image 20251018111113.png]]


#### 3. Verificar Acceso a S3 desde EC2:
Abre el navegador y ve a la IP pública de tu WebServer-1 de nuevo.
La imagen de S3 debería cargarse correctamente. Si no, revisa el nombre del bucket en tu User Data del EC2 y los permisos del bucket de S3.

La imagen se cargó correctamente

![[Pasted image 20251018111404.png]]


Puedes también hacer SSH a tu instancia EC2 y ejecutar: aws s3 ls s3://TU-NOMBRE-DE BUCKET-S3 para verificar que el rol de IAM está funcionando (si tiene los permisos correctos). 
##### Verificación Final y Puntos Clave:

IAM: ¿Creaste el rol EC2 con AmazonS3ReadOnlyAccess y lo asignaste a la instancia EC2? 

- Si

VPC: o ¿Tienes una VPC aislada? o ¿Tus subredes pública y privada están configuradas correctamente?
 ¿El Internet Gateway está adjunto a la VPC y en la tabla de rutas pública? o ¿El NAT Gateway está en la subred pública y su Elastic IP asociada? o ¿La tabla de rutas privada tiene la ruta a 0.0.0.0/0 apuntando al NAT Gateway?

- Si tengo una VPC aislada, mis subredes estan configuradas correctamente
- IGW para la subred publica
- NAT para la subred privada

EC2:
¿Tu servidor web está en la subred pública? o ¿Tiene asignado el sg-webserver? o ¿La página web se carga correctamente? 

- Si, tengo asignado el sg-webserver tmb, la pagina se carga correctamente

EBS: ¿El volumen de arranque de EC2 es un volumen EBS?
- Si

RDS: o ¿La base de datos está en la subred privada? o ¿Su "Acceso público" está en "No"? o ¿Está usando el sg-database que restringe el acceso solo a tu sg-webserver?

- No, la DB esta en un subgrupo de redes privadas restringida

S3: o ¿Creaste un bucket? o ¿Subiste una imagen? o ¿La imagen se carga en la página web del EC2?

Si



## PARTE II

**Describa los beneficios de esta infraestructura, en relación a la escalabilidad, alta disponibilidad, resiliencia, monitorización y centralización. (3 puntos)**

Esta infraestructura esta pensada para ser escalable, presenta **alta disponibilidad** ya que, por ejemplo la instancia de bd esta asociada a 2 AZ. 

Además es resiliente ya que se esta usando S3 como almacenamiento de persistencia, esto es un beneficio de la infraestructura ya que los S3 no están sujetos a instancias EC2 como los EBS. 

Para la monitorización y centralización se pudo usar CloudWatch, pero en este caso, no realize ninguna gestión respecto a ello.

La infraestructura tambien es centralizada ya que se creo un rol específico para que la instancia EC2 se comunique con S3

