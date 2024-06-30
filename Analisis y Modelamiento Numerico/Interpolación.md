Para repasar polinomio de Taylor: [[Calculo de una variable#Polinomio de Taylor|Polinomio de Taylor]].

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

## Método de los coeficientes indeterminados
Considere un conjunto de $n + 1$ puntos de la forma $(x_i, y_i)$ para $i = 0, 1, \ldots, n$. El objetivo de este capítulo es encontrar un polinomio $P_n$ de grado menor o igual a $n$ tal que cumpla la siguiente condición de interpolación:

$$
P_n(x_i) = y_i, \quad i = 0, 1, 2, \ldots, n. \quad (7)
$$

El primer paso es garantizar la existencia del polinomio $P_n$, el cual, en forma general tiene la forma:

$$
P_n(x) = a_0 + a_1 x + a_2 x^2 + \ldots + a_n x^n. \quad (8)
$$

Como $P_n$ debe de satisfacer $(7)$, entonces:

$$
a_0 + a_1 x_i + a_2 x_i^2 + \ldots + a_n x_i^n = y_i, \quad i = 0, 1, 2, \ldots, n. \quad (9)
$$

El conjunto de ecuaciones dado por $(9)$ al ser escrito de forma matricial queda como sigue:

$$
\begin{pmatrix}
1 & x_0 & x_0^2 & x_0^3 & \ldots & x_0^n \\
1 & x_1 & x_1^2 & x_1^3 & \ldots & x_1^n \\
1 & x_2 & x_2^2 & x_2^3 & \ldots & x_2^n \\
\vdots & \vdots & \vdots & \vdots & \ddots & \vdots \\
1 & x_n & x_n^2 & x_n^3 & \ldots & x_n^n
\end{pmatrix}
\begin{pmatrix}
a_0 \\
a_1 \\
a_2 \\
\vdots \\
a_n
\end{pmatrix}
=
\begin{pmatrix}
y_0 \\
y_1 \\
y_2 \\
\vdots \\
y_n
\end{pmatrix} \quad (10)
$$

donde observamos que la matriz asociada al sistema lineal $(10)$ es conocida como **matriz de Vandermonde** de orden $n + 1$.

El determinante de la matriz de Vandermonde se calcula como:

$$
\begin{vmatrix}
1 & x_0 & x_0^2 & x_0^3 & \ldots & x_0^n \\
1 & x_1 & x_1^2 & x_1^3 & \ldots & x_1^n \\
1 & x_2 & x_2^2 & x_2^3 & \ldots & x_2^n \\
\vdots & \vdots & \vdots & \vdots & \ddots & \vdots \\
1 & x_n & x_n^2 & x_n^3 & \ldots & x_n^n
\end{vmatrix}
=
\prod_{1 \leq i < j \leq n+1} (x_j - x_i). \quad (11)
$$

Podemos observar que para garantizar la existencia y unicidad del polinomio $P_n$ es necesario y suficiente que los $n + 1$ puntos $x_i \, (i = 0, 1, 2, \ldots, n)$ sean todos **distintos**, lo cual será considerado de ahora en adelante salvo se mencione explícitamente lo contrario. Una vez garantizada la existencia y unicidad del polinomio $P_n$, ahora llamado **Polinomio de interpolación**, procedemos a estudiar algunos métodos que nos permiten calcularlo.


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

En este caso, primero construimos, para cada $k = 0, 1, \ldots, n$, una función $L_{n,k}(x)$ con la propiedad de que $L_{n,k}(x_i) = 0$ cuando $i \neq k$ y $L_{n,k}(x_k) = 1$.
$$
L_{n, k}(x_i) = 
\begin{cases} 
0 \, \quad i \neq k \\
1 \, \quad i = k
\end{cases}
$$

 
Para satisfacer $L_{n,k}(x_i) = 0$ para cada $i \neq k$ se requiere que el numerador de $L_{n,k}(x)$ contenga el término

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
L_{n,k}(x) &= \prod_{i=0, \ i \neq k}^n \frac{(x - x_i)}{(x_k - x_i)}.
\end{aligned}
$$

Escribiremos $L_{n,k}(x)$ simplemente como $L_k(x)$ cuando no haya confusión sobre su grado.


## Teorema de Interpolación de Lagrange
Supongamos que $x_0, x_1, \ldots, x_n$ son números distintos en el intervalo $[a, b]$ y $f \in C^{n+1}[a, b]$. Entonces, para cada $x$ en $[a, b]$, existe un número $\xi(x)$ (generalmente desconocido) entre $\min\{x_0, x_1, \ldots, x_n\}$ y el $\max\{x_0, x_1, \ldots, x_n\}$ y, por lo tanto, en $(a, b)$, tal que

$$
f(x) = P(x) + \frac{f^{(n+1)}(\xi(x))}{(n+1)!}(x - x_0)(x - x_1) \cdots (x - x_n),
$$

donde $P(x)$ es el polinomio interpolador.
Esto nos da una expresión para el error $E(x)$ que se comete en algún punto $x \in (a, b)$.

$$
E(x) = \frac{f^{(n+1)}(\xi(x))}{(n+1)!}(x - x_0)(x - x_1) \cdots (x - x_n)
$$

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


## Observación
Dados los puntos $(x_0, y_0), \ldots, (x_n, y_n)$ es relativamente fácil calcular $P_n$ en la forma de Lagrange, pero, ¿qué sucede si agregamos a los puntos iniciales el punto $(x_{n+1}, y_{n+1})$? Ante esta situación, los métodos vistos de coeficientes indeterminados y el método de Lagrange no son muy útiles, porque tenemos que rehacer todos los cálculos para obtener el polinomio $P_{n+1}$, es decir, no aprovechan el trabajo de haber calculado $P_n$. **El método de Newton resuelve este problema.**

## Fenómeno Runge
Tal vez, podemos caer en el error de suponer que una mejor aproximación se logra aumentando el número de puntos a interpolar. Esta suposición es errada. En general, se puede demostrar que
$$
\lim_{n \to \infty} \ \left( \underset{-1 \leq x \leq 1}{\text{max}} \left|f(x) - P_n(x)\right| \right) = \infty
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



# Polinomio de Newton
Sea $f$ una función cuyos valores son conocidos en un conjunto $\{x_0, x_1, \ldots, x_n\}$, de nodos distintos entre sí no necesariamente ordenados. Sabemos que existe un único polinomio $p_n$ que interpola $f$ en $n+1$ nodos

$$p(x_i) = f(x_i), \ \forall \, i = 0, \ldots, n$$

## Teorema
Los polinomios $q_i$ forman una base para el espacio de polinomio de grado $\leq n$, donde
$$q_0(x) = 1$$
$$q_i(x) = (x - x_0)(x - x_1) \ldots (x - x_{i-1}), \quad 0 < i \leq n$$

### Demostración
En efecto, si $a_0 q_0(x) + a_1 q_1(x) + a_2 q_2(x) + \ldots + a_n q_n(x) = 0, \forall x \in \mathbb{R}$ entonces para $x = x_i$

$$a_0 = a_1 = \ldots = a_n = 0$$
## Forma de Newton
La forma de Newton del polinomio de interpolación es

$$p(x) = \sum_{j=0}^{n} c_j q_j(x)$$

Nos queda por determinar los coeficientes $c_0, c_1, \dots, c_n$.
## Diferencias divididas
Los coeficientes $c_i$ que acompañan a $q_i$ cuando $\sum_{i=0}^{n} c_i q_i$ interpola $f$ en $x_0, x_1, \ldots, x_n$ toman el nombre de diferencias divididas y se escriben como
 
$$c_i = f[x_0, x_1, \ldots, x_i]$$
de inmediato vemos que
$$f[x_0] = f(x_0); \quad f[x_0, x_1] = \frac{f(x_1) - f(x_0)}{x_1 - x_0}; \quad f[x_0, x_1, x_2] = \frac{f[x_1, x_2] - f[x_0, x_1]}{x_2 - x_0}$$

Así el polinomio de interpolación de Newton es
$$p(x) = \sum_{i=0}^{n} f[x_0, \ldots, x_i] \prod_{j=0}^{i-1} (x - x_j)$$
### Teorema
Las diferencias divididas se pueden hallar recursivamente
$$f[x_0, x_1, \ldots, x_n] = \frac{f[x_1, \ldots, x_n] - f[x_0, \ldots, x_{n-1}]}{x_n - x_0}$$
#### Demostración:
Sea $q(x)$ el polinomio de grado $n - 1$ que interpola a $f$ en $x_1, x_2, \ldots, x_n$ entonces

$$p(x) = q(x) + \frac{x - x_n}{x_n - x_0} [q(x) - p_{n-1}(x)]$$

interpola a $f$ en $x_0, x_1, x_2, \ldots, x_n$.

Además
$$
p(x) = \frac{q(x)(x-x_0) - p_{n-1}(x)(x-x_n)}{x_n-x_0}
$$
$$
p(x) = \sum_{i=1}^{n} f[x_0, \ldots, x_i] \prod_{j=0}^{i-1} (x - x_j) - \sum_{i=0}^{n-1} f[x_0, \ldots, x_i] \prod_{j=0}^{i-1} (x - x_j)
$$


$p(x) = \dfrac{1}{x_n - x_0} \left(f[x_1](x-x_0) + f[x_1, x_2](x-x_0)(x-x_1) + \dots + f[x_1, \dots, x_n] (x-x_0)(x-x_1)\dots (x-x_{n-1})\right.$$- \left.f[x_0](x-x_0) + f[x_0, x_1](x-x_0)(x-x_1) + \dots + f[x_0, \dots, x_{n-1}] (x-x_0)(x-x_1)\dots (x-x_{n-1}) \right)$
Los últimos términos son de grado $n$ por tanto el coeficiente que acompaña a $x^n$ es de la forma

$$
\frac{f[x_1, \dots, x_n] - f[x_0, \dots, x_{n-1}]}{x_n - x_0}
$$
Por tanto:
$$
f[x_0, x_1, \ldots, x_n] = \frac{f[x_1, \ldots, x_n] - f[x_0, \ldots, x_{n-1}]}{x_n - x_0}$$

### Cuadro de diferencias divididas
Se acostumbra construir un cuadro sinóptico para el cálculo de las diferencias divididas:

$$
\begin{array}{c|c|c|c|c}
x_0 & f[x_0] & f[x_0, x_1] & f[x_0, x_1, x_2] & f[x_0, x_1, x_2, x_3] \\
x_1 & f[x_1] & f[x_1, x_2] & f[x_1, x_2, x_3] \\
x_2 & f[x_2] & f[x_2, x_3] \\
x_3 & f[x_3]
\end{array}
$$

Los coeficientes que resultan en la primera fila son los que forman el polinomio de interpolación de Newton:

$P_3(x) = f[x_0] + f[x_0, x_1](x - x_0) + f[x_0, x_1, x_2](x - x_0)(x - x_1) + f[x_0, x_1, x_2, x_3](x - x_0)(x - x_1)(x - x_2)$

### Teorema
La diferencia dividida es una **función simétrica** de sus argumentos. Es decir si $(z_0, z_1, \ldots, z_n)$ es una permutación de $(x_0, x_1, \ldots, x_n)$ entonces
$$
f[z_0, z_1, \ldots, z_n] = f[x_0, x_1, \ldots, x_n]
$$
#### Demostración:
$f[z_0, z_1, \ldots, z_n]$ es el coeficiente de $x^n$ en el polinomio que interpola $f$ en $\{z_0, z_1, \ldots, z_n\}$, y $f[x_0, x_1, \ldots, x_n]$ es el coeficiente de $x^n$ en el polinomio que interpola $f$ en $\{x_0, x_1, \ldots, x_n\}$, como dicho polinomio es único entonces esas cantidades son iguales.

### Teorema
Sea $p$ el polinomio interpolante de $f$ en $\{x_0, x_1, \ldots, x_n\}$. Si $t$ es distinto de los nodos entonces

$$
f(t) - p(t) = f[x_0, x_1, \ldots, x_n, t] \prod_{j=0}^{n} (t - x_j)
$$
#### Demostración
Sea $q$ el polinomio interpolante de $f$ en $\{x_0, x_1, \ldots, x_n, t\}$ entonces

$$
q(x) = p(x) + f[x_0, x_1, \ldots, x_n, t] \prod_{j=0}^{n} (x - x_j)
$$

si $x = t$, $f(t) = q(t)$, luego

$$
f(t) = p(t) + f[x_0, x_1, \ldots, x_n, t] \prod_{j=0}^{n} (t - x_j)
$$

### Teorema

Si $f$ es $n$ veces derivable y $f^{(n)}$ es continua en $[a, b]$ entonces existe $c$ en $\langle a, b \rangle$ tal que

$$
f[x_0, x_1, \ldots, x_n] = \frac{1}{n!} f^{(n)}(c)
$$

#### Demostración
Sea $p$ el polinomio interpolante de $f$ en $\{x_0, x_1, \ldots, x_{n-1}\}$ entonces el error cometido en la interpolación es

$$
f(x_n) - p(x_n) = \frac{1}{n!} f^{(n)}(c) \prod_{j=0}^{n-1} (x_n - x_j)
$$
por el teorema anterior

$$
f(x_n) - p(x_n) = f[x_0, x_1, \ldots, x_{n-1}, x_n] \prod_{j=0}^{n-1} (x_n - x_j)
$$

## Forma de Newton Progresiva
Si suponemos que los nodos igualmente espaciados, $h = x_{i+1} - x_i$ y usamos la notación $\Delta$ para diferencia progresiva $\Delta f(x) = f(x + h) - f(x)$ entonces

$$
f[x_0, x_1] = \frac{f(x_1) - f(x_0)}{x_1 - x_0} = \frac{1}{h} \Delta f(x_0)
$$

$$
f[x_0, x_1, x_2] = \frac{\Delta f(x_1) - \Delta f(x_0)}{2h} = \frac{1}{2h^2} \Delta^2 f(x_0)
$$

y en general

$$
f[x_0, x_1, x_2, \ldots, x_k] = \frac{1}{k! h^k} \Delta^k f(x_0)
$$

Para $x = x_0 + sh$ el polinomio interpolante tiene la forma

$$
\begin{align*}
p(x) &= p(x_0 + sh) = f[x_0] + sh f[x_0, x_1] + s(s - 1)h^2 f[x_0, x_1, x_2] \\
&\quad + \ldots + s(s - 1) \cdots (s - n + 1)h^n f[x_0, x_1, \ldots, x_n] \\
&= f[x_0] + \sum_{k=1}^{n} s(s - 1) \cdots (s - k + 1)h^k f[x_0, x_1, \ldots, x_k] \\
&= f[x_0] + \sum_{k=1}^{n} \binom{s}{k} k! h^k f[x_0, x_1, \ldots, x_k]
\end{align*}
$$

#### Fórmula de Newton progresiva

$$
p(x) = f[x_0] + \sum_{k=1}^{n} \binom{s}{k} \Delta^k f(x_0)
$$
