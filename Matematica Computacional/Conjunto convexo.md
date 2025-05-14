
# Norma
La norma es una función que asigna a cada vector un número real no negativo, que puede interpretarse como la "longitud" del vector. Formalmente, la norma en un espacio vectorial $\mathbb{R}^n$ se define como:

$$
\|\mathbf{x}\| = \sqrt{x_1^2 + x_2^2 + \dots + x_n^2}
$$

donde $\mathbf{x} = (x_1, x_2, \dots, x_n)$.

# Distancia Euclidiana
La distancia euclidiana entre dos puntos $\mathbf{x} = (x_1, x_2, \dots, x_n)$ y $\mathbf{y} = (y_1, y_2, \dots, y_n)$ en $\mathbb{R}^n$ es la norma de la diferencia de los vectores que representan estos puntos:

$$
d(\mathbf{x}, \mathbf{y}) = \|\mathbf{x} - \mathbf{y}\| = \sqrt{(x_1 - y_1)^2 + (x_2 - y_2)^2 + \dots + (x_n - y_n)^2}
$$


# Bola Abierta
Sea un punto $\mathbf{a} \in \mathbb{R}^n$. La bola abierta de radio $r > 0$ y centro en $\mathbf{a}$ es el conjunto de todos los puntos que están a una distancia menor que $r$ del punto $\mathbf{a}$.

$$
B(\mathbf{a}, r) = \{\mathbf{x} \in \mathbb{R}^n : d(\mathbf{x}, \mathbf{a}) < r\}
$$

# Conjunto Acotado
Un conjunto $A \subseteq \mathbb{R}^n$ es acotado si existe una bola abierta que lo contenga completamente. Es decir, $A$ es acotado si existe un número real $M > 0$ tal que:

$$
\|\mathbf{x}\| \leq M \quad \text{para todo } \mathbf{x} \in A.
$$

# Punto Interior
Un punto $\mathbf{x} \in A$ se denomina punto interior de $A$ si existe una bola abierta centrada en $\mathbf{x}$ que está completamente contenida en $A$. Formalmente:

$$
\mathbf{x} \text{ es interior a } A \iff \exists r > 0 \text{ tal que } B(\mathbf{x}, r) \subset A
$$
Denotaremos por $int(A)$ al conjunto de puntos interiores de $A$.
# Conjunto Abierto
Un conjunto $A \subseteq \mathbb{R}^n$ es abierto si para cada punto $\mathbf{x} \in A$, $\mathbf{x}$ es un punto interior de $A$. Decimos que $A$ es abierto si $A=int(A)$.

# Conjunto Cerrado
Un conjunto $A \subseteq \mathbb{R}^n$ es cerrado si contiene todos sus puntos límite. Alternativamente, un conjunto es cerrado si su complemento es un conjunto abierto.

# Segmento lineal

Un segmento en $\mathbb{R}^n$ es el conjunto de todos los puntos que se pueden escribir como una combinación convexa de dos puntos $\mathbf{x}, \mathbf{y} \in \mathbb{R}^n$. 

- **Cerrado**
$$
[\mathbf{x}, \mathbf{y}] = \{ \mathbf{z} \in \mathbb{R}^n : \mathbf{z} = \lambda \mathbf{x} + (1 - \lambda) \mathbf{y}, \, 0 \leq \lambda \leq 1 \}
$$

