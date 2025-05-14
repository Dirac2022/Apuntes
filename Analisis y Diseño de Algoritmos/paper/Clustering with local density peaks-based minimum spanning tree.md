Clustering con árbol de expansión mínima basado en picos de densidad local
# Resumen

==El análisis de clustering ha sido ampliamente utilizado en estadísticas, aprendizaje automático, reconocimiento de patrones, procesamiento de imágenes, entre otros campos. Uno de los mayores desafíos para la mayoría de los algoritmos de clustering existentes es descubrir clusters con formas arbitrarias==. ==Los algoritmos de clustering basados en Árbol de Expansión Mínima (MST) pueden descubrir clusters con formas arbitrarias, pero son computacionalmente costosos y susceptibles a puntos de ruido==. En este trabajo, utilizamos picos de densidad local (LDP) para representar todo el conjunto de datos y definimos una distancia basada en vecinos compartidos entre picos de densidad local para medir mejor la disimilitud entre objetos en datos manifolds. ==Basándonos en los picos de densidad local y en la nueva distancia, proponemos un nuevo algoritmo de clustering basado en MST llamado LDP-MST==. Este utiliza primero picos de densidad local para construir el MST y luego corta repetidamente la arista más larga hasta encontrar un número dado de clusters. Los resultados experimentales en conjuntos de datos sintéticos y reales muestran que nuestro algoritmo es competitivo con métodos de vanguardia al descubrir clusters con estructuras complejas.

>[!summary]+
>El análisis de clustering es utilizado en diversos campos como estadísticas y aprendizaje automático. Los algoritmos basados en Árbol de Expansión Mínima (MST) pueden descubrir clusters con formas arbitrarias, pero son costosos y sensibles al ruido. Este trabajo propone el algoritmo LDP-MST, que utiliza picos de densidad local (LDP) y una distancia basada en vecinos compartidos para construir el MST y cortar repetidamente la arista más larga. Los resultados experimentales muestran que LDP-MST es efectivo para descubrir clusters con estructuras complejas.

# Palabras Clave

Árbol de expansión mínima, clustering, picos de densidad local, distancia basada en vecinos compartidos

# I. INTRODUCCIÓN

El clustering, como método importante de ==aprendizaje no supervisado==, ha sido ampliamente estudiado y aplicado en estadísticas, aprendizaje automático, reconocimiento de patrones y procesamiento de imágenes. Su objetivo es clasificar objetos en varios grupos de manera que los objetos dentro del mismo grupo sean lo más similares posible, mientras que los objetos en diferentes grupos sean lo más distintos posible. Se han propuesto muchos algoritmos de clustering.

K-means [1] y K-medoids [2] son algoritmos típicos de clustering por particionamiento, pero requieren inicializar centros de clústeres. Para evitar la inicialización de centros de clústeres, el algoritmo de Propagación de Afinidad (AP) [3] considera todos los puntos de datos como potenciales centros. ==Un algoritmo de clustering basado en la búsqueda rápida y localización de picos de densidad [4] (DP por sus siglas en inglés) selecciona puntos con máxima densidad local como centros de clústeres y asigna los puntos restantes al mismo clúster que su vecino más cercano de mayor densidad. Sin embargo, estos algoritmos no pueden descubrir clusters con formas arbitrarias==. Los autores en [5] asumen que cada clúster tiene núcleos de densidad reducida que conservan aproximadamente la forma del clúster y proponen un algoritmo de clustering basado en núcleos de densidad, llamado Dcore. ==El algoritmo de clustering basado en densidad DBSCAN [6] define clusters como regiones densas separadas por regiones dispersas. Su idea clave es que para cada punto central de un clúster, el vecindario dentro de un radio dado debe contener al menos un número mínimo de puntos==. Dcore y DBSCAN son efectivos para reconocer clusters con formas arbitrarias, pero requieren configurar muchos parámetros. En [7], los autores utilizan un método analítico para estimar el radio del vecindario en DBSCAN.

Recientemente, se ha prestado más atención al clustering basado en grafos. Algunos métodos basados en grafos [8], [9] construyen un grafo de k-vecinos más cercanos para representar un conjunto de datos. Chameleon [8] primero construye un grafo de k-vecinos más cercanos, luego divide el grafo en subgrafos y obtiene los clústeres finales mediante la fusión repetida de subgrafos más similares. Sin embargo, es un proceso que consume mucho tiempo. Un clustering aglomerativo rápido en [9] utiliza un grafo de vecinos más cercanos aproximado para reducir el número de cálculos de distancia.

Algunos otros métodos basados en grafos [10], [11] aprovechan el árbol de expansión mínima (MST) para el clustering. ==Los enfoques de clustering basados en MST no asumen que los puntos de datos están agrupados alrededor de centros o separados por curvas geométricas regulares. En cambio, utilizan la información de las aristas del árbol para dividir un conjunto de datos en clústeres y son capaces de detectar clústeres con formas arbitrarias.==

Guidotti et al. [12] proponen un algoritmo de clustering en dos pasos (TOSCA) para la detección de ubicaciones personales. TOSCA combina los algoritmos de clustering X-means y de clustering jerárquico de enlace único, y aplica pruebas estadísticas para seleccionar los parámetros necesarios. ==El algoritmo de clustering basado en MST propuesto en [10] define aristas inconsistentes como aquellas cuyos pesos son significativamente mayores que el peso promedio de las aristas cercanas en el árbol. Sin embargo, al utilizar solo las aristas contenidas en un MST para dividir un conjunto de datos, puede no detectar clústeres con estructuras complejas y se ve fácilmente afectado por puntos de ruido.==

El algoritmo en [13] utiliza un grafo compuesto por dos rondas de árboles de expansión mínima para el clustering. Hay otros algoritmos de clustering basados en MST que maximizan o minimizan los grados de enlace de los vértices [14], [15]. Sin embargo, estos algoritmos son computacionalmente costosos. Además, la presencia de puntos de ruido puede reducir la distancia entre puntos en diferentes clústeres y hacer que las aristas más largas sean una medida poco confiable de las separaciones entre clústeres. Para evitar la influencia de puntos de ruido, el método en [16] (denominado LOF-MST en este trabajo) emplea el factor local de outliers (LOF) [17] para descartar puntos de ruido cuyos factores de densidad sean mayores que un umbral durante la construcción del MST. Sin embargo, LOF-MST tiende a considerar puntos normales como puntos de ruido.

Para evitar la influencia de puntos de ruido y reducir el tiempo de ejecución de los métodos de clustering basados en MST, una forma potencial es seleccionar algunos puntos como representantes para que estos conserven aproximadamente la forma de los clústeres y excluyan la interferencia de puntos de ruido. Además, construir el MST sobre representantes reduce significativamente el tiempo de ejecución en comparación con el uso de todos los puntos. Inspirados en esta idea, proponemos un método de clustering basado en árbol de expansión mínima con picos de densidad local, llamado LDP-MST, que es tanto eficiente computacionalmente como competente con otros enfoques de clustering de vanguardia al descubrir clústeres complejos. En LDP-MST, primero encontramos picos de densidad local y asignamos los puntos restantes a los picos de densidad local correspondientes. Luego, definimos una nueva distancia entre picos de densidad local basada en vecinos compartidos y utilizamos esta nueva distancia para construir el árbol de expansión mínima sobre los picos de densidad local. Obtenemos los clústeres finales eliminando continuamente la arista más larga.

