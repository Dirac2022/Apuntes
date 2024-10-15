
# Conceptos básicos

## El campo de los números complejos  ($\mathbb{C}$)
Tienen la forma
$$z = a + bi \quad \quad a, b \in \mathbb{R} $$
### Conjugada de un complejo
$$ \overline{z} = a - bi $$
#### Propiedades
- $\overline{\overline{y}} = y$
- $y\overline{y} = |y|^2$
### Modulo de un complejo
$$ |z| = \sqrt{a^2 + b^2} $$
### Espacio vectorial ($\mathbb{C}^n$)
Consiste en todas las n-tuplas complejas $X = (x_1, x_2, ..., x_n)^T$.
$\mathbb{C}^n$ es un espacio vectorial sobre el campo $\mathbb{C}$. 

En el espacio $\mathbb{C}^n$ el **producto interno** y la **norma euclideana** se definen como
$$ \langle \mathbf{a}, \mathbf{b} \rangle = \sum_{j=1}^n x_j \overline{y}_j $$
$$ \| x\|_2 = \sqrt{\langle x, x\rangle}$$
Se puede ver que 
- $\langle x, y\rangle = \overline{\langle y, x\rangle}$
- $\langle x, \lambda y\rangle = \overline{\lambda} \langle x, y\rangle$
- $\langle x + y, z\rangle = \langle x, z\rangle + \langle y, z\rangle$


### Transpuesta conjugada de una matriz
Si $A$ es una matriz que elementos complejos, denotamos como $A^*$ a su **matriz transpuesta conjugada**
$$ (A^*)_{ij} = \overline{A}_{ji} $$
En particular, si $x$ es un vector columna, entonces $x^* = (\overline{x}_i)$ es un vector fila y
$$ y^*x = \langle x, y \rangle = \sum_{i=1}^n x_i\overline{y}_i$$
$$ x^*x = \langle x, x \rangle = \|x\|^2_2 = \sum_{i=1}^n x_i\overline{x}_i = \sum_{i=1}^n |x_i|^2 $$


# Problema de la matriz de valores propios: Método de potencias

Este procedimiento esta diseñado para calcular el **valor propio dominante** y su correspondiente **vector propio**. Es necesario que $A$ tiene las siguientes propiedades

1. Existe un único valor propio de máximo módulo.
2. Existe un conjunto linealmente independiente de $n$ vectores propios.

De acuerdo con la primera propiedad, los valores propios 
$$ |\lambda_1| \geq |\lambda_2| \geq \cdots \geq |\lambda_n|  $$
De acuerdo con la segunda propiedad, existe una base $\{ u^{(1)}, u^{(2)}, ..., u^{(n)}\}$ para $\mathbb{C}^n$



# Teorema de Schur

Dos matrices $A$ y $B$ son **semejantes** si existe un matriz no singular $P$ tal que 
$$ B = PAP^{-1}$$

