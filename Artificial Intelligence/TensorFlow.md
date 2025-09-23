
# Introducción
TensorFlow es una biblioteca de **código abierto** desarrollada por **Google** para realizar tareas de aprendizaje automático y, más específicamente, de **aprendizaje profundo (Deep Learning)**. Lo puedes pensar como una gran herramienta que te ayuda a construir y entrenar redes neuronales, que son modelos matemáticos diseñados para imitar la forma en que funciona el cerebro humano.


#### ¿Qué es el aprendizaje profundo y por qué TensorFlow es útil?
El aprendizaje profundo es una técnica de **aprendizaje automático** que se basa en redes neuronales artificiales. Este tipo de redes tiene muchas "capas", como una cebolla. Cada capa toma una entrada (como una imagen o un dato), la procesa y la pasa a la siguiente capa. Cuantas más capas tiene, más compleja es la representación que puede crear de los datos.

TensorFlow es útil porque automatiza gran parte de las operaciones matemáticas complejas detrás de estas redes neuronales. No necesitas escribir a mano todas las ecuaciones, porque TensorFlow ya tiene eso cubierto.

#### ¿Qué es TensorFlow?

TensorFlow es una **biblioteca de software** diseñada para construir y entrenar **modelos de aprendizaje automático**. Es como una **fábrica inteligente** que te ayuda a automatizar la tarea de aprender patrones a partir de datos, y luego usar esos patrones para hacer predicciones. Lo poderoso de TensorFlow es que maneja operaciones matemáticas complejas en segundo plano, permitiéndote enfocarte en el diseño y el entrenamiento de tus modelos.

#### ¿Cómo funciona TensorFlow?

TensorFlow utiliza un concepto llamado **"grafo computacional"**. Imagínate un grafo como un **mapa de instrucciones** que muestra cómo los datos fluyen a través de tu red neuronal. En lugar de hacer cada operación una a una, TensorFlow te permite definir todas las operaciones por adelantado en forma de grafo. Luego, ese grafo se ejecuta para entrenar el modelo.

- **Tensores:** La unidad básica de datos en TensorFlow es un "tensor", que es básicamente un arreglo multidimensional. Puedes pensar en un tensor como una caja de datos con diferentes dimensiones. Si piensas en una foto en blanco y negro, es una caja de dos dimensiones (alto y ancho). Si piensas en una imagen a color, es una caja de tres dimensiones (alto, ancho y color). 
  - Ejemplo: Un tensor de 3 dimensiones podría ser una imagen de 64x64 píxeles con 3 canales de color (rojo, verde y azul).

- **Flujo (Flow):** Una vez que tienes tus tensores, los envías a través de un "grafo" de operaciones matemáticas. Cada nodo en este grafo es una operación (por ejemplo, suma, multiplicación, convolución). El flujo de tensores a través de este grafo es lo que da nombre a TensorFlow (Flujo de Tensores).

#### Alcances de TensorFlow

TensorFlow es extremadamente poderoso y versátil, pero para mantenerlo accesible en esta explicación introductoria, destacaré algunos de los usos más comunes y sus límites:

1. **Aprendizaje Supervisado:** TensorFlow es ampliamente utilizado para tareas de aprendizaje supervisado, donde tienes datos etiquetados (ejemplo: imágenes con etiquetas que indican qué objeto aparece en cada una). Puedes entrenar modelos para hacer predicciones, como la clasificación de imágenes, el reconocimiento de voz o la predicción de texto.

2. **Redes Neuronales Convolucionales (CNNs):** Estas redes son especialmente buenas para procesar datos que tienen una estructura de grilla, como imágenes. TensorFlow permite construir CNNs fácilmente, que se utilizan en problemas de visión por computadora.

3. **Redes Neuronales Recurrentes (RNNs):** TensorFlow también facilita la construcción de modelos que procesan datos secuenciales, como texto, audio o series temporales (por ejemplo, el precio de las acciones). Las RNNs y sus variantes, como las LSTMs, se usan mucho en procesamiento del lenguaje natural (NLP).

4. **Aprendizaje por Refuerzo:** Este es un tipo de aprendizaje en el que un "agente" aprende interactuando con un entorno y recibiendo recompensas o castigos. TensorFlow se usa para construir sistemas de aprendizaje por refuerzo que entrenan agentes para jugar juegos, conducir coches autónomos o manejar robots.

5. **TensorFlow Lite:** Esto es una versión optimizada para dispositivos móviles y sistemas embebidos. Permite desplegar modelos de aprendizaje profundo en dispositivos con menos capacidad de procesamiento, como teléfonos inteligentes o dispositivos de IoT.

6. **TensorFlow.js:** Esta versión permite ejecutar modelos de aprendizaje profundo en el navegador usando JavaScript. Esto abre la puerta para llevar modelos directamente a aplicaciones web sin necesidad de un servidor que haga los cálculos.

7. **TensorFlow Extended (TFX):** TensorFlow no es solo para entrenar modelos, sino que también ayuda a llevar los modelos entrenados a producción con TFX, que es un conjunto de herramientas para el flujo de trabajo completo: desde la preparación de datos hasta el despliegue del modelo y la supervisión en producción.

### Alcances y Limitaciones

#### Alcances:
1. **Versatilidad:** TensorFlow se puede usar tanto en modelos muy simples como en arquitecturas extremadamente complejas. Esto lo hace útil tanto para principiantes como para investigadores avanzados.
  
