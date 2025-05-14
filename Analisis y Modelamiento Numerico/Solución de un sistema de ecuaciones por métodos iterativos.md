
# Conceptos básicos
Un tipo general de proceso iterativo para resolver el sistema 
$$Ax = b \quad \quad  (1) $$ puede describirse como sigue: Se prescribe una cierta matriz Q, llamada matriz de partición, y el problema original se reescribe en la forma equivalente.
$$ Qx = (Q-A)x + b \quad \quad (2)$$
Esta ecuación sugiere un proceso iterativo, definido como
$$ Qx^{(k)} = (Q-A)x^{(k-1)} + b \quad \quad (k \geq 1) \quad \quad (3) $$
El vector inicial $x^{(0)}$ puede ser arbitrario, si se cuenta con una buena estimación de la solución, debería utilizarse para $x^{(0)}$. El método iterativo en la ecuación (3) converge si converge para cualquier valor inicial $x^{(0)}$. 

Una secuencia de vectores $x^{(1)}, x^{(2)}, ...$ pueden ser calculador a partir de la ecuación (3), y nuestro objetivo es elegir un $Q$ tal que se cumplan estas dos condiciones

1. La secuencia $[x^{(k)}]$ se calcula fácilmente.
2. La secuencia $[x^{(k)}]$ converge rápidamente a una solución.

Ambas condiciones se cumplen si es fácil de calcular $Qx^{(k)} = y$ y si $Q^{-1}$ se aproxima a $A^{-1}$

![[Pasted image 20240501180612.png]]
Repitiendo el paso (9), eventualmente llegamos a la desigualdad
$$ \|x^{(k)} - x \| \leq \|I - Q^{-1}A \|^k  \|x^{(0)} - x \| $$
Por tanto, si $\|I - Q^{-1}A \| <1$, podemos concluir que $\underset{k \to \infty}{lim} \|x^{(k)} - x \| = 0$ para algún $x^{(0)}$

# Teorema 1: Teorema sobre la convergencia de métodos iterativos
Si $\|I - Q^{-1}A \| <1$ para alguna norma matricial subordinada, entonces la secuencia producida por (3) converge a la solución de $Ax = b$ para cualquier vector inicial $x^{(0)}$.


# Método de Richardson
En este método se elige a la identidad $I$ como $Q$. Entonces la ecuación (3) queda de la siguiente forma
$$ x^{(k)} = (I-A)x^{(k-1)} + b = x^{(k-1)} + r^{(k-1)}  \quad \quad (12)$$
donde $r^{(k-1)}$ es el **vector residual** definido por $r^{(k-1)} = b - Ax^{(k-1)}$

## Convergencia

- La iteración de Richardson producirá una solución a $Ax = b$ en el límite si $\|I-A\| \leq 1$ para alguna norma matricial subordinada. $\rho(I-A) < 1$.

- Si la matriz $A$ tiene la siguiente propiedad, $a_{ii} = 1 > \sum_{j = 1, j \neq i}^n |a_{ij}|$ , es decir,  si es diagonalmente dominante unitaria por filas, entonces la iteración de Richardson es exitosa

- Si la matriz $A$ es diagonalmente dominante unitaria por columnas, $a_{jj} = 1 > \sum_{i = 1, i \neq j}^n |a_{ij}|$ entonces la iteración de Richardson es exitosa


Para un sistema de $n \times n$ el método de Richardson se escribe como
$$ x_i^{(k+1)} = x_i^{(k)} - \sum_{j=1}^n a_{ij}x_j^{(k)} + b_i \: ,  \quad i = 1, \dots, n \quad k = 0, \dots  .$$


# Método de Jacobi
En este tipo de iteración se elige a $Q$ como una matriz diagonal cuyos valores para su diagonal son los mismos que en la matriz $A$. En este caso, el elemento genérico para $Q^{-1}A$ es $a_{ij}/a_{ii}$. La diagonal de $Q^{-1}A$ son todos unos, y
$$ \|I - Q^{-1}A \|_{\infty} = \underset{1 \leq i \leq n}{max} \underset{\begin{matrix} j = 1 \\ j \neq i\end{matrix}}{\sum^n} \left| \frac{a_{ij}}{a_{ii}} \right| \quad \quad (13) $$

El **método iterativo de Jacobi** se obtiene al resolver la *i-ésima* ecuación en $Ax = b$ para $x_i$
para obtener (siempre que $a_{ii} \neq 0$)
![[Pasted image 20240507114913.png]]

En general, las técnicas iterativas para resolver sistemas lineales implican un proceso que convierte el sistema $Ax = b$ en un sistema equivalente de la forma $x = T x+c$ para una
matriz fija $T$ y vector $c$. Después de seleccionar el vector inicial $x^{(0)}$, la sucesión de los vectores solución aproximados se generan al calcular
$$ x^{(k)} = Tx^{(k-1)} + c  $$
para cada $k = 1, 2, 3 \cdots$

