---
tags:
  - IA
  - NLP
aliases:
  - Tranformadores
---
---
Los **Transformadores** son una arquitectura de modelo en el campo del aprendizaje profundo y el procesamiento del lenguaje natural (NLP). Fueron introducidos en el artículo "Attention is All You Need" por Vaswani et al. en 2017. Los transformadores han revolucionado la forma en que se manejan las tareas de secuencia a secuencia, reemplazando modelos tradicionales como los RNN y LSTM.

# Estructura del Transformador

La arquitectura del transformador se divide en dos componentes principales: el **codificador** (encoder) y el **decodificador** (decoder), los cuales están compuestos por múltiples capas que interactúan entre sí para procesar y generar secuencias de texto. 
![](https://i.imgur.com/35kVKpl.png)
La imagen proporcionada ilustra una estructura típica de 6 capas para ambos componentes, pero aquí se explicará un modelo generalizado con múltiples capas.


## Codificador

Cada capa del codificador consta de varios subcomponentes clave que trabajan en conjunto para transformar la entrada en una representación que el decodificador puede utilizar eficazmente.

### 1. Embedding de Entrada

Este es el primer paso en el procesamiento del codificador. Convierte cada token de la secuencia de entrada en un vector de alta dimensión.

$$ \text{Embedding}_{\text{entrada}}(token) = W_e token + W_p pos $$

Donde:

- $W_e$: Matriz de embedding de palabras.
- $token$: Representación del token de entrada.
- $W_p$: Matriz de embedding posicional.
- $pos$: Posición del token en la secuencia.

### 2. Codificación Posicional

Añade información sobre la posición relativa de cada token en la secuencia de entrada. Esto es crucial ya que el modelo de atención no tiene en cuenta la posición de los tokens sin esta información.

$$ \text{PE}_{(pos, 2i)} = \sin\left(\frac{pos}{10000^{2i/d_{model}}}\right) $$
$$ \text{PE}_{(pos, 2i+1)} = \cos\left(\frac{pos}{10000^{2i/d_{model}}}\right) $$

Cada letra en la fórmula de codificación posicional significa:

- $\text{PE}$: Codificación posicional (Position Encoding).
- $pos$: Posición del token en la secuencia.
- $i$: Índice de la dimensión.
- $2i$: Índice par en la dimensión del vector de embedding.
- $2i+1$: Índice impar en la dimensión del vector de embedding.
- $d_{model}$: Dimensión del vector de embedding.

### 3. Bloques de Atención y Redes Neuronales

Cada capa del codificador contiene un bloque de atención seguido de un bloque residual y una red neuronal feed-forward. Estos bloques se describen de la siguiente manera:

#### Bloque de Atención en el Codificador

El bloque de atención es uno de los componentes más importantes en la arquitectura del transformador, ya que permite al modelo enfocarse en diferentes partes de la secuencia de entrada para capturar relaciones y dependencias complejas. Aquí se explica detalladamente cómo funciona el mecanismo de atención dentro del bloque de atención.

##### 1. Matrices de Consulta, Clave y Valor (Q, K, V)

El mecanismo de atención comienza con la transformación de la entrada en tres matrices: la matriz de consultas (Q), la matriz de claves (K) y la matriz de valores (V). Estas matrices se obtienen multiplicando la entrada por tres matrices de pesos diferentes.

$$
Q = XW_Q
$$

$$
K = XW_K
$$

$$
V = XW_V
$$

Donde:
- $X$ es la entrada a la capa de atención.
- $W_Q$, $W_K$, y $W_V$ son matrices de pesos aprendibles.

**¿Por qué se realiza este proceso?**

Separar la entrada en consultas, claves y valores permite que el modelo aprenda a buscar información relevante (consultas), identificar esa información (claves) y recuperar el contenido relacionado (valores).

##### 2. Cálculo de la Atención Escalada por Dot-Product

El siguiente paso es calcular la similitud entre las consultas y las claves usando el producto punto. Esto se escala dividiendo por la raíz cuadrada de la dimensión de las claves ($d_k$) para evitar grandes valores que podrían hacer que el softmax sature.

$$
\text{scores} = \frac{QK^T}{\sqrt{d_k}}
$$

**¿Por qué se realiza este proceso?**

Escalar el producto punto evita que los valores grandes en el producto punto causen problemas de saturación en el softmax, lo que podría llevar a gradientes muy pequeños y dificultar el aprendizaje.

##### 3. Aplicación de la Función Softmax

Los puntajes se pasan a través de una función softmax para convertirlos en probabilidades. Esto permite normalizar los puntajes y hacer que sumen 1. Estas probabilidades indican la importancia relativa de cada token en la secuencia.

$$
\text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)
$$

