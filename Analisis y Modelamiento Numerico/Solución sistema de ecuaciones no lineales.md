

# Punto fijo
Una función $G$ de $D \subseteq \mathbb{R}^n$ en $\mathbb{R}^n$ tiene un punto fijo en $p \in D$ si $G(p)=p$.

## Teorema
Sea
$$
D = \{ (x_1, x_2, \ldots, x_n)^T \mid a_i \leq x_i \leq b_i, \text{ para cada } i = 1, 2, \ldots, n \}
$$

para alguna colección de constantes $a_1, a_2, \ldots, a_n$ y $b_1, b_2, \ldots, b_n$. Supongamos que $G$ es una función continua de $D \subseteq \mathbb{R}^n$ en $\mathbb{R}^n$ con la propiedad de que $G(x) \in D$ siempre que $x \in D$. Entonces $G$ tiene un punto fijo en $D$.

Además, supongamos que todas las funciones componentes de $G$ tienen derivadas parciales continuas y que existe una constante $\lambda <1$ tal que

$$
\left| \frac{\partial g_i(x)}{\partial x_j} \right| \leq \frac{\lambda}{n}, \text{ siempre que } x \in D,
$$

para cada $j=1, 2, \ldots, n$ y cada función componente $g_i$. 
O también, si $\|JG(x)\| \leq \lambda < 1$. Entonces la secuencia de puntos fijos $\{ x^{(k)} \}_{k=0}^\infty$ definida por un $x^{(0)}$ arbitrariamente seleccionado en $D$ y generada por

$$
x^{(k)} = G(x^{(k-1)}), \text{ para cada } k \geq 1
$$

converge al único punto fijo $p \in D$ y

$$
\| x^{(k)} - p \|_\infty \leq \frac{\lambda^k}{1 - \lambda} \| x^{(1)} - x^{(0)} \|_\infty
$$

# Métodos de Homotopía y Continuación
Los métodos de homotopía, o de continuación, para sistemas no lineales incrustan el problema a resolver dentro de una colección de problemas. Específicamente, para resolver un problema de la forma:

$$
F(x) = 0
$$

que tiene la solución desconocida $x^*$, consideramos una familia de problemas descritos utilizando un parámetro $\lambda$ que asume valores en $[0, 1]$. Un problema con una solución conocida $x(0)$ corresponde a la situación cuando $\lambda = 0$ y el problema con la solución desconocida $x(1) \equiv x^*$ corresponde a $\lambda = 1$.

Por ejemplo, supongamos que $x(0)$ es una aproximación inicial a la solución de $F(x^*) = 0$.
Definimos
$$
G: [0, 1] \times \mathbb{R}^n \to \mathbb{R}^n
$$

por
$$
\begin{aligned}
G(\lambda, x) &= \lambda F(x) + (1 - \lambda) [F(x) - F(x(0))] \\ \\
G(\lambda, x)  &= F(x) + (\lambda - 1) F(x(0)).
\end{aligned}
$$

Determinaremos, para varios valores de $\lambda$, una solución para

$$
G(\lambda, x) = 0.
$$

Cuando $\lambda = 0$, esta ecuación asume la forma

$$
0 = G(0, x) = F(x) - F(x(0)),
$$

y $x(0)$ es una solución. Cuando $\lambda = 1$, la ecuación asume la forma

$$
0 = G(1, x) = F(x),
$$

y $x(1) = x^*$ es una solución.

La función $G$, con el parámetro $\lambda$, nos proporciona una familia de funciones que puede llevar desde el valor conocido $x(0)$ hasta la solución $x(1) = x^*$. La función $G$ se llama una **homotopía** entre la función $G(0, x) = F(x) - F(x(0))$ y la función $G(1, x) = F(x)$.

## Método de Continuación
El problema de continuación es:

- Determinar una forma de proceder desde la solución conocida $x(0)$ de $G(0, x) = 0$ hasta la solución desconocida $x(1) = x^*$ de $G(1, x) = 0$, es decir, la solución de $F(x) = 0$.

