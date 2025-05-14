
# Repaso de matrices
## Teorema de los sistemas equivalentes
Si un sistema de ecuaciones es obtenido de otro sistema de ecuaciones mediante una secuencia finita de operaciones elementales, entonces los dos sistemas son equivalentes


## Teorema de la inversa por la derecha
Una matriz cuadrada puede poseer a lo más una matriz inversa por la derecha

## Teorema de la matriz inversa
Si $A$ y $B$ son matrices cuadradas tal que $AB = I$ , entonces $BA=I$.

## Matriz elemental
Una matriz elemental se define como una matriz cuadrada $n\times n$ que se produce cuando se realiza una operación elemental a la matriz identidad $I_d$

## Teorema sobre las propiedades de matrices no singulares
Dada una matriz $n\times n$, las siguientes propiedades son equivalentes
1. Si la inversa de una matriz $A$ existe, $A$ es *no singular*.
2. El determinante de $A$ no es cero.
3. Las filas de $A$ forman una base para $\mathbb{R}$.
4. Las columnas de $A$ forman una base para $\mathbb{R}$.
5. Como una transformación lineal de $\mathbb{R}^n$ a $\mathbb{R}^n$, $A$ es inyectiva.
6. Como una transformación lineal de $\mathbb{R}^n$ a $\mathbb{R}^n$, $A$ es sobreyectiva.
7. La ecuación $Ax = 0$ implica que $x=0$.
8. Para cada $b \in \mathbb{R}^n$, existe exactamente un $x \in \mathbb{R}^n$ tal que $Ax=b$.
9. $A$ es un producto de matrices elementales.
10. $0$ no es un valor propio de $A$.


## Matriz definida positiva
Una matriz es **definida positiva** si $x^TAx > 0$ para todo vector $x$ diferente de $0$. La expresión $x^TAx$ es llamada **forma cuadrática**. Si $A$ es definida positiva y simétrica, entonces sus valores propios son reales y positivos.


## Matrices particionadas
Sean $A$, $B$ y $C$ matrices que han sido particionadas en submatrices.

$$ \begin{array}{cc} A = \begin{bmatrix} A_{11} & A_{12} & \cdots & A_{1n} \\ A_{21} & A_{22} & \cdots & A_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ A_{m1} & A_{m2} & \cdots & A_{mn} \\ \end{bmatrix} \hfill & B = \begin{bmatrix} B_{11} & B_{12} & \cdots & B_{1k} \\ B_{21} & B_{22} & \cdots & B_{2k} \\ \vdots & \vdots & \ddots & \vdots \\ B_{n1} & B_{n2} & \cdots & B_{nk} \\ \end{bmatrix} \end{array} $$
$$ C = \begin{bmatrix} C_{11} & C_{12} & \cdots & C_{1k} \\ C_{21} & C_{22} & \cdots & C_{2k} \\ \vdots & \vdots & \ddots & \vdots \\ C_{m1} & C_{m2} & \cdots & C_{mk} \\ \end{bmatrix} $$
### Teorema de la multiplicación de matrices particionadas
Si cada producto $A_{is}B_{sj}$ se puede formar y si $C_{ij} = \sum_{s=1}^{n} A_{is}B_{sj}$, entonces $C=AB$.


# Métodos directos
Un sistema de ecuaciones lineales tiene la forma
$$ \begin{bmatrix} a_{11} & a_{12} & \cdots & a_{1n} \\ a_{21} & a_{22} & \cdots & a_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ a_{m1} & a_{n2} & \cdots & a_{mn} \\ \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \\ \vdots \\ x_n \\ \end{bmatrix} = \begin{bmatrix} b_1 \\ b_2 \\ \vdots \\ b_m \\ \end{bmatrix} $$
Definiendo $A = (a_{ij}) \in \mathbb{R}^{m \times n}$ y $b = (b_i) \in \mathbb{R}^m$ resulta 
$$ Ax = b  \quad \quad (1) $$
### Matriz aumentada
Dado el sistema lineal $(1)$, definimos la matriz aumentada $M$ asociada al sistema lineal de la siguiente forma
$$ M = (A | b) $$

