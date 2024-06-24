
# Teorema del valor intermedio
El Teorema del Valor Intermedio establece que si $f$ es una función continua en el intervalo cerrado $[a, b]$ y $N$ es un número real tal que $f(a) \leq N \leq f(b)$ o $f(b) \leq N \leq f(a)$, entonces existe al menos un número $c$ en $(a, b)$ tal que:
$$
f(c) = N
$$
## Notación matemática
$$
\forall f \in C([a, b]), \: \exists \,c \in (a, b) : f(c) = N, \ \text{  si  } \ \ f(a) \leq N \leq f(b)
$$

## Interpretación geométrica

Geométricamente, el Teorema del Valor Intermedio afirma que si dibujamos la gráfica de una función continua entre dos puntos $(a, f(a))$  y  $(b, f(b))$, y trazamos una línea horizontal en cualquier punto entre $f(a)$ y $f(b)$, esta línea intersecará la gráfica de la función al menos una vez.




# Teorema de Rolle
Sea $f:[a, b]$ una función continua en $[a, b]$ y derivable en $\langle a, b\rangle$. Si $f(a)=f(b)$, entonces existe $x_0 \in \langle a, b \rangle$ tal que $f'(x_0)=0$.

## Demostración
Si $f$ es constante en $[a; b]$, entonces para cada $x_0 \in \langle a; b \rangle$ se cumple que $f'(x_0) = 0$.

Supongamos que $f$ no es constante en $[a, b]$. Como $f$ es continua en $[a, b]$, entonces $f$ alcanza sus valores máximos y mínimos en $[a, b]$. Supongamos que $f$ alcanza su valor mínimo en $x_1$ y su valor máximo en $x_2$. Luego, uno de ellos debe estar en $\langle a; b \rangle$, pues si ambos estuvieran en el conjunto $\{a, b\}$ de la condición $f(a) = f(b)$ se tendría que $f$ es constante.

Supongamos que $x_1 \in \langle a, b \rangle$. Luego, se tiene $f(x_1) \le f(x)$, $\forall x \in [a, b]$ 

$$
\frac{f(x)-f(x_1)}{x-x_1} \le 0, \quad \forall x \in [a, x_1]
$$
y como $f$ es derivable en $x_1$, entonces

$$
\lim_{x \to x_1^-} \frac{f(x) - f(x_1)}{x - x_1} \le 0
$$

lo que implica que $f'(x_1) = f'(x_1) \le 0$.

De la misma forma
$$
\forall x \in \langle x_1, b \ ] \ \ \text{se tiene} \ \ \frac{f(x)-f(x_1)}{x-x_1} \ge 0
$$
y como $f$ es derivable en $x_1$, entonces
$$
\lim_{x \to x_1^+} \frac{f(x) - f(x_1)}{x - x_1} \ge 0
$$

lo que implica que $f^{'}_+ (x_1) = f'(x_1) \geq 0$
Así, se tiene que $f'(x_1)=0$.
Si $x_2 \in (a, b)$, la prueba es similar.


## Teorema Generalizado de Rolle

Supongamos que $f \in C[a, b]$ es $n$ veces diferenciable en $(a, b)$. Si $f(x) = 0$ en los $n + 1$ números distintos $a \leq x_0 < x_1 < \ldots < x_n \leq b$, entonces existe un número $c$ en $(x_0, x_n)$ y, por lo tanto, en $(a, b)$ tal que $f^{(n)}(c) = 0$.
# Aplicaciones de la derivada


## Punto crítico
Sea $f : X \rightarrow \mathbb{R}$ y $x_0 \in X$. Decimos que $x_0$ es un **punto crítico** de $f$ si $f$ es diferenciable en $x_0$ y $f'(x_0)=0$.

> No todos los valores extremos de una función se dan en puntos críticos


## Función convexa
Sea $I$ un intervalo y $f : I \rightarrow \mathbb{R}$ diremos que $f$ es **convexa** en $I$ si para todo par de puntos $x_1 , x_2 \in I$ y para cualquier $0 \leq t \leq 1$ se cumple que

$$
f(tx_1 + (1-t)x_2)  \ \leq \ tf(x_1) + (1-t)f(x_2)
$$

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Analisis y Modelamiento Numerico\imgs\convexa.png" alt="" width=400>
    <figcaption>Funcion convexa</figcaption>
    </figure>
</div>

## Función cóncava
Sea $I$ un intervalo y $f : I \rightarrow \mathbb{R}$ diremos que $f$ es **cóncava** en $I$ si para todo par de puntos $x_1 , x_2 \in I$ y para cualquier $0 \leq t \leq 1$ se cumple que

$$
f(tx_1 + (1-t)x_2) \ \geq \ tf(x_1) + (1-t)f(x_2)
$$

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Analisis y Modelamiento Numerico\imgs\concava.png" alt="" width=400>
    <figcaption>Funcion cóncava</figcaption>
    </figure>
</div>


# Serie de Taylor
Si una función $f$ posee una derivada continua de orden $(n+1)$ en un intervalo $(c-\delta, c + \delta)$, entonces
$$
f(x) = p_n(x) + E_n(x)
$$
donde $p_n$ es un polinomio de grado $\leq n$ y $E_n$ es la función *residuo*. Estos se definen como

$$
\begin{aligned}
p_n(x) &= \sum_{k=0}^{n} \frac{1}{k!} f^{(k)}(c)(x-c)^k \\ \\
E_n(x) &= \frac{1}{(n+1)!} f^{(n+1)}(\xi_x)(x-c)^{(n+1)} \quad \quad |\xi_x -c|<\delta \\
\end{aligned}
$$
Un caso muy importante tiene lugar cuando $c=0$, esta serie se conoce como **serie de Maclaurin**.
Usando el teorema de Taylor junto con un análisis de $E_n(x)$ conforme $n \rightarrow \infty$, obtenemos la serie de Taylor para muchas funciones importantes, como:

$$
\begin{aligned}
cos(x) &= \sum_{k=0}^{\infty}(-1)^k \frac{x^{2k}}{(2k)!} \quad \quad (-\infty < x < \infty) \\ \\
\frac{1}{x} &= \sum_{k=0}^{\infty}(-1)^k (x-1)^k \quad \quad (0 < x < 2)
\end{aligned}
$$
Estas series se conocen como **serie de potencias**.

## Teorema
Para toda serie de potencias
$$
\sum_{k=0}^{\infty} a_k(x-c)^k
$$
existe un número $r$ en el intervalo $[0, \infty]$ tal que la serie diverge para $|x-c|>r$ y converge para $|x-c|<r$.

El número $r$ (puede ser $+\infty$) se denomina **radio de convergencia** de la serie. Con frecuencia puede calcularse mediante el *criterio de la razón*.