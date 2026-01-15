**MITCHEL SOTO CUYA**

### PARTE 1 – Preparación y Seguridad (IAM + S3) 

Tareas 
1. Diseña un IAM Role para SageMaker que permita:
	- Lectura/escritura en buckets S3 específicos
		- Escritura en CloudWatch Logs
		- Uso de claves KMS 

Procedí a crear el **IAM Role**

![[Pasted image 20251220101252.png]]


- **Rol name**: `Rol-EF-SageMaker`
- **ARN**: `arn:aws:iam::980829302003:role/Rol-EF-SageMaker`

![[Pasted image 20251220102603.png]]

Procedí a añadir los permisos:

Para **S3**
- `GetObject`
- `PutObject`
- `ListBucket`

Para **CloudWatch Logs**

- `CreateLogGroup`
- `CreateLogStream`
- `PutLogEvents`

Para **KMS**

- `DescribeKey`
- `GetKeyPolicy`
- `Decrypt`
- `Encrypt`
- `GenerateDataKey`
- `GenerateDataKeyWithoutPlaintext`
- `ReEncryptFrom`
- `ReEncryptTo`
- `CreateGrant`
- `RetireGrant`
- ``RevokeGrant``

**Policy Name**: `Policy-S3-CloudWatchLogs-KMS`

![[Pasted image 20251220110100.png]]


2. Define la estructura de buckets S3: 
```
s3://fraud-ml-project/ 
	├── raw-data/ 
	├── processed-data/ 
	├── model-artifacts/ 
	├── evaluation/ 
```


Procedí a crear el **S3 bucket**

- **Bucket name**: `fraud-ml-project-mitchel-soto`

![[Pasted image 20251220110040.png]]


3. Explica cómo asegurarías los datos en reposo y en tránsito.

> Para asegurar los datos almacenados en S3, implementé cifrado del lado del servidor usando AWS Key Management Service (SSE-KMS). Esta configuración cifra automáticamente todos los objetos almacenados en el bucket `fraud-ml-project-mitchel-soto` con claves administradas por KMS. Adicionalmente, habilité el versionado del bucket para mantener un historial completo de cambios y permitir recuperación ante eliminaciones accidentales o modificaciones no autorizadas



### PARTE 2 – Procesamiento y Entrenamiento (SageMaker) 
Tareas 
4. Describe un Processing Job que: o Elimine valores nulos o Normalice variables numéricas o Separe datos en train/test (80/20)

> En el panel izquierdo ingrese a Data Preparation -> Processing jobs -> Create Processing Job

- **job name**: `fraud-preprocessing-job`
- **Container**: `683313688378.dkr.ecr.us-east-1.amazonaws.com/sagemaker-scikit-learn:0.23-1-cpu-py3`

Implemente el script : `preprocessing.py` y lo subí en una nueva carpeta de mi **bucket** llamado `scripts`:

![[Pasted image 20251220112243.png]]


Cargué `credit.csv` en el folder `raw_data`

![[Pasted image 20251220113210.png]]


5. Configura un Training Job que: o Use un algoritmo supervisado o Registre métricas (accuracy, precision, recall) o Guarde el modelo en S3


6. Explica cómo versionarías modelos entrenados.