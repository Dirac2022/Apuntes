	
Sea $V$ un $\mathbb{K}$-espacio vectorial, y sea $T$ : $V$ $to$ $V$ una transformación lineal. Se dice que $v \in V - \{0\}$  es un **vector propio**, **autovector** o **eigenvector** de $T$ si existe $\lambda \in \mathbb{K}$ tal que 
$$
T(v) = \lambda v
$$
El elemento $\lambda \in \mathbb{K}$ se denomina **valor propio**, **autovalor** o **eigenvalue**.

Como toda transformación lineal esta asociada a una matriz, si $A$ es la matriz de la transformación $T$, los autovalores $\lambda$ y autovectores $v$ de $A$ están definidos por la expresión
$$
Av = \lambda v
$$

# Teorema
Sea $A \in \mathbb{K}^{n \times n}$, entonces $A$ es diagonalizable, si y solo si, existe una base $B$ de $\mathbb{K}^{n \times 1}$ formada por autovectores de A.



# Espacio de autovectores
Sea $A \in \mathbb{K}^{n \times n}$ y sea $\lambda$ un autovalor de $A$, se define el espacio de autovectores como:
$$
E_{\lambda}(A) = \{ v \in \mathbb{K}^{n \times 1}, v \neq 0 : Av = \lambda v  \}
$$




# Teorema de los valores propios de matrices semejantes
Matrices semejantes tienen los mismos valores propios

## Prueba
Sea $A$ y $B$ matrices similares; es decir,

$$
B = PAP^{-1}
$$
Veremos que $A$ y $B$ tienen el mismo polinomio característico. En efecto,

$$
\begin{aligned}
\det(B - \lambda I) &= \det(PAP^{-1} - \lambda I) \\ \\
&= \det(P(A - \lambda I)P^{-1}) \\ \\
&= \det P \det(A - \lambda I) \det P^{-1} \\ \\
&= \det(A - \lambda I)
\end{aligned}
$$


# Teorema sobre los valores propios de $p(A)$

Si $\lambda$ es un valor propio de la matriz $A$ y $p$ es un polinomio, entonces $p(\lambda)$ es un valor propio de $p(A)$.
![[Pasted image 20240516115747.png]]
## Prueba
Sea $Ax = \lambda x$ con $x \ne 0$. Entonces $A^2 x = \lambda Ax = \lambda^2 x$. Por inducción y una verificación separada para $k = 0$, tenemos

$$
A^k x = \lambda^k x \quad (k \ge 0)
$$

Por lo tanto, $\lambda^k$ es un valor propio de $A^k$. Para un polinomio $p$, escribimos $p(z) = \sum_{k=0}^{m} c_k z^k$. Entonces
$$
p(A)x = \sum_{k=0}^{m} c_k A^k x = \sum_{k=0}^{m} c_k \lambda^k x = p(\lambda) x \quad \quad \blacksquare
$$
# Radio espectral
El radio espectral de una matriz $A$ esta definida por
$$ \rho(A) = max \{|\lambda|: det(A-\lambda I) = 0 \} $$
Es decir, el radio espectral de $A$ es el máximo de los valores absolutos de los valores propios de $A$.

Entonces, $\rho(A)$ es el menor valor tal que un circulo con este radio y centro en el origen en el plano complejo contiene todos los valores propios de $A$.

## Teorema sobre el radio espectral
El radio espectral satisface la siguiente ecuación
$$ \rho(A) = \underset{\|\cdot\|}{\text{inf}} \: \|A\| $$
en la cual el ínfimo se toma sobre todas las normas matriciales subordinadas.
![[Pasted image 20240507145703.png]]
![[Pasted image 20240507145713.png]]
