


<div style="text-align:center">
<img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*IQb3NTMtOEKOINcCRXIMQg.jpeg
" />
</div>

## Features

Estas son algunas de las características responsables de la popularidad de Apache Spark:

1. **Velocidad de Procesamiento Rápida**
    
    La velocidad ha sido el principal atractivo de Apache Spark desde sus inicios. ==Ofrece un rendimiento hasta 100 veces más rápido en memoria y 10 veces más rápido en disco en comparación con Hadoop MapReduce==. Spark ha establecido récords mundiales en clasificación de datos a gran escala, demostrando su velocidad ultrarrápida.
    
2. **Almacenamiento en Caché (Caching)**
    
    El rendimiento es clave para cualquier aplicación de Big Data. El almacenamiento en caché (o persistencia) en Spark permite almacenar DataFrames o RDDs en memoria, lo que ==puede generar una mejora de 10 a 100 veces en el rendimiento de las aplicaciones, al evitar recalcular transformaciones repetitivas==.
    
3. **Despliegue y Compatibilidad**
    
    Spark es muy flexible y puede ejecutarse en diversos entornos, incluyendo ==Hadoop YARN, Apache Mesos, Kubernetes, en modo Standalone (independiente) o en la nube==. Además, puede conectarse a múltiples fuentes de datos.
    
4. **Procesamiento en Tiempo Real**
    
    A diferencia del modelo MapReduce de Hadoop que solo procesa datos almacenados, Spark puede manejar tanto ==cargas de trabajo por lotes (batch)== como ==procesamiento en tiempo real a través de su librería Spark Streaming==.
    
5. **Polyglot: Soporte para Múltiples Lenguajes**
    
    Las aplicaciones de Spark se pueden escribir en ==varios lenguajes como Scala, Java, Python, R y Clojure==. Gracias a sus APIs de alto nivel y a un shell interactivo para Python y Scala, los desarrolladores pueden trabajar con su lenguaje de preferencia.
    
6. **Bibliotecas Poderosas**
    
    El ecosistema de Spark va más allá de las operaciones básicas de procesamiento de datos. Incluye librerías especializadas como ==Spark SQL== (para consultas SQL y DataFrames), ==MLlib== (para Machine Learning), ==GraphX== (para procesamiento de grafos) y ==Spark Streaming==, que ofrecen herramientas avanzadas para todo tipo de análisis.
    

---

# Arquitectura

<div style="text-align:center">
<img src="https://img-blog.csdn.net/20170911221635721?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvaGp3MTk5MDg5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center" />
</div>


Cuando se ejecuta una aplicación en Spark, el `Driver` es el programa principal que crea el `SparkContext`, el cual contiene las funciones básicas de Spark. El `Driver` incluye componentes clave como el **DAG Scheduler** y el **Task Scheduler**, que son responsables de traducir el código del usuario en trabajos que se ejecutan en el clúster.

El `Driver` colabora con un **Cluster Manager** para negociar y asignar los recursos necesarios para el trabajo. Una vez que el trabajo se divide en tareas más pequeñas, estas se distribuyen a los **Worker Nodes**. Dentro de cada `Worker Node`, los **Executors** son los procesos que finalmente ejecutan estas tareas y pueden almacenar datos en caché.

## Arquitectura de una Aplicación Spark

Una vista de alto nivel de la arquitectura de una aplicación Apache Spark es la siguiente:

### Spark Driver

==El **`Driver`** es el proceso maestro que coordina los **`Worker Nodes`** (nodos trabajadores) y supervisa la ejecución de las tareas==. ==Un trabajo (`Job`) de Spark se divide y se programa para ejecutarse en los **`Executors`** distribuidos en el clúster==.

El **`Driver`** crea el **`SparkContext`**, que actúa como la puerta de enlace principal para conectarse y comunicarse con el clúster. Es a través del `SparkContext` que se monitorea y coordina todo el trabajo. Cada `SparkSession` utiliza un `SparkContext` para interactuar con el clúster.