**¿Por qué se realiza este proceso?**

La función softmax convierte los puntajes en probabilidades, haciendo que sea fácil interpretar la importancia relativa de cada token en la secuencia.

##### 4. Multiplicación por la Matriz de Valores

Finalmente, se multiplica la matriz de valores (V) por los puntajes de atención para obtener la representación final de la atención. Esto pondera los valores por la importancia relativa de cada token.

$$
\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V
$$

**¿Por qué se realiza este proceso?**

Ponderar los valores por los puntajes de atención permite que el modelo agregue información relevante de manera ponderada, capturando dependencias contextuales.

#### b. Bloque Residual y Normalización

Después de la atención, cada salida pasa por una conexión residual seguida de una capa de normalización. Esto ayuda a prevenir el problema del desvanecimiento del gradiente en modelos muy profundos.

$$ \text{LayerNorm}(x + \text{Sublayer}(x)) $$

Donde $\text{Sublayer}(x)$ es la operación realizada por el bloque de atención o la red feed-forward.

#### c. Red Neuronal Feed-Forward

Después del mecanismo de atención, cada posición de salida pasa por una red neuronal feed-forward (FFN), que es un componente crucial para introducir no linealidades en el modelo. La presencia de esta capa densa permite al modelo aprender relaciones más complejas que no se capturan simplemente a través de la atención lineal.

La fórmula para la red feed-forward es:

$$ \text{FFN}(x) = \max(0, xW_1 + b_1)W_2 + b_2 $$

Donde:

- $x$ es la entrada a la red feed-forward.
- $W_1$ y $W_2$ son matrices de pesos.
- $b_1$ y $b_2$ son los vectores de sesgo.
- $\max(0, z)$ es la función de activación ReLU, aplicada elemento a elemento, que introduce no linealidad en el proceso de transformación y ayuda a mitigar el problema del gradiente desvaneciente.


## Decodificador

El decodificador también está compuesto por capas que incluyen bloques de atención enmascarados para prevenir la fuga de información futura, atención sobre la salida del codificador, y redes neuronales feed-forward.

#### 1. Embedding de Salida

Similar al embedding de entrada, convierte los tokens de salida en vectores.

#### 2. Codificación Posicional

Igual que en el codificador, añade información posicional a los embeddings de salida.

#### 3. Bloques de Atención, Atención Enmascarada y Atención al Codificador

Estos bloques son similares a los del codificador, pero con la adición de la atención enmascarada para prevenir que el decodificador acceda a información futura.

$$ \text{MaskedAttention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}} - \infty \times \text{mask}\right)V $$

#### 4. Bloques Residuales y Redes Feed-Forward

Estos componentes son idénticos en su función a los del codificador, aplicando la normalización y la red feed-forward tras cada paso de atención.

## Salida Final

La salida del último decodificador pasa por una capa lineal y una función softmax para generar la secuencia de salida final, prediciendo el siguiente token en la secuencia.

$$ \text{softmax}(W_s \text{DecoderOutput}) $$

Donde $W_s$ es la matriz de pesos que transforma la salida del decodificador al tamaño del vocabulario.




# Ventajas de los Transformadores

1. **Paralelización**: A diferencia de los RNN, los transformadores permiten procesar todas las posiciones de una secuencia en paralelo.
2. **Atención**: El mecanismo de atención permite manejar dependencias a largo plazo de manera más efectiva.
3. **Escalabilidad**: Los transformadores pueden escalarse eficientemente a grandes cantidades de datos y parámetros.

# Aplicaciones

Los transformadores se utilizan en diversas aplicaciones, incluyendo:

- Traducción automática
- Resumen de textos
- Generación de texto
- Reconocimiento de voz
- Análisis de sentimiento

# Conclusión

La arquitectura del transformador ha cambiado significativamente el campo del PLN y del aprendizaje profundo. Su capacidad para manejar grandes secuencias y su eficiencia en el procesamiento paralelo lo han convertido en una herramienta indispensable en la investigación y desarrollo de tecnologías avanzadas.

# Referencias

- Vaswani, A., Shazeer, N., Parmar, N., Uszkoreit, J., Jones, L., Gomez, A. N., ... & Polosukhin, I. (2017). Attention is all you need. Advances in neural information processing systems, 30.
- [attention is all that you need](file:///C:/Users/kikhe/OneDrive%20-%20UNIVERSIDAD%20NACIONAL%20DE%20INGENIERIA/Enrique%20PV/ambito%20academico/UNI/ACECOM/attention%20is%20all%20that%20you%20need.pdf)
