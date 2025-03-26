
---

En los capítulos 3 y 4, consideramos modelos para regresión y clasificación que comprenden combinaciones lineales de funciones base fijas. Vimos que tales modelos tienen propiedades analíticas y computacionales útiles, pero su aplicabilidad práctica está limitada por la maldición de la dimensionalidad. Para aplicar tales modelos a problemas a gran escala, es necesario adaptar las funciones base a los datos.

Las máquinas de vectores de soporte (SVM), discutidas en el capítulo 7, abordan esto primero definiendo funciones base centradas en los puntos de datos de entrenamiento y luego seleccionando un subconjunto de estas durante el entrenamiento. Una ventaja de las SVM es que, aunque el entrenamiento implica una optimización no lineal, la función objetivo es convexa, por lo que la solución del problema de optimización es relativamente sencilla. El número de funciones base en los modelos resultantes es generalmente mucho menor que el número de puntos de entrenamiento, aunque a menudo sigue siendo relativamente grande y típicamente aumenta con el tamaño del conjunto de entrenamiento. La máquina de vectores relevantes, discutida en la sección 7.2, también elige un subconjunto de un conjunto fijo de funciones base y típicamente resulta en modelos mucho más dispersos. A diferencia de las SVM, también produce salidas probabilísticas, aunque esto es a expensas de una optimización no convexa durante el entrenamiento.

Un enfoque alternativo es fijar el número de funciones base de antemano pero permitir que sean adaptativas, en otras palabras, usar formas paramétricas para las funciones base en las cuales los valores de los parámetros se adaptan durante el entrenamiento. El modelo más exitoso de este tipo en el contexto del reconocimiento de patrones es la red neuronal de propagación hacia adelante, también conocida como el perceptrón multicapa, discutida en este capítulo. De hecho, "perceptrón multicapa" es realmente un nombre inapropiado, porque el modelo comprende múltiples capas de modelos de regresión logística (con no linealidades continuas) en lugar de múltiples perceptrones (con no linealidades discontinuas). Para muchas aplicaciones, el modelo resultante puede ser significativamente más compacto y, por lo tanto, más rápido de evaluar que una máquina de vectores de soporte con el mismo rendimiento de generalización. El precio a pagar por esta compacidad, al igual que con la máquina de vectores relevantes, es que la función de verosimilitud, que forma la base para el entrenamiento de la red, ya no es una función convexa de los parámetros del modelo. En la práctica, sin embargo, a menudo vale la pena invertir recursos computacionales sustanciales durante la fase de entrenamiento para obtener un modelo compacto que sea rápido en el procesamiento de nuevos datos.

Nuestro enfoque en este capítulo es en las redes neuronales como modelos eficientes para el reconocimiento estadístico de patrones. En particular, restringiremos nuestra atención a la clase específica de redes neuronales que han demostrado ser de mayor valor práctico, a saber, el perceptrón multicapa.

Comenzamos considerando la forma funcional del modelo de red, incluyendo la parametrización específica de las funciones base, y luego discutimos el problema de determinar los parámetros de la red dentro de un marco de máxima verosimilitud, lo cual implica la solución de un problema de optimización no lineal. Esto requiere la evaluación de derivadas de la función de log-verosimilitud con respecto a los parámetros de la red, y veremos cómo se pueden obtener eficientemente utilizando la técnica de retropropagación del error. También mostraremos cómo el marco de retropropagación se puede extender para permitir que se evalúen otras derivadas, como las matrices Jacobiana y Hessiana. A continuación, discutimos varios enfoques para la regularización del entrenamiento de redes neuronales y las relaciones entre ellos. También consideramos algunas extensiones al modelo de red neuronal, y en particular describimos un marco general para modelar distribuciones de probabilidad condicionales conocidas como redes de densidad de mezcla. Finalmente, discutimos el uso de tratamientos bayesianos de redes neuronales. Se puede encontrar información adicional sobre modelos de redes neuronales en Bishop (1995a).

---

# 5.1. Funciones de Red de Propagación Directa

Los modelos lineales para regresión y clasificación discutidos en los Capítulos 3 y 4, respectivamente, se basan en combinaciones lineales de funciones base no lineales fijas $\phi_j(x)$ y toman la forma

$$
y(\mathbf{x}, \mathbf{w}) = f\left(\sum_{j=1}^{M} w_j \phi_j(x)\right) \tag{5.1}
$$

^3556e5

donde $f(\cdot)$ es una función de activación no lineal en el caso de clasificación y es la identidad en el caso de regresión. Nuestro objetivo es extender este modelo haciendo que las funciones base $\phi_j(x)$ dependan de parámetros y permitir que estos parámetros se ajusten, junto con los coeficientes $\{w_j\}$, durante el entrenamiento. Existen muchas maneras de construir funciones base no lineales paramétricas. Las redes neuronales usan funciones base que siguen la misma forma que (5.1), de modo que cada función base es en sí misma una función no lineal de una combinación lineal de las entradas, donde los coeficientes en la combinación lineal son parámetros adaptativos.

Esto conduce al modelo básico de red neuronal, que puede describirse como una serie de transformaciones funcionales. Primero construimos $M$ combinaciones lineales de las variables de entrada $x_1, \ldots, x_D$ en la forma

$$
a_j = \sum_{i=1}^{D} w_{ji}^{(1)} x_i + w_{j0}^{(1)} \tag{5.2}
$$

^4358e4

donde $j = 1, \ldots, M$, y el superíndice $(1)$ indica que los parámetros correspondientes están en la primera "capa" de la red. Nos referimos a los parámetros $w_{ji}^{(1)}$ como pesos y a los parámetros $w_{j0}^{(1)}$ como sesgos. Las cantidades $a_j$ se conocen como activaciones. Cada una de ellas se transforma usando una función de activación no lineal diferenciable $h(\cdot)$ para dar

$$
z_j = h(a_j). \tag{5.3}
$$