Primero asumimos que $x(\lambda)$ es la solución única de la ecuación

$$
G(\lambda, x) = 0, \quad \quad (*)
$$

para cada $\lambda \in [0, 1]$. El conjunto $\{ x(\lambda) \mid 0 \leq \lambda \leq 1 \}$ puede verse como una curva en $\mathbb{R}^n$ desde $x(0)$ hasta $x(1) = x^*$ parametrizada por $\lambda$. Un método de continuación encuentra una secuencia de pasos a lo largo de esta curva correspondiente a $\{x(\lambda_k)\}_{k=0}^m$, donde $0 = \lambda_0 < \lambda_1 < \cdots < \lambda_m = 1$.

Si las funciones $\lambda \to x(\lambda)$ y $G$ son diferenciables, entonces diferenciando la ecuación $(*)$ con respecto a $\lambda$ se obtiene

$$
0 = \frac{\partial G(\lambda, x(\lambda))}{\partial \lambda} + \frac{\partial G(\lambda, x(\lambda))}{\partial x} \frac{dx(\lambda)}{d\lambda}.
$$

Resolviendo para $\frac{dx(\lambda)}{d\lambda}$ se obtiene

$$
\frac{dx(\lambda)}{d\lambda} = - \left[ \frac{\partial G(\lambda, x(\lambda))}{\partial x} \right]^{-1} \frac{\partial G(\lambda, x(\lambda))}{\partial \lambda}.
$$

Este es un sistema de ecuaciones diferenciales con la condición inicial $x(0)$. Dado que

$$
G(\lambda, x(\lambda)) = F(x(\lambda)) + (\lambda - 1) F(x(0)),
$$

podemos determinar ambos

$$
\frac{\partial G(\lambda, x(\lambda))}{\partial x} =
\begin{bmatrix}
\frac{\partial f_1}{\partial x_1} & \frac{\partial f_1}{\partial x_2} & \cdots & \frac{\partial f_1}{\partial x_n} \\
\frac{\partial f_2}{\partial x_1} & \frac{\partial f_2}{\partial x_2} & \cdots & \frac{\partial f_2}{\partial x_n} \\
\vdots & \vdots & \ddots & \vdots \\
\frac{\partial f_n}{\partial x_1} & \frac{\partial f_n}{\partial x_2} & \cdots & \frac{\partial f_n}{\partial x_n}
\end{bmatrix}
= J(x(\lambda)),
$$

la matriz Jacobiana, y

$$
\frac{\partial G(\lambda, x(\lambda))}{\partial \lambda} = F(x(0)).
$$

Por lo tanto, el sistema de ecuaciones diferenciales se convierte en

$$
x'(\lambda) = -[J(x(\lambda))]^{-1} F(x(0)), \quad \text{para} \quad 0 \leq \lambda \leq 1,
$$

con la condición inicial $x(0)$. el siguiente teorema proporciona las condiciones bajo las cuales el método de continuación es factible.

### Teorema
Sea $F(x)$ continuamente diferenciable para $x \in \mathbb{R}^n$. Supongamos que la matriz Jacobiana $J(x)$ es no singular para todo $x \in \mathbb{R}^n$ y que existe una constante $M$ con $\| J(x)^{-1} \| \leq M$, para todo $x \in \mathbb{R}^n$. Entonces, para cualquier $x(0) \in \mathbb{R}^n$, existe una función única $x(\lambda)$, tal que

$$
G(\lambda, x(\lambda)) = 0,
$$

para todo $\lambda \in [0, 1]$. Además, $x(\lambda)$ es continuamente diferenciable, y

$$
x'(\lambda) = -J(x(\lambda))^{-1} F(x(0)), \quad \text{para cada} \quad \lambda \in [0, 1].
$$

El siguiente ejemplo muestra la forma del sistema de ecuaciones diferenciales asociado a un sistema de ecuaciones no lineal

### Ejemplo
Consideremos el sistema no lineal