El **`Driver`** incluye componentes esenciales para planificar la ejecución, y es responsable de adquirir recursos de un **`Cluster Manager`**. Cuando se ejecuta un trabajo (`Job`) en el clúster, este se divide en **`Stages`** (etapas), que a su vez se componen de **`Tasks`** (tareas) que son programadas para su ejecución.

### Spark Executors

==Un **`Executor`** es un proceso lanzado en un `Worker Node` que es responsable de ejecutar las `Tasks` y almacenar datos en **`cache`**==. Al iniciarse la aplicación, los `Executors` se registran con el **`Driver`**.

Estos **`Executors`** disponen de recursos (como núcleos de CPU) para ejecutar múltiples `Tasks` en paralelo. Se ejecutan como procesos de la Máquina Virtual de Java (JVM) y ==su ciclo de vida está atado al de la aplicación Spark==. En configuraciones con asignación dinámica de recursos, los `Executors` pueden ser agregados o eliminados según la carga de trabajo. El **`Driver`** monitorea constantemente el estado y desempeño de los `Executors`.

### Cluster Manager

==El **`Cluster Manager`** es el componente responsable de adquirir y gestionar los recursos del clúster (como CPU y memoria) para la aplicación Spark==. Ejemplos comunes de `Cluster Managers` son YARN, Mesos o el modo Standalone de Spark.

Los **`Executors`**, una vez que son lanzados por el `Cluster Manager` en los `Worker Nodes`, se registran con el **`Driver`**. Estos procesos no solo ejecutan tareas, sino que también leen y escriben datos en fuentes externas. ==El **`Driver`** es quien monitorea a los `Executors` mientras realizan las tareas asignadas==.



De acuerdo, aquí tienes la corrección de la sección que faltaba, siguiendo los mismos criterios de antes para mejorar la precisión y la terminología.

---

## Worker Nodes

==Los **`Worker Nodes`** (nodos trabajadores) son las máquinas que componen el clúster y que alojan los procesos **`Executor`**==. Estos `Executors` son los que realmente procesan las **`Tasks`** (tareas) y devuelven los resultados al **`Driver`**.

El flujo correcto es que el **`Driver`** envía las `Tasks` a los `Executors` para que las ejecuten. La distribución de estas `Tasks` a través de los `Worker Nodes` permite manejar grandes volúmenes de trabajo en paralelo.

==En Spark, la unidad fundamental de los datos es la **partición**==. Cada `Task` generalmente procesa una partición de datos. Por lo tanto, un `Worker Node` aloja los `Executors` que ejecutan las `Tasks` asignadas por el `Driver` para procesar las particiones de datos distribuidas.


Vale la pena recordar los siguientes puntos sobre la arquitectura de Spark:

- **Aislamiento de Aplicaciones:** Cada aplicación de Spark obtiene sus propios procesos **`Executor`**, que se ejecutan en sus propias Máquinas Virtuales de Java (JVM). Esto aísla las aplicaciones entre sí: el **`Driver`** de cada aplicación programa sus tareas de forma independiente y los `Executors` de diferentes aplicaciones no interfieren entre ellos.
    
- **Intercambio de Datos:** Como consecuencia de este aislamiento, no se pueden compartir datos directamente entre diferentes aplicaciones de Spark a través de la memoria. Si dos aplicaciones necesitan trabajar sobre los mismos datos, estos deben ser leídos y escritos a través de un sistema de almacenamiento externo (como HDFS, S3, etc.).
    
- **Compatibilidad con Gestores de Recursos:** Spark puede operar eficientemente sobre un **`Cluster Manager`** que también gestiona otras aplicaciones (como Hadoop MapReduce o Flink). Siempre que el `Cluster Manager` (por ejemplo, YARN o Mesos) pueda asignarle recursos para lanzar sus `Executors`, Spark funcionará sin problemas.
    
- **Comunicación en Red:** Es fundamental que la red permita la comunicación bidireccional. El **`Driver`** debe poder conectarse con sus **`Executors`** para asignarles tareas, y los **`Executors`** deben poder conectarse de vuelta con el **`Driver`** para enviar sus resultados y estado.
    
