
## Task 1: Launch Your Amazon EC2 Instance


- En **Services/Compute** seleccioné la opción **EC2**
- Validé que la región sea **N. Virginia (us-east-1)**
- Ejecuté **Launch instance**


![[Pasted image 20250922225335.png]]

### Step 1: Name and tags

Añadí el tag `Name` 
`Name` : `Web Server`

### Step 2: Application and OS Images (Amazon Machine Image)
Elegí como AMI: **Amazon Linux**

![[Pasted image 20250922231100.png]]


### Step 3: Instance type
Deje el tipo por defecto: **t3.micro**


### Step 4: Key pair (login)
Seleccioné **vockey**

![[Pasted image 20250922231125.png]]


### Step 5: Network settings

- Para VPC seleccioné: **`Lab VPC`**
- Para el subnet seleccioné: **`PublicSubnet1`***
- Para el **Security group name**: `Web Server security group`
	- Y Descripción: `Security group for my web server`



![[Pasted image 20250922230253.png]]

- Se removió con el botón **Remove** debajo de **Inbound security group rules**

![[Pasted image 20250922230556.png]]

### Step 6: Configure storage

Se mantuvieron las configuraciones por defecto
- 8GB, gp3

### Step 7: Advanced details

A continuación detalle las configuraciones que se introdujo
- **Termination protection**: Enable
- **User data** 

```sh
#!/bin/bash
dnf install -y httpd
systemctl enable httpd
systemctl start httpd
echo '<html><h1>Hello From Your Web Server!</h1></html>' > /var/www/html/index.html
```



### Step 8: Launch the instance

Después de ejecutar el botón **Launch instance**, se pudo observar el éxito al lanzar la instancia y el estado en **Running**:

![[Pasted image 20250922232129.png]]



## Task 2: Monitor Your Instance

A continuación detallo las configuraciones y/o estados en cada tab, después de lanzar la instancia:

- **Status check**: `3/3 checks passed`
- **Monitor**: `disable`

Se verificó el **System Log**:

![[Pasted image 20250922232509.png]]

![[Pasted image 20250922232621.png]]

Se observó como se vería la pantalla de la consola a partir de la opción **Get instance screenshot** de **Actions/Monitor and troubleshoot**

![[Pasted image 20250922232749.png]]


## Task 3: Update Your Security Group and Access the Web Server



- Se copió el **Public IPv4 address** del tab **Details**
- Al intentar acceder, falla, esto se debe a la configuración previa en los **Security Groups**

![[Pasted image 20250922234157.png]]

Luego, en **Security Groups**:
- Se seleccionó el security group: **Web Server security group**
- En **Inbound rules** se seleccionó **Edit inbound rules**
- Se agregó la regla:
	- **Type**: `HTTP`
	- **Source**: `Anywhere-IPv4`
- Se guardó la regla

![[Pasted image 20250922234555.png]]

Al volver a recargar la página, se observo:

![[Pasted image 20250922234631.png]]

## Task 4: Resize Your Instance: Instance Type and EBS Volume


### Stop Your Instance

- Se detuvo la instancia **Web Server** mediante el botón **Stop instance** de **Instance state**

![[Pasted image 20250922235011.png]]


### Change The Instance Type and enable stop protection

![[Pasted image 20250922235040.png]]

Se configuró a:
- **Instance Type**: `t2.small`

Se observó que si se aplicaron los cambios:

![[Pasted image 20250922235309.png]]


Luego se hizo la siguiente configuración:

![[Pasted image 20250922235337.png]]

![[Pasted image 20250922235412.png]]

### Resize the EBS Volume

- Se seleccionó la instancia
- En la pestaña **Storage** se seleccionó el **Volume ID**
- Se seleccionó **Modify volume** en el menú **Actions**

![[Pasted image 20250922235935.png]]

- Se cambió la capacidad a 10GB
- Se seleccionó el botón **Modify**
- Se pudo comprobar que efectivamente se realizo el cambio:

![[Pasted image 20250923000156.png]]

### Start the Resized Instance

Se inicio la instancia, con los cambios efectuados:

- Se seleccionó **Start instance** en el menú **Actions**


![[Pasted image 20250923000948.png]]



## Task 5: Explore EC2 Limits


Se exploro los límites del servicio EC2:

- **Services/Service Quotas** -> **Amazon Elastic Compute Cloud (Amazon EC2)** en el buscador.
- Luego se busco en la barra de búsqueda: `running on-demand`

![[Pasted image 20250923000755.png]]


## Task 6: Test Stop Protection


- Se intento detener la instancia:

![[Pasted image 20250923001122.png]]

Se observo el siguiente error:

![[Pasted image 20250923001230.png]]

- Se desactivo el **Change stop protection** en **Actions/Instance settings**
- 
![[Pasted image 20250923001321.png]]

- Esta vez si se pudo detener la instancia:

![[Pasted image 20250923001404.png]]

Se observó la instancia detenida:

![[Pasted image 20250923001437.png]]


**Fin del laboratorio**