## Teorema de Frobenius
Garantiza la existencia y unicidad de la solución de un sistema de ecuaciones lineales
1. Si $rango(A) = rango(M)$ entonces el sistema tiene solución. Se subdivide en dos casos:
	1. Si $rango(A) = rango(B) < n$, entonces el sistema **tiene infinitas soluciones**. La solución general depende de $n-rango(A)$ variables libres.
	2. Si $rango(A) = rango(B) = n$, entonces el sistema **tiene una única solución**.
2. Si $rango(A) \neq rango(M)$, entonces el sistema **no tiene solución**.

## Operaciones elementales fila
Dada una matriz $A \in \mathbb{R}^{n\times n}$, definimos como operaciones elementales fila para la matriz $A$ a
cualquiera de las siguientes operaciones:
1. Intercambiar la fila $i$ con la fila $j$, denotado por $F_{ij}$ .
2. Asignar a la fila $i$ la misma fila $i$ pero multiplicada por un número no nulo $λ$. Esto es denotado por $F_i(λ)$.
3. Asignar a la fila $i$ la misma fila $i$ y sumándole $λ$ veces la fila $j$ donde $λ \neq 0$. Esto es denotado por $F_{ij}(λ)$.

## Eliminación de Gauss
Dado el sistema lineal $Ax = b$, el método consiste en aplicar *operaciones elementales fila* a la matriz aumentada $M$ asociada al sistema lineal de forma tal que la matriz $A$ sea transformada a una matriz triangular superior.

#### Algoritmo de Eliminación Gaussiana

Entrada: Numero de ecuaciones
		Matriz aumentada M = ($m_{ij}$), donde $i=1, ..., n$ y $j=1, ..., n+1$
Salida: Solución $x$ o  mensaje que el sistema no tiene solución.

Paso 1: Para $i=1,...,n-1$ hacer los Pasos del 2 al 4.
Paso 2: Sea $p$ el menor entero tal que $i \neq p \neq n$ y $m_{pi} \neq 0$.
		Si no puede encontrarse $p$ entonces **PARAR**.
		No existe solución
Paso 3: Si $p \neq i$ entonces calcule $F_{ip}M$.
Paso 4: Para $j=i+1, ..., n$ hacer los Pasos 5 y 6.
Paso 5: Calcule $f_{ij} = \frac{m_{ji}}{m_{ii}}$
Paso 6: Calcule $F_{ji}(f_{ji})$
Paso 7: Si $m_{nn} = 0$ entonces **PARAR**. 
		No existe solución
Paso 8: Calcule $x_n = \frac{m_{n, n+1}}{m_{nn}}$
Paso 9: Para $i = n-1, ..., 1$ calcule $x_i \leftarrow \left ( m_{i, n+1}  - \sum_{j=i+1}^{n} m_{ij}x_j \right) / a_{ii}$
Paso 10: Solución encontrada $x = (x_1, x_2, ... x_n)$ **PARAR**.



# Factorizaciones LU y Cholesky
Sea un sistema de $n$ ecuaciones lineales con $n$ incógnitas.
$$ \begin{bmatrix} a_{11} & a_{12} & \cdots & a_{1n} \\ a_{21} & a_{22} & \cdots & a_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ a_{n1} & a_{n2} & \cdots & a_{nn} \\ \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \\ \vdots \\ x_n \\ \end{bmatrix} = \begin{bmatrix} b_1 \\ b_2 \\ \vdots \\ b_n \\ \end{bmatrix} $$
Las matrices en la ecuación denotadas por $A$, $x$ y $b$ forman la ecuación $Ax=b$.

## Matrices fáciles de resolver