- **Localidad del Driver:** El **`Driver`** es responsable de orquestar todo el trabajo, por lo que su ubicación en la red es importante. Debe ejecutarse en un nodo con baja latencia de red respecto a los **`Worker Nodes`** para evitar que la comunicación se convierta en un cuello de botella. Ejecutar el `Driver` lejos de los `Workers` puede degradar significativamente el rendimiento.



<div style="text-align:center">
<img src="https://www.interviewbit.com/blog/wp-content/uploads/2022/06/Worker-Nodes-550x600.png" width=400 />
</div>



## Modos de Ejecución

Spark se puede ejecutar en tres modos diferentes, los cuales determinan dónde se ubican físicamente los recursos de la aplicación (el `Driver` y los `Executors`).

- Modo Clúster (`Cluster Mode`)
- Modo Cliente (`Client Mode`)
- Modo Local (`Local Mode`)

**Modo Clúster** 
Es la forma más común de ejecutar aplicaciones en producción. En este modo, ==un usuario envía su aplicación== (un archivo JAR, un script de Python o R) ==al **`Cluster Manager`**. Este se encarga de lanzar el proceso **`Driver`** en uno de los **`Worker Nodes`** dentro del clúster, junto con los procesos **`Executor`**==. Esto significa que el `Cluster Manager` gestiona el ciclo de vida de todos los procesos de la aplicación Spark.

**Modo Cliente**
A diferencia del modo clúster, ==el proceso **`Driver`** se ejecuta en la máquina cliente desde la cual se envió la aplicación== (también conocida como _gateway_ o _edge node_). La máquina cliente es responsable de mantener vivo el proceso `Driver`, mientras que los **`Executors`** sí se ejecutan en el clúster. Este modo ==es útil para trabajos interactivos donde se necesita una respuesta inmediata en la consola del cliente==.

**Modo Local**
En este modo, ==toda la aplicación Spark (tanto el `Driver` como los `Executors`) se ejecuta en una sola máquina, utilizando múltiples **`threads`** (hilos) para simular el paralelismo==. No utiliza procesos distribuidos. Es una forma común de desarrollar, probar y experimentar con Spark sin la necesidad de un clúster, pero **no se recomienda para ejecutar aplicaciones en producción**.


## Tipos de Administradores de Clústeres

Hay varios `Cluster Managers` compatibles con Spark:

### Standalone

Es el gestor de clústeres simple que viene incluido en Spark, ideal para una configuración rápida. Sus componentes principales son un nodo **`Master`** (que actúa como gestor de recursos) y varios nodos **`Worker`**. Cuando el `Driver` de una aplicación se conecta al `Master`, este último lanza los `Executors` en los `Workers` disponibles.

<div style="text-align:center">
<img src="https://www.interviewbit.com/blog/wp-content/uploads/2022/06/Standalone-768x389.png" />
</div>



### Apache Mesos

Es un gestor de recursos de clúster de propósito general que puede compartir y aislar recursos dinámicamente entre diferentes `frameworks` (como Spark, Hadoop MapReduce, etc.). Sus tres componentes principales son:
    
- **Mesos Master:** Proporciona tolerancia a fallos y coordina a los nodos `Slave`.
    
- **Mesos Slave:** Es un nodo que ofrece los recursos de su máquina al `Master` para que este pueda asignarlos a los `frameworks`.
    
- **Mesos Frameworks:** Son las aplicaciones, como Spark, que se registran con el `Master` para solicitar recursos y ejecutar sus tareas.
    

<div style="text-align:center">
<img src="https://www.interviewbit.com/blog/wp-content/uploads/2022/06/Apache-Mesos-1024x545.png" width=500/>
</div>


### ¿Qué son los RDD, DataFrames y Datasets?

Para continuar con la analogía de la cocina, estas son las formas de organizar los "ingredientes" (datos) en Spark:

- **RDD (Resilient Distributed Dataset):** Es como tener bolsas de ingredientes desordenadas pero resistentes. Puedes hacer cualquier receta (`operaciones`), pero necesitas dar instrucciones muy detalladas (`escribir mucho código`). Es flexible pero más complejo y manual.
    
