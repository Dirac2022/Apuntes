

# Problema General con Restricciones

El problema de optimización con restricciones consiste en maximizar o minimizar una función objetivo $f(x_1, x_2, ..., x_n)$ sujeta a un conjunto de restricciones. Estas restricciones pueden ser igualdades o desigualdades. El problema se plantea como:
Sea la función $f : \Omega \subset \mathbb{R}^n \to \mathbb{R}$ se tiene el siguiente problema de optimización con restricciones de igualdad:

$$
\begin{aligned}
\text{min o max} &\quad f(x) \\
\text{sujeto a} \\
&\phi_1 (x) = 0 , \\
&\phi_2 (x) = 0 , \\
&\vdots \\
&\phi_m (x) = 0 , \\
&x \in \Omega \subset \mathbb{R}^n
\end{aligned}
$$
donde las funciones $f$, $\phi_i , \ i = 1, 2, \dots , m$ son continuas, y con segundas derivadas parciales continuas.

# Función de Lagrange

La **función de Lagrange** transforma un problema de optimización con restricciones en uno sin restricciones mediante el uso de multiplicadores de Lagrange $\lambda_i$. La función de Lagrange se define como:

$$
\mathcal{L} : \mathcal{R}^m \times \Omega \to \mathcal{R}
$$
$$
\mathcal{L}(x_1, x_2, ..., x_n, \lambda_1, ..., \lambda_m) = f(x_1, x_2, ..., x_n) + \sum_{i=1}^{m} \lambda_i g_i(x_1, x_2, ..., x_n)
$$
$$
\mathcal{L}(\lambda, x) = f(x) + \langle \lambda, \phi(x) \rangle = f(x) + \sum_{i=1}^m \lambda_i \phi_i (x)
$$

a esta nueva función se le denomina la función de Lagrange y los $\lambda_i$ son los **multiplicadores de Lagrange**

Los multiplicadores $\lambda_i$ son variables auxiliares que penalizan cualquier desviación de las restricciones $g_i(x) = 0$. El objetivo es encontrar los valores de $x_j$ y $\lambda_i$ que satisfacen las condiciones necesarias de óptimo.


## Teorema
Se cumple que si $(\lambda_0, x_1, x_2, \dots , x_n)$ es un máximo o un mínimo relativo de la función de Lagrange $\mathcal{L}$ entonces $(x_1, x_2, \dots , x_n)$ es un máximo o mínimo relativo de la función $f$ sujeto a la restricción $\phi(x_1, x_2, \dots , x_n) = 0$ 


# Matriz Hessiana Orlada o Aumentada

La **matriz Hessiana orlada** o **aumentada** es una herramienta que se utiliza para verificar si un punto crítico es un mínimo o un máximo cuando se trabaja con restricciones. Esta matriz combina la segunda derivada de la función objetivo con la información de las restricciones. Se construye a partir de la Hessiana de la función objetivo y las derivadas de las restricciones. 


$$ H (\phi_1, \dots \phi_m, x_1, \dots, x_n) =
\begin{pmatrix}
0 & \cdots & 0 & \phi_{1x_1} & \cdots & \phi_{1x_n} \\
\vdots & \cdots & \vdots & \vdots & \cdots & \vdots \\
0 & \cdots & 0 & \phi_{mx_1} & \cdots & \phi_{mx_n} \\
\phi_{1x_1} & \cdots & \phi_{mx_1} & \mathcal{L}_{x_1x_1} & \cdots & \mathcal{L}_{x_1x_n} \\
\vdots & \cdots & \vdots & \vdots & \cdots & \vdots \\
\phi_{1x_n} & \cdots & \phi_{mx_n} & \mathcal{L}_{x_nx_1} & \cdots & \mathcal{L}_{x_nx_n} \\
\end{pmatrix}
$$

$$ H (\phi_1, \dots \phi_m, x_1, \dots, x_n) =
\begin{pmatrix}
0 & \cdots & 0 & (\nabla \phi_{1})^T \\
\vdots & \cdots & \vdots & \vdots \\
0 & \cdots & 0 & (\nabla\phi_{m})^T \\
\nabla\phi_{1} & \cdots & \nabla\phi_{m} & \nabla^2 L
\end{pmatrix}
$$


Donde:
- $\nabla^2 \mathcal{L}$ es la matriz Hessiana de la función objetivo $\mathcal{L}$ (las segundas derivadas de $\mathcal{L}$ respecto a las variables $x_1, x_2, ..., x_n$).
- $\nabla \phi_i$ son los gradientes de las funciones de restricción.

# Procedimiento de Optimización

- Determinar los puntos críticos (posibles máximos o mínimos)
- Aplicar el siguiente teorema (Criterio de la Segunda Derivada)

## Teorema
Sean $H_1, \dots, H_{n+1}$ los menores principales de la matriz hessiana orlada $H$ evaluada en un punto crítico. Si
1. $H_k < 0$ para todo $k = 2m + 1, \dots , \ n+m$ (esto corresponde a los $n-m$ últimos menores principales), entonces el punto crítico es un mínimo.
2. $(-1)^kH_k < 0$ para todo $k=2m + 1 , \dots , \ n + m$ , entonces el punto crítico es un máximo.



