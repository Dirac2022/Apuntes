
Una función real de variable vectorial es toda función del tipo
$$
f : X \rightarrow \mathbb{R},
$$
donde $X \subset \mathbb{R}^m$ es un conjunto no vacío.

Se denomina:
- **Dominio** de la función $f$, al conjunto $X$;
- **Rango** de la función $f$, al conjunto $f(X)$; y
- **Gráfica** de la función $f$, al conjunto
$$
\text{Gráfica}(f) = \{(x, f(x)) \mid x \in X\}.
$$


# Conjuntos de nivel
Sea $f : X \rightarrow \mathbb{R}$ una función definida en el conjunto no vacío $X \subset \mathbb{R}^n$. Se llama conjunto de nivel $c$ ($c \in \mathbb{R}$) de la función $f$, al conjunto $f_c$ constituido por todos aquellos $x \in X$ de imagen igual a $c$, esto es
$$
f_c = \{x \in X \mid f(x) = c\}.
$$

**Observación 1**
Los conjuntos de nivel de una función son aquellos conjuntos $Y$ contenidos en el dominio, donde la función se mantiene constante.


# Teorema de Weierstrass
Sea $A \subset \mathbb{R}^n$ un conjunto compacto y $f : A \rightarrow \mathbb{R}$ una función continua en $A$. Entonces $f$ alcanza su máximo y su mínimo en $A$; es decir, existen puntos $x_0, x_1 \in A$ en donde $f$ tiene un mínimo y un máximo absolutos.

**Demostración:** Sabemos que $f(A)$ es cerrado y acotado. Por ser acotado existen $\alpha = \inf f(A)$ y $\beta = \sup f(A)$, números reales. Por definición, $\alpha$ y $\beta$ son puntos de acumulación de $f(A)$; pero como $f(A)$ es cerrado, se debe tener que $\alpha, \beta \in f(A)$. Es decir, existen $x_0, x_1 \in A$ tales que $\alpha = f(x_0)$ y $\beta = f(x_1)$




# Derivada direccional
Sea $f : U \rightarrow \mathbb{R}$ una función definida en un conjunto abierto $U \subset \mathbb{R}^n$. La derivada direccional de $f$ en el punto $x_0$, en la dirección del vector no nulo $v$, es
$$
f_v(x_0) := \frac{\partial f}{\partial v}(x_0) := D_v f(x_0) := \lim_{h \rightarrow 0} \frac{f(x_0 + h v) - f(x_0)}{h},
$$
en el caso que el límite exista.

La función derivada direccional de $f$ en la dirección de $v$ es la función $D_v f : U \rightarrow \mathbb{R}$ definida como
$$
(D_v f)(x) = D_v f(x).
$$


y su dominio es el conjunto de puntos donde esté definida la
derivada direccional.

# Teorema del valor medio
Sea $f : U \rightarrow \mathbb{R}$ una función definida en un conjunto abierto $U \subset \mathbb{R}^n$, tal que $D_v f$ existe en cada punto del segmento rectilíneo cerrado $[x, x + v]$ contenido en $U$. Entonces, en el segmento $[x, x + v]$ hay un punto $x + \lambda v$, para algún escalar $0 < \lambda < 1$, tal que
$$
f(x + v) - f(x) = D_v f(x + \lambda v).
$$

## Demostración
Parametricemos el segmento $[x, x + v]$ mediante la función $g : [0, 1] \rightarrow [x, x + v]$ definida como $g(t) = x + t v$. Con respecto a la composición
$$
[0, 1] \xrightarrow{g} [x, x + v] \xrightarrow{f} \mathbb{R},
$$
es claro que es continua. Afirmo que esta función es diferenciable en el intervalo abierto $(0, 1)$. En efecto, dado $a \in (0, 1)$ tenemos que

$$
\begin{aligned}
(f \circ g)'(a) &= \lim_{h \rightarrow 0} \frac{(f \circ g)(a + h) - (f \circ g)(a)}{h} \\
&= \lim_{h \rightarrow 0} \frac{f(x + a v + h v) - f(x + a v)}{h} = \frac{\partial f}{\partial v}(x + a v)
\end{aligned}
$$

Luego, por el Teorema del Valor Medio para funciones reales, existe $\lambda \in (0, 1)$ tal que
$$
(f \circ g)(1) - (f \circ g)(0) = (f \circ g)'(\lambda),
$$
esto es
$$
f(x + v) - f(x) = D_v f(x + \lambda v).
$$

# Derivadas parciales

>[!info] Las derivadas direccionales en la dirección de los vectores canónicos se llaman derivadas parciales.