- **DataFrame:** Es como tener los ingredientes ya organizados en bandejas etiquetadas (`columnas con nombre y tipo`). Es mucho más ordenado y fácil de procesar. Puedes aplicar instrucciones más generales (como "asa todas las verduras") sin preocuparte por cada paso individual, ya que Spark optimiza la ejecución.
    
- **Dataset:** (Principalmente en Scala/Java) Es una combinación de la estructura optimizada de un `DataFrame` y la flexibilidad de un `RDD`, añadiendo chequeo de tipos en tiempo de compilación para mayor seguridad.


### YARN (Yet Another Resource Negotiator)

YARN es como el gerente del edificio donde ocurre el festival. Se asegura de que no todos los cocineros usen el horno al mismo tiempo, que nadie se quede sin espacio de trabajo, y que todas las tareas estén bien distribuidas entre las estaciones disponibles.

==Cuando ejecutas un programa en Spark con YARN, el Cluster Manager de Spark habla con YARN para pedir recursos. YARN le asigna contenedores (espacios de trabajo), y en esos espacios Spark lanza sus executors. Esto permite que múltiples trabajos (no solo de Spark, sino también de otras herramientas como Hive, Flink, etc.) puedan coexistir en un mismo clúster sin conflictos.==

**Componentes de YARN:**       

- **Resource Manager:** Es el maestro global que gestiona la asignación de recursos entre todas las aplicaciones del clúster.
    
- **Node Manager:** Es un agente que se ejecuta en cada `Worker Node`, responsable de lanzar y monitorear los `Containers` en esa máquina específica.
    

<div style="text-align:center">
<img src="https://www.interviewbit.com/blog/wp-content/uploads/2022/06/Hadoop-YARN-1024x679.png" width=500/>
</div>



---

# Transición a SparkSQL

Si los `RDDs` y `DataFrames` son como preparar ingredientes con instrucciones detalladas, **SparkSQL** es como darle a nuestro equipo de cocina una receta en un lenguaje de alto nivel (SQL) y dejar que el motor la interprete y optimice automáticamente. Con SparkSQL, podemos realizar consultas complejas sobre grandes volúmenes de datos estructurados usando el conocido lenguaje SQL, aprovechando el motor de optimización **Catalyst** para una ejecución eficiente.

### ¿Por qué optimizar antes del entrenamiento?

En machine learning, el rendimiento de un modelo depende en gran medida de la eficiencia con la que se acceden y transforman los datos. Optimizar antes de entrenar significa reducir el volumen de datos innecesarios, corregir inconsistencias y usar formatos de almacenamiento eficientes. Esto impacta directamente en:

- **Velocidad:** Reducir los tiempos de entrenamiento implica ==filtrar los datos innecesarios, evitar transformaciones costosas durante la ejecución y utilizar estructuras de almacenamiento optimizadas==. Esto permite iterar más rápidamente sobre distintos modelos y enfoques.
    
- **Escalabilidad:** ==Un flujo de datos que funciona en pequeña escala puede colapsar al trabajar con millones de registros== si no se han considerado aspectos como el particionado lógico, el uso de ==formatos columnares== o el acceso selectivo a columnas relevantes.
    
- **Eficiencia del modelo:** La calidad de los datos y la forma en que son consultados tienen un impacto directo en la capacidad del modelo para generalizar. ==Datos mal consolidados, desbalanceados o contaminados por errores de consulta pueden degradar severamente la precisión y robustez del modelo.==
    

### Casos prácticos que ilustran la necesidad de optimización

En entornos reales, es común encontrar proyectos de analítica que fracasan o se estancan no por errores en los algoritmos, sino por fallas en la ingeniería previa de datos. Por ejemplo, empresas que intentan predecir la demanda agregando múltiples fuentes de datos sin una normalización adecuada, o sin control sobre la calidad del join entre tablas, enfrentan modelos lentos, inestables y poco fiables. Otro caso frecuente es el uso de archivos planos mal estructurados para entrenar modelos complejos, lo que genera tiempos de carga extensos, duplicación de registros y errores silenciosos en la interpretación de campos.

---

# SparkSQL