El método de Jacobi se puede escribir en la forma $x^{(k)} = Tx^{(k-1)} +c$ al dividir $A$ en sus
partes diagonal o fuera de la diagonal. Para observar esto, permita que $D$ sea la matriz diagonal cuyas entradas diagonales sean las de $A$, $-L$ es la parte estrictamente triangular inferior de $A$ y $-U$ es la parte estrictamente triangular superior de $A$. Con esta notación,

$$
A = 
\begin{pmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
a_{21} & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{n1} & a_{n2} & \cdots & a_{nn} \\
\end{pmatrix}

$$

$$
A = 
\begin{pmatrix}
a_{11} & 0 & \cdots & 0 \\
0 & a_{22} & \cdots & 0 \\
\vdots & \vdots & \ddots & \vdots \\
0 & 0 & \cdots & a_{nn} \\
\end{pmatrix}
-
\begin{pmatrix}
0 & 0           & \cdots & 0 \\
-a_{21} & 0       & \cdots & 0 \\
\vdots & \vdots & \ddots & \vdots \\
-a_{n1} & -a_{n2} & \cdots   & 0 \\
\end{pmatrix}

-
\begin{pmatrix}
0 &  -a_{12}       & \cdots & -a_{1n} \\
0 & 0  & \cdots & -a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
0 & 0 & \cdots   & 0 \\
\end{pmatrix}

$$

$$ A = D - L - U $$
![[Pasted image 20240507122114.png]]
Al introducir la notación $T_j = D^{-1}(L + U)$ y $c_j = D^{-1}b$, obtenemos la forma de la técnica de Jacobi
$$ x^{(k)} = T_jx^{(k-1)} + c_j \quad \quad \text{(7.7)}$$
En la práctica, la ecuación (7.5) se usa en el cálculo y la ecuación (7.7) para propósitos teóricos.

## Algoritmo de Jacobi

![[Pasted image 20240507123159.png]]


## Teorema sobre la convergencia del método de Jacobi
SI $A$ es **diagonalmente dominante** entonces la secuencia producida por la iteración de Jacobi converge a la solución de $Ax=b$ para cualquier vector inicial

### Prueba
Diagonal dominante significa

$$
|a_{ii}| > \sum_{\begin{aligned} j &= 1 \\ j &\neq i\end{aligned}}^n |a_{ij}| \quad \quad (1 \leq i \leq n)
$$

Como 
$$
\| I - Q^{-1}A \|_{\infty} = \underset{1 \leq i \leq n}{\text{max}} \sum_{\begin{aligned} j &= 1 \\ j &\neq i\end{aligned}}^n \left| \frac{a_{ij}}{a_{ii}} \right|
$$
Concluimos que 
$$
\| I - Q^{-1} A\|_{\infty} < 1
$$
Por el [[#Teorema 1 Teorema sobre la convergencia de métodos iterativos|teorema sobre la convergencia]], la iteración de Jacobi converge.


# Análisis

## Teorema sobre las condiciones suficientes y necesarias para la convergencia de un método iterativo
Para que la fórmula de iteración
$$ x^{(k)} = Gx^{(k-1)} + c $$
produzca una secuencia que converja a $(𝐼−𝐺)^{-1}𝑐$ para cualquier vector inicial $𝑥^{(0)}$, es necesario y suficiente que el radio espectral de $G$ sea menor que 1, $\rho(G) < 1$

![[Pasted image 20240501221243.png]]
![[Pasted image 20240501221255.png]]

## Corolario 1
La formula de iteración (3) producirá una secuencia convergiendo a la solución de $Ax=b$ para cualquier $x^{(0)}$ si $\rho(I - Q^{-1}A) <1$

# Método Gauss-Seidel
En este método se elige a $Q$ como la matriz triangular inferior de $A$ incluyendo su diagonal.

![[Pasted image 20240507123645.png]]
Con las definiciones de $D$, $L$ y $U$ proporcionadas previamente, tenemos el método Gauss-Seidel representado por 
$$ (D-L)x^{(k)} = Ux^{(k-1)} + b $$
y 
$$ x^{(k)} = (D-L)^{-1}Ux^{(k-1)} + (D-L)^{-1}b  $$
para cada $k=1, 2, \dots$ .
Si permitimos que $T_g = (D-L)^{-1}U$ y $c_g = (D-L)^{-1}b$, obtenemos la técnica de Gauss-Seidel de la forma
$$ x^{(k)} = T_gx^{(k-1)} + c_g $$
Para la matriz triangular inferior $D-L$ no singular, es necesario y suficiente que $a_ii \neq 0$ para cada $i = 1, 2, \dots, n$.

## Algoritmo Gauss-Seidel
![[Pasted image 20240507125957.png]]

## Teorema sobre la convergencia del método de Gauss-Seidel
Si $A$ es diagonalmente dominante, entonces el método de Gauss-Seidel converge para cualquier vector inicial

![[Pasted image 20240501224937.png]]
![[Pasted image 20240501224951.png]]


# Métodos de iteración general
Para estudiar la convergencia de técnicas de iteración general, necesitamos analizar la fórmula
$$ x^{(k)} = Tx^{(k-1)} + c$$
para cada $k = 1, 2, \dots, n$. Donde $x^{(0)}$ es arbitraria.


## Lema
Si el radio espectral satisface $\rho(T) < 1$, entonces $(I-T)^{-1}$ existe y
$$ (I-T)^{-1} = \sum_{j=0}^{\infty} T^j $$
### Demostración
Por el [[Valores y vectores propios#Teorema sobre el radio espectral|teorema sobre el radio espectral]] se tiene que $\rho(T) < \|T\|$ para cualquier norma $\|\cdot\|$ y por el [[#Teorema sobre la serie de Neumann]] se cumple el lema. 
![[Pasted image 20240507150032.png]]


## Teorema 
Para cualquier $x^{(0)} \in \mathbb{R}^n$, la sucesión $\{x^{(k)}\}_{k=0}^{\infty}$ definida por
$$ x^{(k)} = Tx^{(k-1)} + c $$
para cada $k \geq 1$, converge a la solución única de $x = Tx + c$ si y solo si $\rho(T) < 1$
![[Pasted image 20240507160139.png]]
![[Pasted image 20240507160157.png]]



# Técnicas de relajación para la solución de sistemas de ecuaciones lineales

## Vector residual
Suponga que $\tilde{x} \in \mathbb{R}$ es una aproximación de la solución del sistema lineal definido por $Ax=b$. El vector residual para $\tilde{x}$ respecto del sistema es $r=b-A\tilde{x}$.

## Métodos de relajación (SOR)
En procedimientos como el método de Jacobi o el método de Gauss-Seidel, un vector residual esta asociado con cada cálculo de un componente aproximado del vector solución. El  verdadero objetivo es generar una secuencia de aproximaciones que causen que el vector residual converja rápidamente a cero. Supongamos que 
$$ r^{(k)}_i = (r^{(k)}_{1i}, r^{(k)}_{2i}, \dots, r^{(k)}_{ni})^t $$
denota el vector residual para el método de Gauss-Seidel correspondiendo al vector solución aproximada $x^{(k)}_i$ definido por
$$  x^{(k)}_i = (x^{(k)}_{1}, x^{(k)}_{2}, \dots, x^{(k)}_{i-1}, x^{(k-1)}_{i}, \dots, x^{(k-1)}_{n})^t  $$

![[Pasted image 20240513112825.png]]
![[Pasted image 20240513112900.png]]
Entonces para ciertas elecciones de $\omega$ positivo podemos reducir la norma del vector residual y obtener significativamente una convergencia más rápida.

Los métodos que involucran la ecuación (7.17) se denominan **métodos de relajación**. Para elecciones de $\omega$ con $0<\omega <1$ los procedimiento se denominan **under-relaxation methods**. Si $1<\omega$ se denominan **over-relaxation methods**. Estos son usados para acelerar la convergencia para sistemas que son convergentes por la técnica de Gauss-Seidel. Los métodos son abreviados a **SOR** (*Successive Over-Relaxation*).

![[Pasted image 20240513113715.png]]
![[Pasted image 20240513113730.png]]


## Valores apropiados para $\omega$

### Teorema de Kahan
Si $a_{ii} \neq 0$ para cada $i=1, 2, \dots, n$, entonces $\rho(T_{\omega}) \geq |\omega - 1|$. Esto implica que el método **SOR** converge si y solo si $0<\omega <2$. Donde $T_{\omega} = (D-\omega L)^{-1}[(1-\omega)D + \omega U]$

### Teorema de Ostrowski-Reich
Si $A$ es una matriz definida positiva y $0 < \omega <2$ , entonces el método **SOR** converge para cualquier elección de un vector aproximado $x^{(0)}$.

### Teorema
Si $A$ es definida positiva y tridiagonal, entonces $\rho(T_g) = [\rho(T_j)]^2<1$, y la elección óptima de $\omega$ para el método **SOR** es
$$ \omega = \frac{2}{1+ \sqrt{1-[\rho(T_j)]^2}} $$
con esta elección para $\omega$ tenemos que $\rho(T_{\omega}) = \omega - 1$.

## Algoritmo para el método SOR

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Analisis y Modelamiento Numerico\imgs\Algoritmo SOR.png" alt="">
    <figcaption>Algoritmo SOR I</figcaption>
    </figure>
</div>

