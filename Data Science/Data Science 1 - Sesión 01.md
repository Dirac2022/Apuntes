# Aim

## Machine Learning

### Supervised Learning
Trabaja con datos etiquetados
#### Regression
- Advertising Popularity Prediction
- Weather Forecasting
- Market Forecasting
- Estimating life expectancy
- Population Growth Prediction
#### Classification
- Customer Retention
- Image Classification
- Identity Fraud Detection

### Unsupervised Learning  
#### Clustering
- Recommender Systems
- Targeted Marketing
- Customer Segmentation
#### Dimensionality Reduction
- Meaningful Compression
- Structure Discovery
- Big Data Visualization
- Feature Elicitation
### Reinforcement Learning

# What is Data Science?

![[proceso data scientist.png]]

## Collection

### Estructurada
Es data que se puede tabular (columnas)

### Data semiestructurada
Bitacoras de sistemas informáticos

### Data no estructurada
Audio, videos, etc

# Tipos de datos
## Datos categóricos
- Datos nominales
- Datos ordinales

## Datos numéricos
- Datos discretos
- Datos contínuos




# Data Science Life Cycle

![[data science lifecycle.png]]
1. **Business Understanding**: Ask relevant questions and define objectives for the problem that needs to be tackled
2. **Data Mining**: Gather and scrape the data necessary for the project
3. **Data Cleaning**: Fix the inconsistencies within the data and handle the missing values
4. **Data Exploration**: Form hypotheses about your defined problem by visually analyzing the data
5. **Feature Engineering**: Select important features and construct more meaningful ones using the raw data that you have
6. **Predictive Modeling**: Train machine learning models evaluate their performance, and use them to make predictions
7. **Data Visualization**: Communicate the finding with key stakeholders using plots and interactive visualizations

# Machine learning

Se tiene data con etiquetas, eso se introduce al algoritmo de machine learning, este algoritmo de alguna manera halla la relación entre los datos y las etiquetas, de modo que cuando se le proporcione data nueva, este halla la etiqueta correspondiente.


- Es una rama de la inteligencia artificial. El termino se usa desde 1959
- Es la capacidad de las máquinas para aprender a partir de los datos de manera automatizada.
- Al aprender de manera automatizada, esto implica que no necesitan ser programadas para dicha tarea.
- Esto último es una habilidad indispensable para construir sistemas capaces de identificar patrones entre los datos para hacer predicciones de manera eficiente y confiable.
- El aprendizaje automático es excelente para resolver problemas que requieren mucho trabajo para los humanos, mucho procesamiento de datos.


## Aprendizaje supervisado

El entrenamiento se basa en clasificar a las datos por etiquetas, y con el adecuado entrenamiento al ingresar nueva data, el algoritmo asignará la etiqueta adecuada. Estos algoritmos supervisados se dividen en algoritmos de regresión y algoritmos de clasificación

## Aprendizaje no supervisado
En este caso no hay un conjunto de datos de entrenamiento. Los modelos basados en aprendizaje no supervisado encuentran patrones ocultos entre los datos. Los algoritmos no supervisados se dividen en dos tipos: clustering  y association


## Aprendizaje reforzado
El modelo se basa en un programa de recompensas y penalizaciones, esto hace que el agente aprenda de su entorno, donde el agente puede ser una pieza de software.



>[!info]
>La ciencia de datos es esencialmente métodos computacionales y estadísticos que se aplican a los datos. Esto puede incluir al **Análisis Exploratorio de Datos**, donde los datos se examinan y se visualizan para ayudar al científico a comprender mejor los datos y hacer inferencias a partir de ellos.


# Análisis Descriptivo
Consiste en estudiar todo lo que tiene que ver con el pasado. Se utiliza para describir todos los eventos que han ocurrido, considerando parámetro y referencias que se reflejarán en la toma de decisiones.
- **Estadísticas**
- **GráficosNo**
- **Tablas**

