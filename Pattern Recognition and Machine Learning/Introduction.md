# Example: Polynomial Curve Fitting

![[figure 1.1.png]]

![[figure 1.2.png]]


![[figure 1.3.png]]


![[figure 1.4.png]]


![[figure 1.5.png]]


![[table 1.1.png]]


![[figure 1.6.png]]


![[figure 1.7.png]]


![[table 1.2.png]]

![[figure 1.8.png]]



# Probability Theory

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Pattern Recognition and Machine Learning\imgs\figure 1.10.png" width=350>
    <figcaption></figcaption>
    </figure>
</div>

> Podemos derivar las reglas de la suma y el producto de la probabilidad considerando dos variables aleatorias, $X$, que toma los valores $\{x_i\}$ donde $i = 1, \dots, M$, y $Y$, que toma los valores $\{y_j\}$ donde $j = 1, \dots, L$. En esta ilustración tenemos $M = 5$ y $L = 3$. Si consideramos un número total $N$ de instancias de estas variables, entonces denotamos el número de instancias donde $X = x_i$ y $Y = y_j$ como $n_{ij}$, que es el número de puntos en la celda correspondiente de la matriz. El número de puntos en la columna $i$, correspondiente a $X = x_i$, se denota como $c_i$, y el número de puntos en la fila $j$, correspondiente a $Y = y_j$, se denota como $r_j$.


Para derivar las reglas de probabilidad, consideremos el ejemplo ligeramente más general mostrado en la Figura 1.10, que involucra dos variables aleatorias $X$ y $Y$. Supondremos que $X$ puede tomar cualquiera de los valores $x_i$ donde $i = 1, \dots, M$, y $Y$ puede tomar los valores $y_j$ donde $j = 1, \dots, L$. Consideremos un total de $N$ ensayos en los cuales muestreamos ambas variables $X$ y $Y$, y denotemos el número de dichos ensayos en los que $X = x_i$ y $Y = y_j$ como $n_{ij}$. Además, dejemos que el número de ensayos en los cuales $X$ toma el valor $x_i$ (independientemente del valor que tome $Y$) se denote como $c_i$, y de manera similar, dejemos que el número de ensayos en los que $Y$ toma el valor $y_j$ se denote como $r_j$.

La probabilidad de que $X$ tome el valor $x_i$ y $Y$ tome el valor $y_j$ se escribe como $p(X = x_i, Y = y_j)$ y se llama la probabilidad conjunta de $X = x_i$ y $Y = y_j$. Esta se obtiene dividiendo el número de puntos que caen en la celda $i,j$ entre el número total de puntos, y por lo tanto:

$$
p(X = x_i, Y = y_j) = \frac{n_{ij}}{N} \tag{1.5}
$$

^af674c

Aquí estamos considerando implícitamente el límite $N \rightarrow \infty$. De manera similar, la probabilidad de que $X$ tome el valor $x_i$ independientemente del valor de $Y$ se escribe como $p(X = x_i)$ y se obtiene dividiendo el número total de puntos que caen en la columna $i$, por lo tanto:

$$
p(X = x_i) = \frac{c_i}{N} \tag{1.6}
$$

^faa7c5

Dado que el número de instancias en la columna $i$ en la [[figure 1.10.png|Figura 1.10]] es simplemente la suma del número de instancias en cada celda de esa columna, tenemos $c_i = \sum_j n_{ij}$ y, por lo tanto, de (1.5) y (1.6), obtenemos:

$$
p(X = x_i) = \sum_{j=1}^{L} p(X = x_i, Y = y_j) \tag{1.7}
$$

^809676

Esta es la **regla de la suma** de la probabilidad. Nótese que $p(X = x_i)$ a veces se llama la probabilidad marginal, porque se obtiene marginalizando, o sumando, las otras variables (en este caso $Y$).

