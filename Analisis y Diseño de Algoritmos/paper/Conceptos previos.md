
# Clustering

**Clustering** es una técnica de análisis de datos que agrupa un conjunto de objetos de manera que los objetos en el mismo grupo (o clúster) son más similares entre sí que a los de otros grupos. Es una forma de aprendizaje no supervisado, lo que significa que el algoritmo aprende a partir de los datos sin etiquetas predefinidas.

#### Objetivos del Clustering

1. **Agrupamiento de datos**: Identificar grupos o clústeres en los datos que tienen características similares.
2. **Reducción de dimensionalidad**: Simplificar los datos representándolos con menos características importantes.
3. **Detección de patrones**: Descubrir estructuras ocultas en los datos.

#### Tipos de Clustering

1. **Particional**: Divide los datos en clústeres sin superposición, por ejemplo, K-means.
2. **Jerárquico**: Construye una jerarquía de clústeres, puede ser aglomerativo (de abajo hacia arriba) o divisivo (de arriba hacia abajo).
3. **Basado en densidad**: Agrupa puntos en regiones densas separadas por regiones menos densas, por ejemplo, DBSCAN.
4. **Basado en modelos**: Asume que los datos se generan a partir de una mezcla de distribuciones probabilísticas, por ejemplo, Gaussian Mixture Models.

#### Ejemplo Visual

Imagina un conjunto de puntos en un plano bidimensional. El objetivo del clustering es agrupar esos puntos en conjuntos, de manera que los puntos dentro del mismo conjunto estén más cerca unos de otros que de los puntos en otros conjuntos.

#### Aplicaciones del Clustering

1. **Segmentación de clientes**: Identificar grupos de clientes con comportamientos o características similares.
2. **Análisis de redes sociales**: Descubrir comunidades dentro de una red de usuarios.
3. **Compresión de imágenes**: Reducir el número de colores en una imagen.
4. **Reconocimiento de patrones**: Identificar estructuras o patrones en datos biométricos, como huellas dactilares o rostros.

#### Algoritmos de Clustering Populares

1. **K-means**: Un algoritmo particional que minimiza la variabilidad dentro de los clústeres. 
2. **DBSCAN**: Un algoritmo basado en densidad que puede encontrar clústeres de forma arbitraria y manejar ruido.
3. **Agglomerative Hierarchical Clustering**: Un método jerárquico que construye un árbol de clústeres.

### Ejemplo de K-means en Python

```python
from sklearn.cluster import KMeans
import numpy as np
import matplotlib.pyplot as plt

# Datos de ejemplo
X = np.array([[1, 2], [1.5, 1.8], [5, 8], [8, 8], [1, 0.6], [9, 11]])

# Aplicar K-means
kmeans = KMeans(n_clusters=2)
kmeans.fit(X)

# Obtener centros de clúster
centros = kmeans.cluster_centers_
etiquetas = kmeans.labels_

# Visualizar los clústeres
colores = ["g.", "r."]
for i in range(len(X)):
    plt.plot(X[i][0], X[i][1], colores[etiquetas[i]], markersize=10)
plt.scatter(centros[:, 0], centros[:, 1], marker="x", s=150, linewidths=5)
plt.show()
```

Este código aplica el algoritmo K-means a un conjunto de datos bidimensional y visualiza los clústeres formados.

### Conclusión

El clustering es una herramienta fundamental en el análisis de datos que permite descubrir estructuras ocultas y patrones en los datos sin etiquetas predefinidas. Al elegir el algoritmo de clustering adecuado, se pueden abordar una amplia variedad de problemas en diferentes dominios, desde la segmentación de clientes hasta la compresión de imágenes y más.


# Datos Manifold

**Datos manifold** se refiere a datos que se encuentran distribuidos en una subvariedad de menor dimensión dentro de un espacio de mayor dimensión. En otras palabras, aunque los datos pueden vivir en un espacio de alta dimensión, su estructura intrínseca es de menor dimensión y se puede describir mediante una manifold (subvariedad).