# Ciclo de vida de la ciencia de datos

## Análisis exploratorio de los datos

![[Pasted image 20240130171453.png]]

1. Análisis descriptivo
2. Ajuste de tipos de variables
3. Detección y tratamiento de datos faltantes
4. Identificación de datos atípica
5. Correlación de variables

En esta fase se debe comprender bien los datos que se están usando, se debe medir su calidad y detectar datos atípicos *outliers*. 
**EDA** consiste en aplicar un conjunto de técnicas estadísticas destinadas a explorar, describir y resumir la naturaleza de los datos, de forma que podamos entender claramente como están relacionadas nuestras variables de interés


## Feature engineering

La ingeniería de variables es el proceso de seleccionar, manipular y transformar datos sin procesar en características que se pueden usar en el aprendizaje supervisado.

La ingeniería de variables se refiere al proceso de diseñar características artificiales en un algoritmo. Estas características artificiales son luego utilizadas por ese algoritmo para mejorar su rendimiento o, en otras palabras, obtener mejores resultados.

- Feature creation
- Transformations
- Feature Extraction
- Exploratory Data Analysis
- Benchmark

## Model building

Una parte importante de la generación de datos es agregar ruido aleatorio a las etiquetas ya que en cualquier proceso, natural o artificial, los datos no se ajustan exactamente a una tendencia. Siempre existe ruido o variables que no se pueden medir.

Para elegir un buen modelo, una regla es comenzar de manera simple y luego avanzar.

## Underfitting

Cuando un modelo no ha aprendido bien los patrones en los datos de entrenamiento y no puede generalizar bien los nuevos datos, se conoce como ajuste insuficiente *underfitting*

El *underfitting* ocurre debido al alto sesgo y la baja varianza
La varianza se refiere a cuánto depende el modelo de los datos de entrenamiento.

## Overfitting

Este es un modelo con una varianza alta, porque cambiará significativamente dependiendo de los datos de entrenamiento. En este caso, nuestro modelo termina ajustando el ruido.

# Train, validation and test sets

### Conjunto de entrenamiento
Suele ser el conjunto más grande. Los puntos de datos incluidos en este conjunto se utilizan para aprender los parámetros del modelo de interés. Por ejemplo,  durante el entrenamiento se desea que el modelo aprenda la verdadera función que describe la data, o se aproxime. Con este conjunto el modelo aprende a calcular los parámetros necesarios para describir la función.


### Conjunto de validación
Se usa para ajustar los híper parámetros de un clasificador. En este caso, este conjunto servirá para probar la precisión del modelo.

### Conjunto de prueba
Se utiliza para evaluar el rendimiento del modelo y garantizar que pueda generalizarse bien a puntos de datos nuevos e invisibles

## Enter validation (Validación cruzada)

![[validacion cruzada.png]]

La validación cruzada es una técnica que nos ayuda a medir en rendimiento de un modelo. En lugar de usar un conjunto de validación separado, dividimos el conjunto de entrenamiento en varios subconjuntos, llamados folds. Esto se hace dividiendo el conjunto de entrenamiento en particiones llamados “folds” donde uno de ellos servirá para la validación y el resto para el entrenamiento. El fold escogido para la validación se itera entre todos los folds y luego se hace un promedio para determinar el rendimiento general.

El procedimiento típico de validación cruzada implica los siguientes pasos:

1. **División del Conjunto de Datos:**
    - El conjunto de datos se divide en k subconjuntos más pequeños llamados "folds". La elección de k, el número de folds, es un parámetro que puede variar, pero comúnmente se utiliza $k=5$ o $k=10$.
2. **Iteración sobre Folds:**
    - Se realiza un bucle a través de los $k$ folds. En cada iteración, un fold se utiliza como conjunto de prueba, y los $k-1$ folds restantes se utilizan como conjunto de entrenamiento.
3. **Entrenamiento del Modelo:**
    - Se entrena el modelo en el conjunto de entrenamiento utilizando los $k-1$ folds.
