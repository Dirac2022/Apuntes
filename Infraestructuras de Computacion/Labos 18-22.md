
# Lab 18 - IAM Administración de Identidades

**Procedí a crear un Rol** 
Para ello:
- Ingrese al servicio **IAM**
- En el panel izquierdo seleccioné **Roles**
- Seleccioné el botón **Create Rol**

![[Pasted image 20251108132429.png]]

- **Trusted entity type**: `AWS service`
- **Service or use case**: `Lambda`

Para la política de permisos:

- `AmazonS3FullAccess`

![[Pasted image 20251108132616.png]]


- **Rol name**: `ROL_PROYECTO_1`

![[Pasted image 20251108132702.png]]

Luego procedí a crear el Rol.

Se puede observar el Rol creado:

![[Pasted image 20251108132812.png]]


# Lab 19 - Amazon CloudWatch

**Agregar los permisos de CloudWatch al Rol creado** `ROL_PROYECTO_1`

![[Pasted image 20251108140203.png]]


- Seleccioné **Add permissions / Attach policies**

> [!warning] Sobre `AWSOpsWorksCloudWatchLogs`
> No encontré el permiso. Elegí un permiso que a mi parecer se acerca al permiso:
> - `CloudWatchLogsFullAccess`

![[Pasted image 20251108140549.png]]



# Lab 20 - AWS Lambda - Configuración de parámetros y Log


Seleccioné el servicio **Lambda**

![[Pasted image 20251108140845.png]]

Procedí a crear una función con las siguientes configuraciones:
- **Author from scratch**
- **Function name**: `FN_PROCESA_1`
- **Runtime**: `Python 3.12`
- **Architecture**: `x86_64`

![[Pasted image 20251108141049.png]]

- Usé el Rol creado `ROL_PROYECTO_1`
- Procedí a crear la función

![[Pasted image 20251108141157.png]]


Una vez creada la función procedí a codificar la función especificada en el archivo  `SCRIPT_001.py`

![[Pasted image 20251108141354.png]]

Seleccioné **Deploy** para guardar los cambios
Procedí a crear un **Test** con la siguiente configuración:
- **Event Name**: `Prueba001`
- **Event sharing settings**: `Private`
- **Event JSON**: Copiado de `PARAMETROS_001.json`
- Click en **Save**

![[Pasted image 20251108141744.png]]


Procedí a ejecutar el **Test** creado. Se puede observar que se ejecutó exitosamente:

![[Pasted image 20251108141921.png]]

**Para ver los detalles del log**
- En la pestaña **Monitor** seleccioné el botón **View CloudWatch Logs**
- En **Logs streams** seleccioné la ultima ejecución (la única)

![[Pasted image 20251108142510.png]]

Se puede observar el log de la ejecución:

![[Pasted image 20251108142543.png]]



# Lab 21 - AWS Lambda - Integración con S3


Ingresé al servicio **Amazon S3**

> [!info] Sobre el nombre del Bucket
> En la guía se indica poner las iniciales del nombre en las `XXX` de `storagebdaXXXdata` sin embargo preferí usar mi `nombreapellido` para evitar un nombre de bucket repetido

- **Bucket name**: `storagebdamitchelsotodata`


![[Pasted image 20251108143035.png]]

Bucket creado:

![[Pasted image 20251108143205.png]]


Procedí a crear la carpeta `landingtmp`
- Seleccioné el botón **Create folder**
- **Folder name**: `landingtmp`

![[Pasted image 20251108143237.png]]


Dentro de `landingtmp` procedí a crear la carpeta `PERSONA`

![[Pasted image 20251108143331.png]]

Dentro de la carpeta `PERSONA` procedí a subir el archivo `persona.data`

![[Pasted image 20251108143457.png]]


**Crear una nueva función en Lambda**

Configuración:
- **Author from scratch**
- **Function name**: `FN_PROCESA_2`
- **Runtime**: `Python 3.12`
- **Architecture**: `x86_64`
- **Existing role**: `ROL_PROYECTO_1`

Función creada:

![[Pasted image 20251108143917.png]]

Procedí a insertar el código. Para ello necesité la librería **pandas**. Procedí a añadirla yendo a **Add a layer** en el ultimo módulo de la pestaña **Code**

Se detalla las configuraciones:

- **AWS layers**:  `AWSSDKPandas-Python312`
- **Version**: 19

![[Pasted image 20251108144242.png]] 


Una vez creada la capa, procedí a inserta el código de `SCRIPT_002.py` en `lambda_function.py`

![[Pasted image 20251108144419.png]]



![[Pasted image 20251108144541.png]]

- `Prueba001`
- `Private`
- Copiado de `PARAMETROS_002.json`




{

    "bucket": "storagebdamitchelsotodata",

    "ruta": "landingtmp/PERSONA/",

    "nombreDeArchivo": "persona.data"

}

# Lab 22 - AWS Lambda - Integración con DynamoDB

**En el servicio IAM agregué el siguiente permiso en el rol `ROL_PROYECTO_1`**: 

- `AmazonDynamoDBFullAccess`


![[Pasted image 20251108145354.png]]

Se observa el permiso agregado:

![[Pasted image 20251108145530.png]]


> [!tip] Laboratorios finalizados