#### Conceptos Clave

1. **Manifold**: Una manifold es un espacio que localmente se asemeja a un espacio euclidiano de menor dimensión. Un ejemplo común es la superficie de una esfera en 3D, que localmente parece un plano 2D.
2. **Dimensión Intrínseca**: Es la dimensión real en la que los datos tienen su estructura. Por ejemplo, una curva en 3D puede tener una dimensión intrínseca de 1D.
3. **Embeded en Alta Dimensión**: Aunque la estructura intrínseca de los datos es de menor dimensión, los datos están embebidos en un espacio de mayor dimensión.

#### Importancia de los Datos Manifold

Los datos manifold son importantes en el análisis de datos porque muchas veces los datos de alta dimensión pueden ser descritos y manipulados de manera más eficiente si se considera su estructura de baja dimensión subyacente.

#### Ejemplos de Datos Manifold

1. **Imágenes**: Aunque una imagen digital puede ser representada como un conjunto de píxeles en un espacio de alta dimensión (cada píxel es una dimensión), la información relevante suele residir en una manifold de menor dimensión.
2. **Datos de Sensores**: Los datos recolectados por múltiples sensores pueden tener redundancia y depender de un número menor de variables latentes.
3. **Datos Temporales**: Series de tiempo de múltiples variables pueden residir en una manifold de menor dimensión que captura la dinámica subyacente.

#### Técnicas de Reducción de Dimensionalidad

Para trabajar con datos manifold, a menudo se utilizan técnicas de reducción de dimensionalidad que intentan descubrir la estructura de baja dimensión. Algunas de las técnicas más populares incluyen:

1. **PCA (Análisis de Componentes Principales)**: Una técnica lineal que proyecta datos en una dirección que maximiza la varianza.
2. **t-SNE (t-Distributed Stochastic Neighbor Embedding)**: Una técnica no lineal que intenta preservar las relaciones de vecindad en una proyección de baja dimensión.
3. **LLE (Locally Linear Embedding)**: Una técnica no lineal que preserva la estructura local de los datos.
4. **Isomap**: Una técnica no lineal que preserva las distancias geodésicas en la proyección de baja dimensión.

#### Ejemplo de Reducción de Dimensionalidad con t-SNE en Python

```python
from sklearn.manifold import TSNE
import matplotlib.pyplot as plt
import numpy as np

# Generar datos de ejemplo (3D)
np.random.seed(0)
n_points = 1000
X = np.random.randn(n_points, 3)

# Aplicar t-SNE para reducir la dimensionalidad a 2D
tsne = TSNE(n_components=2)
X_2D = tsne.fit_transform(X)

# Visualizar los datos en 2D
plt.scatter(X_2D[:, 0], X_2D[:, 1])
plt.title("Reducción de Dimensionalidad con t-SNE")
plt.show()
```

Este código aplica t-SNE a un conjunto de datos tridimensional y visualiza la proyección en dos dimensiones.

### Conclusión

Los datos manifold son una categoría importante en el análisis de datos, donde los datos de alta dimensión tienen una estructura subyacente de menor dimensión. Reconocer y utilizar esta estructura puede llevar a representaciones más eficientes y a un análisis más efectivo de los datos. Técnicas de reducción de dimensionalidad, como PCA, t-SNE, LLE e Isomap, son herramientas esenciales para trabajar con datos manifold.
# K-means y K-medoids en Clustering

**K-means** y **K-medoids** son algoritmos populares de clustering que se utilizan para agrupar datos en un número predefinido de clústeres, $k$. Ambos algoritmos buscan minimizar la variabilidad dentro de los clústeres, pero utilizan diferentes enfoques para determinar los centros de los clústeres.

#### K-means

**K-means** es un algoritmo de clustering basado en particiones que funciona de la siguiente manera:

1. **Inicialización**:
   - Selecciona $k$ centros de clúster iniciales, llamados centroides, de manera aleatoria.

