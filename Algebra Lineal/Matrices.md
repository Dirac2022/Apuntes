

# Multiplicación de matrices

## Multiplicación por un vector
Sea $A \in R^{m \times n}$ y $x \in R^n$ entonces $Ax \in R^n$   y es combinación lineal de las columnas de $A$. Es decir $Ax$ pertenece al espacio columna de $A$.

$$
\begin{aligned}
\begin{bmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
a_{21} & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{m1} & a_{m2} & \cdots & a_{mn}
\end{bmatrix}

\begin{bmatrix}
x_1 \\
x_2 \\
\vdots \\
x_n
\end{bmatrix}
 &=
 \begin{bmatrix}
a_{11}x_1 & a_{12}x_2 & \cdots & a_{1n}x_n \\
a_{21}x_1 & a_{22}x_2 & \cdots & a_{2n}x_n \\
\vdots & \vdots & \ddots & \vdots \\
a_{m1}x_1 & a_{m2}x_2 & \cdots & a_{mn}x_n
\end{bmatrix} \\ \\
&=
\begin{bmatrix}
x_1
\begin{pmatrix}
a_{11} \\
a_{21} \\
\vdots \\
a_{m1}
\end{pmatrix}
&
x_2
\begin{pmatrix}
a_{12} \\
a_{22} \\
\vdots \\
a_{m2}
\end{pmatrix}
&
\cdots
&
x_n
\begin{pmatrix}
a_{1n} \\
a_{2n} \\
\vdots \\
a_{mn}
\end{pmatrix}

\end{bmatrix}
\end{aligned}
$$

Es decir
$$
Ax = x_1A^1 + x_2A^2 + \dots + x_nA^n
$$
Donde $A^j$ es la $j$-ésima columna de $A$.


## Multiplicación por una matriz
Sea $A \in R^{m \times n}$ y $B \in R^{n \times p}$ entonces $C = AB \in R^{m \times p}$   y los vectores columna de $C$ son combinaciones lineales de los vectores columna de $A$, es decir cada vector columna de $C$ pertenece al espacio columna de $A$. 


# Matriz transpuesta

Una matriz $A^T$ es la matriz transpuesta de una matriz $A$ de orden $m \times n$, si las filas de $A^T$ son las columnas de A y las columnas de $A^T$ son las filas de A, invirtiendo el orden.

$$ A = [a_{ij}]_{m \times n} \leftrightarrow A^T = [a_{ji}]_{n \times m} $$
Ejemplo
$$
A = \begin{bmatrix}
1 & 2 & 3 \\
4 & 5 & 6
\end{bmatrix}

\quad \quad
A^T = \begin{bmatrix}
1 & 4 \\
2 & 5 \\
3 & 6
\end{bmatrix}
$$
## Propiedades
Sean $A$, $B$ matrices y $k$ un escalar, entonces
1. $(A^T)^T = A$
2. $(A + B)^T = A^T + B^T$
3. $(kA)^T = kA^T$
4. $(AB)^T = B^TA^T$
5. Si $A^{-1}$ existe, entonces $(A^{-1})^T = (A^T)^{-1}$


# Inversa de una matriz

## Teorema
La matriz cuadrada $A_n$ tiene inversa si y solo si $|A| \neq 0$. En este caso dicha inversa es única y se denota por $A^{-1}$. 
## Propiedades
Sean $A, B  \in \mathbb{R}^{n \times n}$ matrices invertibles y $\lambda \in \mathbb{R}$, $\lambda \neq 0$ , se cumplen las siguientes propiedades.

1. $(A^{-1})^{-1} = A$
2. $\lambda A$ es invertible y $(\lambda A)^{-1} = \lambda^{-1} A^{-1}$
3. $(AB)^{-1} = B^{-1}A^{-1}$
4. $A^T$ es invertible y $(A^T)^{-1} = (A^{-1})^{T}$
5. $A^n$ es invertible para todo $n$ no negativo y $(A^n)^{-1} = (A^{-1})^n$

## Cálculo de la inversa de una matriz
Para calcular la inversa de una matriz $A_n$ primero construimos la matriz
$$ [A \ | \ I_n] $$
Usando [[Sistemas de ecuaciones lineales#Eliminación Gaussiana|eliminación gaussiana]] es posible reducir la matriz a la forma
$$ [ I_n \ | \ A^{-1}] $$

# Rango
El rango es una función que asigna a una matriz el número de [[#^77d55a|pivotes]] de la matriz reducida obtenida al aplicar [[Sistemas de ecuaciones lineales#Eliminación Gaussiana|eliminación gaussiana]]. Denotamos este número por $rango(A)$.


# Matriz Hermitiana
Sea $M = (m_{ij})$ una matriz de $m \times n$ con $m_{ij} = a_{ij} + ib_{ij}$. Es decir
$$M = A + iB$$
donde $A$ y $B$ tienen entradas reales.

$\overline{M}$ es la matriz formada por la conjugada de todas las entradas de $M$. La transpuesta de $\overline{M}$ se denota como $M^H$. El espacio vectorial de todas las matrices $m \times n$ con entradas complejas se denota como $C^{m \times n}$. Si $A$ y $B$ son elementos de $C^{m \times n}$ y $C \in C^{m \times r}$, se cumplen las siguientes propiedades

- $(A^H)^H = A$
- $(\alpha A + \beta B)^H = \overline{\alpha}A^H + \overline{\beta}B^H$
- $(AC)^H = C^HA^H$

Se dice que $M$ es **Hermitiana** si $M = M^H$

## Teorema
Los valores propios de una matriz hermitiana son todos reales. Además, los vectores que corresponden a distintos valores propios son ortogonales.
![[Pasted image 20240424164725.png]]

Continuar libro Algebra Lineal Aplicada

## Matriz unitaria
Una matriz $U_{n \times n}$ se dice que es **unitaria** si sus vectores columna forman un conjunto ortonormal en $\mathbb{C}^n$.

Por tanto, $U$ es unitaria si y solo si $U^HU = I$.
Una matriz unitaria real es una matriz ortogonal.

## Corolario
Si los valores propios de una matriz hermitiana $A$ son distintos, entonces existe una matriz unitaria $U$ tal que diagonalize $A$.

Let $\textbf{x}_i$ be an eigenvector belonging to $\lambda_i$ for each eigenvalue $\lambda_i$ of $A$. Let $\textbf{u}_i = ( 1 / \| \textbf{x}_i \| ) \textbf{x}_i$. Thus, $\textbf{u}_i$ is a unit eigenvector belonging to $\lambda_i$ for each $i$. It follows from Theorem 6.4.1 (Burden pag 357) that ${\textbf{u}_i, \dots, \textbf{u}_n}$ is an orthonormal set in $\mathbb{C}^n$. Let $U$ be the matrix whose $i$th column vector is $\textbf{u}_i$ for each $i$; then $U$ is unitary and $U$ is unitary and $U$ diagonalizes $A$.


# Matrices semejantes
Sean $A$ y $B$ dos matrices, decimos que $A$ y $B$ son semejantes si existe una matriz $P$ no singular tal que 
$$ B = PAP^{-1} $$

## Teorema sobre los valores propios de matrices semejantes
Matrices semejantes tienen los mismos valores propios


# Matriz Menor
Si $A_n$ es una matriz cuadrada, la matriz menor ($i, j$) de $A$, denotada por $M_ij$ se define como la matriz de orden $(n-1) \times (n-1)$ que resulta de eliminar la $i$-ésima fila y $j$-ésima columna.
## Menor principal de una matriz
Un **menor principal** de una matriz es el determinante de alguna submatriz cuadrada que se obtiene seleccionando un conjunto igual de filas y columnas desde la matriz original. Lo particular de los menores principales es que siempre involucran las filas y columnas desde el primer elemento hasta un elemento en la diagonal principal de la matriz.
### Formulación Matemática
Si tienes una matriz $A$ de tamaño $n \times n$, un menor principal de orden $k$ (con $1 \leq k \leq n$) se define como el determinante de la submatriz que se forma tomando las primeras $k$ filas y$k$ columnas de $A$. Esta submatriz es denotada como $A_k$.

### Notación Matemática
$$
A_k = \begin{bmatrix}
a_{11} & a_{12} & \cdots & a_{1k} \\
a_{21} & a_{22} & \cdots & a_{2k} \\
\vdots & \vdots & \ddots & \vdots \\
a_{k1} & a_{k2} & \cdots & a_{kk} \\
\end{bmatrix}
$$

El menor principal es entonces $\text{det}(A_k)$.

### Aplicación
Una matriz es definida positiva si todos sus menores principales son positivos.

# Matriz escalonada
1. Una matriz se dice nula cuando todos sus elementos son ceros.
2. El pivote de una fila no nula es el primer elemento no nulo de dicha fila. ^77d55a
3. Una matriz se dice escalonada cuando cumple las siguientes condiciones:
	- Las filas nulas están por debajo de las filas no nulas.
	- El pivote de cada fila está a la derecha del pivote de la fila anterior.

**Ejemplo**

$$ A = 
\begin{pmatrix}
1 & 0 & 7 & 1 \\
0 & 2 & 6 & 0 \\
0 & 0 & 0 & 4 \\
0 & 0 & 0 & 0
\end{pmatrix}
$$
Es una matriz escalonada.


## Matriz Reducida
Una matriz [[#Matriz escalonada|escalonada]] es reducida cuando se cumple que 
1. Todos los pivotes son iguales a 1.
2. Los otros elementos de una columna que contiene un pivote son ceros.

**Ejemplo**

$$
A = 
\begin{pmatrix}
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
0 & 0 & 0 & 1 \\
0 & 0 & 0 & 0
\end{pmatrix}
$$
Es una matriz escalonada reducida.

# Operaciones elementales

## Teorema
Dos matrices son **equivalentes** por filas cuando realizando operaciones elementales en una tiene como resultado la otra.

## Teorema
Toda matriz es equivalente por filas a una única [[#Matriz Reducida|matriz reducida]].



# 📜 Teorema Espectral

## Enunciado
Sea $A \in \mathbb{R}^{n \times n}$ una matriz **simétrica real** ($A = A^T$).  
Entonces:
- Todos los **autovalores** de $A$ son **reales**.
- $A$ es **diagonalizable** mediante una **matriz ortogonal** $Q$, es decir:

$$
A = Q \Lambda Q^T
$$

donde:
- $Q \in \mathbb{R}^{n \times n}$ tiene columnas ortonormales ( $Q^T Q = I$ ),
- $\Lambda$ es diagonal, con los autovalores de $A$ en su diagonal.

---

## 📚 Explicación Intuitiva

El teorema dice que **toda matriz simétrica real se puede "alinear" perfectamente a un sistema de coordenadas ortonormal** donde su acción (multiplicación) se comporta simplemente como un **escalado** a lo largo de esas direcciones especiales (sus autovectores).

En otras palabras:  
Matriz simétrica → puedes encontrar un conjunto de vectores perpendiculares que la "diagonalizan".

---

## 🛠️ Demostración detallada

### 1. Los autovalores de una matriz simétrica real son reales

Supongamos que $\lambda$ es un autovalor de $A$ con autovector $v \neq 0$:

$$
A v = \lambda v
$$

Multiplicamos a izquierda por $v^T$:
$$
v^T A v = \lambda v^T v
$$

Pero usando la simetría de $A$:

$$
v^T A v = (A v)^T v = (\lambda v)^T v = \lambda v^T v
$$

- $v^T v$ es un número real positivo (es el cuadrado de la norma de $v$),
- Entonces $\lambda$ debe ser real.

✅ Conclusión: los autovalores son reales.

---

### 2. Autovectores asociados a autovalores distintos son ortogonales

Supongamos $v$ y $w$ son autovectores de $A$ con autovalores $\lambda$ y $\mu$, respectivamente:

$$
A v = \lambda v, \quad A w = \mu w
$$

Tomamos:

$$
v^T A w
$$

De dos maneras:

Primero:

$$
v^T A w = v^T (\mu w) = \mu v^T w
$$

Segundo (usando simetría):

$$
v^T A w = (A v)^T w = (\lambda v)^T w = \lambda v^T w
$$

Entonces:

$$
\mu v^T w = \lambda v^T w
$$

Por lo tanto:

$$
(\mu - \lambda) v^T w = 0
$$

Si $\lambda \neq \mu$, necesariamente:

$$
v^T w = 0
$$

✅ Son ortogonales.

---

### 3. $A$ es diagonalizable ortogonalmente

- Los autovectores forman un conjunto ortogonal,
- Podemos normalizarlos para formar una base ortonormal,
- Entonces, existe una matriz ortogonal $Q$ tal que:

$$
Q^T A Q = \Lambda
\quad \Rightarrow \quad
A = Q \Lambda Q^T
$$

donde $\Lambda$ es diagonal, con los autovalores en la diagonal.

---

## 🎯 Resumen visual

$$
\boxed{\text{Matriz simétrica}} 
\quad \xrightarrow{\text{Base ortonormal de autovectores}} \quad
\boxed{Q^T A Q = \Lambda}
\quad \Rightarrow \quad
\boxed{A = Q \Lambda Q^T}
$$

---

## ⚡ Aplicaciones del Teorema Espectral

- **PCA:** La matriz de covarianza es simétrica; su diagonalización da los componentes principales.
- **Métodos numéricos:** Se aprovecha para cálculos estables.
- **Mecánica cuántica:** Observables representados como matrices hermíticas (versión compleja).
- **Optimización cuadrática:** El espectro de la Hessiana determina la forma de la función.





