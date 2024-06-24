# Interpolación y el polinomio de Lagrange
## Introducción
Una de las clases de funciones más útiles y conocidas que mapean el conjunto de números reales en sí mismo son los **polinomios algebraicos**, el conjunto de funciones de la forma:

$$
P_n(x) = a_n x^n + a_{n-1} x^{n-1} + \cdots + a_1 x + a_0,
$$

donde $n$ es un entero no negativo y $a_0, \ldots, a_n$ son constantes reales. Una razón para su importancia es que aproximan uniformemente funciones continuas. Esto significa que para cualquier función, definida y continua en un intervalo cerrado y acotado, existe un polinomio que es tan "cercano" a la función dada como se desee. Este resultado se expresa precisamente en el **Teorema de Aproximación de Weierstrass**.

## Teorema de Aproximación de Weierstrass
Supongamos que $f$ está definida y es continua en $[a, b]$. Para cada $\epsilon > 0$, existe un polinomio  $P(x)$ con la propiedad de que

$$
|f(x) - P(x)| < \epsilon, \quad \text{para todo } x \in [a, b].
$$

Los polinomios de Taylor concuerdan lo más posible con una función dada en un punto específico, pero concentran su precisión cerca de ese punto. Un buen polinomio de aproximación necesita proporcionar una precisión relativa en todo un intervalo, y los polinomios de Taylor generalmente no lo hacen. Para los polinomios de Taylor, toda la información utilizada en la aproximación se concentra en el número único $x_0$, por lo que estos polinomios generalmente dan aproximaciones inexactas a medida que nos alejamos de $x_0$. Esto limita la aproximación del polinomio de Taylor a la situación en la que las aproximaciones son necesarias solo en números cercanos a $x_0$. Para fines computacionales ordinarios, es más eficiente usar métodos que incluyan información en varios puntos.

## Polinomios Interpoladores de Lagrange

El problema de determinar un polinomio de grado uno que pase por los puntos distintos $(x_0, y_0)$ y $(x_1, y_1)$ es el mismo que aproximar una función $f$ para la cual $f(x_0) = y_0$ y $f(x_1) = y_1$ mediante un polinomio interpolador de primer grado, o concordante con los valores de $f$ en los puntos dados. Usar este polinomio para la aproximación dentro del intervalo dado por los extremos se llama **interpolación polinómica**.

Definimos las funciones:

$$
L_0(x) = \frac{x - x_1}{x_0 - x_1} \quad \text{y} \quad L_1(x) = \frac{x - x_0}{x_1 - x_0}
$$

El polinomio lineal interpolador de Lagrange que pasa por $(x_0, y_0)$ y $(x_1, y_1)$ es:

$$
P(x) = L_0(x) f(x_0) + L_1(x) f(x_1) = \frac{x - x_1}{x_0 - x_1} f(x_0) + \frac{x - x_0}{x_1 - x_0} f(x_1).
$$
Notamos que

$$
\begin{align*}
L_0(x_0) &= 1, \quad L_0(x_1) = 0, \\
L_1(x_0) &= 0, \quad L_1(x_1) = 1,
\end{align*}
$$
lo que implica que

$$
P(x_0) = 1 \cdot f(x_0) + 0 \cdot f(x_1) = f(x_0) = y_0
$$
y
$$
P(x_1) = 0 \cdot f(x_0) + 1 \cdot f(x_1) = f(x_1) = y_1.
$$

Por lo tanto, $P$ es el único polinomio de grado a lo más uno que pasa por $(x_0, y_0)$ y $(x_1, y_1)$.

## Interpolación Polinómica de Lagrange Generalizada

Para generalizar el concepto de interpolación lineal, consideremos la construcción de un polinomio de grado a lo sumo $n$ que pasa por los $n + 1$ puntos:

$$
(x_0, f(x_0)), \quad (x_1, f(x_1)), \quad \ldots, \quad (x_n, f(x_n)).
$$

En este caso, primero construimos, para cada $k = 0, 1, \ldots, n$, una función $L_{n,k}(x)$ con la propiedad de que $L_{n,k}(x_i) = 0$ cuando $i \neq k$ y $L_{n,k}(x_k) = 1$. Para satisfacer $L_{n,k}(x_i) = 0$ para cada $i \neq k$ se requiere que el numerador de $L_{n,k}(x)$ contenga el término

