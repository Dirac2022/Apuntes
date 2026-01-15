
**Mitchel Soto Cuya**

## Task 1: Create a Lambda function

Estando en la consola, ingresé al servicio **AWS Lambda** y eleccioné el botón **Create a function**
- **Function Name**: `myStopinator`
- **Runtime**: `Python 3.11`
- **Existing Role**: `myStopinatorRole`

![[Pasted image 20251103121847.png]]

Procedí a crear la función con **Create Function**

## Task 2: Configure the trigger

Una vez creada la función, esta es la vista de la consola:

![[Pasted image 20251103122036.png]]

Seleccione **Add trigger**
- **Trigger configuration**: `EventBridge (CloudWatch Events)`
- **Rule name**: `everyMinute`
- **Rule type**: Schedule expression
- **Schedule expression**: `rate(1 minute)`

![[Pasted image 20251103122631.png]]

Procedí a añadir el **trigger** seleccionando el botón **Add**

## Task 3: Configure the Lambda function


En el panel inferior, seleccioné la pestaña **Code** y el script `lambda_function.py`.

- Copié el siguiente código en el editor:

```python
import boto3
region = 'us-east-1'
instances = ['i-05668e51d61f661e3']
ec2 = boto3.client('ec2', region_name=region)

def lambda_handler(event, context):
    ec2.stop_instances(InstanceIds=instances)
    print('stopped your instances: ' + str(instances))
```

- **region**: 'us-east-1'
- **Instance id**: `i-05668e51d61f661e3`

Obtuve el **instance id** de la instancia `instace 1` de servicio **EC2**:

![[Pasted image 20251103123716.png]]

Guarde los cambios y seleccioné el botón **Deploy**:

![[Pasted image 20251103124038.png]]

Ingresé a la pestaña **Monitor** para observar las gráficas de métricas:

![[Pasted image 20251103124231.png]]

## Task 4: Verify that the Lambda function worked


Al retornar a mi instancia de **EC2** pude observar que la instancia fue detenida:

![[Pasted image 20251103124442.png]]


Procedí a iniciar nuevamente la instancia **instance1**:

![[Pasted image 20251103124559.png]]

Estados:
- `Pending`
- `Initializing` (Status check)
- `Running`

Sin embargo, al pasar el minuto vuelve a estar en `Stopped`

Para la pregunta 20: **Try starting the instance again. What do you think will happen?**

> La instancia volvería a detenerse después de un minuto


> [!tip] Actividad Completada