> [!info]
> Recordar [[Valores y vectores propios#Teorema de los valores propios de matrices semejantes|Valores propios en matrices semejantes]]

## Factorización de Schur
Si queremos encontrar los valores propios de una matriz $A$ semejante a $B$ una forma forma de hacerlo es calcular los valores propios de $B$ si es que esta es una matriz más simple. Específicamente, si $B$ es triangular, sus valores propios serán simplemente los elementos de su diagonal.

Sea una matriz $U$ unitaria, es decir, si $UU^* = I$, donde $U^*$ es la transpuesta conjugada de $U$. Las matrices $A$ y $B$ son **semejante unitariamente** si $B = UAU^*$

## Teorema de Schur
Toda matriz cuadrada es unitariamente similar a una matriz triangular.
![[Pasted image 20240423194823.png]]


## Corolario
Toda matriz cuadrada es similar a una matriz triangular.

# Factorizaciones Ortogonales y Problemas de Mínimos Cuadrados
Un conjunto de vectores indexados $[v_1, v_2, \dots v_k]$ en $\mathbb{C}^n$ se dice que es **ortogonal** si $\langle v_i, v_j \rangle = 0$ siempre que $i\neq j$. Si $\langle v_i, v_j \rangle = \delta_{ij}$ se dice que el conjunto es **ortonormal**. Si el conjunto $[v_1, v_2, \dots v_k]$ forman las columnas de una matriz de A de $n \times k$, entonces la ortonormalidad se expresa por mediante la ecuación $A^*A=I$.

## Conceptos Básicos
Supongamos ahora que $[v_1, v_2, \ldots, v_n]$ es una base ortonormal para $\mathbb{C}^n$. Cada elemento $x \in \mathbb{C}^n$ tiene una representación única en la forma

$$
x = \sum_{i=1}^{n} c_i v_i
$$

para los escalares complejos apropiados $c_i$. Al tomar el producto interno de ambos lados de esta ecuación con algún $v_j$, obtenemos

$$
\langle x, v_j \rangle = \left\langle \sum_{i=1}^{n} c_i v_i, v_j \right\rangle = \sum_{i=1}^{n} c_i \langle v_i, v_j \rangle = \sum_{i=1}^{n} c_i \delta_{ij} = c_j
$$

Esto establece que para todo $x \in \mathbb{C}^n$,

$$
x = \sum_{i=1}^{n} \langle x, v_i \rangle v_i
$$

El término $\langle x, v_i \rangle v_i$ se refiere como el **componente** de $x$ en la dirección $v_i$. 

## Proceso de Gram-Schmidt
El clásico proceso Gram-Schmidt se puede utilizar para obtener el sistema ortonormal en cualquier espacio interior del producto. Para describirlo, suponemos que una secuencia lineal independiente de vectores se da en un espacio de producto interno: $[x_1, x_2, \dots]$. (Esta secuencia puede ser finita o infinita.) Generamos una secuencia ortonormal $[u_1, u_2, \dots]$ por la fórmula
$$
u_k = \left\|x_k - \sum_{i<k} \langle x_k, u_i \rangle u_i  \right\|^{-1}_2 \left(x_k - \sum_{i<k} \langle x_k, u_i \rangle u_i\right) \tag{2}
$$

### Teorema sobre la secuencia Gram-Schmidt
La **secuencia de Gram-Schmidt** $[u_1, u_2, \dots ]$ tiene la propiedad que $\{u_1, u_2, \dots \}$ es una base ortonormal para el span lineal de $\{u_1, u_2, \dots \}$ para $k\geq1$.

![[Pasted image 20240531235614.png]]

### Algoritmo Gram-Schmidt
Aplicamos el proceso a las columnas $A^1, A^2, \dots, A^n$ de una matriz $A$ de $m \times m$, llegando después de $n$ pasos a una matriz $B$ de $m \times n$ cuyas columnas forman un conjunto ortonormal.

![[Pasted image 20240601012531.png]]


### Teorema sobre la factorización de Gram-Schmidt
El proceso Gram-Schmidt, cuando se aplica a las columnas de una matriz  $A$ de $m \times n$ de rango $n$, produce una factorización
$$ A=BT $$
en la cual $B$ es una matriz $m \times n$ con columnas ortonormales y $T$ es una matriz triangular superior $n \times n$ con diagonal positiva.

#### Prueba
Primero, observe que el algoritmo anterior está llevando a cabo el proceso de Gram-Schmidt encapsulado en la Ecuación $(2)$. A continuación, completamos la definición de la matriz $T$ estableciendo $t_{ij} = 0$ cuando $i > j$. Por el [[#Teorema sobre la secuencia Gram-Schmidt]] , las columnas de $B$ forman un conjunto ortonormal de $n$ vectores en $\mathbb{R}^m$, y cada $A_j$ es una combinación lineal de $B_1, B_2, \ldots, B_j$. De hecho, por la Ecuación $(1)$,

$$
A_j = \sum_{i=1}^{j} \langle A_j, B_i \rangle B_i = \sum_{i=1}^{j-1} \langle A_j, B_i \rangle B_i + \langle A_j, B_j \rangle B_j
$$

$$
= \sum_{i=1}^{j-1} t_{ij} B_i + \langle A_j, B_j \rangle B_j \tag{5}
$$

Ahora, nos detenemos para calcular

$$
\langle A_j, B_j \rangle = \left\langle C_j + \sum_{i<j} t_{ij} B_i, B_j \right\rangle = \langle C_j, B_j \rangle
$$

$$
= (C_j, C_j) / t_{jj} = t_{jj} \tag{6}
$$

Cuando el resultado de la Ecuación $(6)$ se usa en la Ecuación $(5)$, obtenemos

$$
A_j = \sum_{i=1}^{j} t_{ij} B_i = \sum_{i=1}^{n} t_{ij} B_i \quad (1 \le j \le n) \tag{7}
$$

Esta es otra forma de expresar la Ecuación $(4)$.

## Algoritmo de Gram-Schmidt modificado
El algoritmo de Gram-Schmidt modificado es el siguiente
![[Pasted image 20240601012846.png]]

Aquí $A^j$ es la columna $j$th en la matriz $A$. Podemos ver que los componentes de $A^j$ en la dirección del vector base $A^k$ se están eliminando lo antes posible y uno a la vez. En este algoritmo, hay sobre escritura considerable, y al final el conjunto original $\{A^1, A^2, \dots , A^n\}$ ha sido reemplazado por un conjunto ortonormal.

Para evitar las raíces cuadradas involucradas en el cálculo de $\|x\|_2$, el algoritmo Gram-Schmidt modificado a menudo se da en la siguiente forma, que produce una factorización ligeramente diferente

![[Pasted image 20240601014018.png]]

### Teorema sobre la factorización modificada de Gram-Schmidt
Si el proceso Gram-Schmidt modificado se aplica a las columnas de una matriz $A$ de $m \times n$ de rango $n$, la matriz transformada $B$ de $m \times n$ tiene un conjunto ortonormal de columnas y satisface 
$$ A=BT $$ donde $T$ es una matriz triangular superior unitaria de $n \times n$ cuyos elementos $t_{kj}$ (para $j>k$) se generan en el algoritmo.

![[Pasted image 20240601014952.png]]


## Problemas de mínimos cuadrados
Una aplicación importante de las factorizaciones ortogonales que nos ocupan es el problema de los **mínimos cuadrados** para sistemas de ecuaciones lineales. Considere un sistema de $m$ ecuaciones con $n$ incógnitas escrito en la forma
$$
Ax=b
$$
Donde $A_{m\times n}$ ,  $x_{n\times 1}$ y $b_{m\times 1}$. Supondremos que el rango de $A$ es $n$, por tanto $m\geq n$. Por lo general, el sistema $Ax=b$ no tiene solución debido a que $b$ no pertenece al subespacio de $\mathbb{C}^m$ de dimensión $n$, generado por las columnas de $A$. Es frecuente en tales casos que se requiera encontrar una $x$ que minimice la norma del vector residual $b-Ax$. La *solución* en mínimos cuadrados de $Ax=b$ es el vector $x$ que hace $\|b-Ax\|_2$ un mínimo. (Según lo que hemos supuesto acerca del rango de $A$, esta $x$ será única).

### Lema sobre el problema de los mínimos cuadrados
Si $x$ es un punto tal que $A^*(Ax-b)=0$, entonces $x$ es una solución del problema de los mínimos cuadrados.
#### Prueba
Sea $y$ cualquier otro punto. Dado que $A^*(Ax - b) = 0$, concluimos que $b - Ax$ es ortogonal al espacio de columnas de $A$. Además, dado que $A(x - y)$ está en el espacio de columnas de $A$, tenemos $\langle b - Ax, A(x - y) \rangle = 0$, y la regla de Pitágoras nos da

$$
\| b - Ay \|_2^2 = \| b - Ax + A(x - y) \|_2^2
$$

$$
= \| b - Ax \|_2^2 + \| A(x - y) \|_2^2 \ge \| b - Ax \|_2^2 \quad  \quad \blacksquare
$$



## Factorización QR de Householder
 El objetivo es factorizar una matriz $A$ de $m \times n$ en un producto
$$A = QR$$

donde $Q$ es una matriz unitaria de $m \times m$ y $R$ es una matriz triangular superior de $m \times n$. El algoritmo de factorización en realidad produce

$$Q^* A = R$$

y $Q^*$ se construye paso a paso como un producto de matrices unitarias que tienen la forma especial

$$\begin{bmatrix}
I_k & 0 \\
0 & I_{m-k} - vv^*
\end{bmatrix}$$


Estas se llaman reflexiones o transformaciones de Householder. No hacemos ninguna suposición sobre el rango de $A$.

Primero, determinamos $v \in \mathbb{C}^m$ para que $I - vv^*$ sea unitario y de manera que $(I - vv^*)A$ comience a parecerse a $R$. Específicamente, su primera columna debe ser de la forma correcta, a saber, $(\beta, 0, 0, \ldots, 0)^T$. Sea la columna original de $A$ denotada por $A_1$. Queremos $(I - vv^*)A_1 = \beta e^{(1)}$, donde $e^{(1)}$ denota el primer vector unitario estándar $e^{(1)} = (1, 0, \ldots, 0)^T$. Por la prueba del Lema 2 de la Sección 5.2 (p. 267), esto se logra como sigue: 
1. Seleccionar un número complejo $\beta$ tal que $|\beta| = ||A_1||_2$ y tal que $\langle A_1, \beta e^{(1)} \rangle$ sea real.
2. Hacemos $v = \alpha(A_1 - \beta e^{(1)})$ con $\alpha = \sqrt{2}/||A_1 - \beta e^{(1)}||_2$. Esta descripción admite dos opciones para $\beta$, y seleccionamos la que hace que haya menos cancelación al computar el primer componente de $v$. 
3. Así, definimos $\beta$ por $\beta = -\|A_1\|_2 \ a_{11} / |a_{11}|$


El algoritmo para obtener la matriz $U$ en este primer paso es el siguiente:

1. $\beta \leftarrow - (a_{11}/|a_{11}|)\|A_1\|_2$   ($A_1$ es la primera columna de $A$)
2. $y \leftarrow A_1 - \beta e^{(1)}$   ($e^{(1)}$ es el primer vector canónico)
3. $\alpha \leftarrow \sqrt{2}/\|y\|_2$\\
4. $v \leftarrow \alpha y$
5. $U \leftarrow I - vv^*$


Los pasos siguientes en la factorización QR son similares al primer paso. En la siguiente iteración se evalúa la matriz $UA$, en general en el paso $i$ se evalúa la matriz la columna $i$ a partir de la fila $i$ en la matriz $U_{i-1} \dots U_1 \, A$.

Después de $k$ pasos, habremos multiplicado $A$ por la izquierda por $k$ matrices unitarias y el resultado será una matriz que tiene sus primeras $k$ columnas en la forma correcta; es decir, tienen ceros debajo de la diagonal. La situación puede resumirse por

$$U_k U_{k-1} \cdots U_1 A = \begin{bmatrix}
J & H \\
0 & W
\end{bmatrix}$$

donde $J$ es una matriz triangular superior de $k \times k$,  $0$ es una matriz nula de $m \times k$, $H$ es de $k \times (n - k)$, y $W$ es de $m - k \times (n - k)$. Por el análisis anterior, existe un vector $v \in \mathbb{C}^{m - k}$ tal que $I - vv^*$ es una matriz unitaria de orden $m - k$ y tal que $(I - vv^*)W$ tiene ceros debajo del elemento inicial en su primera columna. Ahora observe que

$$\begin{bmatrix}
I & 0 \\
0 & I - vv^*
\end{bmatrix}
\begin{bmatrix}
J & H \\
0 & W
\end{bmatrix}
= \begin{bmatrix}
J & H \\
0 & (I - vv^*)W
\end{bmatrix}$$

El primer factor a la izquierda en esta ecuación es unitario y es lo que denotamos por $U_{k+1}$.

El proceso descrito termina cuando la $(n - 1)$-ésima columna de $R$ ha sido puesta en forma adecuada. En esa etapa, tenemos una ecuación $Q^* A = R$, donde $Q^*$ denota el producto de todas las matrices unitarias que se han usado como factores. Desde que $Q$ es unitario, $A = QR$, como deseamos. Esta es la factorización QR de Householder. La ecuación $Q^* = U_{n-1} U_{n-2} \cdots U_1$ lleva a $Q = U_1^* U_2^* \cdots U_{n-1}^*$. De la forma de $U_k$, 

$$U_k = \begin{bmatrix}
I_{k-1} & 0 \\
0 & I_{n-k+1} - vv^*
\end{bmatrix}$$
podemos ver que $U_k$ es hermitiana ($U^*_k = U_k$), por lo que
$$
Q = U_1 \, U_2 \dots U_{n-1}
$$

# Descomposición por valores singulares (SVD)

## Teorema
Toda matriz compleja $A$ de $m \times n$ puede ser factorizada como
$$ A = U\Sigma V^T $$
donde:
- $U_{m \times m}$ es una [[Matrices#Matriz Hermitiana#Matriz unitaria|matriz unitaria]]
- $\Sigma_{m \times n}$ es una matriz diagonal
- $V^T_{n \times n}$ es una [[Matrices#Matriz Hermitiana#Matriz unitaria|matriz unitaria]]

### Prueba
La matriz $A^*A$ es una matriz $n \times n$ hermitiana. Tambien es [[Formas cuadráticas|semidefinida  positiva]]. Además los valores propios de $A^*A$ son no negativos. Sean $\sigma_1^2, \sigma_2^2, \cdots, \sigma_r^2$ valores propios positivos y $\sigma_{r+1}^2, \cdots, \sigma_n^2$ ceros. Con un cierto orden (Se recomienda orden no decreciente). Sea $\{u_1, \cdots, u_n\}$ un conjunto **ortonormal** de vectores propios de $A^*A$ (con el orden asociado a sus respectos valores propios $\sigma_i^2$), tal que
$$ A^* A u_i = \sigma_i^2 u_i $$
Tambien, se tiene que $r = rango(A^*A) \leq min\{m, n\}$
Formamos la matriz $V_{n \times n}$ cuyas columnas  sean los vectores $u_i,  \cdots u_n$. Ahora definamos
$$ v_i = \sigma_i^{-1} A u_i \quad \quad (1 \leq i \leq r) $$
Los vectores $v_i$ forman un conjunto ortonormal, ya que para $(1 \leq i, j \leq r)$

$$
v_i^*v_j = \sigma_1^{-1} \ (Au_i)^*\sigma_j^{-1}(Au_j) = (\sigma_i \ \sigma_j)^{-1} \ (u_i^* A^* A u_j) = (\sigma_i \sigma_j)^{-1} (u_i^* \ \sigma_j^2 \ u_j) = \delta_{ij}
$$

Seleccionemos vectores adicionales $v_i$ tal que $\{v_1, \cdots v_m\}$ sea una base ortonormal para $\mathbb{C}^m$. 

Sea $U_{m \times m}$ la matriz cuyas columnas son $v_1, \cdots v_m$. Y sea $\Sigma_{m \times n}$ una matriz con $\sigma_1, \cdots, \sigma_r$ en su diagonal y ceros en lo demás. Entonces
$$ A = U\Sigma V^T $$
#### Observación
El orden para los $\sigma_1, \cdots, \sigma_r$ es arbitrario, por tanto, una matriz puede tener muchas descomposiciones por valores singulares
## Singular values
Los números $\sigma_1, \cdots, \sigma_n$ se llaman **valores singulares** de $A$. Son raíces cuadradas no negativas de los valores propios de $A^*A$ .









