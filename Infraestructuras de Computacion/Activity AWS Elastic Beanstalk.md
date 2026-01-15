**Mitchel Soto Cuya**
## Task 1: Access the Elastic Beanstalk environment

Me situé en el servicio **Elastic Beanstalk**. Pude observar un **Environment**:

![[Pasted image 20251103130756.png]]

A continuación se presenta el dashboard:

![[Pasted image 20251103131039.png]]

Pude comprobar al abrir el link del dominio en otra pestaña, arrojaba el error: `HTTP Status 404 - Not Found`. Ya que el servidor aun no esta corriendo ninguna aplicación.

![[Pasted image 20251103130924.png]]



## Task 2: Deploy a sample application to Elastic Beanstalk

Procedí a descargar el siguiente *zip*:
[https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/samples/tomcat.zip](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/samples/tomcat.zip)

- Seleccioné el botón `Upload and deploy` y cargue el reciente *zip* descargado:
- Seleccioné el botón **Deploy**

![[Pasted image 20251103131422.png]]


Al volver a abrir el **Domain URL** en una nueva pestaña observé lo siguiente:

![[Pasted image 20251103131831.png]]

Lo que me indica que la aplicación ha sido correctamente desplegada con **Elastic Beanstalk**

Al ingresar a **Configuration** en el panel lateral izquierdo, al ingresar al panel **Instance traffic and scaling** pude observar lo siguiente:
- **EC2 Segurity Groups**
- **Min instances** / **Max instances**
- **Instance types**, etc.

![[Pasted image 20251103132222.png]]

En el panel **Networking, database, and tags** elegí el botón **Edit**

![[Pasted image 20251103132441.png]]

En este panel podría haber habilitado una base de datos para este *environment*

Al seleccionar **Monitoring** en el panel izquierdo, pude observar las siguientes métricas:

![[Pasted image 20251103132616.png]]


## Task 3: Explore the AWS resources that support your application

Al volver al servicio **EC2** pude observar las dos instancias:

![[Pasted image 20251103132820.png]]

A su vez, también pude observar las métricas en ambas instancias


> [!tip] Actividad completada