Sea $f$ una función real definida sobre un conjunto abierto de $\mathbb{R}^n$. La $k$-ésima derivada parcial de $f$ en el punto $x_0$ es la derivada direccional $D_{e_k} f(x_0)$ de dicha función en dicho punto, en la dirección del vector canónico $e_k$, $1 \leq k \leq n$, esto es
$$
\frac{\partial f}{\partial x_k}(x_0) := D_k f(x_0) := \lim_{h \rightarrow 0} \frac{f(x_0 + h e_k) - f(x_0)}{h}.
$$

# Gradiente de una función
El **gradiente** de una función de varias variables es un vector que contiene todas las derivadas parciales de la función. Si tenemos una función $f(x_1, x_2, \dots, x_n)$, su gradiente es:

$$
\nabla f(x_1, x_2, \dots, x_n) = \left( \frac{\partial f}{\partial x_1}, \frac{\partial f}{\partial x_2}, \dots, \frac{\partial f}{\partial x_n} \right)
$$

> [!tip]
El gradiente apunta en la dirección del máximo incremento de la función, y se utiliza en métodos de optimización, como el **gradiente descendente**, para minimizar funciones.


# Funciones dos veces diferenciables
Sea $f : U \rightarrow \mathbb{R}$ diferenciable en el abierto $U \subset \mathbb{R}^n$. Si todas las derivadas parciales $\frac{\partial f}{\partial x_i} : U \rightarrow \mathbb{R}$ son diferenciables en $a \in U$, entonces se dice que $f$ es dos veces diferenciable en $a$. Diremos que $f$ es 2 veces diferenciable sobre $U$ si es 2 veces diferenciable en cada punto de $U$.

**Observación**
Si $f$ es dos veces diferenciable en $a$, entonces para todo $i, j = 1, 2, \ldots, n$, existen las derivadas de segundo orden:
$$
\frac{\partial}{\partial x_j} \left( \frac{\partial f}{\partial x_i} \right) (a) = \frac{\partial^2 f}{\partial x_j \partial x_i} (a).
$$
Además, como sus derivadas parciales son diferenciables, entonces son continuas y por tanto $f$ es de clase $C^1$.

# Funciones k veces diferenciables
Si $f : U \rightarrow \mathbb{R}$ es $k - 1$ veces diferenciable en el abierto $U \subset \mathbb{R}^n$ y si todas las derivadas parciales de orden $k - 1$ son diferenciables en $a \in U$, entonces se dice que $f$ es $k$ veces diferenciable en $a$.



# Teorema de Schwartz Global

Dado $U \subset \mathbb{R}^2$ abierto. Sea $f : U \rightarrow \mathbb{R}$ tal que existen las siguientes funciones derivadas 
$$\frac{\partial f}{\partial y} : U \rightarrow \mathbb{R}$$ y $$\frac{\partial^2 f}{\partial x \partial y} : U \rightarrow \mathbb{R}$$.
Si dichas funciones son continuas en $U$, entonces existe $\frac{\partial^2 f}{\partial y \partial x} : U \rightarrow \mathbb{R}$ y se verifica
$$
\frac{\partial^2 f}{\partial x \partial y} = \frac{\partial^2 f}{\partial y \partial x}.
$$

## Demostración
i) Dado $(x, y) \in U$, $b \in \mathbb{R}$ con $(x, b) \in U$, se tiene por el Teorema Fundamental del Cálculo:
$$
\int_b^y \frac{\partial f}{\partial y} (x, t) \, dt = f(x, y) - f(x, b).
$$

ii) Derivamos con respecto a $x$ e ingresamos la derivada a la integral (Regla de Leibniz). Debido a la continuidad de $\frac{\partial^2 f}{\partial x \partial y}$, se obtiene
$$
\int_b^y \frac{\partial}{\partial x} \frac{\partial f}{\partial y} (x, t) \, dt = \frac{\partial f}{\partial x} (x, y) - \frac{\partial f}{\partial x} (x, b).
$$

iii) Se deriva con respecto a $y$. La conclusión se sigue usando de nuevo el Teorema Fundamental del Cálculo:
$$
\frac{\partial^2 f}{\partial x \partial y} (x, y) = \frac{\partial^2 f}{\partial y \partial x} (x, y) \quad \forall (x, y) \in U.
$$


# Funciones de clase $C^k$

Se dice que $f$ es de clase $C^k$, con $k \in \mathbb{N}$, sobre un conjunto abierto $U \subset \mathbb{R}^n$, lo que escribiremos: $f \in C^k(U)$, si todas las derivadas parciales de orden $k$ de $f$ existen y son continuas en $U$.