2. **Escalabilidad:** Se puede ejecutar en CPUs, GPUs, TPUs y en grandes clústeres de computadoras. Si tienes un problema con grandes cantidades de datos, TensorFlow te permite escalar tu modelo a múltiples máquinas sin cambiar demasiado tu código.

3. **Compatibilidad con otros lenguajes:** Aunque se usa principalmente en Python, TensorFlow también se puede utilizar en otros lenguajes como C++ y JavaScript.

4. **Modelos preentrenados:** TensorFlow tiene una gran cantidad de modelos ya entrenados que puedes usar y adaptar a tu problema sin tener que entrenar desde cero.

#### Limitaciones:
1. **Curva de aprendizaje:** A pesar de que TensorFlow ha simplificado mucho las cosas con su API de alto nivel (Keras), sigue siendo una herramienta con una curva de aprendizaje bastante empinada para los principiantes.

2. **Optimización manual:** Aunque TensorFlow automatiza muchas cosas, en modelos más avanzados, puede que tengas que hacer ajustes manuales para optimizar tu rendimiento, lo cual puede volverse complicado.

3. **Tamaño del modelo:** Algunos modelos de aprendizaje profundo son enormes y no siempre es fácil desplegarlos en dispositivos más pequeños sin reducir su precisión.

### Ejemplo sencillo en TensorFlow

Vamos a construir un modelo básico con TensorFlow usando su API de alto nivel, **Keras**, para realizar una simple tarea de clasificación:



```python
import tensorflow as tf
from tensorflow.keras import layers

# Definir el modelo
model = tf.keras.Sequential([
    layers.Dense(64, activation='relu', input_shape=(784,)),
    layers.Dense(64, activation='relu'),
    layers.Dense(10, activation='softmax')
])

# Compilar el modelo
model.compile(optimizer='adam', 
              loss='sparse_categorical_crossentropy', 
              metrics=['accuracy'])

# Datos de ejemplo (supón que tienes X_train y y_train)
# Entrenamiento del modelo
model.fit(X_train, y_train, epochs=5)

# Evaluar el modelo
model.evaluate(X_test, y_test)
```

En este ejemplo, hemos creado una red neuronal con dos capas ocultas de 64 neuronas cada una, y una capa de salida de 10 neuronas (suponiendo que estamos clasificando en 10 categorías). Entrenamos el modelo en un conjunto de datos `X_train` y `y_train` y luego lo evaluamos en un conjunto de prueba `X_test` y `y_test`.

### ¿Qué es la validación cruzada?

Cuando entrenamos un modelo de machine learning, queremos asegurarnos de que no solo funcione bien en los datos que ha visto (datos de entrenamiento), sino que también pueda generalizar a datos nuevos que no ha visto antes. Aquí es donde entra la **validación cruzada**.

Imagina que estás preparando un examen y tienes un libro lleno de preguntas. Si solo te preparas con unas pocas páginas del libro (datos de entrenamiento) y luego te haces una prueba solo con esas páginas, puedes llegar a aprenderte las respuestas de memoria. Esto sería equivalente a que tu modelo se está **sobreajustando**: funciona muy bien en los datos de entrenamiento pero falla en datos nuevos. La validación cruzada te ayuda a evitar este problema.

#### ¿Cómo funciona?

La validación cruzada es un método para evaluar la capacidad de generalización de tu modelo. El enfoque más común es el llamado **validación cruzada k-fold**. Aquí está la idea básica:

1. **Divide tu conjunto de datos** en **k grupos (o "folds")**. Supongamos que tienes 1000 datos y decides hacer una validación cruzada con **k=5**, entonces dividirías tu conjunto de datos en 5 grupos de 200 datos cada uno.
   
2. **Entrena el modelo k veces**, cada vez usando **k-1 folds como conjunto de entrenamiento** y el fold restante como **conjunto de validación**. Esto significa que entrenarás el modelo 5 veces, y cada vez usarás un fold diferente como conjunto de validación.

   - En la primera iteración, usarás el primer fold como datos de validación y los otros cuatro como datos de entrenamiento.
   - En la segunda iteración, usarás el segundo fold como datos de validación, y así sucesivamente.

3. **Calcula el rendimiento promedio** de tu modelo en las k pruebas. Esto te dará una mejor idea de qué tan bien está generalizando tu modelo a nuevos datos.

De esta manera, el modelo se entrena varias veces y cada parte del conjunto de datos se usa tanto para entrenar como para validar. Esto evita que el rendimiento dependa demasiado de una partición específica de los datos.

### Ventajas de la validación cruzada

1. **Mejor estimación del rendimiento del modelo:** Debido a que evalúas el modelo en diferentes subconjuntos de los datos, obtienes una mejor estimación de cómo funcionará tu modelo en datos que no ha visto antes. Esto reduce el riesgo de tener una estimación demasiado optimista o demasiado pesimista.
   
2. **Aprovechas al máximo los datos:** En lugar de simplemente dividir tu conjunto de datos en dos (entrenamiento y prueba), la validación cruzada permite que **cada dato** participe tanto en el entrenamiento como en la validación.

3. **Evitar el sobreajuste (overfitting):** Al probar el modelo en diferentes subconjuntos, es más probable que detectes si tu modelo está ajustándose demasiado a los datos de entrenamiento y no está generalizando bien.

### Ejemplo paso a paso con K-Fold Validation

