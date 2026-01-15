
**Mitchel Soto Cuya**


### Parte II

Procedí a crear la instancia 1 `instance1` con el tag `BackupEnable: true`

Configuraciones:
- **AMI**: `Amazon Linux`
- **Instance type**: `t3.micro`
- **key pair**: Cree uno nuevo `pc3` de tipo pem
- Las demás configuraciones fueron por defecto

![[Pasted image 20251122090042.png]]

Procedí a crear la instancia 2 `instance2` con el tag `BackupEnable: false`
Configuraciones:
- **AMI**: `Amazon Linux`
- **Instance type**: `t3.micro`
- **key pair**: Cree uno nuevo `pc3` de tipo pem
- Las demás configuraciones fueron por defecto

![[Pasted image 20251122090406.png]]


Procedí a crear un **bucket S3** para la parte de **auditoría**:

- **Bucket name**: `audit-reports-bucket-mitchel-soto`
- Las demás configuraciones se dejaron por defecto

![[Pasted image 20251122091523.png]]


Procedí a crear un SQS:

- **Name**: `backup-failures`
- Las demás configuraciones las deje por defecto

![[Pasted image 20251122091719.png]]

- **URL**: `https://sqs.us-east-1.amazonaws.com/980829302003/backup-failures`

Procedí a crear el rol para el servicio **lambda**

![[Pasted image 20251122092110.png]]

Añadí la política indicada en la guía (aunque luego indica que falta una acción)

- `AmazonSQSReadOnlyAccess`

![[Pasted image 20251122092428.png]]

- **Role Name**: `lambdaRolePC3`

![[Pasted image 20251122092650.png]]


Procedí a crear la función lambda

- **Lambda name** `lambdaFunPC3`
- **Runtime**: `Python 3.11`
- **Rol**: `lambdaRolePC3`

![[Pasted image 20251122092912.png]]


Procedí a añadir el **trigger** **`EventBridge`** para la función lambda:

En la pantalla principal de la función lambda, seleccioné el botón **+ Add trigger**
- **Trigger configuration**: `EventBridge (CloudWatch Events)`
- **Rule name**: `SnapshotPorHora`
- **scheduled expression**: `rate(1 hour)`

![[Pasted image 20251122093558.png]]


<h5>Implementación y corrección del código</h5>
Procedí a copiar el código de la guía:

![[Pasted image 20251122093916.png]]

Reemplazo los nombres correctos de mi bucket y SQS:

```python
BUCKET_NAME = "audit-reports-bucket-mitchel-soto"

SQS_QUEUE_URL = "https://sqs.us-east-1.amazonaws.com/980829302003/backup-failures"
```

**TODO 1**:

```python
# TODO 1: Inicializar los clientes de Boto3 para EC2, S3 y SQS
ec2_client = boto3.client('ec2')
s3_client = boto3.client('s3')
sqs_client = boto3.client('sqs')
```


A continuación presento las correcciones para el método `lambda_handler`:

**TODO 2**:

```python
        # TODO 2: Filtrar volúmenes.
        # Requerimiento: Estado 'in-use' Y Tag 'BackupEnabled' = 'true'
        volumes_response = ec2_client.describe_volumes(
            Filters=[
                {'Name': 'status', 'Values': ['in-use']},
                {'Name': 'tag:BackupEnabled', 'Values': ['true']}
            ]
        )
```


**TODO 3**:

```python
                # TODO 3: Crear el Snapshot
                description = f"Backup automatico para {vol_id} en {timestamp}"
                snap_response = ec2_client.create_snapshot(
                    VolumeId=vol_id,
                    Description=description
                )
```


**TODO 4**:

```python
                # TODO 4: Enviar mensaje de error a SQS (Dead Letter pattern manual)
                # El cuerpo del mensaje debe ser un JSON string
                error_payload = {
                    "FailedVolume": vol_id,
                    "Error": str(e),
                    "Time": timestamp
                }

                sqs_client.send_message(
                    QueueUrl=SQS_QUEUE_URL,
                    MessageBody=json.dumps(error_payload)
                )
```



**TODO 5**:

```python
        # TODO 5: Guardar el reporte de auditoría en S3
        # El nombre del archivo debe ser único usando el timestamp
        file_key = f"reports/backup-{timestamp}.json"

        if snapshot_report:
            s3_client.put_object(
                Bucket=BUCKET_NAME,
                Key=file_key,
                Body=json.dumps(snapshot_report),
                ContentType='application/json'
            )

        logger.info("Reporte de auditoría subido a S3.")
```



### Parte II


Pregunta 1: Tiempos de Ejecución (Lambda Timeout)

Respuesta: A

Justificación: si le subes la ram a 10gb la lambda se vuelve super rapida y procesa todo al mas rapido antes q pasen los 3 segundos.

Pregunta 2: Permisos IAM

Respuesta: B

Justificación: obvio falta el sendmessage, si tienes readonly solo puedes leer la cola pero no enviar nada, x eso falla.

Pregunta 3: S3 Consistency

Respuesta: A

Justificación: el s3 siempre demora un poco en mostrar los archivos nuevos en todos lados, eso es la consistencia eventual de siempre.
Pregunta 4: Escalabilidad y API Limits (Paginación)

Respuesta: B

Justificación: cuando son miles de volumenes aws no te da todo de golpe, te lo manda por paginas y tienes que iterar con el token sino solo ves el principio.

Pregunta 5: Optimización de Costos y Almacenamiento

Respuesta: B

Justificación: tranqui q los snapshots son incrementales, solo guardan los bloques q cambiaron asi que no te van a cobrar x todo el disco cada vez.

Pregunta 6: Observabilidad y Troubleshooting

Respuesta: C

Justificación: la lambda necesita permisos explicitos para crear los grupos de logs, si no se los das en el rol no va a aparecer nada en cloudwatch.