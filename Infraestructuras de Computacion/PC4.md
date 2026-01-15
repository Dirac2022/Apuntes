
Primero creo un **Rol IAM** para **SageMaker** para no tener problemas luego

![[Pasted image 20251206093654.png]]

También incluyo el permiso total para **S3** `AmazonS3FullAccess`

![[Pasted image 20251206105559.png]]

**Rol name**: `SageMaker-S3-PC4-Rol`

---

Estando en el servicio **Amazon SageMaker** selecciono la opción **Amazon SageMaker AI** del panel lateral izquierdo:

![[Pasted image 20251206095549.png]]

Luego selecciono la opción **Notebooks** del panel lateral izquierdo

![[Pasted image 20251206095702.png]]

Estando en **Notebooks** creo una instancia dando click a **Create notebook instance**

![[Pasted image 20251206095828.png]]

- **Notebook instance name**: `notebook-pc4`
- **Notebook instance type**: `ml.t3.medium`

En **Permissions and encryption** vemos que me aparece el Rol que cree anteriormente:
![[Pasted image 20251206100113.png]]

Una vez completado la instancia, procedí a abrir el **JupyterLab**

![[Pasted image 20251206100658.png]]


## Paso 1: Preparación de Datos y Carga a S3

Empiezo a trabajar en el jupyter notebook:

![[Pasted image 20251206101403.png]]

Es importante tener el **ARN** del rol, en mi caso es: `arn:aws:iam::980829302003:role/SageMaker-S3-PC4-Rol`
![[Pasted image 20251206102434.png]]

Con ello evito problemas en:

```python
sagemaker_session = sagemaker.Session()
# role = sagemaker.get_execution_role()
role = 'arn:aws:iam::980829302003:role/SageMaker-S3-PC4-Rol'
bucket = sagemaker_session.default_bucket()
prefix = 'sagemaker/teledata-churn-lowcost'
```


### TAREA 1: Subir datos a S3

No tuve complicaciones adicionales realizando la tarea:

![[Pasted image 20251206104216.png]]


## Paso 2: Script de Entrenamiento 

(`entry_point_teledata.py`)

El Paso 2 me indica lo siguiente

> # **Paso 2: Script de Entrenamiento (`entry_point_teledata.py`)**
> # Crea un archivo de texto en tu JupyterLab llamado `entry_point_teledata.py`.

Para ello abro el Launcher y selecciono Text File:

![[Pasted image 20251206103211.png]]

Copio el script completo y modifico nombre del archivo de texto a `entry_point_teledata.py`

![[Pasted image 20251206103354.png]]

Completo las tareas dentro de `entry_point_teledata.py`

![[Pasted image 20251206103841.png]]


## Paso 3: Ejecución en Instancia Económica (Notebook)


```python
from sagemaker.sklearn.estimator import SKLearn

# TAREA 4: Configurar el Estimador con Instancia Básica
# 1. entry_point: Tu script 'entry_point_teledata.py'
# 2. instance_type: Usa 'ml.t3.medium' (Esta es una de las más económicas)
# 3. hyperparameters: Pasa los valores para '--n-arboles' y '--profundidad'

sklearn_estimator = SKLearn(
    entry_point='entry_point_teledata.py',
    role=role,
    instance_count=1,
    instance_type='ml.t3.medium',   # <--- ¡Pon aquí la instancia económica!
    framework_version='1.2-1',
    py_version='py3',
    hyperparameters={
        'n-arboles': 100,  # OJO: Usa el nombre del argumento externo (--n-arboles) sin guiones si es dict
        'profundidad': 4
    }
)

# Iniciar el Job
sklearn_estimator.fit({'train': s3_train_path, 'test': s3_test_path})
```

Al ejecutar la celda me sale este error: 

> [!error] 
> ResourceLimitExceeded: An error occurred (ResourceLimitExceeded) when calling the CreateTrainingJob operation: The 
requested resource training-job/ml.t3.medium is not available in this region

Hago el viejo truco de colocar otro valor en `instance_type` para ver si en el error me salen las opciones disponibles: `instance_type='ml.t9.medium',` . En efecto me salió esto como parte del error: 