Vamos a suponer que tienes un conjunto de datos de 1000 ejemplos, y decides usar validación cruzada con **k=5**:

1. **División de los datos**: Se dividen los 1000 ejemplos en 5 grupos de 200 ejemplos cada uno:
   - Fold 1: Datos 1 a 200
   - Fold 2: Datos 201 a 400
   - Fold 3: Datos 401 a 600
   - Fold 4: Datos 601 a 800
   - Fold 5: Datos 801 a 1000

2. **Primera iteración**: 
   - Entrenas tu modelo usando los datos de los **folds 2, 3, 4 y 5** (800 ejemplos).
   - Validas tu modelo usando los datos del **fold 1** (200 ejemplos).

3. **Segunda iteración**:
   - Entrenas tu modelo usando los datos de los **folds 1, 3, 4 y 5**.
   - Validas tu modelo usando los datos del **fold 2**.

4. **Siguiente iteración**: Repites el proceso para los siguientes folds, hasta que hayas validado usando cada fold.

5. **Cálculo final**: Al final, calculas el promedio de las métricas de rendimiento (por ejemplo, precisión o error) que obtuviste en cada iteración.

#### Código de ejemplo en TensorFlow usando Keras

Afortunadamente, TensorFlow hace que la validación cruzada sea bastante fácil con la API de `Keras`. Aquí tienes un ejemplo sencillo usando `K-fold`:

```python
import numpy as np
import tensorflow as tf
from sklearn.model_selection import KFold

# Datos de ejemplo (X son las características, y las etiquetas)
X = np.random.rand(1000, 20)  # 1000 ejemplos con 20 características
y = np.random.randint(0, 2, 1000)  # Etiquetas binarias (0 o 1)

# Definir el modelo
def create_model():
    model = tf.keras.Sequential([
        tf.keras.layers.Dense(64, activation='relu', input_shape=(20,)),
        tf.keras.layers.Dense(64, activation='relu'),
        tf.keras.layers.Dense(1, activation='sigmoid')  # salida binaria
    ])
    model.compile(optimizer='adam',
                  loss='binary_crossentropy',
                  metrics=['accuracy'])
    return model

# Configurar la validación cruzada K-fold
k = 5
kf = KFold(n_splits=k)

# Almacenar las puntuaciones de precisión
accuracy_scores = []

# Validación cruzada
for train_index, val_index in kf.split(X):
    X_train, X_val = X[train_index], X[val_index]
    y_train, y_val = y[train_index], y[val_index]
    
    model = create_model()  # Crear un nuevo modelo para cada fold
    model.fit(X_train, y_train, epochs=5, verbose=0)  # Entrenamos el modelo
    score = model.evaluate(X_val, y_val, verbose=0)  # Evaluar en los datos de validación
    accuracy_scores.append(score[1])  # Guardamos la precisión (índice 1)

# Resultado final
print(f'Precisión promedio en {k} folds: {np.mean(accuracy_scores)}')
```

### Explicación del código:
1. **`create_model()`**: Es una función que crea un modelo simple de red neuronal para clasificación binaria.
2. **`KFold()`**: De `sklearn`, es la herramienta que nos ayuda a dividir nuestros datos en los diferentes folds.
3. **`kf.split(X)`**: Esto divide los datos `X` en los índices de entrenamiento y validación correspondientes para cada fold.
4. **`model.fit()`**: Entrenamos el modelo en los datos de entrenamiento (los folds que no están en validación).
5. **`model.evaluate()`**: Evaluamos el modelo en los datos de validación.

### Conclusión

La validación cruzada es una técnica fundamental para asegurarse de que el modelo de aprendizaje automático no solo memorice los datos de entrenamiento, sino que también generalice bien a datos nuevos. Es particularmente útil cuando tienes una cantidad limitada de datos y no quieres desperdiciar información al dividir el conjunto de datos en solo dos partes (entrenamiento y prueba).

¿Te queda más claro el concepto de validación cruzada? ¿Te gustaría practicar con algún ejemplo específico o necesitas aclaración en algún detalle técnico?



# Funciones de perdida (`loss`)

La función de pérdida mide qué tan bien o mal está funcionando el modelo durante el entrenamiento. La idea es que el modelo intente minimizar esta pérdida en cada paso, lo que mejora su rendimiento.

## `sparse_categorical_crossentropy`
Esta es una función de pérdida especifica para problemas de clasificación multiclase, cuando las etiquetas (clases) están en formato de enteros (por ejemplo, 0, 1, 2, ...).
Calcula la distancia entre la distribución de salida del modelo (que devuelve probabilidades para cada clase) y la clase verdadera. La `crossentropy` penaliza fuertemente las predicciones incorrectas y da menos penalización cuando la probabilidad asignada a la clase correcta es alta.

### Diferencia con `categorical_crossentropy`
Ambas se usan para clasificación multiclase, pero con `categorical_crossentropy`, las etiquetas deben estar en formato *one-hot-encoded* (vectores binarios como [1, 0, 0, ...]).


# Optimizadores (`optimizer`)

Este parámetro especifica el algoritmo que se usará para ajustar los pesos del modelo durante el entrenamiento. En redes neuronales, el optimizador es crucial porque determina cómo el modelo aprende a mejorar sus predicciones en cada paso de entrenamiento.
## `adam`
De **Adam** (Adaptive Moment Estimation) es un optimizador avanzado que combina las ventajas de otros optimizadores como **AdaGrad** y **RMSProp**.