### Matriz diagonal
$$ \begin{bmatrix} a_{11} & 0 & \cdots & 0 \\ 0 & a_{22} & \cdots & 0 \\ \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \cdots & a_{nn} \\ \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \\ \vdots \\ x_n \\ \end{bmatrix} = \begin{bmatrix} b_1 \\ b_2 \\ \vdots \\ b_n \\ \end{bmatrix} $$
El sistema colapsa a $n$ ecuaciones simples y la solución es
$$ x = \begin{bmatrix} b_1/a_{11} \\ b_2/a_{22} \\ \vdots \\ b_n/a_{nn} \\ \end{bmatrix} $$
- Si $a_{ii} = 0$ para algún índice $i$ si $b_i = 0$ , entonces $x_i$ puede tomar cualquier número real 
- Si $a_{ii} = 0$ y $b_i \neq 0$ no existe solución para el sistema.

### Matriz triangular inferior
$$ \begin{bmatrix} a_{11} & 0 & \cdots & 0 \\ a_{21} & a_{22} & \cdots & 0 \\ \vdots & \vdots & \ddots & \vdots \\ a_{n1} & a_{n2} & \cdots & a_{nn} \\ \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \\ \vdots \\ x_n \\ \end{bmatrix} = \begin{bmatrix} b_1 \\ b_2 \\ \vdots \\ b_n \\ \end{bmatrix} $$
Un algoritmo formal para la solución en este caso es llamado **sustitución regresiva**.

#### Algoritmo de sustitución hacia adelante.

input $n$, ($a_{ij}$), ($b_i$)
for $i=0$ to $n-1$ do
	$x_i \leftarrow \left ( b_i  - \sum_{j=0}^{i-1} a_{ij}x_j \right) / a_{ii}$
end do
output ($x_i$)


### Matriz superior inferior
$$ \begin{bmatrix} a_{11} & a_{12} & \cdots & a_{1n} \\ 0 & a_{22} & \cdots & a_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \cdots & a_{nn} \\ \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \\ \vdots \\ x_n \\ \end{bmatrix} = \begin{bmatrix} b_1 \\ b_2 \\ \vdots \\ b_n \\ \end{bmatrix} $$
Un algoritmo formal para la solución en este caso es llamado **sustitución regresiva**.

#### Algoritmo de sustitución hacia atrás.

input $n$, ($a_{ij}$), ($b_i$)
for $i=n-1$ to $0$ do
	$x_i \leftarrow \left ( b_i  - \sum_{j=i+1}^{n-1} a_{ij}x_j \right) / a_{ii}$
end do
output ($x_i$)

## Factorizaciones LU
Supongamos que $A$ puede ser factorizados como el producto de una matriz triangular inferior $L$ y una matriz triangular superior $U$, $A=LU$. Entonces para resolver el sistema de ecuaciones $Ax=b$, es suficiente resolver el problema en dos etapas.
$$ Lz = b \quad \quad \text{resuelve para } z$$
$$ Ux = z \quad \quad \text{resuelve para } x$$
**No toda matriz puede tiene una factorización LU**
Comenzamos con una matriz $A_{n \times n}$ y buscamos matrices

![](matrices-LU.png)

tal que
$$ A = LU $$
Cuando es posible, decimos que $A$ tiene **descomposición $LU$**. Resulta que $L$ y $U$ no son únicas.

Para derivar un algoritmo para la factorización $LU$ de $A$, comenzamos con la fórmula para la multiplicación de matrices:

$$
a_{ij} = \sum_{s=1}^{n} \ell_{is} u_{sj} = \sum_{s=1}^{\min(i,j)} \ell_{is} u_{sj} \tag{5}
$$

Aquí hemos usado el hecho de que $\ell_{is} = 0$ para $s > i$, y $u_{sj} = 0$ para $s > j$.

Cada paso en este proceso determina una nueva fila de $U$ y una nueva columna en $L$. En el paso $k$, podemos asumir que las filas $1, 2, \ldots, k-1$ han sido calculadas en $U$ y que las columnas $1, 2, \ldots, k-1$ han sido calculadas en $L$. (Si $k=1$, esta suposición es vacuamente verdadera.) Poniendo $i=j=k$ en la Ecuación $(5)$, obtenemos

$$
a_{kk} = \sum_{s=1}^{k-1} \ell_{ks} u_{sk} + \ell_{kk} u_{kk} \tag{6}
$$