4. **Evaluación del Modelo:**
    - Se evalúa el rendimiento del modelo en el fold de prueba que se excluyó en esa iteración. La métrica de evaluación (como precisión, exactitud, error cuadrático medio, etc.) se registra.
5. **Promedio de Resultados:**
    - Se repiten los pasos 2-4 para cada fold. Al final, se promedian los resultados de evaluación para obtener una estimación más robusta del rendimiento del modelo.


## Bias-variance tradeoff

![[optimal balance.png]]
Cuando varia la complejidad de un algoritmo existe una relación entre el sesgo y la varianza, empezando desde un algoritmo “simple” tal que la varianza el relativamente pequeña pero el sesgo es alto, cuando se agrega complejidad al algoritmo esto ayuda a reducir el sesgo del mismo pero como consecuencia aumenta la varianza. El trade-off entre el sesgo y la varianza nos ayuda a calcular la complejidad adecuada que minimice o encuentre un equilibrio entre ambas medidas
### Bias
El bias nos indica cuan diferente es el valor estimado que produce el modelo vs el valor real de un conjunto de datos. Un sesgo alto o *underfitting* significa que el modelo no puede capturar la tendencia o el patrón en los datos. 

### Variance
Se refiere a la capacidad del modelo para medir la dispersión de los datos. Varianza alta o *overfitting* significa que el modelo se ajusta demasiado a los datos de entrenamiento pero no generaliza bien para predecir con datos nuevos.

Un modelo con varianza alta se desempeña muy bien en el conjunto de entrenamiento, pero deficientemente en el conjunto de prueba o validación cruzada.



# Machine Learning

## Evaluación del modelo

![[evaluacion modelo.png]]

- En el aprendizaje supervisado, el *underfitting* ocurre cuando un modelo no puede capturar el patrón subyacente de los datos. Estos modelos suelen tener un alto sesgo y una baja varianza. Ocurre cuando tenemos muy poca cantidad de datos para construir un modelo preciso o cuando intentamos construir un modelo con datos no lineales
- En el aprendizaje supervisado, el *overfitting* ocurre cuando nuestro modelo captura el ruido junto con el patrón subyacente en los datos. Ocurre cuando entrenamos mucho nuestro modelo sobre un conjunto de datos ruidoso. Estos modelos tienen un sesgo bajo y una varianza alta

### Arreglar el alto sesgo

- Realizar ingeniería de características
- Aumentar el grado del polinomio
- Disminuir el parámetro alfa de regularización

### Arreglar la alta varianza

- Reducir la cantidad de features en el modelo
- Aumentar el tamaño del conjunto de entrenamiento
- Disminuir el grado del polinomio


## Función de perdida y función de costo

Una función de pérdida $J(x)$ mide que tan insatisfechos estamos con las predicciones de nuestro modelo con respecto a una respuesta correcta y utilizando ciertos valores de $\theta$ .

Una función que calcula la pérdida para 1 punto de datos se llama **función de pérdida**, mientras que **función de costo** es el promedio de todos los errores de la muestra en todo el conjunto de entrenamiento.

La evaluación del modelo es un método para evaluar la corrección de los modelos en los datos de prueba. Los datos de prueba consisten en puntos de datos que el modelo no ha visto antes.

### Métricas de performance para regresión (Funciones de pérdida)

#### Error absoluto medio (MAE)
$$ \dfrac{1}{n} \sum_{1}^{n} |y_i - \hat{y}_i | $$
Es el promedio de los valores de error absoluto. Las puntuaciones aumentan linealmente con el aumento de los errores. 

#### Error cuadrático medio (MSE)

$$ \dfrac{1}{n} \sum_{1}^{n} ( y_i - \hat{y}_i)^2 $$

ES una medida combinada de sesgo y varianza.

#### Raíz del error cuadrático medio (RMSE)
$$ \sqrt{MSE} $$