## Funciones de clase $C^0$ y $C^{\infty}$ 
Se dice que $f$ es de clase $C^0$ sobre el abierto $U \subset \mathbb{R}^n$, si $f$ es continua sobre $U$. También diremos que $f$ es de clase $C^\infty$ sobre $U$, si $f \in C^k(U)$ para todo $k \geq 0$.

**Observación**
- Si $f \in C^k(U)$, con $U \subset \mathbb{R}^n$ abierto, entonces $f$ es $k$-veces diferenciable.
- La viceversa generalmente no se cumple


## Teorema de Schwartz (Local)
Dada $f : U \rightarrow \mathbb{R}$ definida en el abierto $U \subset \mathbb{R}^n$ y $c \in U$. Si $f \in C^2(V)$, donde $V$ es una vecindad de $c$, entonces se cumple para $i, j = 1, \cdots, n$:

$$
\frac{\partial^2 f}{\partial x_i \partial x_j}(c) = \frac{\partial^2 f}{\partial x_j \partial x_i}(c).
$$

# Teorema de Taylor

## Derivada segunda
Si $f : U \rightarrow \mathbb{R}$ es dos veces diferenciable en $a \in U \subset \mathbb{R}^n$, entonces, la segunda derivada de $f$ en $a$ se define como la aplicación bilineal:

$$
f^{(2)}(a) : \mathbb{R}^n \times \mathbb{R}^n \rightarrow \mathbb{R},
$$

cuyo valor en el punto $(v, w) \in \mathbb{R}^n \times \mathbb{R}^n$ es el escalar:

$$
f^{(2)}(a)(v, w) := \frac{\partial}{\partial w} \left( \frac{\partial f}{\partial v} \right)(a) = \frac{\partial^2 f}{\partial w \partial v}(a).
$$

## Derivada de Orden $k > 2$
Si $f : U \rightarrow \mathbb{R}$ es $k > 2$ veces diferenciable en $a \in U \subset \mathbb{R}^n$, entonces la $k$-ésima derivada de $f$ en $a$ se define como la aplicación $k$-lineal:

$$
f^{(k)}(a) : \mathbb{R}^n \times \cdots \times \mathbb{R}^n \quad (\text{$k$ veces}) \rightarrow \mathbb{R},
$$

para todo $(v_1, \cdots, v_k) \in \mathbb{R}^n \times \cdots \times \mathbb{R}^n$:

$$
f^{(k)}(a)(v_1, \cdots, v_k) = \frac{\partial^k f}{\partial v_k \cdots \partial v_1}(a).
$$

1|Hessiana)**

Sea $f : U \rightarrow \mathbb{R}$ una función en el abierto $U \subset \mathbb{R}^n$. La matriz Hessiana de $f$ en $x \in U$, denotada por $H(x)$, se define como:

$$
H(x) = \left[ \frac{\partial^2 f}{\partial x_j \partial x_i}(x) \right]_{i, j=1, \cdots, n},
$$

siempre que existan las derivadas parciales de segundo orden $\frac{\partial^2 f}{\partial x_j \partial x_i}$ en $x$ para $i, j = 1, \cdots, n$.

**Teorema (Taylor de Orden 2)**

Sea $f : U \rightarrow \mathbb{R}$ definida en el abierto $U \subset \mathbb{R}^n$ y $x_0 \in U$. Si $f \in C^2(V)$, donde $V$ es una vecindad de $x_0$, entonces, para todo $h \in \mathbb{R}^n$ con $x_0 + h \in V$, existe $0 < \xi < 1$ tal que:

$$
f(x_0 + h) = f(x_0) + \nabla f(x_0) \cdot h + \frac{1}{2} h^T H(x_0 + \xi h) h.
$$

**Teorema (Taylor de Orden 2) Continuación**

También se puede escribir como:

$$
f(x_0 + h) = f(x_0) + \nabla f(x_0) \cdot h + \frac{1}{2} h^T H(x_0) h + r(h),
$$

donde $r(h)$ tiene la propiedad:

$$
\lim_{h \rightarrow 0} \frac{r(h)}{\|h\|^2} = 0.
$$

**Observación**

Por el Teorema de Schwartz Local se tiene que la matriz Hessiana es simétrica.

**Observación**

Dado $h = (h_1, \cdots, h_n) \in \mathbb{R}^n$, la segunda derivada de $f$ en $a$ se expresa como:

$$
\frac{\partial^2 f}{\partial h^2}(a) = \frac{\partial}{\partial h} \left( \sum_{j=1}^n h_j \frac{\partial f}{\partial x_j} \right)(a) = \sum_{i=1}^n \sum_{j=1}^n h_i h_j \frac{\partial^2 f}{\partial x_i \partial x_j}(a) = h^T H(a) h.
$$