Adam adapta la tasa de aprendizaje individual para cada parámetro basándose en el promedio de los gradientes y la varianza (es decir, ajusta de acuerdo con cuán rápido cambia el error).


# Functions

## `tf.random.uniform`

Generates random values from a **uniform distribution**, where every number in the given range has the same probability of being chosen.

```python
tf.random.uniform(shape, minval=0, maxval=1, dtype=tf.float32, sed=None, name=None)
```

- `shape` : Tuple or list of integers. (3x2 tensor: `shape=(3, 2)`)
- `minval` : Lower vound of the uniform distribution, inclusive. Default 0
- `maxval` : Upper bound of the uniform distribution, exclusive. Default 1
- `seed` : Sets a random seed for reproducibility
- `name` : Name of the operation (useful for graph naming)


---




# Introduction to TensorFlow in Python


## Introduction to TensorFlow

**TensorFlow is**

- Open-source library for graph-based numerical computation
	- Developed by the Google Brain Team
- **Low and high level APIs**
	- Addition, multiplication, differentiation
	- Machine learning models
- Important changes in TensorFlow 2.0
	- Eager execution by default
	- Model building with Keras and Estimators

 
### Tensors in TensorFlow

```python
import tensorflow as tf

# 0D Tensor
d0 = tf.ones((1,))

# 1D
d1 = tf.ones((2,))

# 2D
d2 = tf.ones((2, 2))

# 3D
d3 = tf.ones((2, 2, 2))

# Print 3D tensor
print(d3.numpy())
# [[[1. 1.] 
#  [1. 1.]] 
# [[1. 1.] 
#  [1. 1.]]]
```


<h5>Constants in TensorFlow</h5>
- A constant is the simples category of a tensor
	- Not trainable
	- Can have any dimension


```python
from tensorflow import constant

# 2x3 constant
a = constant(3, shape=[2, 3])
```


**Convenience functions to define constants**


| Operation         | Example                    |
| ----------------- | -------------------------- |
| `tf.constant()`   | `constant([1, 2, 3, 4]`    |
| `tf.zeros()`      | `zeros([2, 2])`            |
| `tf.zeros_like()` | `zeros_like(input_tensor)` |
| `tf.ones()`       | `ones([2, 2])`             |
| `tf.ones_like()`  | `ones_like(input_tensor)`  |
| `tf.fill()`       | `fill([3, 3], 7)`          |

<h5>Variables</h5>

```python
import tensorflow as tf

a0 = tf.Variable([1, 2, 3, 4, 5, 6], dtype=tf.float32)
a1 = tf.Variable([1, 2, 3, 4, 5, 6], dtype=tf.int16)

# Define a constant
b = tf.constant(2, tf.float32, (2, 1))

# Compute their product
# Both element-wise multiplication
c0 = tf.multiply(a0, b)
c1 = a0 * b
# output for c1
# <tf.Tensor: shape=(2, 6), dtype=float32, numpy=
# array([[ 2.,  4.,  6.,  8., 10., 12.],
#       [ 2.,  4.,  6.,  8., 10., 12.]], dtype=float32)>
```


### Basic operations

<h5>Addition operator</h5>
- The `add()` operation performs **element-wise addition** with two tensors
- Both tensors must have same shape
- The `add()` operator is overloaded
	- Automatically adapts to tensors of different shapes and dimensions, performing element-wise addition

```python
from tensorflow import constant, add


A0 = constant([1])
B0 = constant([2])

A1 = constant([1, 2])
B1 = constant([3, 4])

A2 = constant([[1, 2], [3, 4]])
B2 = constant([[5, 6], [7, 8]])

C0 = add(A0, B0)
C1 = add(A1, B1)
C2 = add(A2, B2)
```



<h5>Multiplication in TensorFlow</h5>
- **Element-wise multiplication**: performed using `multiply()` operation
- **Matrix multiplication**: performed with `matmul()` operator


```python
from tensorflow import ones, matmul, multiply

A1 = constant([1, 2])
A2 = constant([[1, 2], [3, 4]])
B2 = constant([[5, 6], [7, 8]])

multiply(A1, A2)
# <tf.Tensor: shape=(2, 2), dtype=int32, numpy=
# array([[1, 4],
#       [3, 8]], dtype=int32)>

matmul(A2, B2)
# <tf.Tensor: shape=(2, 2), dtype=int32, numpy=
# array([[19, 22],
#        [43, 50]], dtype=int32)>
```


<h5>Summing over tensor dimensions </h5>
The `reduce_sum()` operator sums over the dimensions of a tensor
- `reduce_sum(A)` : sum over all dimensions of A
- `reduce_sum(A, i)` : sums over dimension $i$


```python
from tensorflow import ones, reduce_sum

A = ones([2, 3, 4])

# Sum over all dimensions
B = reduce_sum(A)
# Output B
# <tf.Tensor: shape=(), dtype=float32, numpy=24.0>

# Sum over dimensions 0, 1, and 2
B0 = reduce_sum(A, 0)
# <tf.Tensor: shape=(3, 4), dtype=float32, numpy=
# array([[2., 2., 2., 2.],
#        [2., 2., 2., 2.],
#        [2., 2., 2., 2.]], dtype=float32)>
B1 = reduce_sum(A, 1)
# <tf.Tensor: shape=(2, 4), dtype=float32, numpy=
# array([[3., 3., 3., 3.],
#        [3., 3., 3., 3.]], dtype=float32)>
B2 = reduce_sum(A, 2)
# <tf.Tensor: shape=(2, 3), dtype=float32, numpy=
# array([[4., 4., 4.],
#        [4., 4., 4.]], dtype=float32)>
```