==Para demostrar la efectividad de nuestro método, realizamos experimentos comparando LDP-MST con el método de particionamiento Kmeans [1], el método basado en densidad DBSCAN [6], el método basado en centros DP [4] y Dcore [5], y el método basado en MST LOF-MST [16]. Los resultados experimentales en conjuntos de datos sintéticos y reales muestran que el algoritmo propuesto es más efectivo que los métodos comparados.==

El resto de este artículo está organizado de la siguiente manera. En la Sección II, revisamos el trabajo relacionado en algoritmos de clustering basados en centros, basados en densidad y basados en MST. La Sección III introduce el vecino natural. La Sección IV describe el algoritmo de clustering propuesto LDP-MST. Los resultados experimentales se analizan en la Sección V. La Sección VI concluye este trabajo.



>[!summary]+
>Un algoritmo de clustering basado en la búsqueda rápida y localización de picos de densidad (DP por sus siglas en inglés) selecciona puntos con máxima densidad local como centros de clústeres y asigna los puntos restantes al mismo clúster que su vecino más cercano de mayor densidad. Sin embargo, estos algoritmos no pueden descubrir clusters con formas arbitrarias
>El algoritmo de clustering basado en densidad DBSCAN define clusters como regiones densas separadas por regiones dispersas. Su idea clave es que para cada punto central de un clúster, el vecindario dentro de un radio dado debe contener al menos un número mínimo de puntos. Este algoritmo es efectivo para reconocer clusters con formas arbitrarias, pero requieren configurar muchos parámetros. Los enfoques de clustering basados en MST no asumen que los puntos de datos están agrupados alrededor de centros o separados por curvas geométricas regulares. En cambio, utilizan la información de las aristas del árbol para dividir un conjunto de datos en clústeres y son capaces de detectar clústeres con formas arbitrarias. El algoritmo de clustering basado en MST propuesto en [10] define aristas inconsistentes como aquellas cuyos pesos son significativamente mayores que el peso promedio de las aristas cercanas en el árbol. Sin embargo, al utilizar solo las aristas contenidas en un MST para dividir un conjunto de datos, puede no detectar clústeres con estructuras complejas y se ve fácilmente afectado por puntos de ruido. Para demostrar la efectividad de nuestro método, realizamos experimentos comparando LDP-MST con el método de particionamiento Kmeans [1], el método basado en densidad DBSCAN [6], el método basado en centros DP [4] y Dcore [5], y el método basado en MST LOF-MST [16]. Los resultados experimentales en conjuntos de datos sintéticos y reales muestran que el algoritmo propuesto es más efectivo que los métodos comparados.
>
# II. TRABAJO RELACIONADO

## A. Algoritmos de clustering basados en centros

Un paso clave en Kmeans [1] y Kmedoids [2] es encontrar los centros de los clústeres optimizando una función objetivo, típicamente la suma de las distancias a un conjunto de centros. Por lo tanto, también pueden considerarse algoritmos de clustering basados en centros. La diferencia entre ellos es que Kmeans actualiza los centros de clúster utilizando las medias de todos los puntos asignados al mismo clúster y Kmedoids actualiza los centros de clúster con otros objetos que pueden mejorar la calidad del clúster. El algoritmo DP [4] asume que los centros de clúster están rodeados por vecinos con densidad local más baja y que están a una distancia relativamente grande de cualquier punto con una densidad local más alta. Para obtener los centros de clúster, el algoritmo DP mapea los datos en un gráfico de dispersión bidimensional con respecto a la densidad local ρ y la distancia mínima a los puntos con una densidad local más alta δ, llamado gráfico de decisión. Los centros de clúster se destacan con un valor anormalmente alto de ρ y δ en el gráfico de decisión. Sin embargo, dado que simplemente asignan los puntos restantes al centro más cercano o a puntos con densidad local más alta, ==los algoritmos Kmeans, Kmedoids y DP no pueden descubrir clústeres con formas arbitrarias.==
Para procesar conjuntos de datos que contienen clústeres con formas arbitrarias, se propone el algoritmo Dcore [5]. Su idea subyacente es que cada clúster tiene un núcleo de densidad reducida que aproximadamente conserva la forma del clúster. Cada uno de estos núcleos consiste en un conjunto de puntos centrales débilmente conectados con una densidad más alta que la de sus alrededores, y las fronteras y los valores atípicos se distribuyen alrededor de estos núcleos en una estructura jerárquica. Sin embargo, el algoritmo requiere configurar demasiados parámetros para distinguir núcleos, fronteras y valores atípicos, así como para identificar clústeres.

>Los algoritmos Kmeans, Kmedoids no pueden descubrir clústeres con formas arbitrarias.
Para procesar conjuntos de datos que contienen clústeres con formas arbitrarias, se propone el algoritmo Dcore. Su idea subyacente es que cada clúster tiene un núcleo de densidad reducida que aproximadamente conserva la forma del clúster. Cada uno de estos núcleos consiste en un conjunto de puntos centrales débilmente conectados con una densidad más alta que la de sus alrededores, y las fronteras y los valores atípicos se distribuyen alrededor de estos núcleos en una estructura jerárquica. Sin embargo, el algoritmo requiere configurar demasiados parámetros para distinguir núcleos, fronteras y valores atípicos, así como para identificar clústeres.

## B. Algoritmos de clustering basados en la densidad

==Los clústeres basados en la densidad están separados entre sí por regiones contiguas de baja densidad de objetos. DBSCAN es un algoritmo típico de clustering basado en la densidad. Con dos parámetros, Eps y MinPts, DBSCAN proporciona una serie de definiciones: puntos centrales, alcanzables directamente por densidad, alcanzables por densidad y conectados por densidad. Los clústeres están compuestos por puntos conectados por densidad, y los puntos de ruido son aquellos que no pertenecen a ningún clúster. DBSCAN puede reconocer clústeres de formas arbitrarias, pero la configuración unificada de parámetros dificulta descubrir clústeres con diversas densidades.==

Se han realizado muchos trabajos excelentes para resolver los problemas de DBSCAN. El algoritmo basado en celdas Cell-based DBSCAN, utilizando el rectángulo de mínima unión (MBR, por sus siglas en inglés) [18], es una versión exacta de DBSCAN. Divide el conjunto de datos completo en pequeñas celdas y conecta las celdas utilizando criterios de MBR, lo que mejora considerablemente la eficiencia de DBSCAN. NG-DBSCAN [19] es un algoritmo aproximado de clustering basado en la densidad. Su diseño distribuido lo hace escalable para conjuntos de datos muy grandes, y su naturaleza aproximada lo hace rápido. Random Partitioning-DBSCAN (RPDBSCAN) [20] es un algoritmo DBSCAN paralelo que utiliza un esquema de particionado de datos basado en celdas, particionado pseudoaleatorio, para lograr un alto equilibrio de carga independientemente de la asimetría de los datos, manteniendo al mismo tiempo la contigüidad de los datos requerida para DBSCAN. Se propone un nuevo algoritmo de clustering basado en la densidad en cualquier momento (AnyDBC) [21] para conjuntos de datos complejos muy grandes. Comprime los datos en subconjuntos más pequeños conectados por densidad llamados clústeres primitivos y etiqueta los objetos según los componentes conectados de estos clústeres primitivos para reducir el tiempo de propagación de etiquetas. Además, dado que aprende de manera iterativa y activa la estructura actual de clústeres de los datos y selecciona unos pocos objetos más prometedores para refinar los clústeres, realiza menos consultas de rango garantizando el resultado final exacto de DBSCAN. Kriegel et al. [22] presentan la intuición que motiva la definición basada en la densidad de clústeres junto con una visión general de métodos estadísticos y algoritmos eficientes aplicables a grandes conjuntos de datos.