$$
(x - x_0)(x - x_1) \cdots (x - x_{k-1})(x - x_{k+1}) \cdots (x - x_n).
$$

Para satisfacer $L_{n,k}(x_k) = 1$, el denominador de $L_{n,k}(x)$ debe ser este mismo término pero evaluado en $x = x_k$. Así,

$$
L_{n,k}(x) = \frac{(x - x_0) \cdots (x - x_{k-1})(x - x_{k+1}) \cdots (x - x_n)}{(x_k - x_0) \cdots (x_k - x_{k-1})(x_k - x_{k+1}) \cdots (x_k - x_n)}.
$$

El polinomio interpolador se describe fácilmente una vez que se conoce la forma de $L_{n,k}(x)$. Este polinomio, llamado el **n-ésimo polinomio interpolador de Lagrange**, se define en el siguiente teorema.

## Teorema
Si $x_0, x_1, \ldots, x_n$ son $n + 1$ números distintos y $f$ es una función cuyos valores se dan en estos números, entonces existe un único polinomio $P(x)$ de grado a lo sumo $n$ que satisface:

$$
f(x_k) = P(x_k), \quad \text{para cada } k = 0, 1, \ldots, n.
$$

Este polinomio está dado por
$$
P(x) = f(x_0)L_{n,0}(x) + \cdots + f(x_n)L_{n,n}(x) = \sum_{k=0}^n f(x_k)L_{n,k}(x),
$$

donde, para cada $k = 0, 1, \ldots, n$,
$$
\begin{aligned}
L_{n,k}(x) &= \frac{(x - x_0)(x - x_1) \cdots (x - x_{k-1})(x - x_{k+1}) \cdots (x - x_n)}{(x_k - x_0)(x_k - x_1) \cdots (x_k - x_{k-1})(x_k - x_{k+1}) \cdots (x_k - x_n)} \\ \\
&= \prod_{i=0, \ i \neq k}^n \frac{(x - x_i)}{(x_k - x_i)}.
\end{aligned}
$$

Escribiremos $L_{n,k}(x)$ simplemente como $L_k(x)$ cuando no haya confusión sobre su grado.


## Teorema de Interpolación de Lagrange
Supongamos que $x_0, x_1, \ldots, x_n$ son números distintos en el intervalo $[a, b]$ y $f \in C^{n+1}[a, b]$. Entonces, para cada $x$ en $[a, b]$, existe un número $\xi(x)$ (generalmente desconocido) entre $\min\{x_0, x_1, \ldots, x_n\}$ y el $\max\{x_0, x_1, \ldots, x_n\}$ y, por lo tanto, en $(a, b)$, tal que

$$
f(x) = P(x) + \frac{f^{(n+1)}(\xi(x))}{(n+1)!}(x - x_0)(x - x_1) \cdots (x - x_n),
$$

donde $P(x)$ es el polinomio interpolador dado en la ecuación (3.1).

### Demostración

Primero, notemos que si $x = x_k$, para cualquier $k = 0, 1, \ldots, n$, entonces $f(x_k) = P(x_k)$, y elegir $\xi(x)$ arbitrariamente en $(a, b)$ satisface la ecuación (3.3).

Si $x \neq x_k$, para todos $k = 0, 1, \ldots, n$, definimos la función $g$ para $t$ en $[a, b]$ mediante

$$
\begin{aligned}
g(t) &= f(t) - P(t) - [f(x) - P(x)] \frac{(t - x_0)(t - x_1) \cdots (t - x_n)}{(x - x_0)(x - x_1) \cdots (x - x_n)} \\ \\
&= f(t) - P(t) - [f(x) - P(x)] \ \prod_{i=0}^n \frac{(t-x_i)}{(x-x_i)}
\end{aligned}
$$

Dado que $f \in C^{n+1}[a, b]$ y $P \in C^\infty[a, b]$, se sigue que $g \in C^{n+1}[a, b]$. Para $t = x_k$, tenemos