Estas cantidades corresponden a las salidas de las funciones base en [[Neural Network#^3556e5|(5.1)]] que, en el contexto de las redes neuronales, se llaman *unidades ocultas* (*hidden units*). Las funciones no lineales $h(\cdot)$ generalmente se eligen como funciones sigmoides tales como la sigmoide logística o la función 'tanh'. Siguiendo [[Neural Network#^3556e5|(5.1)]], estos valores se combinan nuevamente linealmente para dar las activaciones de las unidades de salida (*output unit activations*)

$$
a_k = \sum_{j=1}^{M} w_{kj}^{(2)} z_j + w_{k0}^{(2)} \tag{5.4}
$$

^87098d

donde $k = 1, \ldots, K$, y $K$ es el número total de salidas. Esta transformación corresponde a la segunda capa de la red, y nuevamente los $w_{k0}^{(2)}$ son parámetros de sesgo. Finalmente, las activaciones de las unidades de salida se transforman usando una función de activación apropiada para dar un conjunto de salidas de red $y_k$. La elección de la función de activación está determinada por la naturaleza de los datos y la distribución asumida de las variables objetivo y sigue las mismas consideraciones que para los modelos lineales discutidos en los Capítulos 3 y 4. Por lo tanto, para problemas de regresión estándar, la función de activación es la identidad, de modo que $y_k = a_k$. De manera similar, para problemas de clasificación binaria múltiple, cada activación de la unidad de salida se transforma usando una función sigmoide logística de modo que

$$
y_k = \sigma(a_k) \tag{5.5}
$$

donde

$$
\sigma(a) = \frac{1}{1 + \exp(-a)}. \tag{5.6}
$$

Finalmente, para problemas de clasificación multiclase, se usa una función de activación softmax de la forma [[Probabilistic Discriminative Models#^3efc00|(4.62)]] . La elección de la función de activación de la unidad de salida se discute en detalle en la Sección 5.2.

Podemos combinar estas diversas etapas para dar la función general de la red que, para funciones de activación de salida sigmoides, toma la forma

$$
y_k(\mathbf{x}, \mathbf{w}) = \sigma \left( \sum_{j=1}^{M} w_{kj}^{(2)} h \left( \sum_{i=1}^{D} w_{ji}^{(1)} x_i + w_{j0}^{(1)} \right) + w_{k0}^{(2)} \right) \tag{5.7}
$$

^44dd50

donde el conjunto de todos los parámetros de peso y sesgo se han agrupado en un vector $\mathbf{w}$. Así, el modelo de red neuronal es simplemente una función no lineal de un conjunto de variables de entrada $\{x_i\}$ a un conjunto de variables de salida $\{y_k\}$ controladas por un vector $\mathbf{w}$ de parámetros ajustables.




![[figure 5.1.png]]



Esta función puede representarse en la forma de un diagrama de red como se muestra en la   [[figure 5.1.png|Figura 5.1]]  El proceso de evaluación de [[Neural Network#^44dd50|(5.7)]]  puede interpretarse entonces como una *forward propagation* de información a través de la red. Debe enfatizarse que estos diagramas no representan modelos gráficos probabilísticos del tipo que se considerará en el Capítulo 8 porque los nodos internos representan variables deterministas en lugar de estocásticas. Por esta razón, hemos adoptado una notación gráfica ligeramente diferente para los dos tipos de modelo. Más adelante veremos cómo dar una interpretación probabilística a una red neuronal.

Como se discutió en la Sección 3.1, los parámetros de sesgo en [[Neural Network#^4358e4|(5.2)]] pueden absorberse en el conjunto de parámetros de peso definiendo una variable de entrada adicional $x_0$ cuyo valor se fija en $x_0 = 1$, de modo que [[Neural Network#^4358e4|(5.2)]] toma la forma

$$
a_j = \sum_{i=0}^{D} w_{ji}^{(1)} x_i. \tag{5.8}
$$

De manera similar, podemos absorber los sesgos de la segunda capa en los pesos de la segunda capa, de modo que la función general de la red se convierte en

$$
y_k(\mathbf{x}, \mathbf{w}) = \sigma \left( \sum_{j=0}^{M} w_{kj}^{(2)} h \left( \sum_{i=0}^{D} w_{ji}^{(1)} x_i \right) \right). \tag{5.9}
$$

Como se puede ver en la [[figure 5.1.png|Figura 5.1]], el modelo de red neuronal consta de dos etapas de procesamiento, cada una de las cuales se asemeja al modelo de perceptrón de la Sección 4.1.7, y por esta razón la red neuronal también se conoce como perceptrón multicapa o MLP. Una diferencia clave en comparación con el perceptrón es que la red neuronal utiliza no linealidades sigmoides continuas en las unidades ocultas, mientras que el perceptrón utiliza no linealidades de función escalonada. Esto significa que la función de la red neuronal es diferenciable con respecto a los parámetros de la red, y esta propiedad jugará un papel central en el entrenamiento de la red.

Si las funciones de activación de todas las unidades ocultas en una red son lineales, entonces para cualquier red de este tipo siempre podemos encontrar una red equivalente sin unidades ocultas. Esto se debe al hecho de que la composición de transformaciones lineales sucesivas es, en sí misma, una transformación lineal. Sin embargo, si el número de unidades ocultas es menor que el número de unidades de entrada o salida, entonces las transformaciones que la red puede generar no son las transformaciones lineales más generales posibles de entradas a salidas porque se pierde información en la reducción de dimensionalidad en las unidades ocultas. En la Sección 12.4.2, mostramos que las redes de unidades lineales dan lugar al análisis de componentes principales. Sin embargo, en general, hay poco interés en las redes multicapa de unidades lineales. 

La arquitectura de red mostrada en la [[figure 5.1.png|Figura 5.1]] es la más comúnmente utilizada en la práctica. Sin embargo, es fácilmente generalizable, por ejemplo, considerando capas adicionales de procesamiento, cada una consistente en una combinación lineal ponderada de la forma [[Neural Network#^87098d|(5.4)]], seguida de una transformación elemento a elemento utilizando una función de activación no lineal. 

Otra generalización de la arquitectura de la red es incluir conexiones de capa de salto, cada una de las cuales está asociada con un parámetro adaptativo correspondiente. Por ejemplo, en una red de dos capas, estas conexiones irían directamente de las entradas a las salidas. En principio, una red con unidades ocultas sigmoides siempre puede imitar conexiones de capa de salto (para valores de entrada acotados) utilizando un peso de primera capa lo suficientemente pequeño que, dentro de su rango operativo, la unidad oculta es efectivamente lineal, y luego compensar con un valor de peso grande de la unidad oculta a la salida. En la práctica, sin embargo, puede ser ventajoso incluir explícitamente conexiones de capa de salto.

Además, la red puede ser dispersa, con no todas las conexiones posibles dentro de una capa presentes. Veremos un ejemplo de una arquitectura de red dispersa cuando consideremos las redes neuronales convolucionales en la Sección 5.5.6.

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Pattern Recognition and Machine Learning\imgs\figure 5.2.png">
    <figcaption></figcaption>
    </figure>
</div>

Dado que existe una correspondencia directa entre un diagrama de red y su función matemática, podemos desarrollar mapeos de red más generales considerando diagramas de red más complejos. Sin embargo, estos deben restringirse a una arquitectura de red de avance (feed-forward), es decir, a una que no tenga ciclos dirigidos cerrados, para asegurar que las salidas sean funciones deterministas de las entradas. Esto se ilustra con un ejemplo simple en la [[figure 5.2.png|Figura 5.2.]] Cada unidad (oculta o de salida) en dicha red computa una función dada por 

$$
z_k = h \ \left( \sum_j w_{kj} \ z_j \right) \tag{5.10}
$$

^150108

donde la suma se realiza sobre todas las unidades que envían conexiones a la unidad \(k\) (y un parámetro de sesgo se incluye en la suma). Para un conjunto dado de valores aplicados a las entradas de la red, la aplicación sucesiva de [[#^150108|(5.10)]] permite evaluar las activaciones de todas las unidades en la red, incluyendo las de las unidades de salida.

Las propiedades de aproximación de las redes de avance han sido ampliamente estudiadas (Funahashi, 1989; Cybenko, 1989; Hornik et al., 1989; Stinchecombe y White, 1989; Cotter, 1990; Ito, 1991; Hornik, 1991; Kreinovich, 1991; Ripley, 1996) y se ha encontrado que son muy generales. Por lo tanto, se dice que las redes neuronales son aproximadores universales. Por ejemplo, una red de dos capas con salidas lineales puede aproximar uniformemente cualquier función continua en un dominio de entrada compacto con una precisión arbitraria, siempre que la red tenga un número suficientemente grande de unidades ocultas. Este resultado se mantiene para una amplia gama de funciones de activación de unidades ocultas, pero excluyendo polinomios. Aunque tales teoremas son tranquilizadores, el problema clave es cómo encontrar valores de parámetros adecuados dado un conjunto de datos de entrenamiento, y en secciones posteriores de este capítulo mostraremos que existen soluciones efectivas a este problema basadas tanto en enfoques de máxima verosimilitud como en enfoques bayesianos.

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Pattern Recognition and Machine Learning\imgs\figure 5.3.png">
    <figcaption></figcaption>
    </figure>
</div>

La capacidad de una red de dos capas para modelar una amplia gama de funciones se ilustra en la Figura 5.3. Esta figura también muestra cómo las unidades ocultas individuales trabajan colaborativamente para aproximar la función final. El papel de las unidades ocultas en un problema de clasificación simple se ilustra en la Figura 5.4 utilizando el conjunto de datos de clasificación sintética descrito en el Apéndice A.

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Pattern Recognition and Machine Learning\imgs\figure 5.4.png">
    <figcaption></figcaption>
    </figure>
</div>


## 5.1.1 Simetrías en el espacio de pesos

Una propiedad de las redes de propagación hacia adelante, que jugará un papel cuando consideremos la comparación de modelos bayesianos, es que múltiples elecciones distintas para el vector de pesos $\mathbf{w}$ pueden dar lugar a la misma función de mapeo desde entradas a salidas (Chen et al., 1993). Consideremos una red de dos capas de la forma mostrada en la [[figure 5.1.png|Figura 5.1]] con $M$ unidades ocultas que tienen funciones de activación ‘tanh’ y conectividad completa en ambas capas. Si cambiamos el signo de todos los pesos y el sesgo que alimenta a una unidad oculta particular, entonces, para un patrón de entrada dado, el signo de la activación de la unidad oculta se invertirá, porque ‘tanh’ es una función impar, de modo que $\tanh(-a) = -\tanh(a)$. Esta transformación puede compensarse exactamente cambiando el signo de todos los pesos que salen de esa unidad oculta. Por lo tanto, al cambiar los signos de un grupo particular de pesos (y un sesgo), la función de mapeo entrada-salida representada por la red permanece sin cambios, y así hemos encontrado dos vectores de peso diferentes que dan lugar a la misma función de mapeo. Para $M$ unidades ocultas, habrá $M$ tales simetrías de ‘cambio de signo’, y así cualquier vector de peso dado será uno de un conjunto de $2^M$ vectores de peso equivalentes.

De manera similar, imaginemos que intercambiamos los valores de todos los pesos (y el sesgo) que conducen tanto hacia dentro como hacia fuera de una unidad oculta particular con los valores de los pesos (y el sesgo) asociados con una unidad oculta diferente. De nuevo, esto claramente deja la función de mapeo entrada-salida de la red sin cambios, pero corresponde a una elección diferente del vector de peso. Para $M$ unidades ocultas, cualquier vector de peso dado pertenecerá a un conjunto de $M!$ vectores de peso equivalentes asociados con esta simetría de intercambio, correspondiente a los $M!$ diferentes ordenamientos de las unidades ocultas. Por lo tanto, la red tendrá un factor general de simetría en el espacio de pesos de $M!2^M$. Para redes con más de dos capas de pesos, el nivel total de simetría será dado por el producto de tales factores, uno para cada capa de unidades ocultas.

Resulta que estos factores representan todas las simetrías en el espacio de pesos (excepto por posibles simetrías accidentales debido a elecciones específicas de los valores de los pesos). Además, la existencia de estas simetrías no es una propiedad particular de la función ‘tanh’ sino que se aplica a una amplia gama de funciones de activación (Kůrková and Kainen, 1994). En muchos casos, estas simetrías en el espacio de pesos tienen poca consecuencia práctica, aunque en la Sección 5.7 encontraremos una situación en la que necesitaremos tenerlas en cuenta.

# 5.2. Entrenamiento de Redes
Hasta ahora, hemos visto las redes neuronales como una clase general de funciones no lineales paramétricas que van desde un vector $\mathbf{x}$ de variables de entrada a un vector $\mathbf{y}$ de variables de salida. Un enfoque simple para el problema de determinar los parámetros de la red es hacer una analogía con la discusión sobre el ajuste de curvas polinomiales en la Sección 1.1 y, por lo tanto, minimizar una función de error de suma de cuadrados. Dado un conjunto de entrenamiento que comprende un conjunto de vectores de entrada $\{\mathbf{x}_n\}$, donde $n = 1, \ldots, N$, junto con un conjunto correspondiente de vectores objetivo $\{t_n\}$, minimizamos la función de error

$$
E(\mathbf{w}) = \frac{1}{2} \sum_{n=1}^{N} \|\mathbf{y}(\mathbf{x}_n, \mathbf{w}) - t_n\|^2. \tag{5.11}
$$

Sin embargo, podemos proporcionar una visión mucho más general del entrenamiento de redes dando primero una interpretación probabilística a las salidas de la red. 

Empezamos discutiendo problemas de regresión, y por el momento consideramos una sola variable objetivo $t$ que puede tomar cualquier valor real. Siguiendo las discusiones en las Secciones 1.2.5 y 3.1, asumimos que $t$ tiene una distribución gaussiana con una media dependiente de $\mathbf{x}$, que está dada por la salida de la red neuronal, de modo que

$$
p(t|\mathbf{x}, \mathbf{w}) = \mathcal{N} \left( t|y(\mathbf{x}, \mathbf{w}), \beta^{-1} \right) \tag{5.12}
$$

donde $\beta$ es la precisión (varianza inversa) del ruido gaussiano. Por supuesto, esta es una suposición algo restrictiva, y en la Sección 5.6 veremos cómo extender este enfoque para permitir distribuciones condicionales más generales. Para la distribución condicional dada por (5.12), es suficiente tomar la función de activación de la unidad de salida como la identidad, porque una red de este tipo puede aproximar cualquier función continua de $\mathbf{x}$ a $\mathbf{y}$. Dado un conjunto de datos de $N$ observaciones independientes y distribuidas idénticamente $\mathbf{X} = \{\mathbf{x}_1, \ldots, \mathbf{x}_N\}$, junto con valores objetivo correspondientes $\mathbf{t} = \{t_1, \ldots, t_N\}$, podemos construir la correspondiente función de verosimilitud

$$
p(\mathbf{t}|\mathbf{X}, \mathbf{w}, \beta) = \prod_{n=1}^{N} p(t_n|\mathbf{x}_n, \mathbf{w}, \beta).
$$

Tomando el logaritmo negativo, obtenemos la función de error

$$
\frac{\beta}{2} \sum_{n=1}^{N} \left\{ y(\mathbf{x}_n, \mathbf{w}) - t_n \right\}^2 - \frac{N}{2} \ln \beta + \frac{N}{2} \ln (2\pi) \tag{5.13}
$$
que se puede usar para aprender los parámetros $\mathbf{w}$ y $\beta$. En la Sección 5.7, discutiremos el tratamiento bayesiano de las redes neuronales, mientras que aquí consideramos un enfoque de máxima verosimilitud. Note que en la literatura de redes neuronales, es usual considerar la minimización de una función de error más bien que la maximización de la verosimilitud (o el log-verosimilitud), y así aquí seguiremos esta convención. Considere primero la determinación de $\mathbf{w}$. Maximizar la función de verosimilitud es equivalente a minimizar la función de error de suma de cuadrados dada por
$$
E(\mathbf{w}) = \frac{1}{2} \ \sum_{n=1}^N \{ y(x_n, \mathbf{w}) - t_n \}^2 \tag{5.14}
$$
donde hemos descartado constantes aditivas y multiplicativas. El valor de $\mathbf{w}$ encontrado al minimizar $E(\mathbf{w})$ será denotado $\mathbf{w}_{ML}$ porque corresponde a la solución de máxima verosimilitud. En la práctica, la no linealidad de la función de red $y(\mathbf{x}_n, \mathbf{w})$ causa que el error $E(\mathbf{w})$ no sea convexo, y así, en la práctica, se pueden encontrar máximos locales de la verosimilitud, correspondientes a mínimos locales de la función de error, como se discute en la Sección 5.2.1.

Habiendo encontrado $\mathbf{w}_{ML}$, el valor de $\beta$ se puede encontrar minimizando el logaritmo negativo de la verosimilitud para dar

$$
\frac{1}{\beta_{ML}} = \frac{1}{N} \sum_{n=1}^{N} \left\{ y(\mathbf{x}_n, \mathbf{w}_{ML}) - t_n \right\}^2. \tag{5.15}
$$

Note que esto se puede evaluar una vez que la optimización iterativa requerida para encontrar $\mathbf{w}_{ML}$ se haya completado. Si tenemos múltiples variables objetivo, y asumimos que son independientes condicionales a $\mathbf{x}$ y $\mathbf{w}$ con precisión de ruido compartida $\beta$, entonces la distribución condicional de los valores objetivo está dada por
$$
p(\mathbf{t}|\mathbf{x}, \mathbf{w}, \beta) = \mathcal{N} \left( t | y(\mathbf{x}, \mathbf{w}), \beta^{-1} \mathbf{I} \right). \tag{5.16}
$$
Siguiendo el mismo argumento que para una sola variable objetivo, vemos que los pesos de máxima verosimilitud se determinan minimizando la función de error de suma de cuadrados (5.11). La precisión del ruido está dada entonces por

$$
\frac{1}{\beta_{ML}} = \frac{1}{NK} \sum_{n=1}^{N} \|y(\mathbf{x}_n, \mathbf{w}_{ML}) - t_n\|^2 \tag{5.17}
$$

donde $K$ es el número de variables objetivo. La suposición de independencia se puede abandonar a expensas de un problema de optimización ligeramente más complejo.

Recuerde de la Sección 4.3.6 que hay una correspondencia natural de la función de error (dada por el logaritmo negativo de la verosimilitud) y la función de activación de la unidad de salida. En el caso de regresión, podemos ver la red como teniendo una función de activación de salida que es la identidad, de modo que $y_k = a_k$. La correspondiente función de error de suma de cuadrados tiene la propiedad

$$
\frac{\partial E}{\partial a_k} = y_k - t_k \tag{5.18}
$$

^1b5072

la cual utilizaremos al discutir la retropropagación de errores (*backpropagation error*)en la Sección 5.3.

Ahora consideremos el caso de la clasificación binaria en la que tenemos una sola variable objetivo $t$ tal que $t = 1$ denota la clase $C_1$ y $t = 0$ denota la clase $C_2$. Siguiendo la discusión de las funciones de enlace canónicas en la Sección 4.3.6, consideramos una red con una sola salida cuya función de activación es un sigmoide logístico

$$
y = \sigma(a) \equiv \frac{1}{1 + \exp(-a)} \tag{5.19}
$$

de modo que $0 \leq y(\mathbf{x}, \mathbf{w}) \leq 1$. Podemos interpretar $y(\mathbf{x}, \mathbf{w})$ como la probabilidad condicional $p(C_1|\mathbf{x})$, con $p(C_2|\mathbf{x})$ dada por $1 - y(\mathbf{x}, \mathbf{w})$. La distribución condicional de los objetivos dados los insumos es entonces una distribución Bernoulli de la forma

$$
p(t|\mathbf{x}, \mathbf{w}) = y(\mathbf{x}, \mathbf{w})^t \left\{ 1 - y(\mathbf{x}, \mathbf{w}) \right\}^{1-t}. \tag{5.20}
$$


Si consideramos un conjunto de entrenamiento de observaciones independientes, entonces la función de error, que está dada por el logaritmo negativo de la verosimilitud, es entonces una función de error de entropía cruzada de la forma
$$
E(\mathbf{w}) = - \sum_{n=1}^{N} \left\{ t_n \ln y_n + (1 - t_n) \ln (1 - y_n) \right\} \quad{5.21}
$$

donde $y_n$ denota $y(\mathbf{x}_n, \mathbf{w})$. Note que no hay un análogo de la precisión del ruido $\beta$ porque se asume que los valores objetivo están correctamente etiquetados. Sin embargo, el modelo se puede extender fácilmente para permitir errores de etiquetado. Simard et al. (2003) encontraron que al usar la función de error de entropía cruzada en lugar de la suma de cuadrados para un problema de clasificación conduce a un entrenamiento más rápido y a una mejor generalización.

Si tenemos $K$ clasificaciones binarias separadas para realizar, entonces podemos usar una red que tenga $K$ salidas, cada una de las cuales tiene una función de activación sigmoide logística. Asociado con cada salida hay una etiqueta de clase binaria $t_k \in \{0, 1\}$, donde $k = 1, \ldots, K$. Si asumimos que las etiquetas de clase son independientes, dado el vector de entrada, entonces la distribución condicional de los objetivos está dada por

$$
p(\mathbf{t}|\mathbf{x}, \mathbf{w}) = \prod_{k=1}^{K} y_k(\mathbf{x}, \mathbf{w})^{t_k} \left[ 1 - y_k(\mathbf{x}, \mathbf{w}) \right]^{1 - t_k}. \tag{5.22}
$$

Tomando el logaritmo negativo de la correspondiente función de verosimilitud obtenemos la siguiente función de error

$$
E(\mathbf{w}) = - \sum_{n=1}^{N} \sum_{k=1}^{K} \left\{ t_{nk} \ln y_{nk} + (1 - t_{nk}) \ln (1 - y_{nk}) \right\} \tag{5.23}
$$

donde $y_{nk}$ denota $y_k(\mathbf{x}_n, \mathbf{w})$. De nuevo, la derivada de la función de error con respecto a la activación para una unidad de salida particular toma la forma (5.18) como en el caso de regresión.

Es interesante contrastar la solución de la red neuronal a este problema con el enfoque correspondiente basado en un modelo de clasificación lineal del tipo discutido en el Capítulo 4. Supongamos que estamos usando una red estándar de dos capas del tipo mostrado en la  [[figure 5.1.png|Figura 5.1]]. Vemos que los parámetros de peso en la primera capa de la red son compartidos entre las diversas salidas, mientras que en el modelo lineal cada problema de clasificación se resuelve de forma independiente. La primera capa de la red se puede ver como realizando una extracción de características no lineal, y el compartir características entre las diferentes salidas puede ahorrar en la computación y también puede llevar a una mejor generalización.

Finalmente, consideramos el problema estándar de clasificación multiclase en el que cada entrada se asigna a una de $K$ clases mutuamente excluyentes. Las variables objetivo binarias $t_k \in \{0, 1\}$ tienen un esquema de codificación 1-de-K que indica la clase, y las salidas de la red se interpretan como $y_k(\mathbf{x}, \mathbf{w}) = p(t_k = 1|\mathbf{x})$, lo que lleva a la siguiente función de error

$$
E(\mathbf{w}) = - \sum_{n=1}^{N} \sum_{k=1}^{K} t_{nk} \ln y_k(\mathbf{x}_n, \mathbf{w}). \tag{5.24}
$$

Siguiendo la discusión de la Sección 4.3.4, vemos que la función de activación de la unidad de salida, que corresponde al enlace canónico, está dada por la función softmax

$$
y_k(\mathbf{x}, \mathbf{w}) = \frac{\exp(a_k(\mathbf{x}, \mathbf{w}))}{\sum_j \exp(a_j(\mathbf{x}, \mathbf{w}))} \quad (5.25)
$$

la cual satisface $0 \leq y_k \leq 1$ y $\sum_k y_k = 1$. Note que los $y_k(\mathbf{x}, \mathbf{w})$ no se modifican si se suma una constante a todos los $a_k(\mathbf{x}, \mathbf{w})$, causando que la función de error sea constante para algunas direcciones en el espacio de pesos. Esta degeneración se elimina si se añade un término de regularización apropiado (Sección 5.5) a la función de error

Una vez más, la derivada de la función de error con respecto a la activación para una unidad de salida particular toma la forma familiar [[#^1b5072|(5.18)]].  En resumen, hay una elección natural tanto de la función de activación de la unidad de salida como de la función de error correspondiente, según el tipo de problema que se esté resolviendo. Para la regresión, usamos salidas lineales y una función de error de suma de cuadrados; para clasificaciones binarias (múltiples independientes), usamos salidas con sigmoide logística y una función de error de entropía cruzada; y para clasificación multiclase, usamos salidas softmax con la correspondiente función de error de entropía cruzada multiclase. Para problemas de clasificación que involucran dos clases, podemos usar una única salida con sigmoide logística o, alternativamente, podemos usar una red con dos salidas que tenga una función de activación softmax.


## 5.2.1 Optimización de Parámetros

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Pattern Recognition and Machine Learning\imgs\figure 5.5.png">
    <figcaption></figcaption>
    </figure>
</div>

Pasamos ahora a la tarea de encontrar un vector de pesos $w$ que minimice la función de error elegida $E(\mathbf{w})$. En este punto, es útil tener una imagen geométrica de la función de error, la cual podemos ver como una superficie que se extiende sobre el espacio de pesos como se muestra en la Figura 5.5. Primero, observemos que si damos un pequeño paso en el espacio de pesos desde $w$ a $w + \delta w$, entonces el cambio en la función de error es $\delta E \approx \delta \mathbf{w}^T \nabla E(\mathbf{w})$, donde el vector $\nabla E(\mathbf{w})$ apunta en la dirección de mayor tasa de incremento de la función de error. Debido a que el error $E(\mathbf{w})$ es una función continua y suave de $\mathbf{w}$, su valor más pequeño ocurrirá en un punto en el espacio de pesos tal que el gradiente de la función de error se anule, de modo que

$$
\nabla E(\mathbf{w}) = 0 \tag{5.26}
$$

ya que de lo contrario podríamos dar un pequeño paso en la dirección de $-\nabla E(\mathbf{w})$ y así reducir aún más el error. Los puntos en los que el gradiente se anula se llaman puntos estacionarios, y pueden clasificarse además en mínimos, máximos y puntos silla.

Nuestro objetivo es encontrar un vector $\mathbf{w}$ tal que $E(\mathbf{w})$ tome su valor más pequeño. Sin embargo, la función de error generalmente tiene una dependencia altamente no lineal con respecto a los parámetros de pesos y sesgos, por lo que habrá muchos puntos en el espacio de pesos donde el gradiente se anule (o sea numéricamente muy pequeño). De hecho, a partir de la discusión en la Sección 5.1.1, vemos que para cualquier punto $\mathbf{w}$ que sea un mínimo local, habrá otros puntos en el espacio de pesos que sean mínimos equivalentes. Por ejemplo, en una red de dos capas del tipo mostrado en la [[figure 5.1.png|Figura 5.1]] , con $M$ unidades ocultas, cada punto en el espacio de pesos es miembro de una familia de $M! \cdot 2^M$ puntos equivalentes.


Además, típicamente habrá múltiples puntos estacionarios no equivalentes y, en particular, múltiples mínimos no equivalentes. Un mínimo que corresponde al valor más pequeño de la función de error para cualquier vector de pesos se dice que es un mínimo global. Cualquier otro mínimo que corresponda a valores más altos de la función de error se dice que es un mínimo local. Para una aplicación exitosa de redes neuronales, puede no ser necesario encontrar el mínimo global (y en general no se sabrá si se ha encontrado el mínimo global), pero puede ser necesario comparar varios mínimos locales para encontrar una solución suficientemente buena.

Dado que claramente no hay esperanza de encontrar una solución analítica a la ecuación $\nabla E(\mathbf{w}) = 0$, recurrimos a procedimientos numéricos iterativos. La optimización de funciones no lineales continuas es un problema ampliamente estudiado y existe una vasta literatura sobre cómo resolverlo de manera eficiente. La mayoría de las técnicas implican elegir algún valor inicial $\mathbf{w}^{(0)}$ para el vector de pesos y luego moverse a través del espacio de pesos en una sucesión de pasos de la forma

$$
\mathbf{w}^{(\tau+1)} = \mathbf{w}^{(\tau)} + \Delta \mathbf{w}^{(\tau)} \tag{5.27}
$$

^262913

donde $\tau$ etiqueta la iteración. Diferentes algoritmos involucran diferentes elecciones para el vector de actualización de pesos $\Delta \mathbf{w}^{(\tau)}$. Muchos algoritmos hacen uso de información de gradiente y, por lo tanto, requieren que, después de cada actualización, el valor de $\nabla E(\mathbf{w})$ sea evaluado en el nuevo vector de pesos $\mathbf{w}^{(\tau+1)}$. Para entender la importancia de la información de gradiente, es útil considerar una aproximación local de la función de error basada en una expansión de Taylor.

## 5.2.2 Aproximación Cuadrática Local

La comprensión del problema de optimización y de las diversas técnicas para resolverlo puede obtenerse considerando una aproximación cuadrática local a la función de error.

Consideremos la expansión de Taylor de $E(\mathbf{w})$ alrededor de algún punto $\hat{\mathbf{w}}$ en el espacio de pesos:

$$
E(\mathbf{w}) = E(\hat{\mathbf{w}}) + (\mathbf{w} - \hat{\mathbf{w}})^\top \mathbf{g} + \frac{1}{2} (\mathbf{w} - \hat{\mathbf{w}})^\top \mathbf{H} \ (\mathbf{w} - \hat{\mathbf{w}}) \tag{5.28}
$$

^0dfc2d

donde los términos cúbicos y de mayor orden han sido omitidos. Aquí $\mathbf{g}$ se define como el gradiente de $E$ evaluado en $\hat{\mathbf{w}}$:

$$
\mathbf{g} = \nabla E|_{\mathbf{w} = \hat{\mathbf{w}}} \tag{5.29}
$$

y la matriz Hessiana $\mathbf{H} = \nabla \nabla E$ tiene sus elementos

$$
(\mathbf{H})_{ij} = \frac{\partial^2 E}{\partial w_i \partial w_j} \bigg|_{\mathbf{w} = \hat{\mathbf{w}}}. \tag{5.30}
$$

De [[#^0dfc2d|(5.28)]], la correspondiente aproximación local al gradiente viene dada por

$$
\nabla E \approx \mathbf{g} + \mathbf{H} (\mathbf{w} - \hat{\mathbf{w}}). \tag{5.31}
$$

Para puntos $\mathbf{w}$ que están suficientemente cerca de $\hat{\mathbf{w}}$, estas expresiones darán aproximaciones razonables para el error y su gradiente.

Consideremos en particular el caso de una aproximación cuadrática local alrededor de un punto $\mathbf{w}^*$ que es un mínimo de la función de error. En este caso no hay términos lineales, porque $\nabla E = \mathbf{0}$, y  se convierte en

$$
E(\mathbf{w}) = E(\mathbf{w}^*) + \frac{1}{2} (\mathbf{w} - \mathbf{w}^*)^T \ \mathbf{H} (\mathbf{w} - \mathbf{w}^*) \tag{5.32}
$$

donde la Hessiana $\mathbf{H}$ se evalúa en $\mathbf{w}^*$. Para interpretar esto geométricamente, considera la ecuación de autovalores para la matriz Hessiana.
$$
\mathbf{H} \mathbf{u}_i = \lambda_i \mathbf{u}_i \tag{5.33}
$$

^6ed956


donde los valores propios $\lambda_i$ forman una matriz diagonal completa, tal que
$$
\mathbf{u}_i^T \mathbf{u}_j = \delta_{ij} \tag{5.34}
$$

^941301

Ahora expandimos  $(\mathbf{w} - \mathbf{w}^*)$ como una combinación lineal de los vectores propios en la forma
$$
\mathbf{w} - \mathbf{w}^* = \sum_i \alpha_i \ \mathbf{u}_i \tag{5.35}
$$
Esto puede considerarse como una transformación del sistema de coordenadas en la que el origen se traslada al punto $\mathbf{w}^*$, y los ejes se rotan para alinearse con los vectores propios (a través de la matriz ortogonal cuyas columnas son los $\mathbf{u}_i$, y se discute con más detalle en el Apéndice C. Sustituyendo (5.35) en (5.32), y usando (5.33) y (5.34), la función de error se puede escribir en la forma

$$
E(\mathbf{w}) = E(\mathbf{w}^*) + \frac{1}{2} \sum_i \alpha_i^2 \lambda_i^2. \tag{5.36}
$$

Una matriz $\mathbf{H}$ es positiva definida si, y solo si:

$$
\mathbf{v}^\top \mathbf{H} \mathbf{v} > 0 \quad \text{para todo} \quad \mathbf{v}. \tag{5.37}
$$

Debido a que los vectores propios $\{\mathbf{u}_i\}$ forman una base completa, un vector arbitrario $\mathbf{v}$ se puede escribir en la forma

$$
\mathbf{v} = \sum_i c_i \mathbf{u}_i. \tag{5.38}
$$

De [[#^6ed956|(5.33)]] y [[#^941301|(5.34)]] , entonces tenemos

$$
\mathbf{v}^\top \mathbf{H} \mathbf{v} = \sum_i c_i^2 \lambda_i. \tag{5.39}
$$

Así, $\mathbf{H}$ será positiva definida si, y solo si, todos sus valores propios son positivos. En el nuevo sistema de coordenadas, cuyos vectores base son los vectores propios de $\mathbf{H}$, la región elíptica centrada en $\mathbf{w}^*$ ilustrada en la [[figure 5.6.png|Figura 5.6.]] Para un espacio de pesos unidimensional, un punto estacionario $\mathbf{w}^*$ será un mínimo si

$$
\frac{\partial^2 E}{\partial w^2} > 0. \tag{5.40}
$$

El resultado correspondiente en $D$ dimensiones es que la matriz Hessiana, evaluada en $\mathbf{w}^*$, debe ser positiva definida.


<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Pattern Recognition and Machine Learning\imgs\figure 5.6.png">
    <figcaption></figcaption>
    </figure>
</div>

## 5.2.3 Uso de la Información del Gradiente

Como veremos en la Sección 5.3, es posible evaluar el gradiente de una función de error eficientemente mediante el procedimiento de retropropagación. El uso de esta información del gradiente puede llevar a mejoras significativas en la velocidad con la que se pueden localizar los mínimos de la función de error. Podemos ver por qué esto es así, de la siguiente manera.

En la aproximación cuadrática a la función de error, dada en [[#^0dfc2d|(5.28)]] , la superficie de error se especifica por las cantidades $\mathbf{b}$ y $\mathbf{H}$, que contienen un total de $W(W + 3)/2$ elementos independientes (porque la matriz $\mathbf{H}$ es simétrica), donde $W$ es la dimensionalidad de $\mathbf{w}$ (es decir, el número total de parámetros adaptativos en la red). La ubicación del mínimo de esta aproximación cuadrática depende de $O(W^2)$ parámetros, y no deberíamos esperar poder localizar el mínimo hasta que hayamos reunido $O(W^2)$ piezas independientes de información. Si no hacemos uso de la información del gradiente, esperaríamos tener que realizar $O(W^2)$ evaluaciones de la función, cada una de las cuales requeriría $O(W)$ pasos. Por lo tanto, el esfuerzo computacional necesario para encontrar el mínimo utilizando tal enfoque sería de $O(W^3)$.

Ahora comparémoslo con un algoritmo que hace uso de la información del gradiente. Debido a que cada evaluación de $\nabla E$ trae $W$ elementos de información, podríamos esperar encontrar el mínimo de la función en $O(W)$ evaluaciones del gradiente. Como veremos, mediante el uso de la retropropagación de errores, cada evaluación de $\nabla E$ solo toma $O(W)$ pasos y, por lo tanto, el mínimo ahora se puede encontrar en $O(W^2)$ pasos. Por esta razón, el uso de la información del gradiente forma la base de los algoritmos prácticos para entrenar redes neuronales.

## 5.2.4 Optimización por Descenso de Gradiente

El enfoque más simple para usar la información del gradiente es elegir la actualización del peso en [[#^262913|(5.27)]] para comprender un pequeño paso en la dirección del gradiente negativo, de modo que

$$
\mathbf{w}^{(\tau+1)} = \mathbf{w}^{(\tau)} - \eta \nabla E(\mathbf{w}^{(\tau)}) \tag{5.41}
$$

donde el parámetro $\eta > 0$ se conoce como la **tasa de aprendizaje**. Después de cada actualización, el gradiente se reevalúa para el nuevo vector de pesos y el proceso se repite. Note que la función de error se define con respecto a un conjunto de entrenamiento, y por lo tanto cada paso requiere que todo el conjunto de datos se procese para evaluar $\nabla E$. Las técnicas que usan el conjunto de datos completo a la vez se llaman métodos de **lote**. En cada paso, el vector de pesos se mueve en la dirección de la mayor tasa de disminución de la función de error, y por lo tanto este enfoque se conoce como **descenso de gradiente** o **descenso más pronunciado**. Aunque tal enfoque puede parecer intuitivamente razonable, en realidad resulta ser un algoritmo pobre, por razones discutidas en Bishop y Nabney (2008).

Para la optimización por lotes, existen métodos más eficientes, como el método de gradientes conjugados y los métodos quasi-Newton, que son mucho más robustos y rápidos que el descenso de gradiente simple (Gill et al., 1981; Fletcher, 1987; Nocedal y Wright, 1999). A diferencia del descenso de gradiente, estos algoritmos tienen la propiedad de que la función de error siempre disminuye en cada iteración a menos que el vector de pesos haya llegado a un mínimo local o global.

Para encontrar un mínimo suficientemente bueno, puede ser necesario ejecutar un algoritmo basado en gradientes múltiples veces, cada vez usando un punto de inicio aleatoriamente elegido y comparando el rendimiento resultante en un conjunto de validación independiente.

Existe, sin embargo, una versión en línea del descenso de gradiente que ha demostrado ser útil en la práctica para entrenar redes neuronales en grandes conjuntos de datos (Le Cun et al., 1989). Las funciones de error basadas en la verosimilitud máxima para un conjunto de observaciones independientes comprenden una suma de términos, uno para cada punto de datos

$$
E(\mathbf{w}) = \sum_{n=1}^N E_n(\mathbf{w}). \tag{5.42}
$$

El descenso de gradiente en línea, también conocido como **descenso de gradiente secuencial** o **descenso de gradiente estocástico**, realiza una actualización del vector de pesos basada en un punto de datos a la vez, de modo que

$$
\mathbf{w}^{(\tau+1)} = \mathbf{w}^{(\tau)} - \eta \nabla E_n(\mathbf{w}^{(\tau)}). \tag{5.43}
$$

Esta actualización se repite al recorrer los datos ya sea en secuencia o seleccionando puntos al azar con reemplazo. Por supuesto, existen escenarios intermedios en los que las actualizaciones se basan en lotes de puntos de datos.

Una ventaja de los métodos en línea en comparación con los métodos por lotes es que los primeros manejan la redundancia en los datos de manera mucho más eficiente. Para ilustrar esto, consideremos un ejemplo extremo en el que tomamos un conjunto de datos y duplicamos su tamaño al duplicar cada punto de datos. Cabe destacar que esto simplemente multiplica la función de error por un factor de 2 y, por lo tanto, es equivalente a usar la función de error original. Los métodos por lotes requerirán el doble del esfuerzo computacional para evaluar el gradiente de la función de error del lote, mientras que los métodos en línea no se verán afectados. Otra propiedad del descenso de gradiente en línea es la posibilidad de escapar de mínimos locales, ya que un punto estacionario con respecto a la función de error para todo el conjunto de datos generalmente no será un punto estacionario para cada punto de datos individualmente.

Los algoritmos de optimización no lineales y su aplicación práctica al entrenamiento de redes neuronales se discuten en detalle en Bishop y Nabney (2008).


# 5.3 Error Backpropagation 
Nuestro objetivo en esta sección es encontrar una técnica eficiente para evaluar el gradiente de una función de error  $E(\mathbf{w})$ para una red neuronal de propagación hacia adelante. Veremos que esto se puede lograr utilizando un esquema de paso de mensajes local en el que la información se envía alternativamente hacia adelante y hacia atrás a través de la red, y que se conoce como propagación del error, o a veces simplemente como *backprop*.

La mayoría de los algoritmos de entrenamiento involucran un procedimiento iterativo para la minimización de una función de error, con ajustes a los pesos realizados en una secuencia de pasos. En cada uno de estos pasos, podemos distinguir entre dos etapas distintas. 
- En la primera etapa, se deben evaluar las derivadas de la función de error con respecto a los pesos. Como veremos, la contribución importante de la técnica de propagación del error es proporcionar un método computacionalmente eficiente para evaluar dichas derivadas. Dado que es en esta etapa cuando los errores se propagan hacia atrás a través de la red, utilizaremos el término "propagación del error" específicamente para describir la evaluación de las derivadas.
- En la segunda etapa, las derivadas se utilizan para calcular los ajustes que deben hacerse a los pesos. La técnica más sencilla, y la que originalmente consideraron Rumelhart et al. (1986), involucra el descenso de gradiente. Es importante reconocer que las dos etapas son distintas. 
Así, la primera etapa, es decir, la propagación de errores hacia atrás a través de la red para evaluar derivadas, se puede aplicar a muchos otros tipos de redes y no solo al perceptrón multicapa. También se puede aplicar a funciones de error que no sean solo la simple suma de cuadrados, y a la evaluación de otras derivadas como las matrices Jacobiana y Hessiana, como veremos más adelante en este capítulo. De manera similar, la segunda etapa de ajuste de pesos utilizando las derivadas calculadas se puede abordar utilizando una variedad de esquemas de optimización, muchos de los cuales son sustancialmente más poderosos que el simple descenso de gradiente.

## 5.3.1 Evaluación de derivadas de funciones de error

Ahora derivamos el algoritmo de propagación del error para una red general con topología de propagación hacia adelante arbitraria, funciones de activación no lineales diferenciables arbitrarias y una amplia clase de funciones de error. Las fórmulas resultantes se ilustrarán utilizando una estructura de red simple con una sola capa de unidades ocultas sigmoideas junto con una función de error de suma de cuadrados.

Muchas funciones de error de interés práctico, por ejemplo, aquellas definidas por máxima verosimilitud para un conjunto de datos i.i.d., comprenden una suma de términos, uno para cada punto de datos en el conjunto de entrenamiento, de modo que
$$
E(\mathbf{w}) = \sum_{n=1}^N E_n(\mathbf{w}). \tag{5.44}
$$
Aquí consideraremos el problema de evaluar $\nabla E_n(\mathbf{w})$ para uno de esos términos en la función de error. Esto puede usarse directamente para la optimización secuencial, o los resultados pueden acumularse sobre el conjunto de entrenamiento en el caso de métodos por lotes.
Primero, consideremos un modelo lineal simple en el cual las salidas $y_k$ son combinaciones lineales de las variables de entrada $x_i$, de manera que
$$
y_k = \sum_i w_{ki} x_i \tag{5.45}
$$

junto con una función de error que, para un patrón de entrada particular $n$, toma la forma
$$
E_n = \frac{1}{2} \sum_k (y_{nk} - t_{nk})^2 \tag{5.46}
$$

donde $y_{nk} = y_k(\mathbf{x}_n, \mathbf{w})$. El gradiente de esta función de error con respecto a un peso $w_{ji}$ está dado por

$$
\frac{\partial E_n}{\partial w_{ji}} = (y_{nj} - t_{nj}) x_{ni} \tag{5.47}
$$

que puede interpretarse como un cálculo ‘local’ que involucra el producto de una ‘señal de error’ $y_{nj} - t_{nj}$ asociada con el extremo de salida del enlace $w_{ji}$ y la variable $x_{ni}$ asociada con el extremo de entrada del enlace. Ahora veremos cómo este resultado simple se extiende al contexto más complejo de redes neuronales de propagación hacia adelante multicapa.
En una red neuronal de alimentación directa general, cada unidad calcula una suma ponderada de sus entradas de la forma


$$
a_j = \sum_i w_{ji} z_i \tag{5.48}
$$

^660860

donde $z_i$ es la activación de una unidad, o entrada, que envía una conexión a la unidad $j$, y $w_{ji}$ es el peso asociado con esa conexión. En la Sección 5.1, vimos que los sesgos pueden ser incluidos en esta suma introduciendo una unidad extra, o entrada, con una activación fija de +1. Por lo tanto, no necesitamos tratar los sesgos explícitamente. La suma en (5.48) se transforma mediante una función de activación no lineal $h(\cdot)$ para dar la activación $z_j$ de la unidad $j$ en la forma
$$
z_j = h(a_j). \tag{5.49}
$$

^5f8336

Nota que una o más de las variables $z_i$ en la suma en (5.48) podrían ser una entrada, y de manera similar, la unidad $j$ en (5.49) podría ser una salida. 
Para cada patrón en el conjunto de entrenamiento, supondremos que hemos suministrado el vector de entrada correspondiente a la red y calculado las activaciones de todas las unidades ocultas y de salida en la red mediante la aplicación sucesiva de (5.48) y (5.49). Este proceso se llama a menudo propagación hacia adelante porque puede considerarse como un flujo de información hacia adelante a través de la red.
Ahora consideremos la evaluación de la derivada de $E_n$ con respecto a un peso $w_{ji}$. Las salidas de las distintas unidades dependerán del patrón de entrada particular $n$. Sin embargo, para simplificar la notación, omitiremos el subíndice $n$ de las variables de red. Primero notamos que $E_n$ depende de $w_{ji}$ solo a través de la entrada sumada $a_j$ a la unidad $j$. Por lo tanto, podemos aplicar la regla de la cadena para las derivadas parciales y obtener

$$
\frac{\partial E_n}{\partial w_{ji}} = \frac{\partial E_n}{\partial a_j} \frac{\partial a_j}{\partial w_{ji}}. \tag{5.50}
$$

Ahora introducimos una notación útil

$$
\delta_j \equiv \frac{\partial E_n}{\partial a_j} \tag{5.51}
$$

donde $\delta$'s a menudo se refieren a errores por razones que veremos en breve. Usando [[#^660860|(5.48)]] , podemos escribir

$$
\frac{\partial a_j}{\partial w_{ji}} = z_i. \tag{5.52}
$$

Sustituyendo (5.51) y (5.52) en (5.50), obtenemos

$$
\frac{\partial E_n}{\partial w_{ji}} = \delta_j z_i. \tag{5.53}
$$

^2fb96f

La ecuación (5.53) nos dice que la derivada requerida se obtiene simplemente multiplicando el valor de $\delta$ para la unidad en el extremo de salida del peso por el valor de $z$ para la unidad en el extremo de entrada del peso (donde $z = 1$ en el caso de un sesgo). Nota que esto toma la misma forma que el modelo lineal simple considerado al inicio de esta sección. Por lo tanto, para evaluar las derivadas, solo necesitamos calcular el valor de $\delta_j$ para cada unidad oculta y de salida en la red, y luego aplicar (5.53). ^0deccf

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Pattern Recognition and Machine Learning\imgs\figure 5.7.png">
    <figcaption></figcaption>
    </figure>
</div>

Como ya hemos visto, para las unidades de salida, tenemos

$$
\delta_k = y_k - t_k \tag{5.54}
$$

^5b540f

hemos proporcionado que estamos usando el enlace canónico como la función de activación de la unidad de salida. Para evaluar los $\delta$ de las unidades ocultas, nuevamente utilizamos la regla de la cadena para derivadas parciales, 

$$
\delta_j \equiv \frac{\partial E_n}{\partial a_j} = \sum_k \frac{\partial E_n}{\partial a_k} \frac{\partial a_k}{\partial a_j} \tag{5.55}
$$

donde la suma abarca todas las unidades $k$ a las que la unidad $j$ envía conexiones. La disposición de unidades y pesos se ilustra en la Figura 5.7. 

Nota que las unidades etiquetadas como $k$ podrían incluir otras unidades ocultas y/o unidades de salida. Al escribir (5.55), estamos utilizando el hecho de que las variaciones en $a_j$ dan lugar a variaciones en la función de error solo a través de variaciones en las variables $a_k$. Si ahora sustituimos la definición de $\delta$ dada por (5.51) en (5.55), y hacemos uso de (5.48) y (5.49), obtenemos la siguiente fórmula de retropropagación 

$$
\delta_j = h'(a_j) \sum_k w_{kj} \delta_k \tag{5.56}
$$

^266594

que nos dice que el valor de $\delta$ para una unidad oculta particular puede obtenerse propagando los $\delta$ hacia atrás desde unidades más arriba en la red, como se ilustra en la Figura 5.7. Nota que la suma en (5.56) se toma sobre el primer índice en $w_{kj}$ (correspondiente a la propagación hacia atrás de la información a través de la red), mientras que en la ecuación de propagación hacia adelante [[#^150108|(5.10)]]  se toma sobre el segundo índice. Debido a que ya conocemos los valores de los $\delta$ para las unidades de salida, se sigue que al aplicar recursivamente (5.56) podemos evaluar los $\delta$ para todas las unidades ocultas en una red de alimentación hacia adelante, independientemente de su topología.

> 
> **Retropropagación del Error**
> 
> 1. Aplica un vector de entrada $x_n$ a la red y propaga hacia adelante a través de la red usando [[#^660860|(5.48)]]  y [[#^5f8336|(5.49)]] para encontrar las activaciones de todas las unidades ocultas y de salida.
> 2. Evalúa los $\delta_k$ para todas las unidades de salida usando [[#^5b540f|(5.54)]] 
> 3. Retropropaga los $\delta$ usando [[#^266594|(5.56)]] para obtener $\delta_j$ para cada unidad oculta en la red.
> 4. Usa [[#^2fb96f|(5.53)]] para evaluar las derivadas requeridas.


Para los métodos por lotes, la derivada del error total $E$ se puede obtener repitiendo los pasos anteriores para cada patrón en el conjunto de entrenamiento y luego sumando todos los patrones: 

$$
\frac{\partial E}{\partial w_{ji}} = \sum_n \frac{\partial E_n}{\partial \ w_{ji}} \tag{5.57}
$$

En la derivación anterior, hemos asumido implícitamente que cada unidad oculta o de salida en la red tiene la misma función de activación $h(\cdot)$. Sin embargo, la derivación se generaliza fácilmente para permitir que diferentes unidades tengan funciones de activación individuales, simplemente manteniendo un registro de qué forma de $h(\cdot)$ corresponde a cada unidad.

## 5.3.2 Un ejemplo simple

La derivación anterior del procedimiento de retropropagación permitió formas generales para la función de error, las funciones de activación y la topología de la red. Para ilustrar la aplicación de este algoritmo, consideraremos un ejemplo particular. Este se elige tanto por su simplicidad como por su importancia práctica, porque muchas aplicaciones de redes neuronales reportadas en la literatura hacen uso de este tipo de red. Específicamente, consideraremos una red de dos capas de la forma ilustrada en la Figura 5.1, junto con un error de suma de cuadrados, en el cual las unidades de salida tienen funciones de activación lineales, de modo que $y_k = a_k$, mientras que las unidades ocultas tienen funciones de activación sigmoide logística dada por

$$
h(a) = \tanh(a) \tag{5.58}
$$
donde

$$
\tanh(a) = \frac{e^a - e^{-a}}{e^a + e^{-a}}. \tag{5.59}
$$

Una característica útil de esta función es que su derivada puede expresarse en una forma particularmente simple:

$$
h'(a) = 1 - h(a)^2. \tag{5.60}
$$

También consideramos una función de error estándar de suma de cuadrados, de modo que para el patrón $n$ el error está dado por

$$
E_n = \frac{1}{2} \sum_{k=1}^K (y_k - t_k)^2 \tag{5.61}
$$

donde $y_k$ es la activación de la unidad de salida $k$, y $t_k$ es el objetivo correspondiente, para un patrón de entrada particular $\mathbf{x}_n$.

Para cada patrón en el conjunto de entrenamiento, primero realizamos una propagación hacia adelante usando

$$
a_j = \sum_{i=0}^D w_{ji}^{(1)} x_i \tag{5.62}
$$

$$
z_j = \tanh(a_j) \tag{5.63}
$$

$$
y_k = \sum_{j=0}^M w_{kj}^{(2)} z_j. \tag{5.64}
$$

A continuación, calculamos los $\delta$'s para cada unidad de salida usando

$$
\delta_k = y_k - t_k. \tag{5.65}
$$

Luego, retropropagamos estos para obtener $\delta$'s para las unidades ocultas usando

$$
\delta_j = (1 - z_j^2) \sum_{k=1}^K w_{kj} \delta_k. \tag{5.66}
$$

Finalmente, las derivadas con respecto a los pesos de la primera y segunda capa están dadas por

$$
\frac{\partial E_n}{\partial w_{ji}^{(1)}} = \delta_j x_i, \quad \frac{\partial E_n}{\partial w_{kj}^{(2)}} = \delta_k z_j. \tag{5.67}
$$


## 5.3.3 Eficiencia de la retropropagación

Uno de los aspectos más importantes de la retropropagación es su eficiencia computacional. Para entender esto, examinemos cómo el número de operaciones informáticas necesarias para evaluar las derivadas de la función de error escala con el número total $W$ de pesos y sesgos en la red. Una sola evaluación de la función de error (para un patrón de entrada dado) requeriría $O(W)$ operaciones, para $W$ suficientemente grande. Esto se debe al hecho de que, excepto en una red con conexiones muy dispersas, el número de pesos es típicamente mucho mayor que el número de unidades, y por lo tanto, la mayor parte del esfuerzo computacional en la propagación hacia adelante se ocupa de evaluar las sumas en (5.48), con la evaluación de las funciones de activación representando un pequeño gasto adicional. Cada término en la suma en (5.48) requiere una multiplicación y una adición, lo que lleva a un costo computacional general que es $O(W)$.
Un enfoque alternativo a la retropropagación para calcular las derivadas de la función de error es usar diferencias finitas. Esto se puede hacer perturbando cada peso a su vez y aproximando las derivadas mediante la expresión

$$ \frac{\partial E_n}{\partial w_{ji}} = \frac{E_n(w_{ji} + \epsilon) - E_n(w_{ji})}{\epsilon} + O(\epsilon) \tag{5.68} $$

donde $\epsilon \ll 1$. En una simulación de software, la precisión de la aproximación a las derivadas puede mejorarse haciendo $\epsilon$ más pequeño, hasta que surjan problemas de redondeo numérico. La precisión del método de diferencias finitas puede mejorarse significativamente utilizando diferencias centrales simétricas de la forma

$$ \frac{\partial E_n}{\partial w_{ji}} = \frac{E_n(w_{ji} + \epsilon) - E_n(w_{ji} - \epsilon)}{2 \epsilon} + O(\epsilon^2)  \tag{5.69} $$

**Ejercicio 5.14**: En este caso, las correcciones $O(\epsilon)$ se cancelan, como puede verificarse mediante la expansión de Taylor en el lado derecho de (5.69), y por lo tanto, las correcciones residuales son $O(\epsilon^2)$. Sin embargo, el número de pasos computacionales se duplica aproximadamente en comparación con (5.68).
El principal problema con la diferenciación numérica es que se ha perdido la escala $O(W)$ altamente deseable. Cada propagación hacia adelante requiere $O(W)$ pasos, y hay $W$ pesos en la red, cada uno de los cuales debe ser perturbado individualmente, por lo que la escala general es $O(W^2)$.
 Sin embargo, la diferenciación numérica juega un papel importante en la práctica, porque una comparación de las derivadas calculadas por retropropagación con aquellas obtenidas usando diferencias centrales proporciona una verificación poderosa de la corrección de cualquier implementación de software del algoritmo de retropropagación. Al entrenar redes en la práctica, las derivadas deben evaluarse usando retropropagación, porque esto proporciona la mayor precisión y eficiencia numérica. Sin embargo, los resultados deben compararse con la diferenciación numérica usando (5.69) para algunos casos de prueba con el fin de verificar la corrección de la implementación.


## 5.3.4 La matriz jacobiana

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Pattern Recognition and Machine Learning\imgs\figure 5.8.png">
    <figcaption></figcaption>
    </figure>
</div>


Hemos visto cómo las derivadas de una función de error con respecto a los pesos pueden obtenerse mediante la propagación de errores hacia atrás a través de la red. La técnica de retropropagación también puede aplicarse al cálculo de otras derivadas. Aquí consideramos la evaluación de la matriz Jacobiana, cuyos elementos están dados por las derivadas de las salidas de la red con respecto a las entradas

$$ J_{ki} \equiv \frac{\partial y_k}{\partial x_i} \tag{5.70} $$

donde cada una de estas derivadas se evalúa manteniendo todas las demás entradas fijas. Las matrices Jacobianas desempeñan un papel útil en sistemas construidos a partir de varios módulos distintos, como se ilustra en la Figura 5.8. Cada módulo puede comprender una función fija o adaptativa, que puede ser lineal o no lineal, siempre que sea diferenciable. Supongamos que deseamos minimizar una función de error $E$ con respecto al parámetro $w$ en la Figura 5.8. La derivada de la función de error está dada por

$$ \frac{\partial E}{\partial w} = \sum_{k,j} \frac{\partial E}{\partial y_k} \frac{\partial y_k}{\partial z_j} \frac{\partial z_j}{\partial w} \tag{5.71} $$

en la cual la matriz Jacobiana para el módulo rojo en la Figura 5.8 aparece en el término medio.

Dado que la matriz Jacobiana proporciona una medida de la sensibilidad local de las salidas a los cambios en cada una de las variables de entrada, también permite que cualquier error conocido $\Delta x_i$ asociado con las entradas se propague a través de la red entrenada para estimar su contribución $\Delta y_k$ a los errores en las salidas, mediante la relación

$$ \Delta y_k \approx \sum_i \frac{\partial y_k}{\partial x_i} \Delta x_i \tag{5.72} $$

que es válida siempre que los $|\Delta x_i|$ sean pequeños. En general, el mapeo de la red representado por una red neuronal entrenada será no lineal, por lo que los elementos de la matriz Jacobiana no serán constantes sino que dependerán del vector de entrada particular utilizado. Así, (5.72) es válida solo para pequeñas perturbaciones de las entradas, y la propia Jacobiana debe ser re-evaluada para cada nuevo vector de entrada.

La matriz Jacobiana puede ser evaluada utilizando un procedimiento de retropropagación similar al derivado anteriormente para evaluar las derivadas de una función de error con respecto a los pesos. Comenzamos escribiendo el elemento $J_{ki}$ en la forma:

$$
J_{ki} = \frac{\partial y_k}{\partial x_i} = \sum_j \frac{\partial y_k}{\partial a_j} \frac{\partial a_j}{\partial x_i} = \sum_j w_{ji} \frac{\partial y_k}{\partial a_j} \tag{5.73}
$$

donde hemos utilizado la ecuación (5.48). La suma en (5.73) se realiza sobre todas las unidades $j$ a las que la unidad de entrada $i$ envía conexiones (por ejemplo, sobre todas las unidades en la primera capa oculta en la topología en capas considerada anteriormente). Ahora escribimos una fórmula de retropropagación recursiva para determinar las derivadas $\partial y_k / \partial a_j$ :

$$
\frac{\partial y_k}{\partial a_j} = \sum_l \frac{\partial y_k}{\partial a_l} \frac{\partial a_l}{\partial a_j} = h'(a_j) \sum_l w_{lj} \frac{\partial y_k}{\partial a_l} \tag{5.74}
$$

donde la suma se realiza sobre todas las unidades $l$ a las que la unidad $j$ envía conexiones (correspondiendo al primer índice de $w_{lj}$). Nuevamente, hemos utilizado las ecuaciones (5.48) y (5.49). Esta retropropagación comienza en las unidades de salida para las cuales las derivadas requeridas pueden encontrarse directamente a partir de la forma funcional de la función de activación de la unidad de salida. Por ejemplo, si tenemos funciones de activación sigmoides individuales en cada unidad de salida, entonces:

$$
\frac{\partial y_k}{\partial a_j} = \delta_{kj} \ \sigma'(a_j) \tag{5.75}
$$

mientras que para salidas softmax tenemos:

$$
\frac{\partial y_k}{\partial a_j} = \delta_{kj} y_k - y_k y_j \tag{5.76}
$$

Podemos resumir el procedimiento para evaluar la matriz Jacobiana de la siguiente manera:

1. Aplicar el vector de entrada correspondiente al punto en el espacio de entrada en el cual se va a encontrar la matriz Jacobiana, y propagar hacia adelante de la manera usual para obtener las activaciones de todas las unidades ocultas y de salida en la red.
2. A continuación, para cada fila $k$ de la matriz Jacobiana, correspondiente a la unidad de salida $k$, retropropagar usando la relación recursiva (5.74), comenzando con (5.75) o (5.76), para todas las unidades ocultas en la red.
3. Finalmente, usar (5.73) para hacer la retropropagación hacia las entradas.

La Jacobiana también puede ser evaluada utilizando un formalismo alternativo de propagación hacia adelante (*fordward propagation*) , que puede derivarse de manera análoga al enfoque de retropropagación dado aquí.

**Ejercicio 5.15**. Nuevamente, la implementación de tales algoritmos puede verificarse utilizando la diferenciación numérica en la forma:

$$
\frac{\partial y_k}{\partial x_i} = \frac{y_k(x_i + \epsilon) - y_k(x_i - \epsilon)}{2\epsilon} + O(\epsilon^2) \tag{5.77}
$$

lo que implica 2D propagaciones hacia adelante para una red con D entradas.


# 5.4. La Matriz Hessiana

Hemos mostrado cómo la técnica de retropropagación puede ser utilizada para obtener las primeras derivadas de una función de error con respecto a los pesos en la red. La retropropagación también puede ser utilizada para evaluar las segundas derivadas del error, dadas por:

$$
\frac{\partial^2 E}{\partial w_{ji} \partial w_{lk}}. \tag{5.78}
$$

Cabe destacar que, a veces, es conveniente considerar todos los parámetros de pesos y sesgos como elementos $w_i$ de un único vector, denotado $\mathbf{w}$, en cuyo caso las segundas derivadas forman los elementos $H_{ij}$ de la matriz Hessiana $\mathbf{H}$, donde $i, j \in \{1, \ldots, W\}$ y $W$ es el número total de pesos y sesgos. La Hessiana juega un papel importante en muchos aspectos de la computación neuronal, incluyendo los siguientes:

1. **Optimización no lineal**: Varios algoritmos de optimización no lineal utilizados para entrenar redes neuronales se basan en consideraciones de las propiedades de segundo orden de la superficie de error, que están controladas por la matriz Hessiana (Bishop y Nabney, 2008).
2. **Reentrenamiento rápido**: La Hessiana forma la base de un procedimiento rápido para reentrenar una red de alimentación directa después de un pequeño cambio en los datos de entrenamiento (Bishop, 1991).
3. **Poda de redes**: La inversa de la Hessiana se ha utilizado para identificar los pesos menos significativos en una red como parte de los algoritmos de "poda" de redes (Le Cun et al., 1990).
4. **Aproximación de Laplace**: La Hessiana juega un papel central en la aproximación de Laplace para una red neuronal bayesiana (ver Sección 5.7). Su inversa se utiliza para determinar la distribución predictiva de una red entrenada, sus valores propios determinan los valores de los hiperparámetros, y su determinante se utiliza para evaluar la evidencia del modelo.

Se han utilizado varios esquemas de aproximación para evaluar la matriz Hessiana para una red neuronal. Sin embargo, la Hessiana también puede ser calculada exactamente utilizando una extensión de la técnica de retropropagación.

Una consideración importante para muchas aplicaciones de la Hessiana es la eficiencia con la que puede ser evaluada. Si hay $W$ parámetros (pesos y sesgos) en la red, entonces la matriz Hessiana tiene dimensiones $W \times W$, por lo que el esfuerzo computacional necesario para evaluar la Hessiana escalará como $O(W^2)$ para cada patrón en el conjunto de datos. Como veremos, existen métodos eficientes para evaluar la Hessiana cuya escala es efectivamente $O(W^2)$.


## 5.4.1 Aproximación Diagonal

Algunas aplicaciones de la matriz Hessiana discutidas anteriormente requieren la inversa de la Hessiana, en lugar de la Hessiana en sí. Por esta razón, ha habido cierto interés en usar una aproximación diagonal de la Hessiana, es decir, una que simplemente reemplaza los elementos fuera de la diagonal por ceros, porque su inversa es trivial de evaluar. Nuevamente, consideremos una función de error que consiste en una suma de términos, uno para cada patrón en el conjunto de datos, de modo que $E = \sum_n E_n$. La Hessiana se puede obtener considerando un patrón a la vez, y luego sumando los resultados sobre todos los patrones. A partir de (5.48), los elementos diagonales de la Hessiana, para el patrón $n$, se pueden escribir como:

$$
\frac{\partial^2 E_n}{\partial w_{ji}^2} = \frac{\partial^2 E_n}{\partial a_j^2} z_i^2. \tag{5.79}
$$

Usando (5.48) y (5.49), las segundas derivadas en el lado derecho de (5.79) se pueden encontrar recursivamente usando la regla de la cadena del cálculo diferencial para dar una ecuación de retropropagación de la forma:

$$
\frac{\partial^2 E_n}{\partial a_j^2} = h'(a_j)^2 \sum_k \sum_{k'} w_{kj} w_{k'j} \frac{\partial^2 E_n}{\partial a_k \partial a_{k'}} + h''(a_j) \sum_k w_{kj} \frac{\partial E_n}{\partial a_k}. \tag{5.80}
$$

Si ahora descartamos los elementos fuera de la diagonal en los términos de la segunda derivada, obtenemos (Becker y Le Cun, 1989; Le Cun et al., 1990):

$$
\frac{\partial^2 E_n}{\partial a_j^2} = h'(a_j)^2 \sum_k w_{kj}^2 \frac{\partial^2 E_n}{\partial a_k^2} + h''(a_j) \sum_k w_{kj} \frac{\partial E_n}{\partial a_k}. \tag{5.81}
$$

Cabe señalar que el número de pasos computacionales necesarios para evaluar esta aproximación es $O(W)$, donde $W$ es el número total de parámetros de peso y sesgo en la red, en comparación con $O(W^2)$ para la Hessiana completa. Ricotti et al. (1988) también utilizaron la aproximación diagonal a la Hessiana, pero retuvieron todos los términos en la evaluación de $\frac{\partial^2 E_n}{\partial a_j^2}$ y así obtuvieron expresiones exactas para los términos diagonales. Sin embargo, esto ya no tiene la escala $O(W)$. El principal problema con las aproximaciones diagonales es que, en la práctica, la Hessiana se encuentra típicamente como fuertemente no diagonal, por lo que estas aproximaciones, que están motivadas principalmente por la conveniencia computacional, deben tratarse con cuidado.

## 5.4.2 Aproximación de Producto Externo

Cuando se aplican redes neuronales a problemas de regresión, es común usar una función de error de suma de cuadrados de la forma

$$
E = \frac{1}{2} \sum_{n=1}^{N} (y_n - t_n)^2 \tag{5.82}
$$

donde hemos considerado el caso de una sola salida para mantener la notación simple (la extensión a varias salidas es sencilla). Podemos entonces escribir la matriz Hessiana en la forma

$$
H = \nabla \nabla E = \sum_{n=1}^{N} \nabla y_n \nabla y_n + \sum_{n=1}^{N} (y_n - t_n) \nabla \nabla y_n. \tag{5.83}
$$

Si la red ha sido entrenada en el conjunto de datos, y sus salidas $y_n$ están muy cerca de los valores objetivo $t_n$, entonces el segundo término en (5.83) será pequeño y puede ser ignorado. Más generalmente, sin embargo, puede ser apropiado ignorar este término por el siguiente argumento. Recordemos de la Sección 1.5.5 que la función óptima que minimiza una pérdida de suma de cuadrados es el promedio condicional de los datos objetivo. La cantidad $(y_n - t_n)$ es entonces una variable aleatoria con media cero. Si asumimos que su valor no está correlacionado con el valor del término de la segunda derivada en el lado derecho de (5.83), entonces todo el término promediará a cero en la suma sobre $n$.

Al ignorar el segundo término en (5.83), llegamos a la aproximación de Levenberg-Marquardt o aproximación de producto externo (porque la matriz Hessiana se construye a partir de una suma de productos externos de vectores), dada por

$$
H \approx \sum_{n=1}^{N} b_n b_n^T \tag{5.84}
$$

donde $b_n = \nabla y_n = \nabla a_n$ porque la función de activación para las unidades de salida es simplemente la identidad. La evaluación de la aproximación de producto externo para la Hessiana es sencilla, ya que solo involucra primeras derivadas de la función de error, que pueden ser evaluadas eficientemente en $O(W)$ pasos usando retropropagación estándar. Los elementos de la matriz se pueden encontrar en $O(W^2)$ pasos mediante multiplicación simple. Es importante enfatizar que esta aproximación solo es probable que sea válida para una red que ha sido entrenada adecuadamente, y que para un mapeo de red general, los términos de la segunda derivada en el lado derecho de (5.83) típicamente no serán despreciables.

En el caso de la función de error de entropía cruzada para una red con funciones de activación de unidades de salida sigmoide logística, la aproximación correspondiente es dada por

$$
H \approx \sum_{n=1}^{N} y_n (1 - y_n) b_n b_n^T. \tag{5.85}
$$

Un resultado análogo se puede obtener para redes multiclas con funciones de activación de unidades de salida softmax.


## 5.4.3 Inversa de la Hessiana

Podemos utilizar la aproximación de producto externo para desarrollar un procedimiento computacionalmente eficiente para aproximar la inversa de la matriz Hessiana (Hassibi y Stork, 1993). Primero, escribimos la aproximación de producto externo en notación matricial como

$$
H_N = \sum_{n=1}^{N} b_n b_n^T \tag{5.86}
$$

donde $b_n ≡ \nabla_w a_n$ es la contribución al gradiente de la activación de la unidad de salida derivada del punto de datos $n$. Ahora derivamos un procedimiento secuencial para construir la Hessiana incluyendo los puntos de datos uno a la vez. Supongamos que ya hemos obtenido la inversa de la Hessiana usando los primeros $L$ puntos de datos. Al separar la contribución del punto de datos $L + 1$, obtenemos

$$
H_{L+1} = H_L + b_{L+1} b_{L+1}^T. \tag{5.87}
$$

Para evaluar la inversa de la Hessiana, consideramos ahora la identidad matricial

$$
(M + vv^T)^{-1} = M^{-1} - \frac{M^{-1} v v^T M^{-1}}{1 + v^T M^{-1} v} \tag{5.88}
$$

donde $I$ es la matriz identidad, que es simplemente un caso especial de la identidad de Woodbury (C.7). Si ahora identificamos $H_L$ con $M$ y $b_{L+1}$ con $v$, obtenemos

$$
H^{-1}_{L+1} = H^{-1}_L - \frac{H^{-1}_L b_{L+1} b_{L+1}^T H^{-1}_L}{1 + b_{L+1}^T H^{-1}_L b_{L+1}}. \tag{5.89}
$$

De esta manera, los puntos de datos son absorbidos secuencialmente hasta que $L + 1 = N$ y todo el conjunto de datos ha sido procesado. Este resultado, por lo tanto, representa un procedimiento para evaluar la inversa de la Hessiana usando un solo paso a través del conjunto de datos. La matriz inicial $H_0$ se elige como $\alpha I$, donde $\alpha$ es una cantidad pequeña, por lo que el algoritmo realmente encuentra la inversa de $H + \alpha I$. Los resultados no son particularmente sensibles al valor preciso de $\alpha$. La extensión de este algoritmo a redes con más de una salida es sencilla.

Notamos aquí que la matriz Hessiana a veces puede ser calculada indirectamente como parte del algoritmo de entrenamiento de la red. En particular, los algoritmos de optimización no lineal cuasi-Newton construyen gradualmente una aproximación a la inversa de la Hessiana durante el entrenamiento. Tales algoritmos se discuten en detalle en Bishop y Nabney (2008).

**Falta 5.4.4, 5.4.5, 5.4.6**





![[figure 5.9.png]]


![[figure 5.10.png]]


![[figure 5.11.png]]


![[figure 5.12.png]]


![[figure 5.13.png]]


![[figure 5.14.png]]


![[figure 5.15.png]]


![[figure 5.16.png]]