## C. Algoritmos de clustering basados en el MST

==Dado un grafo conectado y no dirigido, un árbol de expansión mínima (MST, por sus siglas en inglés) es un subgrafo que conecta todos los vértices con la suma mínima de los pesos de las aristas y sin ciclos. Los algoritmos tradicionales de clustering basados en el MST primero utilizan el algoritmo de Prim [23] o el algoritmo de Kruskal [24] para construir un MST según una medida de distancia, y luego eliminan continuamente aristas inconsistentes para obtener un conjunto de componentes conectados (clústeres) hasta que se cumple la condición terminal. La condición ideal es que los clústeres estén bien separados y que las aristas inconsistentes sean precisamente las aristas más largas, pero el desafío radica en que la existencia de puntos de ruido hace que las aristas más largas sean una indicación poco confiable de las separaciones entre clústeres. Por lo tanto, la definición de aristas inconsistentes y la condición terminal son dos problemas importantes que deben abordarse en los algoritmos de clustering basados en el MST.==

Se han propuesto diferentes tipos de aristas inconsistentes en la literatura. Zahn [10] propone un algoritmo de clustering basado en el MST que define las aristas inconsistentes como aquellas cuyos pesos son significativamente mayores que el peso promedio de las aristas cercanas en el árbol. Sin embargo, esto se ve afectado por el tamaño del vecindario cercano. El método en [25] asume que el límite entre cualquier par de clústeres debe pertenecer a una región dispersa y la medida de inconsistencia se basa en encontrar tales regiones dispersas. Para lograr los mejores resultados de clustering, se proponen diferentes condiciones terminales. Los autores en [26] proponen diferentes funciones objetivo para diferentes problemas de clustering basados en el MST: minimizar el cambio del peso total de los clústeres actuales desde el anterior cuando no se predefine el número de clústeres y, de lo contrario, minimizar la distancia total entre el centro de un clúster y cada punto en ese clúster. El algoritmo LM [27] impone una restricción sobre el tamaño mínimo del clúster en lugar del número de clústeres.

Recientemente, se han propuesto algunos algoritmos novedosos de clustering basados en el MST. Wang et al. [11] presentan un algoritmo rápido de clustering inspirado en el árbol de expansión mínima, que utiliza un enfoque de divide y vencerás para construir el árbol de expansión mínima. En [13], se presenta un método de clustering teórico-gráfico (2-MSTClus). Basado en el grafo compuesto por dos rondas de árboles de expansión mínima, 2-MSTClus divide los problemas de clústeres en problemas de clústeres separados y problemas de clústeres tocantes, identificando automáticamente estos dos problemas. Para representar mejor clústeres con formas arbitrarias, Luo et al. [28] utilizan múltiples prototipos en lugar de un único prototipo y proponen un algoritmo de clustering basado en el MST con múltiples prototipos. Se propone un método jerárquico de clustering de dividir y fusionar (split-and-merge) en [29] para aliviar las deficiencias que presentan la mayoría de los algoritmos de clustering cuando se proporcionan parámetros inadecuados o cuando se procesan conjuntos de datos que contienen clústeres con formas, tamaños y densidades diferentes. Utiliza un grafo basado en el MST para guiar el proceso de división y fusión. En el proceso de división, se seleccionan vértices con altos grados en el grafo basado en el MST como prototipos iniciales, y se utiliza Kmeans para dividir el conjunto de datos. En el proceso de fusión, se filtran pares de subgrupos y solo se consideran pares vecinos para la fusión. Para evitar la influencia de puntos de ruido, el método en [16] mejora el clustering basado en el MST eliminando los valores atípicos. Funciona encontrando un factor de densidad local para cada punto de datos durante la construcción del MST y descartando los valores atípicos cuyo factor de densidad local sea mayor que un umbral para aumentar la separación entre clústeres. Obtiene los clústeres finales eliminando continuamente las aristas más largas hasta encontrar un número dado de clústeres. Algunos algoritmos basados en el MST no requieren un número de clústeres como entrada y son capaces de manejar datos de alta dimensionalidad. En [30], los autores extienden el algoritmo escalable de evaluación visual de tendencia (sVAT) y construyen un MST de un grafo ponderado no dirigido para particionar conjuntos de datos grandes. De manera similar, los autores en [31] proponen un nuevo algoritmo de clustering rápido, que integra una nueva técnica de conjunto basada en proyección aleatoria y una mejora en la evaluación visual de la tendencia de clústeres (iVAT), para tratar con grandes volúmenes de datos de alta dimensionalidad.

>[!summary]+
>Los algoritmos Kmeans, Kmedoids no pueden descubrir clústeres con formas arbitrarias.  
  Para procesar conjuntos de datos que contienen clústeres con formas arbitrarias, se propone el  algoritmo Dcore. Su idea subyacente es que cada clúster tiene un núcleo de densidad reducida que aproximadamente conserva la forma del clúster. Cada uno de estos núcleos consiste en un conjunto de puntos centrales débilmente conectados con una densidad más alta que la de sus alrededores, y las fronteras y los valores atípicos se distribuyen alrededor de estos núcleos en una estructura jerárquica. Sin embargo, el algoritmo requiere configurar demasiados parámetros para distinguir núcleos, fronteras y valores atípicos, así como para identificar clústeres. 
> 
> Los clústeres basados en la densidad están separados entre sí por regiones contiguas de baja densidad de objetos. DBSCAN es un algoritmo típico de clustering basado en la densidad. Con dos parámetros, Eps y MinPts, DBSCAN proporciona una serie de definiciones: puntos centrales, alcanzables directamente por densidad, alcanzables por densidad y conectados por densidad. Los clústeres están compuestos por puntos conectados por densidad, y los puntos de ruido son aquellos que no pertenecen a ningún clúster. DBSCAN puede reconocer clústeres de formas arbitrarias, pero la configuración unificada de parámetros dificulta descubrir clústeres con diversas densidades
>
  Dado un grafo conectado y no dirigido, un árbol de expansión mínima (MST, por sus siglas en inglés) es un subgrafo que conecta todos los vértices con la suma mínima de los pesos de las aristas y sin ciclos. Los algoritmos tradicionales de clustering basados en el MST primero utilizan el algoritmo de Prim [23] o el algoritmo de Kruskal [24] para construir un MST según una medida de distancia, y luego eliminan continuamente aristas inconsistentes para obtener un conjunto de componentes conectados (clústeres) hasta que se cumple la condición terminal. La condición ideal es que los clústeres estén bien separados y que las aristas inconsistentes sean precisamente las aristas más largas, pero el desafío radica en que la existencia de puntos de ruido hace que las aristas más largas sean una indicación poco confiable de las separaciones entre clústeres. Por lo tanto, la definición de aristas inconsistentes y la condición terminal son dos problemas importantes que deben abordarse en los algoritmos de clustering basados en el MST





# III. VECINO NATURAL
El vecino natural [32] es un nuevo concepto de vecindad que ha sido utilizado en análisis de clustering [33], detección de valores atípicos [34] y reducción de prototipos [35], mostrando un rendimiento muy bueno en minería de datos. Sea $d(x, y)$ la distancia entre los puntos $x$ e $y$, y el punto $o$ el k-ésimo vecino más cercano de un punto $p$. Siguiendo [36], [37], las definiciones de los $k$ vecinos más cercanos y los $k$ vecinos más cercanos inversos se pueden dar de la siguiente manera:

### Definiciones

**Definición 1 (k vecinos más cercanos):** Los $k$ vecinos más cercanos del punto $p$ son un conjunto de puntos $x$ en $D$ con $d(p, x) \leq d(p, o)$, es decir, 
$NN_k(p) = \{ x \in D | d(p, x) \leq d(p, o) \}$.

**Definición 2 (k vecinos más cercanos inversos):** Los $k$ vecinos más cercanos inversos del punto $p$ son un conjunto de puntos $x$ en $D$ que consideran a $p$ como uno de sus $k$ vecinos más cercanos, es decir, 
$RNN_k(p) = \{ x \in D | p \in NN_k(x) \}$.

La formación del vecino natural es la siguiente: expandir continuamente el rango de búsqueda de vecinos $r$, y calcular el número de vecinos más cercanos inversos $nb(p)$ de cada punto $p$ en cada iteración, hasta que el número de puntos sin vecinos inversos no cambie. El rango de búsqueda de vecinos $r$ en este momento se llama valor característico natural $\lambda$. La definición formal del valor característico natural es la siguiente.

**Definición 3 (Valor característico natural $\lambda$):** En la formación del vecino natural, cuando el número de puntos sin vecinos inversos no cambie, el rango de búsqueda de vecinos $r$ es el valor característico natural $\lambda$.

El proceso detallado para obtener el valor característico natural se elabora en el Algoritmo 1, donde $NN_r(p)$ son los $r$ vecinos más cercanos del punto $p$ y $RNN_r(q)$ son los $r$ vecinos más cercanos inversos de $q$. $nb(q)$ es el número de vecinos inversos del punto $q$ y es mayor para puntos en regiones densas que en regiones dispersas.

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Analisis y Diseño de Algoritmos\paper\algoritmo1.png" alt="">
    <figcaption>.</figcaption>
    </figure>
</div>



# IV. EL ALGORITMO PROPUESTO
Los algoritmos existentes de clustering basados en MST construyen el MST sobre conjuntos de datos completos y solo utilizan la información de las aristas contenidas en el árbol para particionar un conjunto de datos. Por lo tanto, son computacionalmente costosos y vulnerables a puntos de ruido. En este artículo, proponemos un algoritmo de clustering novedoso basado en árbol de expansión mínima con picos de densidad local (LDP-MST). Tomando como ejemplo un conjunto de datos simple mostrado en la Figura 1, la idea principal de LDP-MST es la siguiente. 
- Primero, seleccionamos puntos con máxima densidad local entre sus vecinos como picos de densidad local, y los puntos restantes se asignan a los picos de densidad local correspondientes, como se muestra en la Figura 1(a). 
- Luego, definimos una nueva distancia entre picos de densidad local que tiene en cuenta la distancia euclidiana y la información de vecindad. Empleamos los picos de densidad local y la nueva distancia para construir el MST, como se muestra en la Figura 1(b). 
- Después, eliminamos continuamente la arista más larga basada en la nueva distancia hasta obtener el número deseado de clusters. Las aristas amarillas mostradas en la Figura 1(c) son las aristas que eliminamos del MST y los números indican el orden en el que se cortan las aristas.
- Finalmente, obtenemos el resultado del clustering mostrado en la Figura 1(d). Debido a la construcción del MST solo sobre picos de densidad local, se reduce la interferencia de puntos de ruido y se mejora considerablemente la eficiencia del algoritmo.

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Analisis y Diseño de Algoritmos\paper\figura1.png" alt="">
    <figcaption>Fig. 1. The main idea of LDP-MST. (a) The local density peaks and their members. (b) The MST constructed with new defined distance. (c) The yellow edges are cut edges. (d) The clustering result of LDP-MST.</figcaption>
    </figure>
</div>


## A. Densidad local
Para encontrar los picos de densidad local, primero definimos la densidad local de los puntos. La suma de distancias entre un punto en una región densa y sus vecinos más cercanos suele ser menor que en una región dispersa. El valor de $nb$ es grande para los puntos en la región densa y pequeño en la región dispersa. Por lo tanto, la densidad local de un punto p es proporcional al valor de $nb(p)$ e inversamente proporcional a la distancia entre él y sus vecinos. Se calcula de la siguiente manera:
$$
\rho(p) = \frac{nb(p)}{\sum_{\ q \ \in \ N \ N_k(p)} d(p, q)} \quad \quad (1)
$$
donde $k =max(nb)$, $nb(p)$ se obtiene del algoritmo de búsqueda $NaN$, $NNk(p)$ son los $k$ vecinos más cercanos del punto p, y d(p, q) es la distancia entre los puntos $p$ y $q$. $A$ diferencia de las definiciones en [4], [38], la densidad local definida aquí no necesita establecer ningún parámetro ya que el algoritmo de búsqueda $NaN$ se compromete a encontrar el parámetro adecuado.

## B. Picos de densidad local

Para explorar un vecindario local adecuado, primero encontramos puntos con densidad máxima local entre los $k$ vecinos más cercanos de cada punto y los llamamos representantes. Se define de la siguiente manera.

**Definición 4 (Representante):** Si la densidad local del punto $q$ es máxima entre $p$ y los $k$ vecinos más cercanos de $p$, entonces $q$ es el representante de $p$, denotado como $Rep(p) = q$.

Esta definición define la relación de cada punto con su representante. Tomemos como ejemplo un conjunto de datos simple mostrado en la Fig. 2(a), donde $k$ se establece en 4 según el algoritmo de búsqueda $NaN$. Para cada punto $p$, seleccionamos un punto con densidad local máxima entre $p$ y sus 4 vecinos más cercanos como su representante, que se muestra como los puntos cuadrados rojos en la Fig. 2(b). La Fig. 2(b) también describe la relación de puntos a puntos. Es un grafo acíclico dirigido denotado como $RDAG$. En $RDAG$, hay un arco dirigido desde cada punto $p$ hacia su representante $Rep(p)$. La propiedad de aciclicidad se demuestra a continuación.

**Propiedad 1:** $RDAG$ no contiene ciclos.
**Demostración por contradicción:**
Para un $RDAG$, asumimos que existe un ciclo. Esto significa que hay una cadena de puntos diferentes $p_1, p_2, \ldots, p_n$ con $Rep(p_1) = p_2, Rep(p_2) = p_3, \ldots, Rep(p_n) = p_1$.
Según la Definición 4, si $Rep(p_1) = p_2$ y $p_1 \neq p_2$, entonces $\rho(p_1) < \rho(p_2)$.
De manera similar, tenemos $\rho(p_2) < \rho(p_3), \ldots, \rho(p_{n-1}) < \rho(p_n), \rho(p_n) < \rho(p_1)$.
Entonces, podemos concluir que $\rho(p_1) < \rho(p_n)$ y $\rho(p_n) < \rho(p_1)$, lo cual es evidentemente contradictorio.
Por lo tanto, la suposición no se sostiene y la afirmación es verdadera.
Desde la Fig. 2(b), podemos ver que hay algunos puntos (los puntos rojos sólidos) que se seleccionan a sí mismos como representantes. Son picos de densidad local, definidos de la siguiente manera.

