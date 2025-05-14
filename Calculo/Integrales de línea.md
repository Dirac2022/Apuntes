La integral de línea puede considerarse como una generalización de la integral $\int_a^b f(x)dx$. El intervalo $[a, b]$ se sustituye por una curva $k$ en $\mathbb{R}^n$ y el integrando, por una **función escalar** (**campo escalar**) definida y acotada en $k$ o por una **función vectorial** (**campo vectorial**) definida y acotada en $k$.

# Integral de línea de primer tipo

## Definición
Sean $k$ un arco o una curva cerrada, suave y simple en $\mathbb{R}^n$, $\vec{r}(t)$ una parametrización de $k$ en $[a, b]$ y $f$ una función escalar definida y acotada en $k$  $(f : k \to \mathbb{R})$. Entonces la integral de línea de primer tipo de $f$ sobre $k$ se denota por 
$$
\int_k f \cdot ds
$$
y se define por
$$
\int_k f \cdot ds = \int_a^b (f \circ \vec{r})(t) \|\vec{r} \ '(t)\|dt
$$
siempre que exista la integral (Riemann) de la derecha.

## Observación

1. Si $k$ es una curva suave a pedazos que es suma de las curvas suaves $k_i$, $i=1,2, \dots n-1$ y además cada $k_i$ es simple, entonces
$$
\int_s f \cdot ds = \sum_{i=0}^n \ \int_{k_i} f \cdot ds
$$
2. f
3. f
4. f
5. f
6. f

## Aplicación

# Integral de línea de segundo tipo
## Definición
Sean $k$ un arco suave y simple o una curva cerrada suave y simple en $\mathbb{R}^n$, $\vec{r}(t)$, $t \in [a, b]$ una parametrización de $k$ y $\vec{F} : k \to \mathbb{R}^n$ una función vectorial definida y acotada sobre $k$. La integral de línea de segundo tipo de $\vec{F}$ sobre $k$ se denota por
$$
\int_k \vec{F} \cdot d\vec{r}
$$
y se define por
$$
\int_k \vec{F} \cdot d\vec{r} = \int_a^b (\vec{F} \circ \vec{r})(t) \ \cdot \vec{r} \ '(t)dt
$$
siempre que exista la integral (Riemann) de la derecha y donde $\cdot$ denota el producto escalar en $\mathbb{R}^n$.

## Observaciones
1. f
2. f
3. f
4. f
5. f
6. f


# Relación entre las integrales de línea de primer y segundo tipo



# Teorema de Green
Se relaciona una integral de línea de segundo tipo sobre un contorno de $\mathbb{R}^2$ con una integral doble.

## Teorema de Green para contornos
Sean $k$ un contorno de $R^2$ y $D$ su interior, $P$, $Q$ funciones reales continuamente diferenciables en un conjunto abierto $U \subset \mathbb{R}^2$, tal que $U \supset k \cup D = R$ y $P, Q : U \to \mathbb{R}$. Entonces
$$
\iint_R \left(\frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y}\right)dxdy = \oint_k Pdx + Qdy
$$
donde el contorno $k$ se recorre en sentido positivo.