$$
f_1(x_1, x_2, x_3) = 3x_1 - \cos(x_2 x_3) - 0.5 = 0,
$$

$$
f_2(x_1, x_2, x_3) = x_1^2 - 81(x_2 + 0.1)^2 + \sin(x_3) + 1.06 = 0,
$$

$$
f_3(x_1, x_2, x_3) = e^{-x_1 x_2} + 20x_3 + \frac{10\pi - 3}{3} = 0.
$$

La matriz Jacobiana es

$$
J(x) =
\begin{bmatrix}
3 & x_3 \sin(x_2 x_3) & x_2 \sin(x_2 x_3) \\
2x_1 & -162(x_2 + 0.1) & \cos(x_3) \\
-x_2 e^{-x_1 x_2} & -x_1 e^{-x_1 x_2} & 20
\end{bmatrix}.
$$


Dejemos que $x(0) = (0, 0, 0)^T$, de modo que

$$
F(x(0)) =
\begin{bmatrix}
-1.5 \\
0.25 \\
\frac{10\pi}{3}
\end{bmatrix}.
$$

El sistema de ecuaciones diferenciales es

$$
\begin{bmatrix}
x_1'(\lambda) \\
x_2'(\lambda) \\
x_3'(\lambda)
\end{bmatrix}
=
\begin{bmatrix}
3 & x_3 \sin(x_2 x_3) & x_2 \sin(x_2 x_3) \\
2x_1 & -162(x_2 + 0.1) & \cos(x_3) \\
-x_2 e^{-x_1 x_2} & -x_1 e^{-x_1 x_2} & 20
\end{bmatrix}^{-1}
\begin{bmatrix}
-1.5 \\
0.25 \\
\frac{10\pi}{3}
\end{bmatrix}.
$$




En general, el sistema de ecuaciones diferenciales que necesitamos resolver para nuestro problema de continuación tiene la forma:

$$
\begin{aligned}
\frac{dx_1}{d\lambda} &= \phi_1(\lambda, x_1, x_2, \ldots, x_n), \\
\frac{dx_2}{d\lambda} &= \phi_2(\lambda, x_1, x_2, \ldots, x_n), \\
&\vdots \\
\frac{dx_n}{d\lambda} &= \phi_n(\lambda, x_1, x_2, \ldots, x_n),
\end{aligned}
$$

donde

$$
\begin{bmatrix}
\phi_1(\lambda, x_1, \ldots, x_n) \\
\phi_2(\lambda, x_1, \ldots, x_n) \\
\vdots \\
\phi_n(\lambda, x_1, \ldots, x_n)
\end{bmatrix}
= -J(x_1, \ldots, x_n)^{-1}
\begin{bmatrix}
f_1(x(0)) \\
f_2(x(0)) \\
\vdots \\
f_n(x(0))
\end{bmatrix}.
\quad \quad (**)
$$


## Método de Runge-Kutta
Para usar el método de Runge-Kutta de cuarto orden para resolver este sistema, primero elegimos un entero $N > 0$ y dejamos que $h = 1 / N$. Particionamos el intervalo $[0, 1]$ en $N$ subintervalos con los puntos de malla

$$
\lambda_j = jh, \quad \text{para cada} \quad j = 0, 1, \ldots, N.
$$

Usamos la notación $w_{i,j}$, para cada $j = 0, 1, \ldots, N$ e $i = 1, \ldots, n$, para denotar una aproximación a $x_i(\lambda_j)$. Para las condiciones iniciales, fijamos

$$
w_{1,0} = x_1(0), \quad w_{2,0} = x_2(0), \quad \ldots, \quad w_{n,0} = x_n(0).
$$

Supongamos que $w_{1,j}, w_{2,j}, \ldots, w_{n,j}$ han sido calculados. Obtenemos $w_{1,j+1}, w_{2,j+1}, \ldots, w_{n,j+1}$ usando las ecuaciones