Si consideramos solo aquellas instancias en las que $X = x_i$, entonces la fracción de dichas instancias en las que $Y = y_j$ se escribe como $p(Y = y_j | X = x_i)$ y se llama la probabilidad condicional de $Y = y_j$ dado $X = x_i$. Esta se obtiene dividiendo el número de puntos en la columna $i$ que caen en la celda $i,j$, por lo tanto:

$$
p(Y = y_j | X = x_i) = \frac{n_{ij}}{c_i} \tag{1.8}
$$

^848707

A partir de  [[#^af674c|(1.5)]], [[#^faa7c5|(1.6)]] y [[#^848707|(1.8)]] , podemos derivar la siguiente relación:

$$
p(X = x_i, Y = y_j) = \frac{n_{ij}}{N} = \frac{n_{ij}}{c_i} \cdot \frac{c_i}{N} = p(Y = y_j | X = x_i)p(X = x_i) \tag{1.9}
$$

Esta es la **regla del producto** de la probabilidad.


 > [!important] Rules of Probability
 > Sum Rule 
$$ p(X) = \sum_{Y} p (X, Y) \tag{1.10} $$
> Product Rule
> 
$$ p(X,Y) = p(Y|X)p(X) \tag{1.11} $$

^1aa30b

Donde $p(X,Y)$ es una **probabilidad conjunta** y se lee como la *probabilidad de X y Y*. De forma similar, la cantidad $p(Y|X)$ es la **probabilidad condicionada** y se lee como *la probabilidad de Y dado X*, mientras que $p(X)$ es la **probabilidad marginal** y es simplemente la *probabilidad de X*.

Vemos que de la [[#^1aa30b|regla del producto]] y la simetría de la probabilidad conjunta $P(X, Y) = P(Y, X)$ se obtiene la siguiente relación
## Bayes' theorem
$$ p(Y|X) = \frac{p(X|Y)p(Y)}{p(X)} \tag{1.12} $$

Usando la [[#^1aa30b|regla de la suma]] el denominador en el teorema de Bayes puede ser expresado en términos de cantidades que aparecen en el numerador
$$ p(X) = \sum_{Y} p(X|Y)p(Y) $$

## Independence
Si la distribución de dos variables se factoriza en el producto de los marginales tal que
$$ p(X,Y) = p(X)p(Y) $$
entonces $X$ y $Y$ se dice que son **independientes**.
De la regla del producto, vemos que 
$$ p(X|Y) = p(Y) $$
y, entonces la *distribución condicional* de $Y$ dado $X$ es de hecho *independiente* del valor de $X$.

## Probability densities

Si la probabilidad de que una variable de valor real $x$ caiga en el intervalo $(x, x + \delta x)$ está dada por $p(x) \delta x$ para $\delta x \to 0$, entonces $p(x)$ se llama la densidad de probabilidad sobre $x$. Esto se ilustra en la Figura 1.12. La probabilidad de que $x$ se encuentre en un intervalo $(a, b)$ está dada por

$$
p(x \in (a, b)) = \int_{a}^{b} p(x) \, dx. \tag{1.24}
$$

Dado que las probabilidades son no negativas, y dado que el valor de $x$ debe estar en algún lugar del eje real, la densidad de probabilidad $p(x)$ debe satisfacer las dos condiciones

$$
p(x) \geq 0, \tag{1.25}
$$

$$
\int_{-\infty}^{\infty} p(x) \, dx = 1. \tag{1.26}
$$

Bajo un cambio no lineal de variable, una densidad de probabilidad se transforma de manera diferente a una función simple, debido al factor jacobiano. Por ejemplo, si consideramos un cambio de variables $x = g(y)$, entonces una función $f(x)$ se convierte en $\tilde{f}(y) = f(g(y))$. Ahora consideremos una densidad de probabilidad $p_x(x)$ que corresponde a una densidad $p_y(y)$ con respecto a la nueva variable $y$, donde los subíndices denotan el hecho de que $p_x(x)$ y $p_y(y)$ son densidades diferentes. Las observaciones que caen en el rango $(x, x + \delta x)$, para valores pequeños de $\delta x$, se transformarán en el rango $(y, y + \delta y)$ donde $p_x(x) \delta x = p_y(y) \delta y$, y por lo tanto

$$
p_y(y) = p_x(x) \left| \frac{dx}{dy} \right| = p_x(g(y)) \left| g'(y) \right| . \tag{1.27}
$$

Una consecuencia de esta propiedad es que el concepto del máximo de una densidad de probabilidad depende de la elección de la variable.
La probabilidad de que $x$ se encuentre en el intervalo $(-\infty, z)$ está dada por la función de distribución acumulativa definida por

$$
P(z) = \int_{-\infty}^{z} p(x) \, dx. \tag{1.28}
$$

que satisface $P'(x) = p(x)$, como se muestra en la Figura 1.12.



<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Pattern Recognition and Machine Learning\imgs\figure 1.12.png" width=400>
    <figcaption></figcaption>
    </figure>
</div>

> El concepto de probabilidad para variables discretas puede extenderse al de una densidad de probabilidad $p(x)$ sobre una variable continua $x$, y es tal que la probabilidad de que $x$ se encuentre en el intervalo $(x, x + \delta x)$ está dada por $p(x)\delta x$ cuando $\delta x \rightarrow 0$. La densidad de probabilidad puede expresarse como la derivada de una función de distribución acumulativa $P(x)$.


Si tenemos varias variables continuas $x_1, \ldots, x_D$, denotadas colectivamente por el vector $x$, entonces podemos definir una densidad de probabilidad conjunta $p(x) = p(x_1, \ldots, x_D)$ tal que la probabilidad de que $x$ caiga en un volumen infinitesimal $\delta x$ que contiene el punto $x$ está dada por $p(x) \delta x$. Esta densidad de probabilidad multivariante debe satisfacer

$$
p(x) \geq 0, \tag{1.29}
$$

$$
\int p(x) \, dx = 1, \tag{1.30}
$$

donde la integral se toma sobre todo el espacio de $x$. También podemos considerar distribuciones de probabilidad conjunta sobre una combinación de variables discretas y continuas. 

Nota que si $x$ es una variable discreta, entonces $p(x)$ a veces se llama una función de masa de probabilidad porque puede considerarse como un conjunto de 'masas de probabilidad' concentradas en los valores permitidos de $x$.

Las reglas de suma y producto de probabilidad, así como el teorema de Bayes, se aplican igualmente al caso de las densidades de probabilidad, o a combinaciones de variables discretas y continuas. Por ejemplo, si $x$ e $y$ son dos variables reales, entonces las reglas de suma y producto toman la forma

$$
p(x) = \int p(x, y) \, dy \tag{1.31}
$$

$$
p(x, y) = p(y|x)p(x). \tag{1.32}
$$

Una justificación formal de las reglas de suma y producto para variables continuas (Feller, 1966) requiere una rama de las matemáticas llamada teoría de medidas y está fuera del alcance de este libro. Sin embargo, su validez se puede ver de manera informal, dividiendo cada variable real en intervalos de ancho $\Delta$ y considerando la distribución de probabilidad discreta sobre estos intervalos. Tomar el límite $\Delta \to 0$ convierte las sumas en integrales y da el resultado deseado.



## Expectations and covariances
El valor promedio de una función $f(x)$ bajo una distribución de probabilidad $p(x)$ se llama la esperanza de $f(x)$ y se denota por $E[f]$. Para una distribución discreta, se da por

$$
E[f] = \sum_{x} p(x)f(x) \tag{1.33}
$$

de modo que el promedio está ponderado por las probabilidades relativas de los diferentes valores de $x$. En el caso de variables continuas, las esperanzas se expresan en términos de una integración con respecto a la densidad de probabilidad correspondiente

$$
E[f] = \int p(x)f(x) \, dx. \tag{1.34}
$$

En cualquier caso, si se nos da un número finito $N$ de puntos extraídos de la distribución de probabilidad o de la densidad de probabilidad, entonces la esperanza se puede aproximar como una suma finita sobre estos puntos

$$
E[f] \approx \frac{1}{N} \sum_{n=1}^{N} f(x_n). \tag{1.35}
$$

La aproximación en $(1.35)$ se vuelve exacta en el límite $N \rightarrow \infty$.


A continuación, te proporciono la traducción con la notación matemática adecuada:

---

A veces consideraremos expectativas de funciones de varias variables, en cuyo caso podemos usar un subíndice para indicar sobre cuál variable se está promediando. Por ejemplo, 

$$ E_x[f(x, y)] \tag{1.36} $$

denota el promedio de la función $f(x, y)$ con respecto a la distribución de $x$. Nota que $E_x[f(x, y)]$ será una función de $y$.

También podemos considerar una expectativa condicional con respecto a una distribución condicional, de modo que

$$ E_x[f|y] = \sum_x p(x|y)f(x) \tag{1.37} $$

con una definición análoga para variables continuas.

La varianza de $f(x)$ se define como

$$ \text{var}[f] = E\left[(f(x) - E[f(x)])^2\right] \tag{1.38} $$

y proporciona una medida de cuánta variabilidad hay en $f(x)$ alrededor de su valor medio $E[f(x)]$. Desarrollando el cuadrado, vemos que la varianza también puede escribirse en términos de las expectativas de $f(x)$ y $f(x)^2$ como

$$ \text{var}[f] = E[f(x)^2] - E[f(x)]^2. \tag{1.39} $$

En particular, podemos considerar la varianza de la variable $x$ en sí misma, que se da por

$$ \text{var}[x] = E[x^2] - E[x]^2. \tag{1.40} $$

Para dos variables aleatorias $x$ e $y$, la covarianza se define como

$$ \text{cov}[x, y] = E_{x,y}[(x - E[x])(y - E[y])] = E_{x,y}[xy] - E[x]E[y] \tag{1.41} $$

lo cual expresa hasta qué punto $x$ e $y$ varían juntas. Si $x$ e $y$ son independientes, entonces su covarianza se anula.

En el caso de dos vectores de variables aleatorias $x$ e $y$, la covarianza es una matriz

$$ \text{cov}[x, y] = E_{x,y}[(x - E[x])(y^T - E[y^T])] = E_{x,y}[xy^T] - E[x]E[y^T]. \tag{1.42} $$

Si consideramos la covarianza de los componentes de un vector $x$ entre sí, entonces usamos una notación ligeramente más simple $\text{cov}[x] \equiv \text{cov}[x, x]$.

> [!tip]
> La covarianza $\text{Cov}[x, y]$ indica la medida en la que dos variables aleatorias, $x$ e $y$, varían juntas. Específicamente:
>
>- **Signo de la covarianza**:
>
> 	- Si $\text{Cov}[x, y] > 0$, indica que cuando $x$ aumenta, $y$ tiende a aumentar también (y viceversa).
> 	- Si $\text{Cov}[x, y] < 0$, sugiere que cuando $x$ aumenta, $y$ tiende a disminuir (y viceversa).
  >	- Si $\text{Cov}[x, y] = 0$, sugiere que no hay una relación lineal clara entre $x$ e $y$, lo que ocurre si son independientes (aunque la independencia no es una condición necesaria para que la covarianza sea cero).
>
>- **Magnitud de la covarianza**:
  >	- La magnitud de $\text{Cov}[x, y]$ indica la fuerza de la relación lineal entre las dos variables. Una covarianza grande en valor absoluto sugiere una fuerte relación lineal, mientras que un valor cercano a cero indica una relación lineal débil o nula.


## Bayesian probabilities

El teorema de Bayes adquiere ahora un nuevo significado. Recuerda que en el ejemplo de las cajas de frutas, la observación de la identidad de la fruta proporcionó información relevante que alteró la probabilidad de que la caja elegida fuera la roja. En ese ejemplo, el teorema de Bayes se utilizó para convertir una probabilidad a priori en una probabilidad a posteriori al incorporar la evidencia proporcionada por los datos observados. Como veremos más adelante en detalle, podemos adoptar un enfoque similar al hacer inferencias sobre cantidades como los parámetros $w$ en el ejemplo de ajuste de curvas polinomiales. Capturamos nuestras suposiciones sobre $w$, antes de observar los datos, en forma de una distribución de probabilidad a priori $p(w)$. El efecto de los datos observados $D = \{t_1, \dots, t_N\}$ se expresa a través de la probabilidad condicional $p(D|w)$, y veremos más adelante, en la Sección [[#Revisión del ajuste de curvas]] cómo esto puede representarse explícitamente. El teorema de Bayes, que toma la forma

$$ p(w|D) = \frac{p(D|w) p(w)}{p(D)} \tag{1.43} $$

nos permite entonces evaluar la incertidumbre en $w$ después de haber observado $D$ en forma de la probabilidad a posteriori $p(w|D)$.

La cantidad $p(D|w)$ en el lado derecho del teorema de Bayes se evalúa para el conjunto de datos observado $D$ y puede verse como una función del vector de parámetros $w$, en cuyo caso se denomina función de verosimilitud. Expresa cuán probable es el conjunto de datos observado para diferentes configuraciones del vector de parámetros $w$. Nota que la verosimilitud no es una distribución de probabilidad sobre $w$, y su integral con respecto a $w$ no es (necesariamente) igual a uno.

Dada esta definición de verosimilitud, podemos expresar el teorema de Bayes en palabras como:

$$\text{posterior} \propto \text{verosimilitud} \times \text{prior} \tag{1.44}$$

donde todas estas cantidades se ven como funciones de $w$. El denominador en la ecuación (1.43) es la constante de normalización, que asegura que la distribución posterior en el lado izquierdo sea una densidad de probabilidad válida e integre a uno. De hecho, integrando ambos lados de la ecuación (1.43) con respecto a $w$, podemos expresar el denominador en el teorema de Bayes en términos de la distribución a priori y la función de verosimilitud:

$$p(D) = \int p(D|w)p(w) \, dw. \tag{1.45}$$

En ambos paradigmas, el bayesiano y el frecuentista, la función de verosimilitud $p(D|w)$ juega un papel central. Sin embargo, la manera en que se utiliza es fundamentalmente diferente en los dos enfoques. En un contexto frecuentista, $w$ se considera un parámetro fijo, cuyo valor es determinado por alguna forma de "estimador", y los márgenes de error de esta estimación se obtienen considerando la distribución de posibles conjuntos de datos $D$. En contraste, desde la perspectiva bayesiana, solo hay un único conjunto de datos $D$ (es decir, el que se observa realmente), y la incertidumbre en los parámetros se expresa mediante una distribución de probabilidad sobre $w$.

Un estimador frecuentista ampliamente utilizado es el de máxima verosimilitud, en el cual $w$ se establece en el valor que maximiza la función de verosimilitud $p(D|w)$. Esto corresponde a elegir el valor de $w$ para el cual la probabilidad del conjunto de datos observado es máxima. En la literatura de aprendizaje automático, el logaritmo negativo de la función de verosimilitud se llama función de error. Debido a que el logaritmo negativo es una función monótonamente decreciente, maximizar la verosimilitud es equivalente a minimizar el error.

Un enfoque para determinar los márgenes de error frecuentistas es el bootstrap (Efron, 1979; Hastie et al., 2001), en el cual se crean múltiples conjuntos de datos de la siguiente manera. Supongamos que nuestro conjunto de datos original consiste en $N$ puntos de datos $X = \{x_1, \dots, x_N\}$. Podemos crear un nuevo conjunto de datos $X_B$ seleccionando $N$ puntos al azar de $X$, con reemplazo, de modo que algunos puntos en $X$ pueden repetirse en $X_B$, mientras que otros puntos en $X$ pueden estar ausentes en $X_B$. Este proceso se puede repetir $L$ veces para generar $L$ conjuntos de datos, cada uno de tamaño $N$ y cada uno obtenido mediante muestreo del conjunto de datos original $X$. La precisión estadística de las estimaciones de los parámetros puede entonces evaluarse observando la variabilidad de las predicciones entre los diferentes conjuntos de datos de bootstrap.




# Distribución Gaussiana

Para el caso de una única variable $x$ con valores reales, la distribución Gaussiana se define por:

$$
N(x|\mu, \sigma^2) = \frac{1}{(2\pi\sigma^2)^{1/2}} \exp\left(-\frac{1}{2\sigma^2}(x - \mu)^2\right) \tag{1.46}
$$

^fc3ae2

Esta distribución está gobernada por dos parámetros: $\mu$, llamado la media, y $\sigma^2$, llamado la varianza. La raíz cuadrada de la varianza, denotada por $\sigma$, se llama desviación estándar, y el recíproco de la varianza, escrito como $\beta = 1/\sigma^2$, se llama precisión. Veremos la motivación para estos términos en breve. La Figura 1.13 muestra un gráfico de la distribución Gaussiana.

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Pattern Recognition and Machine Learning\imgs\figure 1.13.png">
    <figcaption></figcaption>
    </figure>
</div>

A partir de la forma de la ecuación [[#^fc3ae2|(1.46)]]  , vemos que la distribución Gaussiana satisface:

$$
N(x|\mu, \sigma^2) > 0. \tag{1.47}
$$

También es sencillo demostrar que la Gaussiana está normalizada, de modo que:

$$
\int_{-\infty}^{\infty} N(x|\mu, \sigma^2) \, dx = 1. \tag{1.48}
$$

Por lo tanto, la ecuación (1.46) satisface los dos requisitos para ser una densidad de probabilidad válida. 

Podemos encontrar fácilmente las esperanzas de funciones de $x$ bajo la distribución Gaussiana. En particular, el valor promedio de $x$ está dado por:

$$
E[x] = \int_{-\infty}^{\infty} N(x|\mu, \sigma^2) \, x \, dx = \mu. \tag{1.49}
$$

Debido a que el parámetro $\mu$ representa el valor promedio de $x$ bajo la distribución, se le conoce como la media. De manera similar, para el momento de segundo orden:

$$
E[x^2] = \int_{-\infty}^{\infty} N(x|\mu, \sigma^2) x^2 \, dx = \mu^2 + \sigma^2. \tag{1.50}
$$

A partir de las ecuaciones (1.49) y (1.50), se deduce que la varianza de $x$ está dada por:

$$
\text{var}[x] = E[x^2] - E[x]^2 = \sigma^2 \tag{1.51}
$$

y, por lo tanto, $\sigma^2$ se conoce como el parámetro de varianza. El máximo de una distribución se conoce como su moda. Para una distribución Gaussiana, la moda coincide con la media.

También estamos interesados en la distribución Gaussiana definida sobre un vector $x$ de $D$ dimensiones de variables continuas, que está dada por:

$$
N(x|\mu, \Sigma) = \frac{1}{(2\pi)^{D/2}} \frac{1}{|\Sigma|^{1/2}} \exp\left(-\frac{1}{2}(x - \mu)^T \Sigma^{-1} (x - \mu)\right) \tag{1.52}
$$

donde el vector de $D$ dimensiones $\mu$ se llama la media, la matriz $D \times D$ $\Sigma$ se llama la covarianza, y $|\Sigma|$ denota el determinante de $\Sigma$. 








# Revisión del ajuste de curvas
	


# Model Selection


# The Curse of Dimensionality


# Decision Theory


# Information Theory