2. **Asignación**:
   - Cada punto de datos se asigna al centro de clúster más cercano, formando $k$ clústeres basados en la distancia euclidiana.

3. **Actualización**:
   - Calcula la media (centroide) de todos los puntos en cada clúster y actualiza los centros de clúster a estas medias.

4. **Iteración**:
   - Repite los pasos de asignación y actualización hasta que los centros de clúster ya no cambien significativamente (convergencia) o se alcance un número máximo de iteraciones.

**Ventajas**:
- Simple y rápido para conjuntos de datos pequeños y medianos.
- Fácil de implementar y comprender.

**Desventajas**:
- Sensible a la inicialización de los centroides.
- No maneja bien clústeres de formas arbitrarias y de diferentes tamaños.
- No es robusto ante valores atípicos y ruido.

#### K-medoids

**K-medoids**, también conocido como **PAM (Partitioning Around Medoids)**, es similar a K-means, pero utiliza medoids en lugar de centroides. Un medoid es un punto de datos real dentro del clúster, lo que lo hace más robusto a valores atípicos y ruido. El algoritmo funciona de la siguiente manera:

1. **Inicialización**:
   - Selecciona $k$ puntos de datos iniciales como medoids de manera aleatoria.

2. **Asignación**:
   - Cada punto de datos se asigna al medoid más cercano según una métrica de distancia (por ejemplo, la distancia de Manhattan).

3. **Actualización**:
   - Para cada clúster, selecciona un nuevo medoid que minimice la suma de las distancias entre el medoid y todos los otros puntos en el clúster.

4. **Iteración**:
   - Repite los pasos de asignación y actualización hasta que los medoids ya no cambien significativamente o se alcance un número máximo de iteraciones.

**Ventajas**:
- Más robusto ante valores atípicos y ruido que K-means.
- Maneja mejor los clústeres de diferentes formas y tamaños.

**Desventajas**:
- Más lento que K-means, especialmente en conjuntos de datos grandes.
- Requiere más tiempo de cálculo debido a la actualización de los medoids.

#### Comparación

| Aspecto            | K-means                             | K-medoids                            |
|--------------------|-------------------------------------|--------------------------------------|
| Centro del clúster | Centroides (medias)                 | Medoids (puntos de datos reales)     |
| Robustez           | Sensible a valores atípicos         | Robusto ante valores atípicos        |
| Complejidad        | Menor complejidad computacional     | Mayor complejidad computacional      |
| Tipo de datos      | Datos numéricos                     | Datos numéricos y categóricos        |
| Forma de clústeres | No maneja bien formas arbitrarias   | Maneja mejor formas arbitrarias      |

Ambos algoritmos son ampliamente utilizados en diversas aplicaciones, como segmentación de clientes, compresión de imágenes, y reconocimiento de patrones, dependiendo de las características y necesidades específicas del conjunto de datos y del problema a resolver.


# Distancia de Manhattan

La **distancia de Manhattan**, también conocida como **distancia $L_1$** o **distancia de la ciudad**, es una métrica de distancia que calcula la distancia entre dos puntos en un espacio vectorial sumando las diferencias absolutas de sus coordenadas correspondientes. Es especialmente útil en contextos donde el movimiento solo se permite a lo largo de ejes rectos, similar a cómo se movería una persona en una cuadrícula urbana.

#### Fórmula

Si tenemos dos puntos $A = (x_1, y_1)$ y $B = (x_2, y_2)$ en un espacio bidimensional, la distancia de Manhattan $d_m$ entre ellos se define como:

$$ d_m(A, B) = |x_2 - x_1| + |y_2 - y_1| $$

En un espacio de $n$ dimensiones, si los puntos $A$ y $B$ tienen coordenadas $(x_1, x_2, \ldots, x_n)$ y $(y_1, y_2, \ldots, y_n)$ respectivamente, la distancia de Manhattan es:

$$ d_m(A, B) = \sum_{i=1}^{n} |x_i - y_i| $$

#### Ejemplo en un Espacio Bidimensional