==SparkSQL es un módulo de Apache Spark que permite ejecutar consultas SQL sobre datos distribuidos==. Combina la expresividad de SQL con la escalabilidad y el poder del procesamiento paralelo de Spark. Podemos consultar grandes volúmenes de datos estructurados, aplicar filtros, agrupaciones, ordenamientos y uniones con una sintaxis clara, y todo eso se traduce automáticamente en tareas distribuidas que Spark ejecuta de forma eficiente. Además, SparkSQL no es solo “azúcar sintáctico” sobre DataFrames, ==internamente utiliza un motor de optimización llamado Catalyst, que analiza las consultas, las reorganiza y genera planes de ejecución altamente optimizados==.

SparkSQL nos permite

- Escribir consultas complejas en un lenguaje declarativo (SQL).
- Aprovechar la optimización automática de Catalyst.
- Integrar sin problemas con otros lenguajes como Python, Scala o Java.
- Trabajar con múltiples formatos de datos (CSV, Parquet, JSON, JDBC, etc.).
- Y combinar SQL con operaciones de DataFrame imperativas.

### DataFrames vs. SQLContext vs. SparkSession

- **DataFrame:** Es una ==estructura de datos tabular== (similar a una hoja de Excel o una tabla de SQL) que permite aplicar operaciones como ==`select`, `filter`, `groupBy`==, etc. Representa una ==colección de datos estructurados distribuidos en múltiples nodos==.
    
- **`SQLContext`:** Fue la forma original de ejecutar SQL en Spark, pero ya está obsoleta. Era un objeto necesario para crear `DataFrames` y consultar datos usando SQL.
    
- **`SparkSession`:** Introducido en Spark 2.0, es el punto de entrada unificado y moderno. Hoy en día, siempre ==se trabaja a través de una `SparkSession` para acceder a todas las funcionalidades de Spark==.


``

### Integración de SQL y Python en Databricks

En entornos como Databricks, puedes trabajar con SparkSQL de dos formas:

**1. Consultas SQL directas con `%sql`**

Puedes escribir una celda que comience con `%sql` y luego escribir una consulta como:

```sql
SELECT nombre, edad FROM usuarios WHERE edad > 30
```

**2. Consultas con la API de DataFrame en Python**

Alternativamente, puedes escribir la misma consulta en Python usando la sintaxis de DataFrame, algo como:

```python
df.select("nombre", "edad").where(df.edad > 30)
```

Esto te permite combinar la expresividad de SQL con la flexibilidad del lenguaje de programación. Ambas opciones son válidas y terminan ejecutando el mismo tipo de plan lógico de ejecución gracias al motor interno llamado Catalyst Optimizer.

#### Ejemplos típicos en Databricks

Supongamos que tienes un archivo `usuarios.csv` cargado en Databricks, con columnas como `id`, `nombre`, `edad` y `ciudad`.

Una vez que lo lees como DataFrame, puedes registrar ese DataFrame como una ==vista temporal== llamada usuarios. Esto le dice a Spark que puede usar ese nombre como si fuera una tabla de base de datos.

A partir de ahí, puedes hacer cosas como:

Filtrar usuarios mayores de 30 años:

```sql
SELECT nombre, edad FROM usuarios WHERE edad > 30
```

Contar cuántas usuarios hay por por ciudad:

```sql
SELECT ciudad, COUNT(*) AS total FROM usuarios GROUP BY ciudad
```

Ordenar las ciudades con más usuarios:

```sql
ORDER BY total DESC
```

al final de la consulta anterior para obtener un ranking.

Por otro lado, si prefieres hacerlo con la API de DataFrame, puedes usar métodos como `.filter()`, `.select()`, `.groupBy()` y `.orderBy()` para lograr exactamente lo mismo.

Un detalle importante es que, en Databricks, puedes usar la función especial `display()` para mostrar los resultados. Esta función no solo imprime los datos en forma de tabla, sino que permite ordenarlos, filtrarlos o incluso graficarlos sin necesidad de escribir código adicional.

---

# Catalyst Optimizer