> [!error]
> ClientError: An error occurred (ValidationException) when calling the CreateTrainingJob operation: 1 validation 
error detected: Value 'ml.t9.medium' at 'resourceConfig.instanceType' failed to satisfy constraint: Member must 
satisfy enum value set: [ml.r7i.48xlarge, ml.r5.12xlarge, ml.r5d.12xlarge, ml.m6i.xlarge, ml.trn1.32xlarge, 
ml.p2.xlarge, ml.m5.4xlarge, ml.m4.16xlarge, ml.r7i.16xlarge, ml.m7i.xlarge, ml.r5.24xlarge, ml.r5d.24xlarge, 
ml.m6i.12xlarge, ml.p5.48xlarge, ml.r7i.8xlarge, ml.r7i.large, ml.m7i.12xlarge, ml.m6i.24xlarge, ml.p4d.24xlarge, 
ml.m7i.24xlarge, ml.t3.xlarge, ml.r5.16xlarge, ml.r5d.16xlarge, ml.trn2.48xlarge, ml.g5.2xlarge, ml.c5n.xlarge, 
ml.p5e.48xlarge, ml.p3.16xlarge, ml.m5.large, ml.m7i.48xlarge, ml.m6i.16xlarge, ml.g6.2xlarge, ml.p2.16xlarge, ... Y muchas otras opciones

La opción mas cómoda es `ml.m5.large`

Ya que `ml.t3.medium` como vemos en el error no permite **training jobs**.
Vemos que se ejecuto con éxito:

![[Pasted image 20251206114821.png]]

![[Pasted image 20251206120144.png]]

## Paso 4: Despliegue en Endpoint Económico

```python
# TAREA 5: Desplegar el modelo
# Usa instance_type = 'ml.t2.medium' o 'ml.t3.medium'

predictor = sklearn_estimator.deploy(
    initial_instance_count=1,
    instance_type='ml.t2.medium'
)

# Prueba Rápida
# Cliente: Nivel 3 (Básico), Contrato Mensual (0), 22 días activo, 7 GB consumo
# Esto: cliente_nuevo = [[3, 0, 22.0, 1, 0]] no coincidia con las columnas de entrenamiento
cliente_nuevo = [[3, 0, 22.0, 7.0]] # Asegúrate que coincida con las columnas de entrenamiento
print("Predicción de Retención (0=Se va, 1=Se queda):", predictor.predict(cliente_nuevo))
```


Modifique los valores de `cliente_nuevo` para que correspondieran con el dataset de entrenamiento

```python
cliente_nuevo = [[3, 0, 22.0, 7.0]]
```

En vez de:

```python
cliente_nuevo = [[3, 0, 22.0, 1, 0]]
```


## **⚠️ PASO CRÍTICO: Limpieza de Recursos**


```python
import boto3

sm_client = boto3.client('sagemaker')
endpoint_name = 'sagemaker-scikit-learn-2025-12-06-20-32-52-873'

try:
    print(f"Eliminando endpoint {endpoint_name}...")
    sm_client.delete_endpoint(EndpointName=endpoint_name)
    print("Endpoint eliminado")
except Exception as e:
    print(f"Info: {e}")
```






### **🧠 Preguntas de Control (Nivel Infraestructura)**

1. **Instancias T vs M:** En la `TAREA 4` usamos una instancia `ml.t3.medium` para entrenar. Esta instancia funciona con un sistema de "créditos de CPU" (Burstable). ¿Por qué esta instancia es adecuada para este dataset pequeño pero podría ser peligrosa si tuviéramos 500 GB de datos para entrenar durante 10 horas seguidas?

> Porque obviamente
> 1. Agotarías los creditos en poco tiempo
> 2. Tendrías que pagar mucho más

    
2. **Costos Fantasma:** Si borras el Endpoint (`predictor.delete_endpoint()`) pero olvidas apagar tu **Notebook Instance** (donde estás escribiendo el código ahora mismo), ¿AWS te sigue cobrando?

> Si, qye que la instancia del notebook, por ejemplo en mi caso `ml.t3.medium` tiene un costo por hora que se permanece cobrando

    
3. **Seguridad y Argumentos:** ¿Qué pasaría si en el diccionario de `hyperparameters` del paso 4 escribes `{'n_estimators': 100}` en lugar de `{'n-arboles': 100}`? Explica el error basándote en cómo configuraste el `argparse` en tu script.

> Habrá un error, ya que con parser definimos los argumentos **`n_arboles`** y no **`n_estimators`**, entonces el script espera esos argumentos definidos con **parser**, sin embargo luego mapea esos argumentos que recibira el modelo. Pero si o si, de debe respetar los argumentos definidos con parser, sino ocurrida un error. 