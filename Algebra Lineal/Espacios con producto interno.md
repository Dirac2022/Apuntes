Un **espacio de producto interno** es un sistema algebraico abstracto del cual $\mathbb{C}^n$ es un ejemplo. Es un espacio lineal (sobre el campo complejo) en el cual un producto interno ha sido definido sujeto a estos axiomas:

1. $\langle x, x \rangle > 0 \quad \text{si} \quad x \neq 0$
2. $\langle \alpha x + \beta y, z \rangle = \alpha \langle x, z \rangle + \beta \langle y, z \rangle \quad \alpha, \beta \in \mathbb{C}$
3. $\langle x, y \rangle = \overline{\langle y, x \rangle}$

Las definiciones de norma, ortogonalidad y ortonormalidad son dadas en $\mathbb{C}^n$. Un espacio de producto interno no necesita ser de dimensión finita. Es fácil probar de los axiomas precedentes que $\langle x + y, z \rangle = \langle x, z \rangle + \langle y, z \rangle$ y que $\langle x, \alpha y \rangle = \alpha \langle x, y \rangle$.

La regla de Pitágoras es válida en cualquier espacio de producto interno: Si $\langle x, y \rangle = 0$, entonces

$$
\|x+y\|^2_2 = \|x\|^2_2 + \|y\|^2_2
$$

Esto se deduce de escribir

$$
\|x + y\|_2^2 = \langle x + y, x + y \rangle = \langle x, x \rangle + \langle y, x \rangle + \langle x, y \rangle + \langle y, y \rangle = \|x\|_2^2 + \|y\|_2^2
$$




## Proyección vectorial

Sea $v$, $u$ dos vectores en $\mathbb{R}^n$. La proyección de $u$ sobre $v$ es:

$$
\text{proy}_v u = \dfrac{\langle u, v \rangle}{\|v\|^2} v
$$


# Teorema de Representación de Riesz
Sea $\mathbb{V}$ un espacio vectorial con producto interno. Si $w \in \mathbb{V}$, entonces
$$
\begin{align*}
T_w : \mathbb{V} &\to \mathbb{R} \\
v &\to T_w(v) = \langle v, w \rangle
\end{align*}
$$
es un funcional lineal.

## Teorema de representación de Riesz

>[!tip] Dado un espacio vectorial de dimension finita con producto interno, si existe un funcional lineal que va desde el espacio vectorial, entonces existe un único vector que pertenece al espacio vectorial tal que el funcional lineal se calcula como el producto interno con este único vector.

Dado un espacio vectorial $\mathbb{V}$ de dimensión finita con producto interno. Si $f: \mathbb{V} \to \mathbb{R}$ es un funcional lineal, entonces $\exists! \, w \in \mathbb{V}$, tal que
$$
f(v) = \langle v, w \rangle
$$

