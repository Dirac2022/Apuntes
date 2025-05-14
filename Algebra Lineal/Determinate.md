

## Teorema
$$ det(A) = det(A^T) \: ,  \quad \forall \: A \in M_{nn} (\mathbb{K}) $$
## Teorema
Sea $A \in M_{nn} (\mathbb{K})$
- Si $A$ posee una fila (columna) de ceros, entonces $det(A) = 0$
- Si $A$ posee dos filas (columnas) iguales, entonces $det(A) = 0$

## Teorema
Si $A$ es una matriz triangular inferior (superior), entonces el determinante de $A$ es igual al producto de los elementos de la diagonal.

## Teorema
Si una matriz $B$ se ha obtenido de una matriz $A$ por medio de operaciones elementales entre filas (columnas), se tiene que
- Si se intercambio dos filas (columnas) de A, entonces $det(B) = -det(A)$
- Si se multiplico una fila (columna) de $A$ por un escalar $\lambda$, entonces $det(B) = \lambda det(A)$.
- Si se adicionó un múltiplo de una fila (columna) a otra, entonces $det(B) = det(A)$

### Corolario
$$ det(\lambda A) = \lambda^ndet(A)$$

## Teorema
Si $A$ es una matriz invertible, entonces $det(A^{-1}) = det(A)^{-1}$


## Teorema
$$  det(AB) = det(A)det(B) \: ,  \quad \forall \: A \: ,  \: B\in M_{nn} (\mathbb{K}) $$

## Teorema

$$
\begin{vmatrix}
a_1 & b_1 & \dots & (x_1 + u_1) \\
\vdots & \vdots & \dots & \vdots \\
a_1 & b_1 & \dots & (x_n + u_n) \\
\end{vmatrix}

= 

\begin{vmatrix}
a_1 & b_1 & \dots & x_1 \\
\vdots & \vdots & \dots & \vdots \\
a_1 & b_1 & \dots & x_n \\
\end{vmatrix}

+

\begin{vmatrix}
a_1 & b_1 & \dots & u_1 \\
\vdots & \vdots & \dots & \vdots \\
a_1 & b_1 & \dots & u_n \\
\end{vmatrix}

$$



# Teorema
Dada una matriz de tamaño $n \times n$ tiene unos en la diagonal principal, $i$ en las diagonales adyacentes a la principal y cero en las demás entradas, es decir

$$
\begin{pmatrix}
1 & i & 0 & \cdots & 0 \\
i & 1 & i & \cdots & 0 \\
0 & i & 1 & \cdots & 0 \\
\vdots & \vdots & \vdots & \ddots & i \\
0 & 0 & 0 & i & 1
\end{pmatrix}
$$

Entonces $det(A_k) = F_k$ donde $k$ es el orden de la matriz y $F_k$ es el  $k$-ésimo número de Fibonacci.

## Demostración

**Casos base**
- $det(A_1) = 1$
- $det(A_2) = 2$

**Hipótesis inductiva**
Sean $k-1, k, k+1 \in \mathbb{N} : det(A_{k-1}) = F_{k-1} \: , \ det(A_k) = F_k$.

**Inducción**
$$
\begin{aligned}
det(A_{k+1}) &= -idet(idet(A_{k-1})) + det(A_k) \\ \\
&= -i^2 det(A_{k-1}) + det(A_k) \\ \\
&= F_{k-1} + F_{k} \\ \\
&= F_{k+1} \quad \square
\end{aligned}
$$
