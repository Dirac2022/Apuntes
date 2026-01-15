
## Task 1: Connect to an Amazon Linux EC2 instance by using SSH


Descargué el archivo **ppk** mediante el botón **Download PPK** del *dropdown menu* **Details**

Descargué **PuTTY** como lo indicó la guía

![[Pasted image 20251117212522.png]]


En **Connection**
- **Seconds between keepalives**: `30`

En **Session**
- **Host Name** : `107.21.186.165`


En **Connection/SSH/Auth/Credentials**
- Cargué el **private key** descargado anteriormente


![[Pasted image 20251117213208.png]]

Al seleccionar el botón **Open** y **Aceptar** en la ventana de seguridad pude acceder al terminal:

![[Pasted image 20251117213525.png]]


## Task 2: Configure the AWS CLI


Actualicé **AWS CLI**. Para ello usé

- **AWS Access Key ID**: `AKIAYRM2RXF5ON2HESHK`
- **AWS Secret Access Key**: `r5hxzeDBxI4j0I7jdGBMdQDBpijQ1yGQbkcxki`


![[Pasted image 20251117213823.png]]

## Task 3: Create an EC2 instance by using the AWS CLI

### Task 3.1: Observe the script details

Cambié de directorio y creé un backup:

![[Pasted image 20251117214121.png]]

Abrí el **create-lamp-instance** 

![[Pasted image 20251117214155.png]]

Analicé el código según la guía.


### Task 3.2: Try running the script

Se observó los errores, tal como lo indica la guía:

![[Pasted image 20251117214514.png]]


Instalé **nmap** correctamente:

![[Pasted image 20251117215028.png]]


![[Pasted image 20251117215148.png]]


![[Pasted image 20251117215200.png]]

Traté de sortear los errores pero no encontré la solución:
![[Pasted image 20251117215956.png]]