###  Advanced operations


- `gradient()` : Computes the slope of a function at a point
- `reshape()` : Reshapes a tensor (e.g. 10x10 to 100x1)
- `random()` : Populates tensor with entries drawn from a probability distribution


We can use `gradient()` operation to find the optimum of a function (minimum, maximum)


<h5>Gradients</h5>


```python
import tensorflow as tf  

x = tf.Variable(-1.0)  

# Abre un "registro de operaciones" para calcular gradientes automáticamente.  
with tf.GradientTape() as tape: 
    # Le dice explícitamente al tape que vigile la variable x
    tape.watch(x)  
    # Calcula y = x * x, que es la función sobre la cual queremos el gradiente.  
    y = tf.multiply(x, x)  

# Calcula la derivada de y con respecto a x, es decir dy/dx.  
g = tape.gradient(y, x)  

print(g.numpy())  
```


> [!tip] 
> Cuando ejecutas `tape.gradient(y, x)`, TensorFlow revisa todas las operaciones que guardó dentro del `tape` (aquí, `y = x * x`) y aplica automáticamente reglas de derivación (como la del producto, cadena, etc.) para obtener $\frac{dy}{dx}$.



<h5>Reshaping a grayscale image</h5>

```python
import tensorflow as tf

# Generate grayscale image
gray = tf.random.uniform([2, 2], maxval=255, dtype='int32')
# <tf.Tensor: shape=(2, 2), dtype=int32, numpy=
# array([[207, 143],
#        [ 63,  48]], dtype=int32)>


# Reshape grayscale image
gray = tf.reshape(gray, [2*2, 1])

# <tf.Tensor: shape=(4, 1), dtype=int32, numpy=
# array([[207],
#        [143],
#        [ 63],
#        [ 48]], dtype=int32)>
```


<h5>Reshaping a color image</h5>