Si $u_{kk}$ o $\ell_{kk}$ han sido especificados, usamos la Ecuación $(6)$ para determinar el otro. Con $\ell_{kk}$ y $u_{kk}$ ahora conocidos, usamos la Ecuación $(5)$ para escribir para la $k$-ésima fila $(i = k)$ y la $k$-ésima columna $(j = k)$, respectivamente,
$$
a_{kj} = \sum_{s=1}^{k-1} \ell_{ks} u_{sj} + \ell_{kk} u_{kj} \quad (k+1 \le j \le n) \tag{7}
$$
$$
a_{ik} = \sum_{s=1}^{k-1} \ell_{is} u_{sk} + \ell_{ik} u_{kk} \quad (k+1 \le i \le n) \tag{8}
$$
Si $\ell_{kk} \ne 0$, la Ecuación $(7)$ puede usarse para obtener los elementos $u_{kj}$. Similarmente, si $u_{kk} \ne 0$, la Ecuación $(8)$ puede usarse para obtener los elementos $\ell_{ik}$. El cálculo de la $k$-ésima fila en $U$ y la $k$-ésima columna en $L$ como se describe completa el paso $k$ en el algoritmo. Los cálculos requieren división por $\ell_{kk}$ y $u_{kk}$; por lo tanto, si estos divisores son $0$, las computaciones usualmente no pueden completarse. Sin embargo, en algunos casos, pueden completarse.

El algoritmo basado en el análisis anterior es conocido como **factorización de Doolittle** cuando $L$ es **triangular inferior unitaria** ($l_{ii} = 1$ para $1 \leq i \leq n$) y es conocido como **factorización de Crout** cuando $U$ es **triangular superior unitaria** ($u_{ii} = 1$ para $1 \leq i \leq n$).

Cuando $U = L^T$ tal que $l_{ii} = u_{ii}$ para $1 \leq i \leq n$, el algoritmo es llamado **factorización de Cholesky**.


<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Analisis y Modelamiento Numerico/imgs/pseudocode-LU.png" alt="Texto alternativo de la imagen">
    <figcaption>Algoritmo para la factorización LU</figcaption>
    </figure>
</div>

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Analisis y Modelamiento Numerico/imgs/pseudocode-Doolitle.png" alt="Texto alternativo de la imagen">
    <figcaption>Algoritmo para la factorización Doolitle</figcaption>
    </figure>
</div>