**Definición 5 (Pico de densidad local, LDP):** 
Un punto $p$ es un pico de densidad local si $Rep(p) = p$.
La Fig. 2 muestra que $RDAG$ consiste en varios subgrafos. El número de $LDP$s es igual al número de subgrafos. Después de que se han encontrado los picos de densidad local, asignamos cada punto restante a los picos de densidad local correspondientes. Por lo tanto, definimos la regla de transferencia de representantes para cambiar el representante de cada punto restante al pico de densidad local correspondiente.


**Definición 6 (Regla de transferencia de representante, RTR):** Si $Rep(p) = q$ y $Rep(q) = r$, entonces $Rep(p) = r$.

El algoritmo para encontrar picos de densidad local se detalla en el Algoritmo 2. El propósito del Algoritmo 2 es también identificar cada punto con el nodo raíz de su árbol. La Fig. 2(c) muestra el resultado del algoritmo de búsqueda $LDP$ en un conjunto de datos de ejemplo. Los puntos sólidos rojos en la Fig. 2(c) son picos de densidad local y son puntos con densidad máxima local. Los puntos restantes se convierten en miembros de los picos de densidad local correspondientes.

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Analisis y Diseño de Algoritmos\paper\algoritmo2.png" alt="">
    <figcaption>.</figcaption>
    </figure>
</div>

**Definición 7 (Miembros del pico de densidad local, MLDP):** Para un pico de densidad local $p$, sus miembros son puntos cuyos representantes son $p$. Formalmente, se define como:
$$
MLDP(p) = \{ q \in D \mid Rep(q) = p \}
$$

## C. Distancia basada en vecinos compartidos entre picos de densidad local

La distancia euclidiana no es una medida adecuada para datos de variedades y en [39] se sugiere la distancia geodésica para evaluar la disimilitud entre puntos en datos de variedades. Sin embargo, la distancia geodésica exacta no se puede obtener directamente, porque no tenemos información previa sobre las variedades subyacentes. En [40], [41], los autores utilizan la longitud del camino más corto entre dos puntos para aproximar la distancia geodésica, pero este método requiere una complejidad temporal muy alta. En este artículo, basándonos en los vecinos compartidos de los picos de densidad local, proponemos una nueva distancia, que es la distancia basada en vecinos compartidos entre picos de densidad local. Los vecinos y los vecinos compartidos de los picos de densidad local se definen de la siguiente manera.

**Definición 8 (Vecinos de los picos de densidad local, NLDP):** Para un pico de densidad local $p$, sus vecinos son la unión de los $\lambda$ vecinos más cercanos de todos sus miembros, donde $\lambda$ es el valor característico natural. Se define como:
$$
NLDP(p) = \bigcup_{q \in MLDP(p)} NN_{\lambda}(q) \tag{3}
$$

**Definición 9 (Vecinos compartidos entre dos picos de densidad local, SLDP):** Los vecinos compartidos de dos picos de densidad local $p$ y $q$ son la intersección de sus vecinos. Se define como:
$$
SLDP(p, q) = NLDP(p) \cap NLDP(q) \tag{4}
$$

Continuando con el conjunto de datos mostrado en la Fig. 2(a) como ejemplo, la Fig. 3(a) revela los vecinos de cada pico de densidad local, que incluye sus miembros y algunos vecinos adicionales más cercanos, denotados por puntos verdes y rojos, respectivamente. La intersección de los vecinos de los picos de densidad local son los vecinos compartidos que se muestran como puntos amarillos en la Fig. 3(b). Hay 10 vecinos compartidos entre L1 y L2, y 15 vecinos compartidos entre L3 y L4. Para dos LDPs, un mayor número y densidad de vecinos compartidos indica una menor distancia entre ellos. Así, la distancia basada en vecinos compartidos se define de la siguiente manera.

**Definición 10 (Distancia basada en vecinos compartidos entre picos de densidad local, SD):** Para los picos de densidad local $p$ y $q$, su distancia basada en vecinos compartidos se calcula como:
$$
SD(p, q) = 
\begin{cases}
\frac{d(p, q)}{|SLDP(p, q)|} \times \sum_{o \in SLDP(p, q)} \rho(o), & \text{si } |SLDP(p, q)| \neq 0 \\
maxd \times (1 + d(p, q)), & \text{de lo contrario}
\end{cases}
\tag{5}
$$
donde $d(p, q)$ es la distancia entre los picos de densidad local $p$ y $q$, $\rho(o)$ es la densidad local del punto $o$ y $maxd$ es el valor máximo de la distancia entre todos los pares de picos de densidad local.

Debido a que los picos de densidad local no están distribuidos uniformemente en el conjunto de datos, la distancia euclidiana no es adecuada para medir la disimilitud entre picos de densidad local. La distancia basada en vecinos compartidos aprovecha la información de vecindad entre picos de densidad local para acortar la distancia entre picos de densidad local que están estrechamente conectados por regiones densas y amplificar la distancia entre picos de densidad local que están separados por regiones dispersas. Representa la disimilitud entre picos de densidad local de una manera más adecuada. La Tabla I y la Tabla II dan la distancia euclidiana y la SD entre los picos de densidad local en la Fig. 3, respectivamente. La SD entre L1 y L2, y entre L3 y L4 se acorta mientras que las distancias entre otros pares se amplían en comparación con la distancia euclidiana, de modo que las distancias SD entre L1 y L2, y entre L3 y L4 son mucho menores que las de otros pares.


Tomemos como ejemplo el conjunto de datos mostrado en la Fig. 4: la Fig. 4(a) muestra los picos de densidad local y sus miembros, la Fig. 4(b) muestra el MST de los picos de densidad local construido con distancia euclidiana mientras que la Fig. 4(c) muestra el construido con distancia basada en vecinos compartidos. Los picos de densidad local $p$ y $q$ están en el mismo clúster mientras que $q$ y $o$ están en clústeres diferentes, pero la distancia euclidiana entre $p$ y $q$ es mayor que la entre $q$ y $o$, por lo que el MST construido con distancia euclidiana comete errores. Sin embargo, el MST construido con distancia basada en vecinos compartidos conserva correctamente la estructura del conjunto de datos original.

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Analisis y Diseño de Algoritmos\paper\tabla1.png" alt="">
    <figcaption>.</figcaption>
    </figure>
</div>


## D. Clustering basado en picos de densidad local y MST (LDP-MST)

En esta sección, utilizamos los picos de densidad local y la distancia basada en vecinos compartidos para construir el MST. Luego, cortamos repetidamente la arista más larga (la longitud de la arista se refiere a la distancia SD en lugar de la distancia euclidiana) solo cuando los tamaños de ambos clústeres resultantes al cortar esa arista son mayores que un número mínimo de puntos estimado aproximadamente (MinSize), hasta encontrar un número dado de clústeres. Después de agrupar los picos de densidad local, cada punto restante se asigna al mismo clúster al que pertenece el pico de densidad local correspondiente. El algoritmo LDP-MST se detalla en el Algoritmo 3. El MinSize en la condición final del bucle while interno en el Algoritmo 3 se calcula mediante el producto de una proporción y el tamaño de un conjunto de datos. La proporción para calcular MinSize se establece en 0.018 para el Algoritmo 3, lo que se explicará en la Sección V.E. El algoritmo LDP-MST contiene principalmente los siguientes pasos: 
(a) buscar picos de densidad local; 
(b) calcular la distancia basada en vecinos compartidos entre picos de densidad local; 
(c) emplear el algoritmo de clustering basado en MST para agrupar los picos de densidad local. 
El primer paso incluye la búsqueda NaN, el cálculo de la densidad de cada punto y la búsqueda de picos de densidad local. La complejidad temporal de la búsqueda NaN es $O(n^2)$ (donde $n$ es el número de puntos en un conjunto de datos). Al introducir el KD-tree, se puede reducir a $O(n\log n)$. La complejidad temporal del cálculo de la densidad y la búsqueda de picos de densidad local es $O(n)$. Por lo tanto, la complejidad temporal del primer paso es $O(n\log n)$. Suponiendo que el número de picos de densidad local es $n_{ldp}$ ($n_{ldp} \ll n$), la complejidad temporal del segundo paso es $O(n + n_{ldp}^2)$. La complejidad temporal del tercer paso es $O(n_{ldp}^2)$. Por lo tanto, la complejidad temporal general del algoritmo LDP-MST es $O(n\log n)$.