- **Abierto**
$$
]\mathbf{x}, \mathbf{y}[ = \{ \mathbf{z} \in \mathbb{R}^n : \mathbf{z} = \lambda \mathbf{x} + (1 - \lambda) \mathbf{y}, \, 0 < \lambda < 1 \}
$$
# Conjunto Compacto
Un conjunto $A \subseteq \mathbb{R}^n$ es compacto **si es cerrado y acotado**. La compacidad es una propiedad importante porque garantiza que cualquier función continua definida en un conjunto compacto alcanza sus valores máximo y mínimo.

# Frontera
La frontera de un conjunto $A \subseteq \mathbb{R}^n$ es el conjunto de puntos que pueden ser aproximados tanto desde dentro como desde fuera de $A$. Formalmente, la frontera de $A$, denotada como $\partial A$, es el conjunto de puntos $\mathbf{x} \in \mathbb{R}^n$ tales que cualquier bola abierta centrada en $\mathbf{x}$ intersecta tanto $A$ como su complemento.

$$
\partial A = \{\mathbf{x} \in \mathbb{R}^n : \forall r > 0, B(\mathbf{x}, r) \cap A \neq \emptyset \, \text{y} \, B(\mathbf{x}, r) \cap A^c \neq \emptyset \}
$$

# Conjunto Convexo
Un conjunto $C \subseteq \mathbb{R}^n$ es convexo si, para cualquier par de puntos $\mathbf{x}, \mathbf{y} \in C$, el segmento que los une está completamente contenido dentro del conjunto. Es decir:

$$
\begin{aligned}
C \text{ es convexo } &\iff \forall \, \mathbf{x}, \mathbf{y} \in C \ ,\ \forall \lambda \in [0, 1], \lambda \mathbf{x} + (1 - \lambda) \mathbf{y} \in C \\
C \text{ es convexo} &\iff \forall \, \mathbf{x}, \mathbf{y} \in C \ , \ [x, y] \subset C
\end{aligned}
$$

## Teorema
Sean $S_i \in \mathbb{R}^n \, , i = 1, 2, \dots n$ conjuntos convexos arbitrarios, entonces
$$
S = \bigcap^n_{i=1} S_i
$$
es un conjunto convexo.
## Teorema

Sea $\Omega_1, \Omega_2 \subseteq \mathbb{R}^n$ dos conjuntos convexos, entonces:

- $\Omega_1 \cap \Omega_2$ es convexo.
- $\Omega_1 + \Omega_2 = \{ \mathbf{x} + \mathbf{y} \in \mathbb{R}^n : \mathbf{x} \in \Omega_1, \mathbf{y} \in \Omega_2 \}$ es convexo.
- $\Omega_1 - \Omega_2 = \{ \mathbf{x} - \mathbf{y} \in \mathbb{R}^n : \mathbf{x} \in \Omega_1, \mathbf{y} \in \Omega_2 \}$ es convexo.

# Combinación Convexa
Dado $\mathbf{x} \in \mathbb{R}^n$ y $C \subseteq \mathbb{R}^n$, se dice que $\mathbf{x}$ es una combinación convexa de elementos de $C$ si existen $p \in \mathbb{N}$, $\{t_i\}_{i=1}^p \subseteq [0, 1]$ y $\{\mathbf{x}_i\}_{i=1}^p \subseteq C$ tales que:

$$
\mathbf{x} = \sum_{i=1}^p t_i \mathbf{x}_i \quad \text{y} \quad \sum_{i=1}^p t_i = 1
$$

Este texto define formalmente lo que es una combinación convexa en el contexto de un conjunto $C \subseteq \mathbb{R}^n$.



# Cápsula Convexa
Dado un conjunto $C \subseteq \mathbb{R}^n$, la cápsula convexa (o envoltura convexa) de $C$ es el conjunto de todas las combinaciones convexas de los elementos de $C$. Es decir, la cápsula convexa de $C$, denotada por $\text{co}(C)$, se define como:

$$
\text{co}(C) = \left\{ \mathbf{x} \in \mathbb{R}^n : \mathbf{x} = \sum_{i=1}^p t_i \mathbf{x}_i, \text{ con } p \in \mathbb{N}, \{t_i\}_{i=1}^p \subseteq [0, 1], \sum_{i=1}^p t_i = 1, \, \text{y} \, \{\mathbf{x}_i\}_{i=1}^p \subseteq C \right\}
$$

En otras palabras, $\text{co}(C)$ es el conjunto convexo más pequeño que contiene a $C$, formado por todas las posibles combinaciones convexas de los puntos en $C$.

## Teorema
El conjunto $C \subset \mathbb{R}^n$ es convexo $\iff$ $C = co(C)$


# Hiperplano
Sea $\mathbf{a} \in \mathbb{R}^n$ con $\mathbf{a} \neq 0$ y $b \in \mathbb{R}$. Un hiperplano $H$ en $\mathbb{R}^n$ es un conjunto definido como:
$$
H = \{\mathbf{x} \in \mathbb{R}^n : \mathbf{a}^T \mathbf{x} = b\}
$$
El vector $\mathbf{a}$ es un vector normal al hiperplano $H$ y $\mathbf{a}^T \mathbf{x}$ es un producto escalar.
$$
\mathbf{a}^T \mathbf{x} = a_1 x_1 + a_2 x_2 + \cdots + a_n x_n \in \mathbb{R}
$$

**Ejemplo:**

$$
H = \{\mathbf{x} \in \mathbb{R}^2 : 2x_1 + 3x_2 = 5\}
$$

# Semiespacio
Un semiespacio en $\mathbb{R}^n$ es un conjunto definido por una desigualdad lineal. Formalmente, un semiespacio se define como:

$$
H = \{\mathbf{x} \in \mathbb{R}^n : \mathbf{a}^T \mathbf{x} \leq b\ \} 
$$

o el conjunto
$$
H = \{\mathbf{x} \in \mathbb{R}^n :  \mathbf{a}^T \mathbf{x} \geq b\}
$$

donde $\mathbf{a} \in \mathbb{R}^n$ es un vector no nulo y $b$ es un número real. 

> [!tip]
> Los semiespacios son conjuntos convexos.

**Ejemplo:** $$ H = \{\mathbf{x} \in \mathbb{R}^2 : 2x_1 + 3x_2 = 5\} $$
# Poliedro
Un poliedro en $\mathbb{R}^n$ es la intersección finita de semiespacios. Formalmente, se puede definir como:

$$
P = \{\mathbf{x} \in \mathbb{R}^n : \mathbf{a}_i^T \mathbf{x} \leq b_i \text{ para } i = 1, 2, \dots, m\}
$$

donde $\mathbf{a}_i \in \mathbb{R}^n$ y $b_i$ son parámetros que definen los semiespacios. ==Los poliedros son conjuntos convexos== y pueden ser descritos como el conjunto de soluciones a un sistema de desigualdades lineales.

# Punto Extremo
Un punto $\mathbf{x} \in P$ (donde $P$ es un poliedro) se denomina punto extremo si no puede ser representado como una combinación convexa de otros puntos en $P$ distintos de sí mismo. Formalmente, $\mathbf{x}$ es un punto extremo si:

$$
\mathbf{x} \text{ es extremo } \iff \mathbf{x} = \lambda \mathbf{x_1} + (1 - \lambda) \mathbf{x_2} \text{ para } \lambda \in (0, 1) \text{ y } \mathbf{x_1}, \mathbf{x_2} \in P, \Rightarrow \mathbf{x_1} = \mathbf{x_2} = \mathbf{x}.
$$

En otras palabras, $\mathbf{x}$ es un punto extremo si no puede escribirse como una combinación convexa de otros puntos en $P$ distintos de sí mismo. 