$$
\begin{aligned}
k_{1,i} &= h \phi_i (\lambda_j, w_{1,j}, w_{2,j}, \ldots, w_{n,j}), \quad \text{para cada} \quad i = 1, 2, \ldots, n; \\
k_{2,i} &= h \phi_i \left( \lambda_j + \frac{h}{2}, w_{1,j} + \frac{1}{2} k_{1,1}, \ldots, w_{n,j} + \frac{1}{2} k_{1,n} \right), \quad \text{para cada} \quad i = 1, 2, \ldots, n; \\
k_{3,i} &= h \phi_i \left( \lambda_j + \frac{h}{2}, w_{1,j} + \frac{1}{2} k_{2,1}, \ldots, w_{n,j} + \frac{1}{2} k_{2,n} \right), \quad \text{para cada} \quad i = 1, 2, \ldots, n; \\
k_{4,i} &= h \phi_i \left( \lambda_j + h, w_{1,j} + k_{3,1}, \ldots, w_{n,j} + k_{3,n} \right), \quad \text{para cada} \quad i = 1, 2, \ldots, n;
\end{aligned}
$$

y, finalmente,

$$
w_{i,j+1} = w_{i,j} + \frac{1}{6} \left( k_{1,i} + 2k_{2,i} + 2k_{3,i} + k_{4,i} \right), \quad \text{para cada} \quad i = 1, 2, \ldots, n.
$$

La notación vectorial

$$
\mathbf{k_1} = 
\begin{bmatrix}
k_{1,1} \\
k_{1,2} \\
\vdots \\
k_{1,n}
\end{bmatrix},
\quad
\mathbf{k_2} = 
\begin{bmatrix}
k_{2,1} \\
k_{2,2} \\
\vdots \\
k_{2,n}
\end{bmatrix},
\quad
\mathbf{k_3} = 
\begin{bmatrix}
k_{3,1} \\
k_{3,2} \\
\vdots \\
k_{3,n}
\end{bmatrix},
\quad
\mathbf{k_4} = 
\begin{bmatrix}
k_{4,1} \\
k_{4,2} \\
\vdots \\
k_{4,n}
\end{bmatrix},
\quad
\mathbf{w_j} = 
\begin{bmatrix}
w_{1,j} \\
w_{2,j} \\
\vdots \\
w_{n,j}
\end{bmatrix}
$$

simplifica la presentación. Entonces, la Ecuación $(**)$ nos da $x(0) = x(\lambda_0) = \mathbf{w_0}$, y para cada $j = 0, 1, \ldots, N,$

$$
\mathbf{k_1} = h
\begin{bmatrix}
\phi_1(\lambda_j, w_{1,j}, \ldots, w_{n,j}) \\
\phi_2(\lambda_j, w_{1,j}, \ldots, w_{n,j}) \\
\vdots \\
\phi_n(\lambda_j, w_{1,j}, \ldots, w_{n,j})
\end{bmatrix}
= h [-J(w_j)]^{-1} F(x(0)),
$$

$$
\mathbf{k_2} = h \left[ -J \left( w_j + \frac{1}{2} \mathbf{k_1} \right) \right]^{-1} F(x(0)),
$$

$$
\mathbf{k_3} = h \left[ -J \left( w_j + \frac{1}{2} \mathbf{k_2} \right) \right]^{-1} F(x(0)),
$$

$$
\mathbf{k_4} = h \left[ -J \left( w_j + \mathbf{k_3} \right) \right]^{-1} F(x(0)),
$$

y
$$
x(\lambda_{j+1}) = x(\lambda_j) + \frac{1}{6} (\mathbf{k_1} + 2 \mathbf{k_2} + 2 \mathbf{k_3} + \mathbf{k_4}) = \mathbf{w_j} + \frac{1}{6} (\mathbf{k_1} + 2 \mathbf{k_2} + 2 \mathbf{k_3} + \mathbf{k_4}).
$$

Finalmente, $x(\lambda_N) = x(1)$ es nuestra aproximación a $x^*$.
