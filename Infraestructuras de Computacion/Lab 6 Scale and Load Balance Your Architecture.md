
## Task 1: Create an AMI for Auto Scaling


- Se ingresó al servicio **EC2**
- Se valido que la instancia **Web Server 1** tenga el estado *`Running`*
- A partir de la instancia, en el menú **Actions** se seleccionó **Image and templates/Create image**

Para crear el **AMI**
- **Image name**: `WebServerAMI`
- **Image description**: `Lab AMI for Web Server`
- Se seleccionó el botón **Create image**

![[Pasted image 20251004090615.png]]


## Task 2: Create a Load Balancer


- En el panel lateral izquierdo se seleccionó **Target Groups**
- Se seleccionó el botón **Create target group**
	- **target type**: `Instances`
	- **Target group name**: `LabGroup`
	- **VPC**: `Lab VPC`
- Se creó el **target group** mediante los botones **Next** y **Create target group**

![[Pasted image 20251004091215.png]]


- En el panel lateral izquierdo se seleccionó **Create load balancer** en **Load Balancers**
- Se seleccionó el tipo de balanceador de carga  como `Application Load Balancer`
- Las configuraciones de este balanceador de carga fueron:
	- **Load balancer name**: `LabELB`
	- Configuraciones de **Network mapping**:
		- **VPC**: `Lab VPC`
		- **Availability Zones and subnets**:  Se eligió **Public Subnet 1** para el `us-east-1a (use1-az4` y **Pubic Subnet 2** para el `us-east-1b (use1-az6)`
	- Para **Security Group** se eligió como único grupo de seguridad a `Web Security Group` y se descarto el **default**.
	- En **Listeners and routing** se definió el **Default action** como `Forward to target groups` para el **target group** `LabGroup`, el protocolo es HTTP y puerto 80.
- Se creó el **load balancer** mediante el botón **Create load balancer**


![[Pasted image 20251004091846.png]]

![[Pasted image 20251004094506.png]]

Se observa el ELB creado:

![[Pasted image 20251004094637.png]]


## Task 3: Create a Launch Template and an Auto Scaling Group

- Ingresé a **Launch Templates** en el panel lateral izquierdo y luego seleccioné el botón **Create launch template**

Detalles de la configuración

- **Launch template name**: `LabConfig`
- **Amazon Machine Image (AMI)**: *`Web Server AMI`*
- **Instance type**: `t2.micro`
- **Key pair name**: *`vockey`*
- **Security groups**: `Web Security Group`
- En **Advance details / Detailed CloudWatch monitoring** se seleccionó `Enable`

Se seleccionó el botón **Create launch template**

![[Pasted image 20251004095332.png]]

Vemos que el **launch template** se creó con éxito

![[Pasted image 20251004095456.png]]


- Se seleccionó el **Launch template** creado
- En el menú **Actions** se seleccionó **Create Auto Scaling group**

Detalles de la configuración:

- **Auto Scaling group name**: `Lab Auto Scaling Group`
- **Launch template**: `LabConfig`

![[Pasted image 20251004095646.png]]

- **VPC**: `Lab VPC`
- **Availability Zones and subnets**: `Private Subnet 1` y `Private Subnet 2`


![[Pasted image 20251004095820.png]]

- En el Paso 3, en **Configure advanced options**, seleccioné `Attach to an existing load balancer` y elegí el `LabGroup` como **Existing load balancer target groups**

En el Paso 4

- Para **Group size**: **Desired capacity**: 2, **Minimum capacity**: 2, **Maximum capacity**: 6
- Para **Scaling policies** elegí en **Scaling policy name**: `LabScalingPolicy` y **Metric type**: `Average CPU Utilizattion` y en **Target value** en 60.
- Además en **Additional settings** se seleccionó la casilla de `Enable group metrics collection within CloudWatch` en **Metrics** (Se encuentra en el paso 4, no en el Paso 3).

![[Pasted image 20251004102456.png]]

- En el paso 5 se continuo sin configuraciones
- En el paso 6 se agregó un tag: **key**: `Name`, **Value**: `Lab Instance`


## Task 4: Verify that Load Balancing is Working


- En el panel lateral izquierdo se seleccionó **Instances**
- Se observó las dos nuevas instancias **Lab instance**
- En el panel lateral izquierdo se seleccionó **Target Groups**
- Se seleccionó `LabGroup`
- Se ingreso a la pestaña **Targets**


![[Pasted image 20251004111959.png]]

- Se ingreso a **Load Balancers** en el panel lateral izquierdo
- Se seleccionó `LabELB` como **load balancer**

Se observa el **DNS name** en el panel **Detailss**

![[Pasted image 20251004112129.png]]

Al abrir en una nueva pestaña: 

![[Pasted image 20251004112200.png]]


## Task 5: Test Auto Scaling

- En **CloudWatch** 
- Ingresé a **All alarms** en **Alarms** en el panel lateral izquierdo


Se observa el **AlarmHigh** en estado `OK`

![[Pasted image 20251004112501.png]]

- Se seleccionó **Load Test**

![[Pasted image 20251004112816.png]]

Se observa el **AlarmLow** en estado `OK`

![[Pasted image 20251004113213.png]]

Luego de unos minutos se observa:

![[Pasted image 20251004113352.png]]

En **EC22** se pudo observar mas de 2 instancias:

![[Pasted image 20251004113421.png]]





## Task 6: Terminate Web Server 1

Se procedió a terminar la instancia.

![[Pasted image 20251004113514.png]]

**Laboratorio terminado**