Supongamos que tenemos dos puntos $A = (1, 2)$ y $B = (4, 6)$:

$$ d_m(A, B) = |4 - 1| + |6 - 2| = 3 + 4 = 7 $$

#### Aplicaciones

1. **Procesamiento de Imágenes**: Se utiliza para comparar píxeles en imágenes, especialmente cuando los píxeles pueden moverse solo horizontal o verticalmente.
2. **Análisis de Redes**: Es útil en redes donde las conexiones están estructuradas en una cuadrícula, como calles de una ciudad.
3. **Optimización y Algoritmos de Clustering**: Se utiliza en algoritmos de clustering como K-medoids y otros métodos que requieren una métrica de distancia.

#### Ejemplo de Cálculo en Python

A continuación se presenta un ejemplo de cómo calcular la distancia de Manhattan entre dos puntos en Python:

```python
def distancia_manhattan(punto1, punto2):
    return sum(abs(a - b) for a, b in zip(punto1, punto2))

# Ejemplo de puntos en 2D
punto1 = (1, 2)
punto2 = (4, 6)
distancia = distancia_manhattan(punto1, punto2)
print(f"La distancia de Manhattan entre {punto1} y {punto2} es {distancia}")
```

### Conclusión

La distancia de Manhattan es una métrica simple pero poderosa que mide la distancia entre dos puntos sumando las diferencias absolutas de sus coordenadas. Es especialmente útil en situaciones donde solo se permiten movimientos horizontales y verticales, como en cuadrículas urbanas o ciertos tipos de análisis de datos y algoritmos de clustering.

# Dcore en el Contexto de Clustering

**Dcore** es un algoritmo de clustering basado en la densidad que se centra en identificar "núcleos de densidad" dentro de los datos. Estos núcleos de densidad son regiones donde los puntos de datos están densamente agrupados. El concepto principal detrás de Dcore es que cada clúster tiene un núcleo de densidad que retiene la forma del clúster y los bordes y valores atípicos se distribuyen alrededor de estos núcleos en una estructura jerárquica.

#### Características Clave de Dcore

1. **Núcleos de Densidad**: Dcore asume que cada clúster tiene un núcleo de densidad, que es una región donde los puntos de datos están más densamente agrupados que en otras regiones del espacio de datos.
2. **Jerarquía de Bordes y Valores Atípicos**: Los puntos de datos que no pertenecen a los núcleos de densidad se consideran bordes o valores atípicos y se distribuyen alrededor de estos núcleos en una estructura jerárquica.
3. **Múltiples Parámetros**: Dcore requiere la configuración de varios parámetros, como radios esféricos y umbrales de densidad, para identificar correctamente los núcleos de densidad y distinguir entre núcleos, bordes y valores atípicos.

#### Parámetros de Dcore

- **Radio Esférico \( r_1 \) y \( r_2 \)**: Definen el alcance de los núcleos de densidad.
- **Umbral de Densidad \( t_1 \) y \( t_2 \)**: Determinan la densidad mínima requerida para que un conjunto de puntos se considere un núcleo de densidad.
- **Radio de Escaneo \( r \)**: Utilizado para escanear el espacio de datos y encontrar puntos que pertenecen a los núcleos de densidad.

#### Proceso del Algoritmo Dcore

1. **Cálculo de la Densidad Local**: Se calcula la densidad local de cada punto en el conjunto de datos, similar a otros métodos basados en densidad.
2. **Identificación de Núcleos de Densidad**: Utilizando los parámetros \( r_1 \), \( r_2 \), \( t_1 \) y \( t_2 \), se identifican los núcleos de densidad. Estos son puntos donde la densidad local excede los umbrales especificados.
3. **Clasificación de Puntos**: Los puntos se clasifican en núcleos, bordes y valores atípicos basándose en su densidad local y su proximidad a los núcleos de densidad.
4. **Formación de Clústeres**: Los núcleos de densidad forman el corazón de los clústeres, y los puntos de borde se asignan a los clústeres basados en su proximidad a los núcleos.

