
# Bola abierta y cerrada
La bola abierta y la bola cerrada de centro $x_0 \in \mathbb{R}^n$ y radio $r$, son los siguientes conjuntos:
$$
B_r(x_0) = \{x \in \mathbb{R}^n : \|x - x_0\| < r\},
$$
$$
B_r[x_0] = \{x \in \mathbb{R}^n : \|x - x_0\| \leq r\},
$$
respectivamente.

# Punto interior
Sea $A \subset \mathbb{R}^n$ un conjunto no vacío. Un punto $x_0 \in A$ es llamado punto interior de $A$ si
$$
\exists r > 0 \text{ tal que } B_r(x_0) \subset A.
$$

El conjunto se dice:
## Conjunto abierto
**Conjunto abierto**, cuando cada uno de sus puntos es punto interior, es decir, si
$$
\forall x \in A: \exists r > 0 \text{ tal que } B_r(x) \subset A.
$$

## Conjunto cerrado
**Conjunto cerrado**, cuando su complemento $\mathbb{R}^n \setminus A$ es abierto.


# Punto frontera
Sea $A \subset \mathbb{R}^n$ un conjunto no vacío. Un punto $x_0 \in \mathbb{R}^n$ se dice que es punto frontera de $A$ si
$$
\forall r > 0 : B_r(x_0) \cap A \neq \emptyset \text{ y } B_r(x_0) \cap A^c \neq \emptyset.
$$

## Frontera de un conjunto
La frontera de $A$ es el conjunto $\partial A$ constituido por todos los puntos frontera de $A$. La clausura de $A$ es el conjunto $A \cup \partial A$; a este lo denotamos como $\overline{A}$, es decir, $\overline{A} = A \cup \partial A$. El conjunto se dice **acotado** cuando existe $r > 0$ tal que $A \subset B_r(0)$, es decir, cuando
$$
\exists r > 0 \text{ tal que } \forall x \in A : \|x\| < r.
$$

# Punto de acumulación
Sea $A \subset \mathbb{R}^n$. Un punto $x_0 \in \mathbb{R}^d$ se dice que es punto de acumulación (p.a.) de $A$ si toda bola abierta centrada en $x_0$ interseca a $A$ en al menos un punto distinto de $x_0$, es decir,
$$
\forall \delta > 0, \text{ la bola } B_\delta(x_0) \cap A \setminus \{x_0\} \neq \emptyset.
$$