$$
g(x_k) = f(x_k) - P(x_k) - [f(x) - P(x)] \ \prod_{i=0}^n \frac{(x_k-x_i)}{(x-x_i)} = 0 - [f(x) - P(x)] \cdot 0 = 0.
$$

Además,
$$
g(x) = f(x) - P(x) - [f(x) - P(x)] \prod_{i=0}^n \frac{(x-x_i)}{(x-x_i)} = f(x) - P(x) - [f(x) - P(x)] = 0.
$$

Por lo tanto, $g \in C^{n+1}[a, b]$, y $g$ es cero en los $n + 2$ números distintos $x, x_0, x_1, \ldots, x_n$. Por el Teorema Generalizado de Rolle, existe un número $\xi$ en $(a, b)$ para el cual $g^{(n+1)}(\xi) = 0$. Así,

$$
0 = g^{(n+1)}(\xi) = f^{(n+1)}(\xi) - P^{(n+1)}(\xi) - [f(x) - P(x)] \frac{d^{n+1}}{dt^{n+1}} \left[ \prod_{i=0}^n \frac{(t-x_i)}{(x-x_i)} \right]_{t = \xi} \quad (*)
$$

Sin embargo, $P(x)$ es un polinomio de grado a lo sumo $n$, por lo que la $(n+1)$-ésima derivada, $P^{(n+1)}(x)$, es idénticamente cero. Además,

$$
\prod_{i=0}^n \frac{(t - x_i)}{(x - x_i)}
$$

es un polinomio de grado $(n + 1)$, por lo que

$$
\prod_{i=0}^n \frac{(t - x_i)}{(x - x_i)} = \left[ \frac{1}{\prod_{i=0}^n (x - x_i)} \right] t^{n+1} + (\text{términos de grado menor en } t),
$$

y
$$
\frac{d^{n+1}}{dt^{n+1}} \left[ \prod_{i=0}^n \frac{(t - x_i)}{(x - x_i)} \right] = \frac{(n + 1)!}{\prod_{i=0}^n (x - x_i)}.
$$

La ecuación $(*)$ se convierte en
$$
0 = f^{(n+1)}(\xi) - 0 - [f(x) - P(x)] \ \frac{(n + 1)!}{\prod_{i=0}^n (x - x_i)} ,
$$

y, al resolver $f(x)$, tenemos

$$
f(x) = P(x) + \frac{f^{(n+1)}(\xi(x))}{(n+1)!} \prod_{i=0}^n (x - x_i).
$$


# Aproximación de datos y Teorema de Neville

## Método de Neville

### Definición
Sea $f$ una función definida en $x_0, x_1, \dots, x_n$ y sean $m_0, m_1, \dots, m_k$ $k$ distintos enteros, con $0\leq m_i \leq n$ para cada $i$. El polinomio de Lagrange que concuerda con $f(x)$ en los $k$ puntos $x_{m_1}, x_{m_2}, \dots , x_{m_k}$ es denotado por $P_{m_1, m_2, \dots, m_k}(x)$.


## Teorema
Sea $f$ definida en $x_0, x_1, \dots, x_k$ y sea $x_j$ y $x_i$ dos números distintos en este conjunto. Entonces 
$$
P(x) = \frac{(x-x_j) \ P_{0, 1, \dots, j-1, j+1, \dots, k}(x) - (x-x_i) \ P_{0, 1, \dots, i-1, i+1, \dots, k}(x)}{(x_i - x_j)}
$$
es el $k$-ésimo polinomio de Lagrange que interpola a $f$ en los $k+1$ puntos $x_0, x_1, \dots, x_k$.


**Demostración**
Para simplificar la notación, sea $Q = P_{0,1,\ldots,i-1,i+1,\ldots,k}$ y $\hat{Q} = P_{0,1,\ldots,j-1,j+1,\ldots,k}$. 
Dado que $Q(x)$ y $\hat{Q}(x)$ son polinomios de grado $k-1$ o menor, $P(x)$ es de grado a lo sumo $k$.

Primero, note que $\hat{Q}(x_i) = f(x_i)$ implica que
$$
P(x_i) = \frac{(x_i - x_j) \hat{Q}(x_i) - (x_i - x_i) Q(x_i)}{x_i - x_j} = \frac{(x_i - x_j) f(x_i)}{x_i - x_j} = f(x_i).
$$