## Teorema sobre la descomposición LU
Si todos los $n$ [[Matrices#Menor principal de una matriz|menores principales]] de la matriz $A_{n \times n}$ son *no singulares*, entonces $A$ tiene una descomposición $LU$.

### Prueba
Recordemos que el menor principal líder $k$-ésimo de la matriz $A$ es la matriz

$$
A_k = \begin{bmatrix}
a_{11} & a_{12} & \cdots & a_{1k} \\
a_{21} & a_{22} & \cdots & a_{2k} \\
\vdots & \vdots & \ddots & \vdots \\
a_{k1} & a_{k2} & \cdots & a_{kk}
\end{bmatrix}
$$

Sea $A_k$, $L_k$ y $U_k$ los menores principales líderes $k$-ésimos en las matrices $A$, $L$ y $U$, respectivamente. Nuestra hipótesis es que $A_1, A_2, \ldots, A_n$ son no singulares. Para los propósitos de una prueba inductiva, supongamos que $L_{k-1}$ y $U_{k-1}$ han sido obtenidos. En la Ecuación $(5)$, si $i$ y $j$ están en el rango $1, 2, \ldots, k-1$, entonces también lo está $s$. Por lo tanto, la Ecuación $(5)$ establece que

$$
A_{k-1} = L_{k-1} U_{k-1}
$$

Dado que $A_{k-1}$ es no singular por hipótesis, $L_{k-1}$ y $U_{k-1}$ también son no singulares. Dado que $L_{k-1}$ es no singular, podemos resolver el sistema

$$
\sum_{s=1}^{k-1} \ell_{is} u_{sk} = a_{ik} \quad (1 \le i \le k-1)
$$

para las cantidades $u_{sk}$ con $1 \le s \le k-1$. Estos elementos están en la columna $k$-ésima de $U$. Dado que $U_{k-1}$ es no singular, podemos resolver el sistema

$$
\sum_{s=1}^{k-1} \ell_{ks} u_{sj} = a_{kj} \quad (1 \le j \le k-1)
$$

para $\ell_{ks}$ con $1 \le s \le k-1$. Estos elementos están en la fila $k$-ésima de $L$. Del requerimiento

$$
a_{kk} = \sum_{s=1}^{k} \ell_{ks} u_{sk} = \sum_{s=1}^{k-1} \ell_{ks} u_{sk} + \ell_{kk} u_{kk}
$$

podemos obtener $u_{kk}$ desde que $l_{kk}$ ha sido especificado como la unidad. Entonces, todos los nuevos elementos necesarios para formar $L_k$ y $u_k$ han sido definidos. La inducción es completada por nada menos que $l_{11} u_{11} = a_{11}$ y por tanto, $l_{11} = 1$ y $u_{11} = a_{11}$. $\blacksquare$

## Teorema sobre la factorización $LL^T$ de Cholesky
Si $A$ es una matriz real, simétrica y [[Formas cuadráticas|definida positiva]], entonces tiene una única factorización $A=LL^T$, en donde $L$ es una matriz triangular inferior con una diagonal positiva.

### Prueba
Recordemos que una matriz $A$ es simétrica y definida positiva si $A = A^T$ y $x^T A x > 0$ para cada vector $x$ no nulo. Se sigue de inmediato que $A$ es no singular porque $A$ obviamente no puede mapear cualquier vector no nulo en $0$. Además, considerando vectores especiales de la forma $x = (x_1, x_2, \ldots, x_k, 0, 0, \ldots, 0)^T$, vemos que los menores principales líderes de $A$ también son definidos positivos. El [[#Teorema sobre la descomposición LU]] implica que $A$ tiene una descomposición $LU$. Por la simetría de $A$, tenemos entonces

$$
LU = A = A^T = U^T L^T
$$

Esto implica que

$$
U (L^T)^{-1} = L^{-1} U^T
$$

El miembro izquierdo de esta ecuación es triangular superior, mientras que el miembro derecho es triangular inferior. En consecuencia, hay una matriz diagonal $D$ tal que $U (L^T)^{-1} = D$. Por lo tanto, $U = DL^T$ y $A = LDL^T$.  $D$ es definida positiva, y así sus elementos $d_{ii}$ son positivos. Denotando por $D^{1/2}$ la matriz diagonal cuyos elementos diagonales son $\sqrt{d_{ii}}$, tenemos $A = \tilde{L} \tilde{L}^T$, donde $\tilde{L} \equiv L D^{1/2}$, que es la factorización de Cholesky. La prueba de la unicidad queda como un problema. $\blacksquare$

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Analisis y Modelamiento Numerico/imgs/pseudocode-Cholesky.png" alt="Texto alternativo de la imagen">
    <figcaption>Algoritmo para la factorización de Cholesky</figcaption>
    </figure>
</div>
# Serie de Neumann y refinamiento iterativo
Si a un espacio vectorial $V$ se le asigna una norma $\|\cdot \|$, entonces el par ($V, \|\cdot \|$) es un **espacio vectorial normado**. 

Dada una secuencia de vectores $v^{(1)},v^{(2)}, ...$ , decimos que la secuencia converge a un vector $v$ si
$$ \lim_{k \to \infty}  \| v^{(k)} - v\| = 0$$


## Teorema sobre la serie de Neumann
Si $A$ es una matriz de $n \times n$ tal que $\|A\| < 1$, entonces $I-A$ es invertible y
$$ (I-A)^{-1} = \sum_{k=0}^{\infty} A^k $$
### Prueba
Primero, mostraremos que $I - A$ es invertible. Si no es invertible, entonces es singular, y existe un vector $x$ que satisface $\| x \| = 1$ y $(I - A)x = 0$. De esto tenemos que

$$
1 = \| x \| = \| Ax \| \le \| A \| \| x \| = \| A \|
$$

lo cual contradice la hipótesis de que $\| A \| < 1$. A continuación, mostraremos que las sumas parciales de la serie de Neumann convergen a $(I - A)^{-1}$:

$$
\sum_{k=0}^{m} A^k \rightarrow (I - A)^{-1} \quad \text{(cuando } m \rightarrow \infty \text{)}
$$

Será suficiente probar que

$$
(I - A) \sum_{k=0}^{m} A^k \rightarrow I \quad \text{(cuando } m \rightarrow \infty \text{)} \tag{2}
$$

El lado izquierdo puede escribirse como

$$
(I - A) \sum_{k=0}^{m} A^k = \sum_{k=0}^{m} (A^k - A^{k+1}) = A^0 - A^{m+1} = I - A^{m+1}
$$

Dado que $\| A^{m+1} \| \le \| A \|^{m+1} \rightarrow 0$ a medida que $m \rightarrow \infty$, esto establece $(2)$. ¿Por qué? $\blacksquare$


# Matriz tridiagonal
La idea de los dos métodos que estudiaremos a continuación consiste en tener también en cuenta los elementos de la matriz a factorizar que no están en la diagonal principal y a la vez conservar la simetría, no penalizando así la velocidad obtenible $O(n^3 / 6)$.

Los dos métodos calculan una factorización

$$
P A P^T = L T L^T,
$$

donde $L$, de coeficientes $l_{ij}$, es una matriz triangular inferior con $l_{ii} = 1$, $P$ representa una permutación tal que $|l_{ij}| \leq 1$ y $T$ es una matriz tridiagonal de la forma

$$
T = 
\begin{bmatrix}
\alpha_1 & \beta_1 & 0 & 0 & \cdots & 0 \\
\beta_1 & \alpha_2 & \beta_2 & 0 & \cdots & 0 \\
0 & \beta_2 & \alpha_3 & \beta_3 & \cdots & 0 \\
0 & 0 & \beta_3 & \ddots & \ddots & \vdots \\
\vdots & \vdots & \vdots & \ddots & \alpha_{n-1} & \beta_{n-1} \\
0 & 0 & 0 & \cdots & \beta_{n-1} & \alpha_n
\end{bmatrix}.
$$

Mediante una factorización como esta, la resolución del sistema $A x = b$ constaría de las siguientes etapas:

1. $L z = P b;$
2. $T w = z;$
3. $L^T y = w$ y
4. $x = P^T y.$

Para resolver $T w = z$ se utiliza la eliminación de Gauss en su variante para matrices tridiagonales, proceso que requiere $n$ operaciones de multiplicación/división y suma/resta.


# Método de Parlett y Reid

## El método de Parlett y Reid

Este método —Parlett y Reid [1970]— se basa en la utilización de transformaciones de Gauss. Para analizar su mecánica, apliquémoslo a una matriz $A^{5 \times 5}$, suponiendo que estamos en la etapa $k = 2$.

Al comienzo de esta etapa, la matriz $A$ tiene la forma

$$
A^{(1)} = M_1 P_1 A P_1^T M_1^T = 
\begin{bmatrix}
\alpha_1 & \beta_1 & 0 & 0 & 0 \\
\beta_1 & \alpha_2 & v_3 & v_4 & v_5 \\
0 & v_3 & \times & \times & \times \\
0 & v_4 & \times & \times & \times \\
0 & v_5 & \times & \times & \times
\end{bmatrix},
$$

donde $P$ representa una permutación tal que los módulos de los elementos de la transformación o eliminación de Gauss $M_1$ están acotados superiormente por la unidad. En esta etapa $k = 2$ se busca el elemento del vector $[v_3, v_4, v_5]^T$ de mayor valor absoluto y se determina una permutación, que representamos por $P_2$, tal que

$$
\tilde{v_3} = \max(|v_3|, |v_4|, |v_5|).
$$

Si $\tilde{v_3} = 0$, se hace $M_2 = P_2 = I$ y se pasa a la etapa $k = 3$. Si no, se hace $P_2 = \text{diag}(I_2, \tilde{P_2})$, es decir una matriz diagonal en dos bloques (el primero $I_2$ y el segundo $\tilde{P_2}$), y $M_2 = I_5 - \alpha_2 e_3 \tilde{e_3}^T$, donde,

$$
\alpha_2 = 
\begin{bmatrix}
0 \\
0 \\
1 \\
0 \\
0
\end{bmatrix} \cdot \frac{\tilde{v_3}}{v_3}.
$$

El resultado de esta etapa $k = 2$ será una matriz $A^{(2)}$ de la forma

$$
A^{(2)} = M_2 P_2 A^{(1)} P_2^T M_2^T = 
\begin{bmatrix}
\alpha_1 & \beta_1 & 0 & 0 & 0 \\
\beta_1 & \alpha_2 & 0 & 0 & 0 \\
0 & 0 & \tilde{v_3} & \times & \times \\
0 & 0 & \times & \times & \times \\
0 & 0 & \times & \times & \times
\end{bmatrix}.
$$

Este proceso se completa en $n-2$ etapas al final de las cuales se obtiene la matriz tridiagonal que se deseaba:

$$
T = A^{(n-2)} = (M_{n-2} P_{n-2} \cdots M_1 P_1) A (M_{n-2} P_{n-2} \cdots M_1 P_1)^T.
$$

Si se hace $P = P_{n-2} \cdots P_1$ y $L = (M_{n-2} P_{n-2} \cdots M_1 P_1 P^T)^{-1}$, mediante un razonamiento similar al del apartado 1.4, se puede comprobar que

$$
P A P^T = L T L^T.
$$

La primera columna de $L$ es $e_1$; las restantes $k$ $(k > 1)$ las forman los multiplicadores de $M_{k-1}$.

### Ejemplo 1.2 Aplicar el método de Parlett y Reid a

$$
A = 
\begin{bmatrix}
0 & 1 & 2 & 3 \\
1 & 2 & 2 & 2 \\
2 & 2 & 3 & 4 \\
3 & 2 & 3 & 4
\end{bmatrix}.
$$

En la primera etapa se tiene que:

$$
P_1 = [e_1, e_4, e_3, e_2], \quad M_1 = I_4 - 
\begin{bmatrix}
0 & 0 & 1/3 \\
0 & 1 & 0 \\
2/3 & 0 & 0
\end{bmatrix}
$$

$$
A^{(1)} = M_1 P_1 A P_1^T M_1^T = 
\begin{bmatrix}
3 & 4 & 3 & 0 \\
4 & 7/9 & 5/9 & 0 \\
3 & 5/9 & 10/9 & 0 \\
0 & 0 & 0 & 0
\end{bmatrix}.
$$

En la segunda:

$$
P_2 = [e_1, e_2, e_4, e_3], \quad M_2 = I_4 - 
\begin{bmatrix}
0 & 0 & 1/2 \\
0 & 0 & 1/2
\end{bmatrix}
$$

$$
A^{(2)} = M_2 P_2 A^{(1)} P_2^T M_2^T = 
\begin{bmatrix}
3 & 4 & 2/3 & 0 \\
4 & 7/9 & 5/9 & 0 \\
2/3 & 5/9 & 10/9 & 0 \\
0 & 0 & 0 & 0
\end{bmatrix}.
$$

En resumen, $P A P^T = L T L^T$, donde:

$$
P = P_2 P_1 = 
\begin{bmatrix}
1 & 0 & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 1 & 0 & 0 \\
0 & 0 & 0 & 1
\end{bmatrix},
$$

$$
L = (M_2 P_2 M_1 P_1 P^T)^{-1} = 
\begin{bmatrix}
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
1/3 & 0 & 1 & 0 \\
0 & 1/2 & 0 & 1
\end{bmatrix},
$$

y

$$
T = 
\begin{bmatrix}
3 & 4 & 0 & 0 \\
4 & 7/9 & 0 & 0 \\
2/3 & 5/9 & 0 & 0 \\
0 & 0 & 0 & 0
\end{bmatrix}.
$$
