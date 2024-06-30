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
	1. Si $rango(A) = rango(M) < n$, entonces el sistema **tiene infinitas soluciones**. La solución general depende de $n-rango(A)$ variables libres.
	2. Si $rango(A) = rango(M) = n$, entonces el sistema **tiene una única solución**.
2. Si $rango(A) \neq rango(M)$, entonces el sistema **no tiene solución**.