De manera similar, dado que $Q(x_j) = f(x_j)$, tenemos $P(x_j) = f(x_j)$.

Además, si $0 \leq r \leq k$ y $r$ no es ni $i$ ni $j$, entonces $Q(x_r) = \hat{Q}(x_r) = f(x_r)$. Entonces,
$$
P(x_r) = \frac{(x_r - x_j) \hat{Q}(x_r) - (x_r - x_i) Q(x_r)}{x_i - x_j} = \frac{(x_i - x_j) f(x_r)}{x_i - x_j} = f(x_r).
$$

Pero, por definición, $P_{0,1,\ldots,k}(x)$ es el único polinomio de grado a lo sumo $k$ que concuerda con $f$ en $x_0, x_1, \ldots, x_k$. 
Por lo tanto, $P \equiv P_{0,1,\ldots,k}$.



**El teorema implica que la interpolación de polinomios puede ser generado recursivamente**.
Por ejemplo, tenemos
$$
P_{0,1} = \frac{1}{x_1 - x_0} \left[(x-x_0)P_1 + (x-x_1)P_0\right]
$$

$$
P_{1,2} = \frac{1}{x_2 - x_1} \left[(x-x_1)P_2 + (x-x_2)P_1\right]
$$
$$
P_{0,1, 2} = \frac{1}{x_2 - x_0} \left[(x-x_0)P_{1,2} + (x-x_2)P_{0,1}\right]
$$
y así, sucesivamente. Estos polinomios son generados de la manera que se muestra en la tabla, donde cada fila es completada antes de que se inicien las filas siguientes.

| $x_0 \quad \quad \quad P_0$                                                                                                                     |
| ----------------------------------------------------------------------------------------------------------------------------------------------- |
| $x_1 \quad \quad \quad P_1 \quad \quad \quad P_{0,1}$                                                                                           |
| $x_2 \quad \quad \quad P_2 \quad \quad \quad P_{1,2} \quad \quad \quad P_{0,1,2}$                                                               |
| $x_3 \quad \quad \quad P_3 \quad \quad \quad P_{2,3} \quad \quad \quad P_{1,2,3} \quad \quad \quad P_{0,1,2,3}$                                 |
| $x_4 \quad \quad \quad P_4 \quad \quad \quad P_{3,4} \quad \quad \quad P_{2,3,4} \quad \quad \quad P_{1,2,3,4} \quad \quad \quad P_{0,1,2,3,4}$ |


El procedimiento que utiliza el resultado del Teorema 3.5 para generar recursivamente aproximaciones polinomiales de interpolación se llama **método de Neville**. Dado que los puntos aparecen consecutivamente en cada entrada, necesitamos describir solo un punto de inicio y el número de puntos adicionales usados en la construcción de la aproximación.

Para evitar los múltiples subíndices, dejamos que $Q_{i,j}(x)$, para $0 \leq j \leq i$, denote el polinomio de interpolación de grado $j$ en los $j+1$ números $x_{i-j}, x_{i-j+1}, \ldots, x_i$; es decir,
$$
Q_{i,j} = P_{i-j,i-j+1,\ldots,i-1,i}.
$$


| $x_0 \quad \quad P_0 = Q_{0,0}$                                                                                                                                     |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| $x_1 \quad \quad P_1 = Q_{1,0} \quad \quad P_{0,1} = Q_{1,1}$                                                                                                       |
| $x_2 \quad \quad P_2 = Q_{2,0} \quad \quad P_{1,2} = Q_{2,1} \quad \quad P_{0,1,2} = Q_{2,2}$                                                                       |
| $x_3 \quad \quad P_3 = Q_{3,0} \quad \quad P_{2,3} = Q_{3,1} \quad \quad P_{1,2,3} = Q_{3,2} \quad \quad P_{0,1,2,3} = Q_{3,3}$                                     |
| $x_4 \quad \quad P_4 = Q_{4,0} \quad \quad P_{3,4} = Q_{4,1} \quad \quad P_{2,3,4} = Q_{4,2} \quad \quad P_{1,2,3,4} = Q_{4,3} \quad \quad P_{0,1,2,3,4} = Q_{4,4}$ |