# V. ANÁLISIS EXPERIMENTAL

Para evaluar el rendimiento del algoritmo LDP-MST, primero realizamos experimentos en conjuntos de datos sintéticos bidimensionales que contienen clústeres con varias formas, conjuntos de datos reales del repositorio de aprendizaje automático de UCI y de la base de datos de caras Olivetti. Comparamos nuestro método con Kmeans [1], DBSCAN [6], DP [4], Dcore [5] y LOF-MST [16], y la complejidad temporal de estos algoritmos se enumera en la Tabla III. Posteriormente, se compara específicamente el tiempo de ejecución de cada método y se discuten los impactos de la proporción para calcular $MinSize$.

Utilizamos dos criterios externos [42], precisión de clustering (ACC) e información mutua normalizada (NMI), para evaluar la calidad de los resultados del clustering. ACC se calcula de la siguiente manera:
$$
ACC = \frac{1}{n} \sum_{i=1}^{n} \delta(y_i, map(c_i)) \tag{6}
$$
donde $y_i$ es la etiqueta de clúster real, $c_i$ es el número de serie obtenido por clustering, y
$$\delta(x, y) = 
\begin{cases}
1 & x = y \\
0 & x \neq y 
\end{cases}$$
es una función discriminante. Cuanto mayor sea el valor de $ACC$ $(ACC \in [0, 1])$, mejor es el rendimiento de clustering del algoritmo.

NMI se calcula de la siguiente manera:
$$
NMI = \frac{\sum_{i=1}^{k} \sum_{j=1}^{k} n_{i,j} \log \left(\frac{n \cdot n_{i,j}}{n_i \cdot n_j}\right)}{\sqrt{\left(\sum_{i} n_i \log \frac{n_i}{n}\right)\left(\sum_{j} n_j \log \frac{n_j}{n}\right)}} \tag{7}
$$
donde $n$ es el número de instancias en un conjunto de datos, $n_i$ y $n_j$ denotan el número de instancias en la categoría $i$ y el clúster $j$, respectivamente, y $n_{i,j}$ denota el número de instancias en la categoría $i$ así como en el clúster $j$. Un valor mayor de $NMI$ indica un mejor resultado de clustering.

Los experimentos se llevan a cabo en una PC con Intel Core i7 3.6GHz, 16GB de RAM, Windows 10 y MATLAB R2013a.

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Analisis y Diseño de Algoritmos\paper\figura3.png" alt="">
    <figcaption>Fig. 3. The neighbors and shared neighbors of LDPs. (a) NLDP. (b) The yellow points and shared neighbors between local density peaks.</figcaption>
    </figure>
</div>

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Analisis y Diseño de Algoritmos\paper\figura4.png" alt="">
    <figcaption>Fig. 4. The difference between Euclidean distance and shared neighbors-based distance. (a) The local density peaks and their members. (b) The MST
constructed with Euclidean distance. (c) The MST constructed with shared neighbors-based distance.</figcaption>
    </figure>
</div>

## A. Clustering en conjuntos de datos sintéticos

Demostramos la efectividad del algoritmo LDP-MST realizando experimentos en 6 conjuntos de datos sintéticos bidimensionales complejos, ilustrados en la Fig. 5. Utilizamos exclusivamente conjuntos de datos bidimensionales debido a su conveniencia visual para la ilustración del rendimiento. La información detallada de los conjuntos de datos sintéticos se enumera en la Tabla IV.

Para Kmeans, el número deseado de clústeres (NC) se establece en el número real de clústeres y los centros de clúster iniciales se seleccionan aleatoriamente. El rendimiento de DBSCAN depende de dos parámetros: el radio Eps y el número mínimo de puntos MinPts. Para obtener los mejores resultados, debemos ejecutarlo constantemente con diferentes parámetros. La distancia de corte dc de DP se establece en el 2% de la distancia más corta, como se sugiere en [4], de modo que el número promedio de vecinos sea aproximadamente del 1 al 2% del número total de puntos en un conjunto de datos. Los parámetros de Dcore incluyen: radio esférico r1 y r2, umbral de densidad t1 y t2, y radio de escaneo r. Ejecutamos continuamente Dcore con diferentes parámetros para obtener el mejor resultado de clustering para cada conjunto de datos. Para el algoritmo LOF-MST [16], introducimos KD-tree para encontrar los vecinos más cercanos. Para evitar establecer demasiados parámetros, para el MST que consta solo de puntos de datos centrales, siempre cortamos las aristas más grandes hasta encontrar un número dado de clústeres. Además, el algoritmo LOF-MST debe establecer los parámetros k y el umbral del valor LOF para eliminar puntos de ruido. Según [16], k se establece en 30. El umbral del valor LOF se establece en el máximo valor %-ésimo de LOF (0 ≤ % ≤ 30). También ajustamos % varias veces para obtener los mejores resultados de clustering. Para el algoritmo LDP-MST propuesto, para evitar establecer el parámetro k, utilizamos el valor característico natural λ en su lugar, por lo que solo necesitamos dar el número deseado de clústeres NC, que se establece en el número real de clústeres de cada conjunto de datos. Los mejores resultados de clustering de los 6 conjuntos de datos se muestran en las Figs. 1-6 del material suplementario y los parámetros correspondientes se muestran en la Tabla V. Las puntuaciones de ACC y NMI se muestran en la Tabla VI y el tiempo de ejecución se muestra en la Tabla VII.

![[algoritmo3.png]]

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Analisis y Diseño de Algoritmos\paper\tabla3.png" alt="">
    <figcaption></figcaption>
    </figure>
</div>


<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Analisis y Diseño de Algoritmos\paper\tabla4.png" alt="">
    <figcaption></figcaption>
    </figure>
</div>

La Figura 1 del material suplementario muestra los resultados de clustering de estos algoritmos en el Conjunto de Datos 1. Revela que Kmeans y DBSCAN no logran descubrir los clústeres correctos. Kmeans no puede descubrir clústeres esféricos con distribución sesgada y DBSCAN tiende a reconocer algunos clústeres conectados como un solo clúster. LOF-MST separa clústeres eliminando puntos de ruido, pero algunos puntos normales se reconocen como puntos de ruido. Los algoritmos DP, Dcore y LDP-MST funcionan bien en el Conjunto de Datos 1. Las puntuaciones de ACC y NMI de DP, Dcore y LDP-MST en la Tabla VI son todas superiores a 0.98, lo que indica que casi todos los puntos en el Conjunto de Datos 1 están correctamente agrupados.

