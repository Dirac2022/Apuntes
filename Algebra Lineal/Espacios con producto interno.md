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
