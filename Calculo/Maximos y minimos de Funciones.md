
- Puntos de inflexion, teorema respecto a si es dos veces derivable, y si se cumple la reciprocidad
- maximos y minimos (globales y locales)
- Minimizacion y maximizacion de funciones convexas, teorema dada una funcion convexa definida en un conjunto convexo si alcanza su minimo de que naturaleza es, teorema dada una funcion convexa en un conjunto convexo, si tiene un maximo, donde se alcanza ese maximo (si es un punto extremo)
- Punto critico y sus dos condiciones
- Punto critico en una funcion en varias variables (respecto a sus derivadas parciales), teorema respecto a u minimo o maximo local, reciprocidad
- Punto de silla
- Matriz hessiana, matrices menores, menores principales de la matriz hessiana
- Matriz escalonada (usando concepto de pivote)
- Matriz reducida
- Matriz definida positiva, su relacion con la matriz reducida, su relacion con los autovalores, la relacion con los menores principales
- Matriz definida negativa, su relacion con la matriz reducida, su relacion con los autovalores, su relacion con los menores principales
- Teorema que relaciona la continuidad de la segunda derivada, la matriz hessiana y maximos y minimos
- Hessiano para funciones de dos variables
- Maximos y minimos para funciones de dos variables (Criterio de la segunda derivada)
- Maximos y minimos para funciones de dos variables (Criterio de la segunda derivada

---



# Funciones de varias variables (una, dos y tres variables)

- **Funciones de una variable**: Son funciones de la forma $f(x)$, donde $x \in \mathbb{R}$ es el único argumento de la función. Ejemplo: $f(x) = x^2 + 3x + 2$.

- **Funciones de dos variables**: Son funciones de la forma $f(x, y)$, donde $(x, y) \in \mathbb{R}^2$. Ejemplo: $f(x, y) = x^2 + y^2$. Estas funciones se suelen representar mediante superficies en el espacio tridimensional.

- **Funciones de tres variables**: Son funciones de la forma $f(x, y, z)$, donde $(x, y, z) \in \mathbb{R}^3$. Ejemplo: $f(x, y, z) = x^2 + y^2 + z^2$. Se usan frecuentemente en aplicaciones físicas como campos vectoriales.

[[Calculo Multivariable#Funciones reales de variable vectorial]]







#### Teorema de puntos de inflexión:
Si una función es dos veces derivable, un punto de inflexión es un punto donde la segunda derivada es cero y cambia de signo. Sin embargo, la recíproca no siempre se cumple: que la segunda derivada sea cero no implica necesariamente que haya un punto de inflexión.

### 7. **Máximos y mínimos (globales y locales)**

- **Máximo/Mínimo local**: Un punto $x_0$ es un máximo local si existe un entorno $U$ tal que $f(x_0) \geq f(x)$ para todo $x \in U$. Similarmente, es un mínimo local si $f(x_0) \leq f(x)$ para todo $x \in U$.

- **Máximo/Mínimo global**: Un punto $x_0$ es un máximo global si $f(x_0) \geq f(x)$ para todo $x \in C$, donde $C$ es el dominio de la función. De manera similar, un mínimo global satisface $f(x_0) \leq f(x)$.

### 8. **Minimización y maximización de funciones convexas**

#### Teorema sobre la minimización:
Si una función convexa está definida en un conjunto convexo y alcanza su mínimo, este mínimo es un **mínimo global**. La razón es que la convexidad garantiza que no hay otros puntos "mejores" fuera de este mínimo.

#### Teorema sobre la maximización:
Si una función convexa alcanza un máximo, este máximo solo puede estar en un **punto extremo** del conjunto. Esto se debe a la forma de la gráfica de las funciones convexas.

### 9. **Punto crítico y sus dos condiciones**

Un punto crítico es un punto donde todas las derivadas parciales de una función son cero. Para una función $f(x, y)$, el punto crítico $(x_0, y_0)$ es donde:

$$
\frac{\partial f}{\partial x}(x_0, y_0) = 0 \quad \text{y} \quad \frac{\partial f}{\partial y}(x_0, y_0) = 0
$$

Las dos condiciones que deben cumplirse son:
1. Las derivadas parciales deben ser cero en el punto.
2. Deben analizarse las segundas derivadas para clasificar el punto.

### 10. **Punto crítico en una función de varias variables**

Para una función de varias variables, un punto crítico es donde todas las derivadas parciales se anulan. El teorema relevante es que si una función es dos veces diferenciable en un entorno del punto crítico, se puede clasificar el punto usando la matriz Hessiana (segundas derivadas):

- Si la matriz Hessiana es **positiva definida** en el punto, el punto es un mínimo local.
- Si es **negativa definida**, es un máximo local.
- Si no es definida, el punto es un **punto de silla**.


# Punto crítico
Sea $f : A \rightarrow \mathbb{R}$ una función para la cual existen sus derivadas parciales. Diremos que $P$ es un punto crítico de $f$ si todas sus derivadas parciales son cero en $P$, es decir,
$$
\frac{\partial f}{\partial x_i}(P) = 0, \quad \forall i = 1, \ldots, n.
$$

## Teorema
Sea $f : A \rightarrow \mathbb{R}$ una función para la cual existen sus derivadas parciales. Si $f$ tiene un máximo o mínimo local en $P \in A$, entonces $P$ es un punto crítico.
**El recíproco de este teorema es falso.**

# Punto de silla
Diremos que $P$ es un punto de silla de la función $f$ si es un punto crítico, pero no es ni un máximo ni un mínimo local.

> [!tip]
> Un punto de silla es un punto crítico donde la función no alcanza ni un máximo ni un mínimo local, sino que la función crece en una dirección y decrece en otra


### 3. **Hessiana**

La **matriz Hessiana** es una matriz cuadrada de segundas derivadas parciales de una función escalar. Es esencial para analizar la curvatura de una función y determinar si un punto crítico es un mínimo, un máximo o un punto de silla.

Para una función $f(x, y)$, la matriz Hessiana es:

$$
H(f) = \begin{pmatrix}
\frac{\partial^2 f}{\partial x^2} & \frac{\partial^2 f}{\partial x \partial y} \\
\frac{\partial^2 f}{\partial y \partial x} & \frac{\partial^2 f}{\partial y^2}
\end{pmatrix}
$$

- Si $H(f)$ es **positiva definida**, el punto es un **mínimo local**.
- Si $H(f)$ es **negativa definida**, el punto es un **máximo local**.
- Si $H(f)$ tiene signos mixtos en sus valores propios, el punto es un **punto de silla**.

### 4. **Convexidad en funciones de varias variables**

Una función $f: \mathbb{R}^n \to \mathbb{R}$ es **convexa** si para todo $x, y \in \mathbb{R}^n$ y $\lambda \in [0, 1]$, se cumple que:

$$
f(\lambda x + (1 - \lambda) y) \leq \lambda f(x) + (1 - \lambda) f(y)
$$

Esto significa que la gráfica de la función se encuentra por debajo de cualquier línea recta trazada entre dos puntos en el dominio de la función. Para funciones de varias variables, la **convexidad** está asociada con el **gradiente** y la **matriz Hessiana**.

#### Teorema de convexidad con la matriz Hessiana:
Si la matriz Hessiana de una función es positiva definida en todo su dominio, entonces la función es convexa. Es decir:

$$
H(f(x)) \succ 0 \quad \text{para todo } x \in \mathbb{R}^n
$$

### 5. **Condiciones de optimalidad de primer orden (KKT)**

Las **condiciones de Karush-Kuhn-Tucker (KKT)** son una generalización de las condiciones de Lagrange para problemas de optimización que incluyen restricciones. Estas condiciones combinan el gradiente de la función objetivo con los gradientes de las restricciones.

Para un problema de minimización con restricciones $g(x) \leq 0$, $h(x) = 0$, las condiciones KKT son:

1. **Condición de factibilidad**: El punto $x^*$ satisface las restricciones $g(x^*) \leq 0$ y $h(x^*) = 0$.
2. **Multiplicadores de Lagrange no negativos**: Los multiplicadores asociados a las restricciones $g(x^*)$ deben ser no negativos.
3. **Condiciones de estacionariedad**: El gradiente de la función objetivo en $x^*$ debe ser una combinación lineal de los gradientes de las restricciones activas.

Estas condiciones son esenciales en la optimización no lineal con restricciones.

### 6. **Método del gradiente descendente**

El **gradiente descendente** es un método iterativo utilizado para minimizar funciones diferenciables. La idea es moverse en la dirección opuesta al gradiente, ya que esta dirección apunta hacia el descenso más pronunciado de la función.

Dado un punto inicial $x_0$, las iteraciones se calculan como:

$$
x_{k+1} = x_k - \alpha_k \nabla f(x_k)
$$

Donde $\alpha_k$ es el tamaño del paso, o **learning rate**.

### 7. **Condiciones de optimalidad de segundo orden**

Además de las condiciones de primer orden (que involucran el gradiente), las condiciones de segundo orden usan la **matriz Hessiana** para proporcionar información adicional sobre el tipo de punto crítico (mínimo, máximo o punto de silla):

- **Mínimo local**: El gradiente es cero y la matriz Hessiana es positiva definida en el punto crítico.
- **Máximo local**: El gradiente es cero y la matriz Hessiana es negativa definida en el punto crítico.
- **Punto de silla**: El gradiente es cero, pero la matriz Hessiana no es definida positiva ni definida negativa.

### 8. **Punto de silla en funciones de varias variables**

Un **punto de silla** es un punto crítico en una función de varias variables donde la función tiene un mínimo en una dirección y un máximo en otra. Estos puntos son importantes en optimización porque no son ni máximos ni mínimos locales, pero pueden afectar las estrategias de optimización.

Ejemplo: La función $f(x, y) = x^2 - y^2$ tiene un punto de silla en $(0, 0)$. En la dirección $x$, $f(x, 0) = x^2$, lo que implica un mínimo. Pero en la dirección $y$, $f(0, y) = -y^2$, lo que implica un máximo.

### 9. **Máximos y mínimos globales y locales en funciones de varias variables**

En el contexto de funciones de varias variables:

- Un **máximo local** es un punto donde la función alcanza un valor mayor que en cualquier otro punto cercano. 
- Un **mínimo local** es un punto donde la función alcanza un valor menor que en cualquier otro punto cercano.
  
En contraste:

- Un **máximo global** es el punto donde la función alcanza su valor más alto en todo su dominio.
- Un **mínimo global** es el punto donde la función alcanza su valor más bajo en todo su dominio.

### 10. **Teorema sobre funciones convexas y optimización**

Dado un conjunto convexo $C$ y una función convexa $f: C \to \mathbb{R}$, si $f$ tiene un mínimo en $C$, entonces este mínimo es un mínimo **global**.

- **Teorema de los puntos extremos**: Si $f$ es convexa y alcanza un máximo en un conjunto convexo, entonces este máximo se alcanzará en un **punto extremo** del conjunto.

Estos conceptos son fundamentales en **optimización convexa**, ya que garantizan la unicidad de los mínimos y máximos globales en problemas convexos.

### 11. **Lagrangianos y multiplicadores de Lagrange**

El **método de los multiplicadores de Lagrange** se usa para encontrar los máximos y mínimos de una función $f(x)$ sujeta a restricciones. Se introduce una nueva variable, el **multiplicador de Lagrange** $\lambda$, y se resuelve el sistema de ecuaciones derivado de las condiciones de optimalidad.

El **Lagrangiano** es una función que combina la función objetivo y las restricciones:

$$
\mathcal{L}(x, \lambda) = f(x) + \lambda g(x)
$$

Donde $g(x) = 0$ es la restricción.