#### Ejemplo en Python

A continuación se muestra un pseudocódigo simplificado para ilustrar el funcionamiento básico del algoritmo Dcore:

```python
import numpy as np

# Función para calcular la densidad local
def calcular_densidad_local(data, radio):
    densidad = []
    for i in range(len(data)):
        vecinos = 0
        for j in range(len(data)):
            if np.linalg.norm(data[i] - data[j]) <= radio:
                vecinos += 1
        densidad.append(vecinos)
    return np.array(densidad)

# Función para identificar núcleos de densidad
def identificar_nucleos(densidad, umbral):
    nucleos = np.where(densidad >= umbral)[0]
    return nucleos

# Datos de ejemplo
data = np.array([[1, 2], [1.5, 1.8], [5, 8], [8, 8], [1, 0.6], [9, 11]])

# Parámetros de Dcore
radio = 2
umbral = 2

# Calcular densidad local
densidad_local = calcular_densidad_local(data, radio)

# Identificar núcleos de densidad
nucleos = identificar_nucleos(densidad_local, umbral)
print("Núcleos de densidad:", nucleos)

# Visualizar los resultados
import matplotlib.pyplot as plt
plt.scatter(data[:, 0], data[:, 1], c='blue')
plt.scatter(data[nucleos, 0], data[nucleos, 1], c='red')
plt.show()
```

Este pseudocódigo calcula la densidad local para cada punto en un conjunto de datos bidimensional y luego identifica los núcleos de densidad basándose en un umbral de densidad. Los puntos que se identifican como núcleos de densidad se visualizan en rojo.

### Conclusión

Dcore es un algoritmo de clustering basado en densidad que identifica núcleos de densidad dentro de los datos. Utilizando varios parámetros, Dcore puede distinguir entre núcleos, bordes y valores atípicos, permitiendo una clasificación jerárquica de los puntos de datos. Este enfoque es particularmente útil para descubrir clústeres con formas arbitrarias y manejar datos con variaciones de densidad.


# DBSCAN (Density-Based Spatial Clustering of Applications with Noise)

**DBSCAN** es un algoritmo de clustering basado en la densidad que es especialmente útil para identificar clústeres de forma arbitraria y manejar ruido (puntos de datos atípicos). Fue propuesto por Martin Ester, Hans-Peter Kriegel, Jörg Sander y Xiaowei Xu en 1996.

#### Principios Básicos

DBSCAN agrupa puntos en base a la densidad de puntos en el espacio de datos. Utiliza dos parámetros clave:

- **Eps (ε)**: El radio dentro del cual se busca vecinos de un punto.
- **MinPts**: El número mínimo de puntos que debe haber dentro del radio ε para que un punto sea considerado un punto central (core point).

#### Definiciones Clave

1. **Punto Central (Core Point)**:
   - Un punto es un punto central si hay al menos MinPts puntos (incluyendo el mismo) dentro de su radio ε.

2. **Punto Alcanzable por Densidad**:
   - Un punto \( p \) es alcanzable por densidad desde un punto central \( q \) si \( p \) está dentro del radio ε de \( q \).

3. **Punto Conectado por Densidad**:
   - Un punto \( p \) es conectado por densidad a un punto \( q \) si existe una cadena de puntos centrales donde cada punto es alcanzable por densidad desde el anterior.

4. **Punto de Ruido**:
   - Un punto que no es ni un punto central ni alcanzable por densidad desde cualquier punto central. Estos puntos se consideran puntos de ruido o atípicos.

#### Algoritmo

1. **Inicialización**:
   - Elegir un punto arbitrario que no haya sido visitado.

2. **Expansión de Clúster**:
   - Si el punto es un punto central, crear un nuevo clúster y recuperar todos los puntos alcanzables por densidad (dentro del radio ε).
   - Añadir todos estos puntos al clúster, marcándolos como visitados.
   - Repetir el proceso para cada nuevo punto central añadido al clúster.