# Para Funciones de Dos Variables con una Restricción
Sea la función $f : \Omega \subset \mathbb{R}^2 \to \mathbb{R}$

$$
\begin{aligned}
\text{minimizar} &\quad f(x, y) \\
\text{sujeto a} \\
&\phi(x, y) = 0 , \\
\end{aligned}
$$

La [[#Función de Lagrange]] es
$$
\mathcal{L}(\lambda, x, y) = f(x, y) + \lambda \, \phi(x, y)
$$
donde $\lambda \in \mathbb{R}$ y $(x, y) \in \Omega$. La matriz [[#Matriz Hessiana Orlada o Aumentada|hessiana orlada]] es

$$
H(\lambda, x, y) = 
\begin{pmatrix}
0 & \phi_x & \phi_y \\
\phi_x & \mathcal{L}_{xx} & \mathcal{L}_{xy} \\
\phi_y & \mathcal{L}_{yx} & \mathcal{L}_{yy} \\
\end{pmatrix}
$$

Cuando $n = 1$ y $m=1$ se obtiene lo siguiente:

## Teorema (Criterio de la Segunda Derivada)
Sea $(\lambda_0, x_0, y_0)$ un punto crítico de $\mathcal{L}(\lambda, x, y)$

1. Si $\Delta(\lambda_0, x_0, y_0) < 0$ , entonces $(x_0, y_0)$ es **mínimo** relativo de $f$ sujeto a la restricción $\phi(x, y)=0$.
2. Si $\Delta(\lambda_0, x_0, y_0) > 0$ , entonces $(x_0, y_0)$ es **máximo** relativo de $f$ sujeto a la restricción $\phi(x, y)=0$.
### 8. Ejemplo

**Problema**: Minimizar $f(x, y) = x^2 + y^2$ sujeto a la restricción $g(x, y) = x + y - 1 = 0$.

1. **Función de Lagrange**:
   $$
   \mathcal{L}(\lambda, x, y) = x^2 + y^2 + \lambda(x + y - 1)
   $$

2. **Condiciones de primer orden**:
   $$
   \frac{\partial \mathcal{L}}{\partial x} = 2x + \lambda = 0, \quad \frac{\partial \mathcal{L}}{\partial y} = 2y + \lambda = 0, \quad \frac{\partial \mathcal{L}}{\partial \lambda} = x + y - 1 = 0
   $$

3. **Solución del sistema**:
   $$
   2x + \lambda = 0 \quad \Rightarrow \quad \lambda = -2x
   $$
   $$
   2y + \lambda = 0 \quad \Rightarrow \quad \lambda = -2y
   $$
   $$
   -2x = -2y \quad \Rightarrow \quad x = y
   $$
   $$
   x + y - 1 = 0 \quad \Rightarrow \quad 2x = 1 \quad \Rightarrow \quad x = \frac{1}{2}, \, y = \frac{1}{2}
   $$

- El punto $(x, y) = \left( \frac{1}{2}, \frac{1}{2} \right)$ es un candidato a mínimo.
- El punto crítico es $(-1, 1/2, 1/2)$, por criterio de la segunda derivada $det(H_3) = -4 < 0$
- Por tanto $(1/2, 1/2)$ es un mínimo de $f$ sujeto a la restricción $x+y=1$

# Condiciones de Karush-Kuhn-Tucker

Las **Condiciones de Karush-Kuhn-Tucker (KKT)** son un conjunto de condiciones necesarias para que un punto sea una solución óptima en problemas de optimización con restricciones. Estas condiciones son muy utilizadas en la optimización no lineal, especialmente cuando existen restricciones de igualdad y desigualdad.

### Contexto

Cuando se aborda un problema de optimización con restricciones, la idea básica es encontrar un punto donde una función objetivo $f(x)$ sea maximizada o minimizada, sujeto a ciertas restricciones que pueden ser de igualdad o desigualdad. Este tipo de problemas se pueden expresar de la siguiente forma:

$$
\text{Minimizar:} \quad f(x)
$$

$$
\text{Sujeto a:} \quad g_i(x) \leq 0, \quad i = 1, 2, ..., p
$$

$$h_j(x) = 0, \quad j = 1, 2, ..., m
$$
Aquí, $g_i(x)$ son las restricciones de desigualdad y $h_j(x)$ son las restricciones de igualdad.


## Condiciones de Karush-Kuhn-Tucker
Si existe $x_0 \in \Omega$ , $\lambda  \in \mathbb{R}^m$ y $\mu \in \mathbb{R}^p_+$ tal que
	
Función de Lagrange
$$
 f(x) + \sum_{j=1}^m \lambda_j \, h_j \, (x) + \sum_{i=1}^p \mu_j \, g_i (x) = \theta_n
$$

### Condiciones
$$
\begin{aligned}
\nabla f(x_0) + \sum_{j=1}^m \lambda_j \,\nabla h_j \, (x_0) + \sum_{i=1}^p \mu_j \,\nabla g_i (x_0) &= \theta_n  \\ \\
h(x_0) &= \theta_m  \\ \\
g(x_0) &\leq \theta_p \\ \\
\mu \cdot g(x_0) &= 0
\end{aligned}
$$
donde $\theta_k$ es el vector nulo de dimensión $k$. Entonces $x_0$ es un mínimo de $f$.