Los resultados de clustering en el Conjunto de Datos 2 y el Conjunto de Datos 3, mostrados en la Figura 2 y la Figura 3 del material suplementario, indican que los algoritmos LDP-MST, DBSCAN y LOF-MST son buenos para descubrir clústeres de variedades. Los algoritmos DBSCAN y LOF-MST reconocen puntos en regiones dispersas como puntos de ruido. Sin embargo, como se muestra en la Figura 3(e) del material suplementario, LOF-MST reconoce algunos puntos normales en los clústeres como puntos de ruido. Kmeans siempre asigna puntos al centro de clúster más cercano, por lo que no puede descubrir clústeres de variedades. DP asume que los centros de clúster están rodeados por vecinos con densidad local más baja y que están a una distancia relativamente grande de cualquier punto con una densidad local más alta, pero esto no se aplica a los clústeres de variedades. El resultado de Dcore se ve afectado por los parámetros. Como se muestra en la Figura 2(d) y la Figura 3(d) del material suplementario, es difícil encontrar parámetros adecuados para clústeres con diferentes densidades.

La Figura 4 del material suplementario muestra los resultados de clustering en el Conjunto de Datos 4. Los algoritmos Kmeans y DP no logran agrupar los clústeres de variedades complejas. DBSCAN considera erróneamente algunos puntos de ruido como pequeños clústeres y dos clústeres en el medio se reconocen como un solo clúster. Para el algoritmo LOF-MST, aunque eliminamos el 20% de los puntos de ruido, todavía hay varios pequeños clústeres de valores atípicos. Debido a los clústeres de valores atípicos, tres clústeres en el medio no están separados. Cuando se dan los parámetros adecuados, Dcore descubre correctamente los clústeres en el Conjunto de Datos 4, pero hay varios puntos normales que se agrupan incorrectamente. El algoritmo LDP-MST obtiene el número correcto de clústeres y agrupa correctamente todos los puntos normales.

Los Conjuntos de Datos 5 y 6 contienen clústeres con estructuras complejas, formas arbitrarias y densidades diferentes. Los resultados de clustering en los Conjuntos de Datos 5 y 6, mostrados en las Figuras 5 y 6 del material suplementario, indican que solo LDP-MST obtiene el resultado de clustering correcto. Los resultados de los algoritmos Kmeans y DP no son deseables. Debido a la variación de densidad de los clústeres en los Conjuntos de Datos 5 y 6, DBSCAN no logra descubrir clústeres en estos conjuntos de datos. Para el Conjunto de Datos 5, aunque Dcore obtiene el número correcto de clústeres, hay muchos puntos normales que se clasifican incorrectamente. Para el Conjunto de Datos 6, Dcore tiene dificultad en descubrir clústeres con diferentes densidades, de modo que la mayoría de los clústeres se agrupan incorrectamente. LOF-MST elimina puntos de ruido de manera que el límite entre los clústeres es claro. Agrupa correctamente la mayoría de los puntos, pero muchos puntos normales en el límite de los clústeres también se reconocen como puntos de ruido.

Según la Tabla VI, las puntuaciones de ACC y NMI de LDP-MST son las más altas para los Conjuntos de Datos 2-6, lo que muestra su superioridad en el agrupamiento de conjuntos de datos con clústeres estructuralmente complejos y gran cantidad de puntos de ruido. La Tabla VII muestra que el tiempo de ejecución de LDP-MST es mucho menor que el de LOF-MST. A partir de los resultados y análisis anteriores, podemos ver que los algoritmos Kmeans y DP no pueden manejar conjuntos de datos de variedades complejas. Los algoritmos Dcore y DBSCAN son capaces de agrupar conjuntos de datos con formas arbitrarias, pero no pueden procesar clústeres con densidades variadas y sus resultados se ven fácilmente afectados por los parámetros. El algoritmo LOF-MST hace que el límite entre los clústeres sea claro eliminando puntos de ruido según el valor de LOF, de modo que puede descubrir clústeres complejos con diferentes densidades, pero algunos puntos normales también se reconocen como puntos de ruido. Basado en picos de densidad local y distancia basada en vecinos compartidos entre picos de densidad local, LDP-MST puede obtener resultados de agrupamiento satisfactorios para todos los conjuntos de datos, sin importar si los conjuntos de datos contienen clústeres de variedades complejas o si las variaciones de densidad de los clústeres son grandes.

![[tabla7.png]]

## B. Clustering en conjuntos de datos reales de UCI

También comparamos el algoritmo LDP-MST con Kmeans, DBSCAN, DP, Dcore y LOF-MST en varios conjuntos de datos de referencia de UCI. La Tabla VIII ilustra las características de los conjuntos de datos reales. Dado que las dimensiones de wine, control, segment, pendigits y letter son mayores de 10, KD-tree puede no encontrar los vecinos más cercanos para cada conjunto de datos. Primero utilizamos análisis de componentes principales (PCA) para reducir la dimensión de estos conjuntos de datos (PCA es un paso de preprocesamiento y su tiempo de ejecución no se considera aquí). La Tabla IX proporciona los parámetros de cada algoritmo en conjuntos de datos reales. Para el algoritmo LDP-MST, también utilizamos el valor característico natural para establecer $k$. La comparación de las puntuaciones de ACC y NMI se muestra en la Tabla X y el tiempo de ejecución de estos algoritmos se muestra en la Tabla XI.

Según la Tabla X, para iris y wine, la precisión de los algoritmos Kmeans y DP es superior a 0.85, pero sus puntuaciones de ACC y NMI no son altas para otros conjuntos de datos porque no pueden procesar conjuntos de datos complejos. DP y DBSCAN obtienen las puntuaciones más altas de NMI para control y segment, respectivamente. Sin embargo, sus puntuaciones de ACC no son más altas que las de LDP-MST. Los algoritmos DBSCAN y Dcore son capaces de descubrir clústeres con formas arbitrarias, pero su rendimiento puede verse fácilmente afectado por los parámetros, y es difícil encontrar parámetros adecuados para estos conjuntos de datos. El algoritmo LOF-MST es susceptible a los puntos de ruido. Por lo tanto, sus puntuaciones de ACC y NMI no son más altas que las de LDP-MST.

Las puntuaciones de ACC del algoritmo LDP-MST son todas más altas que las de otros algoritmos de clustering para los conjuntos de datos reales. Las puntuaciones de NMI de LDP-MST son cercanas a las puntuaciones más altas para control y segment y son las más altas para otros conjuntos de datos. Además, el tiempo de ejecución de LDP-MST es significativamente menor que el de LOF-MST. Para pendigits y letter, el tiempo de ejecución de LDP-MST es mucho menor que el de DBSCAN, DP, Dcore y LOF-MST. Basándonos en estos resultados, podemos concluir que los resultados de clustering de LDP-MST son mejores que los algoritmos comparados en términos de efectividad y eficiencia del clustering.


![[tabla8.png]]


![[tabla11.png]]

### C. Clustering en la Base de Datos de Caras Olivetti

Para demostrar aún más la efectividad del algoritmo LDP-MST, realizamos experimentos en la Base de Datos de Caras Olivetti [46]. Como un referente ampliamente utilizado para algoritmos de aprendizaje automático, el conjunto de datos contiene 400 imágenes de caras de 40 personas, tomadas en diferentes momentos y con variaciones en la iluminación, expresiones faciales y detalles faciales. El tamaño de cada imagen es de 92x112 píxeles. Seleccionamos las primeras 100 caras, es decir, 10 clústeres, para realizar el experimento. La distancia entre dos caras se calcula con la misma fórmula que en [33].