[[#Functions#`tf.random.uniform`|`tf.random.uniform`]]

```python
import tensorflow as tf

color = tf.random.uniform([2, 2, 3], maxval=255, dtype='int32')
#<tf.Tensor: shape=(2, 2, 3), dtype=int32, numpy=
# array([[[191, 239, 236],
#         [246, 106, 205]],
# 
#        [[ 83,  41,  26],
#         [133, 114, 116]]], dtype=int32)>

color = tf.reshape(color, [2*2, 3])
# <tf.Tensor: shape=(4, 3), dtype=int32, numpy=
# array([[191, 239, 236],
#        [246, 106, 205],
#        [ 83,  41,  26],
#        [133, 114, 116]], dtype=int32)>
```


## Linear models

### Input data

- **Data can be imported using TensorFlow**
	- Useful for managing complex pipelines
	
- **Another simple option**
	- Import data using `pandas`
	- Convert data to `numpy` array
	- Use in `tensorflow` without modification


<h5>Importing data</h5>
Let's say we hava a csv file `kc_housing.csv`

| date            | price  | bedrooms | floors | waterfront | view |
| --------------- | ------ | -------- | ------ | ---------- | ---- |
| 20141013T000000 | 221900 | 3        | 1      | 0          | 0    |
| 20141209T000000 | 538000 | 3        | 2      | 0          | 0    |
| 20150225T000000 | 180000 | 2        | 1      | 1          | 0    |
| 20141209T000000 | 604000 | 4        | 1      | 0          | 0    |
| 20150218T000000 | 510000 | 3        | 1      | 0          | 2    |
| 20140627T000000 | 257500 | 3        | 2      | 0          | 0    |
| 20150115T000000 | 291850 | 3        | 1      | 0          | 4    |
| 20150415T000000 | 229500 | 3        | 1      | 0          | 0    |


```python
import numpy as np
import pandas as pd

# Load data
housing = pd.read_csv('`kc_housing.csv')

# Convert to numpy array
housing = np.array(housing)
```

Panda also supports: `read_json()`, `read_html()`, `read_excel()`


<h5>Setting the data type</h5>

Approach using **array method from numpy**

```python
# Load KC dataset
housing = pd.read_csv('kc_housing.csv')

# Convert price column to float32
price = np.array(housing['price'], np.float32)

# Convert waterfron column to Boolean
waterfront = np.array(housing['waterfront'], np.bool)
```


Approach using **cast operation from tensorflow**

```python
# Load KC dataset
housing = pd.read_csv('kc_housing.csv')

# Convert price column to float32
price = tf.cast(housing['price'], tf.float32)

# Convert waterfron column to Boolean
waterfront = tf.cast(housing['waterfront'], tf.bool)
```



### Loss functions

- **TensorFlow has operations for common loss functions**
	- Mean squared error (MSE)
	- Mean absolute error (MAE)
	- Huber error
- **Loss functions are accesible from `tf.keras.losses()`
	- `tf.keras.losses.mse()`
	- `tf.keras.losses.mae()`
	- `tf.keras.losses.Huber()`


[Comprender la función Huber Loss: información de las aplicaciones | por Bohsun Chen | Medio](https://medium.com/@devcharlie2698619/understanding-huber-loss-function-insights-from-applications-5c1c5145d2c4)



![[Pasted image 20250820230545.png]]


<h5>Defining a loss function</h5>

```python
import tensorflow as tf

targets = tf.constant([4, 3, 7])
predictions = tf.constant([4.2, 2.1, 7.6])

# Compute MSE Loss
loss = tf.keras.losses.mse(targets, predictions)
# <tf.Tensor: shape=(), dtype=float32, numpy=0.4033333361148834>

# Define a linear regression model
def linear_regression(intercept, slope, features):
  return intercept + features * slope

# Define a loss function to compute the MSE
def loss_function(intercept, slope, targets, features):
  predictions=linear_regression(intercept, slope, features)
  # Return the loss
  return tf.keras.losses.mse(targets, predictions)
  
test_targets = tf.constant([8, 5, 8], tf.float32)
slope = tf.constant([2, 1, 0.5], tf.float32)
test_features = tf.constant([2, 3, 5], tf.float32)
intercept = tf.constant(3, tf.float32)
loss_function(intercept, slope, test_targets, test_features)
# <tf.Tensor: shape=(), dtype=float32, numpy=2.75>
```


### Linear regression


<h5>Linear regression in Tensorflow</h5>

[Learning TensorFlow.ipynb - Colab](https://colab.research.google.com/drive/1tJA3DsUnZeeDB0PKxs7spLLtCC81hUcM#scrollTo=AnAj0Sm0Vl63)

```python
import tensorflow as tf
import numpy as np
import pandas as pd

# Cargar dataset
housing = pd.read_csv('/content/drive/MyDrive/Learning IA/kc_house_data.csv')

# Define the targets and features
price = np.array(housing['price'], np.float32)
size = np.array(housing['sqft_living'], np.float32)
bedrooms = np.array(housing['bedrooms'], np.float32)

size_log = np.log(size)
price_log = np.log(price)

# Params (intercept, slope1, slope2)
params = tf.Variable([0.1, 0.05, 0.02], tf.float32)

# Define the Linear regression model
def linear_regression(params, feature1=size_log, feature2=bedrooms):
  return params[0] + feature1 * params[1] + feature2 * params[2]

# Define loss function
def loss_function(params, targets=price_log, feature1=size_log, feature2=bedrooms):
  predictions = linear_regression(params, feature1, feature2)
  return tf.keras.losses.mae(targets, predictions)

# Define an optimization operation
opt = tf.keras.optimizers.Adam(learning_rate=0.001)

# Training loop with GradientTape
for j in range(1000):
    with tf.GradientTape() as tape:
        loss = loss_function(params)
    grads = tape.gradient(loss, [params])
    opt.apply_gradients(zip(grads, [params] ))

    if j % 100 == 0:  # mostrar cada 100 pasos
        print(f"Step {j}: loss = {loss.numpy()}")

print("\nFinal loss:", loss_function(params).numpy())
print("Trained params:", params.numpy())
```


1. **`with tf.GradientTape() as tape:`**

   * `tf.GradientTape` is a context manager that records all operations on tensors that have trainable parameters.
   * Inside this block, TensorFlow keeps track of how the loss depends on `params`, so it can later compute gradients.

2. **`loss = loss_function(params)`**

   * Here you calculate the loss using your custom `loss_function`.
   * The value of `loss` is a scalar (a single number) that measures how well the model fits the data for the current `params`.

3. **`grads = tape.gradient(loss, [params])`**

   * Once you have the loss, you call `tape.gradient` to compute the derivative of `loss` with respect to the variable `params`.
   * The result `grads` is a list (same length as the list of variables you provided). In this case, just one element: the gradient of the loss with respect to `params`.

4. **`opt.apply_gradients(zip(grads, [params]))`**

   * The optimizer (`opt`) updates the value of `params` using the gradient.
   * `zip(grads, [params])` pairs each gradient with the corresponding parameter.
   * The optimizer then applies the update rule (e.g., for SGD: $\theta \leftarrow \theta - \eta \cdot \nabla_\theta L$), reducing the loss step by step.

**In short**

* `GradientTape` records operations.
* You compute the loss.
* `tape.gradient` calculates the gradient of the loss with respect to parameters.
* `apply_gradients` updates the parameters using the optimizer.


### Batch training

- A single pass over all of the batches is called an **epoch**, and the process itself is called **batch training**
	
- Beyond alleviating memory constraints, batch training will also allow you to update model weights and optimizer parameters after each batch, rather than at the end of the epoch


<h5>The Chunksize parameter</h5>

- `pd.read_csv()` allows us to load data in batches
	- Avoid loading entire dataset
- `chunksize` parameter provides batch size

```python
import numpy as np
import pandas as pd

for batch in pd.read_csv('/content/drive/MyDrive/Learning IA/kc_house_data.csv', chunksize=100):
  price = np.array(batch['price'], np.float32)
  size = np.array(batch['sqft_living'], np.float32)
```

- `batch` variable is a pandas DataFrame with, a portion of the real dataset with 100 rows

## Neural Networks


<h5>A simple dense layer</h5>

```python
import tensorflow as tf

# Define inputs (features)
inputs = tf.constant([[1, 35]], tf.float32)

# Define weights
weights = tf.Variable([[-0.05], [-0.01]])

# Define the bias
bias = tf.Variable([0.5])

# Multiply inputs (features) by the weights
product = tf.matmul(inputs, weights)

# Define dense layer
dense = tf.keras.activations.sigmoid(product + bias)
```


<h5>Defining a complete model</h5>

[[Keras Fundamental#`tf.keras.layers.Dense`|`tf.keras.layers.Dense`]]

```python
import tensorflow as tf

# Define input (features) layers
inputs = tf.constant([[1, 35]], tf.float32)

# Define first dense layer
dense1 = tf.keras.layers.Dense(10, activation='sigmoid')(inputs)

# Define a second dense layer
dense2 = tf.keras.layers.Dense(5, activation='sigmoid')(dense1)

# Define output (predictions) layer
outputs = tf.keras.layers.Dense(1, activation='sigmoid')(dense2)
```

>[!info]
>
When you define:
>
>```python
>inputs = tf.constant([[1, 35]], tf.float32)
>```
>
>this creates a **2D tensor** with shape `(1, 2)`:
>
>- `1` → number of samples (batch size)
>- `2` → number of features per sample
   > 
>
>Even if you have only one sample, TensorFlow/Keras expects input data to have the **batch dimension** explicitly, so the shape must be `(batch_size, num_features)`.
>
>If instead you did:
>
>```python
>tf.constant([1, 35], tf.float32)
>```
>
you’d get a shape `(2,)` (a 1D vector). That’s invalid for `matmul` or for feeding into a Dense layer, since those expect a 2D input.
>
> **Bias can safely be 1D:**
>
>```python
>bias = tf.Variable([0.5])  # shape (1,)
>```
>
because TensorFlow uses **broadcasting**: `(1,)` is automatically expanded to match the shape `(1,1)` when you add it to the product.




**High level approach**: High-level API operations, like Keras

```python
dense = keras.layers.Dense(10, activation='sigmoid')
```

**Low-level approach**: Linear-algebraic operations

```python
prod = matmul(input, weights)
dense = keras.activations.sigmoid(prod)
```


### Activation functions


<h5>The sigmoid activation function</h5>

* Used in **binary classification** problems (outputs between 0 and 1).
* **Low-level:** `tf.keras.activations.sigmoid(x)` → takes a tensor and squashes values into `(0,1)`
* **High-level:** `"sigmoid"` → passed as the `activation` parameter in a Keras layer.



<h5>The ReLU activation function</h5>

* Common in **hidden layers**, helps avoid vanishing gradients.
* **Low-level:** `tf.keras.activations.relu(x, alpha=0.0, max_value=None, threshold=0)`
	* `alpha` → slope for negative values (for Leaky ReLU behavior)
	  * `max_value` → caps the activation at a maximum
	  * `threshold` → shifts the cutoff point
	  
* **High-level:** `"relu"` → passed as the `activation` parameter in a Keras layer.


<h5>The softmax activation function</h5>

* Used in the **output layer** when there are **more than 2 classes**, converts logits into probabilities that sum to 1.
* **Low-level:** `tf.keras.activations.softmax(x, axis=-1)`
	* `axis` → dimension along which to normalize (default is `-1`, the last axis)
	
* **High-level:** `"softmax"` → passed as the `activation` parameter in a Keras layer.


**Low-level Example (ReLU)**

```python
import tensorflow as tf

# Input tensor
x = tf.constant([[-2.0, -1.0, 0.0, 2.0]])

# Low-level ReLU activation
y = tf.keras.activations.relu(x)

print("Input:", x.numpy())
print("ReLU output:", y.numpy())
```

**Output:**

```
Input: [[-2. -1.  0.  2.]]
ReLU output: [[0. 0. 0. 2.]]
```


<h5>Activation functions in neural networks</h5>

**High-level activations**

```python
import tensorflow as tf

# Define input layer
inputs = tf.constant(borrower_features, tf.float32)

# Define dense layer 1
dense1 = tf.keras.layers.Dense(16, activation='relu')(inputs)

# Define dense layer 2
dense 2 = tf.keras.layers.Dense(8, activation='sigmoid')(dense1)

# Define output layer
outputs = tf.keras.layers.Dense(4, activation='softmax')(dense2)
```


### Optimizers

![[Pasted image 20250822152217.png]]


<h5>The gradient descent optimizer</h5>
**Stochastic gradient descent (SGD) optimizer
- [[Keras Fundamental#`tf.keras.optimizers.SGD`|`tf.keras.optimizers.SGD`]]
- `learning_rate`



Simple and easy to interpret

<h5>The RMS prop optimizer</h5>
**Root mean squared (RMS) propagation optimizer**
- Applies different learning rates to each feature
- [[Keras Fundamental#`tf.keras.optimizers.RMSprop`|`tf.keras.optimizers.RMSprop`]]
- `learning_rate`
- `momentum`
- `decay`


Allow for momentum to both build and decay


<h5>The adam optimizer</h5>

**Adaptative moment (adam) optimizer**

- [[Keras Fundamental#`tf.keras.optimizers.Adam`|`tf.keras.optimizers.Adam`]]
- `learning_rate`
- `beta1`

Performs well with default parameter values


```python
 import tensorflow as tf 
 
# Define the model function 
def model(bias, weights, features = borrower_features): 
	product = tf.matmul(features, weights) 
	return tf.keras.activations.sigmoid(product+bias) 
	
# Compute the predicted values and loss 
def loss_function(bias, weights, targets = default, features = borrower_features): 
	predictions = model(bias, weights) 
	return tf.keras.losses.binary_crossentropy(targets, predictions)
	
# Minimize the loss function with RMS propagation 
opt = tf.keras.optimizers.RMSprop(learning_rate=0.01, momentum=0.9) 
opt.minimize(lambda: loss_function(bias, weights), var_list=[bias, weights])  
```


### Training a network in TensorFlow

<h5>Random initializers</h5>

**Often need to initialize thousands of variables**
- `tf.ones()` may perform poorly
- Tedious and difficult to initialize variables individually

**Alternatively, draw initial values from distribution**
- Normal
- Uniform
- Glorot initializer ([Xavier initialization - GeeksforGeeks](https://www.geeksforgeeks.org/deep-learning/xavier-initialization/))


```python
import tensorflow as tf

# Define 500x500 random normal variable
weights = tf.Variable(tf.random.normal([500, 500]))

# Define 500x500 truncated random normal variable
weights = tf.Variable(tf.random.truncated_normal([500, 500]))

# Define a dense layer with the default initializer
dense = tf.keras.layers.Dense(32, activation='relu')

# Defie a dense layer with the zeros initializer
dense = tf.keras.layers.Dense(32, activation='relu', kernel_initializer='zeros')
```



### Applying dropout

```python
import numpy as np
import tensorflow as tf

# Define input data
inputs = np.array(borrower_features, np.float32)

# Define dense layer 1
dense1 = tf.keras.layers.Dense(32, activation='relu')(inputs)

# Define dense layer 2
dense2 = tf.keras.layers.Dense(16, activation='relu')(dense1)

# Apply dropout operation
dropout1 = tf.keras.layers.Dropout(0.25)(dense2)

# Define output layer
outputs = tf.keras.layers.Dense(1, activation='sigmoid')(dropout1)
```




## High Level APIs


### Neural networks with Keras

<h5>The sequential API</h5>
Is the simplest way to build models in Keras. Layers are added **one after the other, in a strict sequence**.

It's best when your model has a **single input** and a **single output,** and the architecture is purely feed-forward

- Input layer
- Hidden layers
- Output layer
- Ordered in sequence

[[Keras Fundamental#`tf.keras.Model.compile`|`tf.keras.Model.compile`]]

```python
from tensorflow import keras

# Define a sequential model
model = keras.Sequential()

# Define first hidden layer
model.add(keras.layers.Dense(16, activation='relu', input_shape=(28*28,)))

# Define a second hidden layer
model.add(keras.layers.Dense(16, activation='relu'))

# Define output layer
model.add(keras.layers.Dense(4, activation='softmax'))

# Compile de model
model.compile('adam', loss='categorial_crossentropy')

# Summarize the model
print(model.sumary())
```


> [!info] `input_shape(28*28,)`
> If you wrote `(28*28, 1)`, the model would expect **2D features per input** 
> (shape `[batch_size, 784, 1]`), which is not the same as a flat vector.



<h5>The functional API</h5>
Is more powerful and flexible. It allows:
- Models with **multiple inputs** and/or **multiple outputs**
- Layers that **branch** or **merge**
- Complex directed acyclic graph of layers


[[Keras Fundamental#`tf.keras.Input`|`tf.keras.Input`]]

```python
import tensorflow as tf

# Define model 1 input layer shape
model1_inputs = tf.keras.Input(shape=(28*28,))

# Define model2 input layer shape
model2_inputs = tf.keras.Input(shape=(10,))

# Define layer 1 for model 1
model1_layer1 = tf.keras.layers.Dense(12, activation='relu')(model1_inputs)

# Define layer 2 for model 1
model1_layer2 = tf.keras.layers.Dense(4, activation='softmax')(model1_layer1)

# Define layer 1 for model 2
model2_layer1 = tf.keras.layers.Dense(8, activation='relu')(model2_inputs)

# Define layer 2 for model 2
model2_layer2 = tf.keras.layers.Dense(4, activation='softmax')(model2_layer1)

# Merge model 1 and model 2
merged = tf.keras.layers.add([model1_layer2, model2_layer2])

# Define a functional model
model = tf.keras.Model(inputs=[model1_inputs, model2_inputs], outputs=merged)

# Compile the model
model.compile('adam', loss='categorical_crossentropy')

print(model.summary())
```



### Training with Keras

<h5> Overview of training and evaluation</h5>

1. Load an clean data
2. Define model
3. Train and validate model
4. Evaluate model


### Training a model

[[Keras Fundamental#`tf.keras.Model.fit`|`tf.keras.Model.fit`]]

```python
import tensorflow as tf

# Define a sequential model
model = tf.keras.Sequential()

# Define the hidden layer
model.add(tf.keras.layers.Dense(16, activation='relu', input_shape=(784,)))

# Define the output layer
model.add(tf.keras.layers.Dense(4, activation='softmax'))

# Compile model
model.compile('adam', loss='categorical_crossentropy')

# Train model
model.fit(image_features, image_labels)
```


<h5>Performing validation</h5>

```python
# Train model with validation split
model.fit(features, labels, epochs=10, validation_split=0.20)
```


<h5>Changing the metric</h5>

```python
# Recompile the model with the accuracy metric
model.compile('adam', loss='categorical_crossentropy', metrics=['accuracy'])

# Train model with validation split
model.fit(features, labels, epochs=10, validation_split=0.20)
```


<h5>The evaluation() operation</h5>

[[Keras Fundamental#`tf.keras.Model.evaluate`|`tf.keras.Model.evaluate`]]

```python
# Evaluate the test set
model.evaluate(test)
```