Es significativamente útil cuando los errores grandes son particularmente indeseables


#### Mean absolute percentage error (MAPE)
	$$ \dfrac{100\%}{n} y \sum \left| \dfrac{y - \hat{y}}{y} \right| $$

Similar al MAE pero normalizado.

#### Métrica $R^2$
$$ 1 - \dfrac{\sum (y_i - \hat{y}_i)^2}{\sum (y_i - \overline{y}_i)^2} $$
El coeficiente de determinación es un valor entre 0 y 1 que mide que tan bien un modelo estadístico predice un resultado. Es una medida de bondad de ajuste.




### Métricas de performance para la clasificación

#### Matriz de confusión
Una matriz de confusión es una tabla con las diferentes salidas predichas en un problema de clasificación que nos ayuda a visualizar los resultados en una manera más clara

![[matriz de confusion.png]]

Es especialmente útil cuando se trata de problemas de clasificación binaria, aunque también se puede adaptar a problemas de clasificación multiclase.




Calculando la exactitud (accuracy)
$$ \text{Accuracy} = \dfrac{TP + TN}{TP + FP + TN + FN} $$


##### Precision
Nos dice cuantos de los casos predichos como positivos resultaron de ser positivos realmente.

![[Pasted image 20250507223733.png]]

$$ \text{Precision} = \dfrac{TP}{TP + FP} $$


> [!tip] Ejemplo
> A model predicting if a costumer is a high-value lead far a sales team with limited capacity.
> With limited capacity, the sales team need the model to return the highest proportion of true positives compared to all predicted positives, thus minimizing wasted effort.


##### Recall o sensibilidad
Nos dice de cuántos de los casos positivos reales pudimos predecir correctamente con nuestro modelo.

![[Pasted image 20250507223917.png]]

$$ \text{Recall} = \dfrac{TP}{TP + FN} $$


> [!tip] Ejemplo
> A model predicting the presence of cancer as the positive class.
> This model should **minimize the number of false negatives**, so recall is a more appropiate metric


##### F1 score
Si no esta claro cual métrica es más importante, se procede a combinarlos
$$ F1 - score = \dfrac{2}{\dfrac{1}{Recall} + \dfrac{1}{Precision}} $$

> [!tip] Ejemplo
> A classifier predicting the positive class of a computer program containing malware.
> To avoid installing malware, false negative should be minimize, hence **recall** of **F1-score** are better metrics for this model.


La matriz de confusión tiene cuatro entradas principales:

1. **Verdaderos positivos (True Positives - TP):** Representa la cantidad de observaciones positivas que fueron correctamente clasificadas como positivas por el modelo.

2. **Falsos positivos (False Positives - FP):** Indica la cantidad de observaciones negativas que fueron incorrectamente clasificadas como positivas por el modelo.

3. **Verdaderos negativos (True Negatives - TN):** Muestra la cantidad de observaciones negativas que fueron correctamente clasificadas como negativas por el modelo.

4. **Falsos negativos (False Negatives - FN):** Representa la cantidad de observaciones positivas que fueron incorrectamente clasificadas como negativas por el modelo.

La matriz de confusión se representa de la siguiente manera:

```
                Actual Positivo    Actual Negativo
Predicho Positivo      TP               FP
Predicho Negativo      FN               TN
```

La precisión (accuracy), la sensibilidad (recall o true positive rate), la especificidad y otras métricas se pueden calcular a partir de los valores de la matriz de confusión. Aquí hay algunas fórmulas comunes:

- **Precisión (Accuracy):** (TP + TN) / (TP + FP + FN + TN)
- **Sensibilidad (Recall o True Positive Rate):** TP / (TP + FN)
- **Especificidad:** TN / (TN + FP)
- **Falsos Positivos por tasa (False Positive Rate):** FP / (FP + TN)

La interpretación de estos valores depende del contexto del problema y de cuál de las métricas es más relevante para la aplicación específicaconfusion