3. **Repetición**:
   - Repetir el proceso hasta que todos los puntos hayan sido visitados.

#### Ventajas

- **Forma Arbitraria de Clústeres**: Puede encontrar clústeres de formas arbitrarias.
- **Robusto ante Ruido**: Puede identificar y manejar puntos de ruido.
- **No Requiere Número de Clústeres a Priori**: A diferencia de K-means, no se necesita especificar el número de clústeres antes de ejecutar el algoritmo.

#### Desventajas

- **Sensibilidad a Parámetros**: La elección de ε y MinPts puede ser difícil y afectar significativamente los resultados.
- **Escalabilidad**: Puede ser ineficiente con conjuntos de datos muy grandes y de alta dimensionalidad sin optimización adicional (como el uso de estructuras de datos espaciales como KD-Tree).

#### Ejemplo en Python

```python
from sklearn.cluster import DBSCAN
import numpy as np
import matplotlib.pyplot as plt

# Generar datos de ejemplo
X = np.array([[1, 2], [2, 2], [2, 3],
              [8, 7], [8, 8], [25, 80]])

# Aplicar DBSCAN
db = DBSCAN(eps=3, min_samples=2).fit(X)

# Obtener etiquetas de clúster
labels = db.labels_

# Visualizar los clústeres
plt.scatter(X[:, 0], X[:, 1], c=labels, cmap='viridis')
plt.show()
```

En este ejemplo, `DBSCAN` se aplica a un pequeño conjunto de datos, con `eps` establecido en 3 y `min_samples` en 2. Los clústeres se visualizan mediante colores.

### Resumen

DBSCAN es un algoritmo potente y versátil para clustering, especialmente útil cuando se espera que los clústeres tengan formas arbitrarias y haya puntos de ruido presentes en los datos. Su capacidad para encontrar clústeres basados en densidad y manejar puntos atípicos lo hace ampliamente utilizado en diversas aplicaciones, desde análisis de datos hasta reconocimiento de patrones.

# Clase sobre LDP-MST (Clustering basado en picos de densidad local y árbol de expansión mínima)

#### Introducción

LDP-MST es un algoritmo de clustering basado en la densidad que utiliza picos de densidad local para construir un árbol de expansión mínima (MST). Este método es eficaz para identificar clústeres de formas arbitrarias y es robusto frente al ruido. La idea central es seleccionar puntos de alta densidad local como centros de clústeres y utilizar la distancia basada en vecinos compartidos para construir el MST.

#### Conceptos Básicos

1. **Densidad Local**: Medida que indica cuán "denso" es el entorno alrededor de un punto. Se calcula contando los puntos en un vecindario definido por un radio o por los \( k \) vecinos más cercanos.
2. **Picos de Densidad Local**: Puntos con mayor densidad local que sus vecinos más cercanos. Actúan como centros de clústeres.
3. **Distancia Basada en Vecinos Compartidos**: Distancia entre picos de densidad local que considera no solo la distancia euclidiana sino también la cantidad de vecinos compartidos.

#### Pasos del Algoritmo LDP-MST

1. **Calcular Densidad Local**:
    - Para cada punto en el conjunto de datos, se calcula la densidad local en función de sus \( k \) vecinos más cercanos.

2. **Identificar Picos de Densidad Local**:
    - Comparar la densidad local de cada punto con la de sus vecinos más cercanos.
    - Un punto es un pico de densidad local si su densidad es mayor que la de todos sus vecinos.

3. **Calcular la Distancia Basada en Vecinos Compartidos**:
    - Definir vecinos y vecinos compartidos de los picos de densidad local.
    - Utilizar estos vecinos para calcular la distancia entre picos.

4. **Construir el MST**:
    - Utilizar los picos de densidad local y las distancias basadas en vecinos compartidos para construir un árbol de expansión mínima.

5. **Dividir el MST para Formar Clústeres**:
    - Cortar repetidamente la arista más larga del MST hasta obtener el número deseado de clústeres.
    - Asignar los puntos restantes al clúster correspondiente según el pico de densidad local más cercano.

