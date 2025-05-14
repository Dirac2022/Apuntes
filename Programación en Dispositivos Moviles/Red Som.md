La **red neuronal SOM** (Self-Organizing Map, o Mapa Autoorganizado) es un tipo de red neuronal no supervisada introducida por el profesor Teuvo Kohonen en la década de 1980. Su principal característica es la capacidad de **aprender a representar un conjunto de datos en un espacio de menor dimensión**, usualmente en forma de un mapa bidimensional, de manera que las similitudes en los datos originales se conserven en la representación reducida. Esto permite visualizar y analizar patrones complejos de datos de manera intuitiva.

Aquí te explico el concepto de forma técnica, pero con analogías sencillas:

### 1. ¿Qué es una red neuronal SOM?
Una SOM es una red neuronal que **ordena datos y encuentra patrones** sin la necesidad de etiquetas (no supervisada). Puedes imaginarla como una gran pizarra en la que colocas fichas de diferentes colores y tamaños de manera que las fichas similares terminan agrupadas cerca unas de otras. En lugar de hacerlo manualmente, la SOM es el algoritmo que mueve las fichas a las posiciones más apropiadas según sus características.

### 2. ¿Cómo funciona la red?
La SOM consta de dos componentes principales:
- **Neurona**: Cada punto en la cuadrícula bidimensional es una neurona que representa un "prototipo" de los datos.
- **Vector de características**: Los datos de entrada son vectores que contienen las características numéricas de los ejemplos.

El algoritmo de entrenamiento se lleva a cabo en varias etapas:

#### Etapa de Entrenamiento:
1. **Inicialización**: Cada neurona se inicializa con un vector de pesos aleatorios.
2. **Entrada de datos**: Se presenta un vector de entrada (una ficha con características específicas).
3. **Búsqueda de la mejor coincidencia**: La red encuentra la neurona cuyo vector de pesos es más similar al vector de entrada (esta neurona se llama "la ganadora").
4. **Actualización**: Se actualizan los pesos de la neurona ganadora y de las neuronas vecinas para que se asemejen más al vector de entrada. Este proceso imita un "efecto de atracción", como si la ficha presentada jalara las neuronas cercanas hacia su posición.

Este proceso se repite para múltiples ciclos, lo que permite que la red se autoorganice en función de las características de los datos de entrada.

### 3. Analogía Intuitiva
Imagina que estás organizando una colección de fotografías en un tablero grande. Si una fotografía muestra un paisaje con montañas, la colocas cerca de otras fotos de montañas; si es de la playa, la colocas en otro lugar. La SOM hace esto de manera automática: clasifica las fotos basándose en sus características (como colores y texturas) y las agrupa en áreas donde las fotos similares quedan cerca entre sí. El tablero resultante es un mapa en el que las fotografías que se parecen están en la misma región.

### 4. Aplicaciones de las SOM
Las SOM se usan para:
- **Análisis de datos de alta dimensión**: Como una forma de reducir la dimensionalidad y descubrir patrones.
- **Agrupamiento y clasificación**: En tareas donde no se tienen etiquetas predefinidas.
- **Visualización de datos**: Para ayudar a entender estructuras de datos complejos, como mapas topológicos de textos, imágenes o patrones de comportamiento.

### 5. Beneficios y Limitaciones
- **Beneficios**: Permiten una representación visual intuitiva, simplifican la exploración de datos complejos y no necesitan datos etiquetados.
- **Limitaciones**: Requieren un tiempo de entrenamiento relativamente largo y pueden ser sensibles a la inicialización y a los parámetros, como el tamaño de la vecindad y la tasa de aprendizaje.

### Parte matemática de las SOM
En términos más técnicos, la actualización de los pesos se realiza con la siguiente fórmula:

$$
W_i(t+1) = W_i(t) + \alpha(t) \cdot h_{ci}(t) \cdot (X(t) - W_i(t))
$$

Donde:
- $W_i(t)$ es el vector de pesos de la neurona $i$ en el tiempo $t$.
- $\alpha(t)$ es la tasa de aprendizaje, que decrece con el tiempo.
- $h_{ci}(t)$ es la función de vecindad, que también decrece con la distancia a la neurona ganadora $c$ y con el tiempo.
- $X(t)$ es el vector de entrada.

En resumen, las SOM son herramientas poderosas para **la organización y visualización de datos complejos**, y funcionan de manera muy similar a cómo organizarías un tablero de fichas según sus características comunes, adaptándose continuamente hasta que el tablero refleja la estructura subyacente de los datos.