==Catalyst es el motor de optimización de consultas que utiliza Apache Spark==. Cuando escribimos una consulta SQL o una operación sobre un DataFrame, Spark no la ejecuta inmediatamente. En lugar de eso, genera una representación abstracta del plan que debería seguir para obtener el resultado, y luego aplica una serie de ==optimizaciones automáticas== para mejorar el rendimiento. 

Catalyst se encarga de tomar esa instrucción inicial —que puede estar escrita en SQL o como una serie de comandos en Python/Scala— y transformarla paso a paso en algo que se pueda ejecutar eficientemente sobre un clúster.

Podemos pensar en Catalyst como una “cadena de montaje” donde la consulta pasa por cuatro etapas. Vamos a explicar cada una con una analogía sencilla:

**1. Análisis (Parsing + Resolución de nombres)**

- Revisa la sintaxis de la consulta (por ejemplo: que no falten comillas o paréntesis).
- Verifica que todas las columnas mencionadas existan.
- Traduce la consulta a un árbol lógico (una estructura interna que representa paso a paso lo que debe hacerse).

Ejemplo: si escribes `SELECT edad FROM usuarios WHERE ciudad = 'Lima'`, Spark se asegura de que edad y ciudad existan como columnas en el DataFrame o tabla usuarios.

**2. Optimización lógica**
Una vez que Spark entendió lo que queremos hacer, intenta mejorar el plan, sin cambiar su resultado. Aquí aplica reglas de álgebra relacional, como:

- Reordenar filtros para que se apliquen antes (filtrar menos datos más rápido).
- Eliminar columnas innecesarias.
- Simplificar operaciones redundantes.

**Ejemplo**: si pides primero todas las columnas y luego haces un SELECT nombre, Catalyst puede eliminar las otras columnas desde el inicio.


**3. Planificación física (Physical Planning)

==Aquí es donde Spark decide cómo ejecutar la consulta en términos concretos: cuántos procesos lanzar, cómo distribuir los datos, qué algoritmos usar==.

Spark puede generar varios planes físicos y luego elegir el que tenga el menor costo estimado. Ese costo se calcula en función de cosas como el tamaño de los datos, si están en memoria o en disco, o si están repartidos en varias máquinas.

**4. Generación del plan de ejecución (Code Generation)

==Finalmente, Spark genera código bytecode en tiempo real que puede ser ejecutado directamente por la JVM== (la máquina virtual de Java). Esto hace que Spark sea extremadamente rápido, porque ya no interpreta los pasos uno por uno, sino que ejecuta un plan ya compilado.


---

# Almacenamiento Columnar: Parquet

**Parquet** es un ==formato de archivo diseñado para el almacenamiento columnar==. A diferencia de formatos basados en filas como CSV, donde se debe leer la fila completa para acceder a un solo valor, Parquet almacena los datos columna por columna.

**¿Por qué es más eficiente?**

Imagina que tienes una lista de 10 mil platos servidos en un restaurante, cada uno con información como: nombre del cliente, plato pedido, hora de la comida, propina, forma de pago. 

Si quieres saber cuánto dejaron de propina los clientes, no necesitas revisar toda la información de cada fila: solo necesitas la columna de propinas. Si el archivo está en formato CSV, tienes que leer cada línea completa, aunque solo te interese una parte. Con Parquet, puedes leer directamente solo la columna de interés, lo que ahorra muchísimo tiempo y memoria.

Además, Parquet:

- **Comprime mejor los datos**, ya que los valores de una misma columna suelen ser similares y fáciles de comprimir.
    
- **Conserva el esquema** (los tipos de datos de cada columna).
    
- Está **altamente optimizado** para motores de procesamiento distribuido como Spark.
    

### Comparación de Formatos

|Formato|Estructura|Compresión|Velocidad de Lectura (Selectiva)|Ideal para...|
|---|---|---|---|---|
|**CSV**|Fila por fila|No nativa|Lento|Datos simples o exportaciones rápidas|
|**JSON**|Semi-estructurado (texto)|Media|Lento a medio|Datos con estructuras anidadas o complejas|
|**Parquet**|Columna por columna|Alta|Muy rápido|Análisis de datos, Big Data, Machine Learning|