#### Ejemplo Práctico

Supongamos que tenemos un conjunto de datos bidimensional:

$$ \{(1,2), (2,2), (2,3), (8,7), (8,8), (25,80)\} $$

### Paso 1: Calcular Densidad Local

```python
from sklearn.neighbors import NearestNeighbors
import numpy as np

# Datos
data = np.array([[1, 2], [2, 2], [2, 3], [8, 7], [8, 8], [25, 80]])

# Calcular vecinos más cercanos
nbrs = NearestNeighbors(n_neighbors=2).fit(data)
distances, indices = nbrs.kneighbors(data)

# Calcular densidad local (número de vecinos)
densidad_local = np.array([len(nbrs.radius_neighbors([point], radius=3)[0][0]) for point in data])
print("Densidad Local:", densidad_local)
```

### Paso 2: Identificar Picos de Densidad Local

```python
# Identificar picos de densidad local
picos = []
for i, densidad in enumerate(densidad_local):
    vecinos = indices[i]
    es_pico = True
    for vecino in vecinos:
        if densidad_local[vecino] > densidad:
            es_pico = False
            break
    if es_pico:
        picos.append(i)

print("Picos de Densidad Local:", picos)
```

### Paso 3: Calcular la Distancia Basada en Vecinos Compartidos

```python
from scipy.spatial.distance import euclidean

# Calcular vecinos compartidos
def vecinos_compartidos(p1, p2, data, radius=3):
    vecinos_p1 = set(nbrs.radius_neighbors([data[p1]], radius=radius)[1][0])
    vecinos_p2 = set(nbrs.radius_neighbors([data[p2]], radius=radius)[1][0])
    return len(vecinos_p1.intersection(vecinos_p2))

# Calcular distancia basada en vecinos compartidos
distancias = []
for i in picos:
    for j in picos:
        if i != j:
            dist = euclidean(data[i], data[j]) / (1 + vecinos_compartidos(i, j, data))
            distancias.append((i, j, dist))

print("Distancias Basadas en Vecinos Compartidos:", distancias)
```

### Paso 4: Construir el MST

```python
import networkx as nx

# Crear grafo y añadir aristas
G = nx.Graph()
G.add_weighted_edges_from(distancias)

# Construir MST
mst = nx.minimum_spanning_tree(G)
print("MST Edges:", mst.edges(data=True))
```

### Paso 5: Dividir el MST para Formar Clústeres

```python
import matplotlib.pyplot as plt

# Dibujar MST
pos = {i: data[i] for i in picos}
nx.draw(mst, pos, with_labels=True, node_color='orange', node_size=500, font_size=16)
plt.show()

# Dividir el MST (cortar aristas más largas)
aristas = sorted(mst.edges(data=True), key=lambda x: x[2]['weight'], reverse=True)
num_clusters = 2  # Número deseado de clústeres
for i in range(num_clusters - 1):
    mst.remove_edge(*aristas[i][:2])

# Obtener clústeres
clusters = list(nx.connected_components(mst))
print("Clústeres:", clusters)
```

### Asignar Puntos a los Clústeres

Finalmente, cada punto restante se asigna al clúster correspondiente según el pico de densidad local más cercano.

```python
asignaciones = [-1] * len(data)
for cluster_id, cluster in enumerate(clusters):
    for nodo in cluster:
        asignaciones[nodo] = cluster_id

# Asignar puntos restantes
for i in range(len(data)):
    if asignaciones[i] == -1:
        distancias = [euclidean(data[i], data[nodo]) for nodo in picos]
        asignaciones[i] = distancias.index(min(distancias))

print("Asignaciones Finales:", asignaciones)
```

### Conclusión

LDP-MST es un algoritmo poderoso para el clustering de datos con estructuras complejas y ruido. Al utilizar picos de densidad local y distancias basadas en vecinos compartidos, este algoritmo puede identificar clústeres de formas arbitrarias y es menos sensible al ruido.