Los mejores resultados de clustering de los algoritmos Kmeans, DBSCAN, DP, Dcore, LOF-MST y LDP-MST se muestran en las Figuras 7-12 del material suplementario. En todos los resultados, las caras del mismo color pertenecen al mismo clúster. También consideramos ACC y NMI para evaluar los resultados del clustering. Los resultados de nuestros experimentos se muestran en la Tabla XII.


![[tabla5.png]]

![[tabla6.png]]

![[tabla9.png]]

![[tabla10.png]]



La Figura 7 del material suplementario muestra que Kmeans descubre 10 clústeres, pero muchas caras están clasificadas incorrectamente. Los parámetros de DBSCAN se establecen en Eps = 0.2 y MinPts = 2. La Figura 8 del material suplementario muestra que DBSCAN detecta 12 clústeres y 22 caras (incluyendo un clúster) sin colores son ruidos. La distancia de corte de DP se establece en dc = 0.07 y los parámetros de Dcore se establecen en r1 = 0.0335, r2 = 0.03, r = 0.04, t1 = 1, t2 = 0. Los resultados de DP y Dcore mostrados en la Figura 9 y la Figura 10 del material suplementario indican que DP y Dcore asignan muchas caras a clústeres incorrectos. Para LOF-MST, los parámetros son k = 10 y β = 0.06. La Figura 11 del material suplementario muestra que, aunque algunas caras se detectan como ruidos, LOF-MST todavía combina caras de diferentes clústeres en un solo clúster y divide caras del mismo clúster en diferentes clústeres. Por lo tanto, los resultados de clustering de estos algoritmos no son deseados. Para LDP-MST, k para buscar picos de densidad local se establece en 2 y NC se establece en 10. El resultado de LDP-MST mostrado en la Figura 12 del material suplementario indica que solo dos caras encerradas en cuadros rojos están asignadas a clústeres incorrectos. Las puntuaciones de ACC y NMI de LDP-MST en la Tabla XII son más altas que las de otros algoritmos. Esto indica que LDP-MST obtiene mejores resultados de clustering que otros algoritmos.

## D. Evaluación del tiempo de ejecución

Para explorar específicamente los impactos del número de instancias y dimensiones en el tiempo de ejecución de LDP-MST, realizamos experimentos en conjuntos de datos que se generan aleatoriamente mediante dos distribuciones gaussianas diferentes. Primero, generamos conjuntos de datos bidimensionales y aumentamos el número de instancias de 2000 a 30000, registrando el tiempo de ejecución correspondiente de los algoritmos. El resultado se muestra en la Fig. 6(a). El resultado indica que el tiempo de ejecución de LDP-MST es mayor que el de Kmeans y DBSCAN, pero mucho menor que el de LOF-MST. Cuando el número de instancias es menor de 23000, el tiempo de ejecución de LDP-MST es similar al de DP y Dcore, y cuando el número de instancias es mayor, el tiempo de ejecución de LDP-MST es menor que el de DP y Dcore.

Luego, generamos 5000 instancias y aumentamos el número de dimensiones de 5 a 100. El resultado se muestra en la Fig. 6(b). El resultado revela que el tiempo de ejecución de DBSCAN aumenta drásticamente cuando la dimensión es mayor de 30. Kmeans, DP, Dcore y LDP-MST son menos afectados por el aumento de dimensiones en comparación con DBSCAN y LOF-MST. En general, el tiempo de ejecución de LDP-MST aumenta con el número de instancias y dimensiones, pero el impacto del número de instancias y dimensiones en LDP-MST es menor que en LOF-MST, DP y DBSCAN. Además, LDP-MST funciona mucho mejor que otros algoritmos al descubrir clústeres con estructuras complejas.

## E. Discusión sobre la proporción para calcular MinSize

Para conjuntos de datos sin puntos de ruido o con pocos puntos de ruido, establecer o no establecer MinSize no tiene efecto en los resultados de clustering de LDP-MST, porque la definición de la distancia de vecinos compartidos entre los picos de densidad local hace que las aristas más largas sean una indicación confiable de la separación de clústeres. Los resultados en los Conjuntos de Datos 1 y 2 lo han demostrado. Sin embargo, cuando hay muchos puntos de ruido, los pequeños clústeres de ruido también pueden tener aristas más largas que los clústeres normales. Tomemos como ejemplo el Conjunto de Datos 3 con 7 clústeres. Cuando no establecemos MinSize, el resultado se muestra en la Fig. 7. Debido a la interferencia del pequeño clúster de ruido en el cuadro rojo, los dos clústeres en el cuadro negro se identifican como un solo clúster. Por lo tanto, es necesario establecer MinSize para evitar la obstrucción de los pequeños clústeres de ruido.

Teóricamente, el valor de MinSize debería ser mayor que el tamaño máximo de los clústeres de ruido y menor que el tamaño mínimo de los clústeres normales. El tamaño máximo de un clúster de ruido tiende a tener un pequeño porcentaje del conjunto de datos, aproximadamente menos del 1%. Para datos con una distribución sesgada, como el Conjunto de Datos 5 y el Conjunto de Datos 6, el clúster normal mínimo puede tener un pequeño porcentaje del conjunto de datos, aproximadamente mayor al 2%. Sin embargo, para conjuntos de datos que contienen clústeres de tamaños similares, el clúster normal mínimo tiende a tener un porcentaje mayor que el de una distribución sesgada.

Para explorar el impacto de MinSize, realizamos experimentos en dos conjuntos de datos sintéticos variando la proporción de 0.01 a 0.02, es decir, el Conjunto de Datos 3 y el Conjunto de Datos 5. Estos conjuntos de datos tienen una distribución sesgada y un gran número de puntos de ruido. Los resultados en el Conjunto de Datos 3 y el Conjunto de Datos 5 con diferentes proporciones se muestran en la Fig. 8 y la Fig. 9, respectivamente. A partir de los resultados, podemos aprender que cuando la proporción para calcular MinSize está en [0.01, 0.02], los resultados de LDP-MST son los mismos. Dado que la estimación del tamaño máximo del clúster de ruido puede ser pequeña, es mejor establecer un valor relativamente grande. Por lo tanto, sugerimos elegir un valor relativamente grande pero menor de 0.02 por seguridad, y seleccionamos 0.018 para calcular MinSize para LDP-MST.

# VI. CONCLUSIONES

Este artículo presenta un nuevo algoritmo de clustering llamado LDP-MST. Su idea principal es seleccionar picos de densidad local para construir el MST, evitando la interferencia de puntos de ruido y reduciendo el tiempo de ejecución de los algoritmos de clustering basados en MST. La distancia basada en vecinos compartidos ayuda a LDP-MST a descubrir clústeres de variedades complejas. En LDP-MST, primero calculamos la densidad según los resultados del algoritmo de búsqueda de vecinos naturales. Luego, encontramos los picos de densidad local y definimos la distancia basada en vecinos compartidos entre los picos de densidad local. Después de eso, construimos el MST sobre los picos de densidad local en base a la distancia propuesta. Obtenemos los clústeres finales eliminando las aristas más largas. Los experimentos en conjuntos de datos sintéticos y conjuntos de datos reales demuestran que LDP-MST puede reconocer patrones complejos en los conjuntos de datos y es más efectivo que los algoritmos de clustering existentes.