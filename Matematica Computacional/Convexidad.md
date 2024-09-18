
# Conjunto convexo
## Norma
La norma es una función que asigna a cada vector un número real no negativo, que puede interpretarse como la "longitud" del vector. Formalmente, la norma en un espacio vectorial $\mathbb{R}^n$ se define como:

$$
\|\mathbf{x}\| = \sqrt{x_1^2 + x_2^2 + \dots + x_n^2}
$$

donde $\mathbf{x} = (x_1, x_2, \dots, x_n)$.

## Distancia Euclidiana
La distancia euclidiana entre dos puntos $\mathbf{x} = (x_1, x_2, \dots, x_n)$ y $\mathbf{y} = (y_1, y_2, \dots, y_n)$ en $\mathbb{R}^n$ es la norma de la diferencia de los vectores que representan estos puntos:

$$
d(\mathbf{x}, \mathbf{y}) = \|\mathbf{x} - \mathbf{y}\| = \sqrt{(x_1 - y_1)^2 + (x_2 - y_2)^2 + \dots + (x_n - y_n)^2}
$$


## Bola Abierta
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
Un conjunto $A \subseteq \mathbb{R}^n$ es compacto si es cerrado y acotado. La compacidad es una propiedad importante porque garantiza que cualquier función continua definida en un conjunto compacto alcanza sus valores máximo y mínimo.

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




## Función Convexa
Una función $f: \mathbb{R}^n \rightarrow \mathbb{R}$ se dice que es **convexa** si para todos los puntos $x_1, x_2 \in \mathbb{R}^n$ y para cualquier $\lambda \in [0, 1]$, se cumple la siguiente desigualdad:
$$
f(\lambda x_1 + (1 - \lambda) x_2) \leq \lambda f(x_1) + (1 - \lambda) f(x_2).
$$
Esto significa que la línea recta que conecta cualquier par de puntos en el gráfico de la función se encuentra por encima del gráfico de la función.

![Funcion convexa](https://upload.wikimedia.org/wikipedia/commons/d/d6/Convex_function.svg)
## Función Cóncava
Una función $f: \mathbb{R}^n \rightarrow \mathbb{R}$ se dice que es **cóncava** si para todos los puntos $x_1, x_2 \in \mathbb{R}^n$ y para cualquier $\lambda \in [0, 1]$, se cumple la siguiente desigualdad:
$$
f(\lambda x_1 + (1 - \lambda) x_2) \geq \lambda f(x_1) + (1 - \lambda) f(x_2).
$$
Esto significa que la línea recta que conecta cualquier par de puntos en el gráfico de la función se encuentra por debajo del gráfico de la función.



## Epígrafo
El **epígrafo** de una función $f: \mathbb{R}^n \rightarrow \mathbb{R}$ es el conjunto de puntos en $\mathbb{R}^{n+1}$ que están por encima o sobre el gráfico de la función. Formalmente, el epígrafo se define como:
$$
\text{epi}(f) = \{(x, t) \in \mathbb{R}^n \times \mathbb{R} : t \geq f(x)\}.
$$
El epígrafo es un conjunto crucial en el análisis de funciones convexas.

<div style="text-align: center;">
	<figure>
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/00/Epigrafo.svg/220px-Epigrafo.svg.png">
    <figcaption></figcaption>
    </figure>
</div>

## Hipógrafo
El **hipógrafo** de una función $f: \mathbb{R}^n \rightarrow \mathbb{R}$ es el conjunto de puntos en $\mathbb{R}^{n+1}$ que están por debajo o sobre el gráfico de la función. Formalmente, el hipógrafo se define como:
$$
\text{hypo}(f) = \{(x, t) \in \mathbb{R}^n \times \mathbb{R} : t \leq f(x)\}.
$$
El hipógrafo es útil en el análisis de funciones cóncavas.


<div style="text-align: center;">
	<figure>
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/f6/Hipografo.svg/220px-Hipografo.svg.png">
    <figcaption></figcaption>
    </figure>
</div>

## Teorema sobre la Convexidad en Función de su Epígrafo
Una función $f: \mathbb{R}^n \rightarrow \mathbb{R}$ es convexa si y solo si su epígrafo es un conjunto convexo en $\mathbb{R}^{n+1}$.

### Demostración

- ($\Rightarrow$) Si $f$ es convexa, entonces para cualquier par de puntos $(x_1, t_1), (x_2, t_2) \in \text{epi}(f)$, se tiene que $t_1 \geq f(x_1)$ y $t_2 \geq f(x_2)$. Dado que $f$ es convexa, para cualquier $\lambda \in [0, 1]$,
  $$
  \lambda t_1 + (1 - \lambda) t_2 \geq \lambda f(x_1) + (1 - \lambda) f(x_2) \geq f(\lambda x_1 + (1 - \lambda) x_2).
  $$
  Por lo tanto, $\lambda (x_1, t_1) + (1 - \lambda) (x_2, t_2) \in \text{epi}(f)$, lo que demuestra que $\text{epi}(f)$ es convexo.

- ($\Leftarrow$) Si el epígrafo de $f$ es convexo, para cualquier $x_1, x_2 \in \mathbb{R}^n$ y $\lambda \in [0, 1]$, el punto $\lambda (x_1, f(x_1)) + (1 - \lambda) (x_2, f(x_2))$ está en el epígrafo, lo que implica que
  $$
  f(\lambda x_1 + (1 - \lambda) x_2) \leq \lambda f(x_1) + (1 - \lambda) f(x_2).
  $$
  Esto muestra que $f$ es convexa.


## Funciones Diferenciables en $\mathbb{R}^n$

Una función $f: \mathbb{R}^n \rightarrow \mathbb{R}$ es **diferenciable** en un punto $x_0 \in \mathbb{R}^n$ si se cumplen las siguientes condiciones:

1. **Existencia de Derivadas Parciales:** Todas las derivadas parciales de $f$ existen en el punto $x_0$. Esto significa que los límites que definen las derivadas parciales existen para cada una de las coordenadas:
   $$
   \frac{\partial f}{\partial x_i}(x_0) \quad \text{para } i = 1, 2, \dots, n.
   $$

2. **Aproximación Lineal:** Existe un vector gradiente $\nabla f(x_0) \in \mathbb{R}^n$ tal que la función se puede aproximar linealmente alrededor de $x_0$ de la siguiente manera:
   $$
   \lim_{\|h\| \to 0} \frac{f(x_0 + h) - f(x_0) - \nabla f(x_0)^\top h}{\|h\|} = 0,
   $$
   donde $h \in \mathbb{R}^n$ es un pequeño incremento.

   Aquí, el vector $\nabla f(x_0)$ está compuesto por las derivadas parciales de $f$ en $x_0$:
   $$
   \nabla f(x_0) = \left(\frac{\partial f}{\partial x_1}(x_0), \frac{\partial f}{\partial x_2}(x_0), \dots, \frac{\partial f}{\partial x_n}(x_0)\right).
   $$

   Esto significa que no solo deben existir las derivadas parciales, sino que la función debe ser bien aproximada por su plano tangente en la vecindad del punto $x_0$.

### Aproximación de Taylor de Primer Orden

Cuando $f$ es diferenciable en $x_0$, la función se puede aproximar cerca de $x_0$ usando la expansión de Taylor de primer orden:

$$
f(x) \approx f(x_0) + \nabla f(x_0)^\top (x - x_0).
$$

Esta aproximación lineal es una de las características clave de la diferenciabilidad en el análisis multivariable.

## Teorema sobre la Convexidad con Respecto a la Función Lineal $f(x_0) + \nabla f(x_0)^\top (x - x_0)$

**Teorema**: Si $f: \mathbb{R}^n \rightarrow \mathbb{R}$ es una función convexa, entonces para cualquier $x_0 \in \mathbb{R}^n$, la siguiente desigualdad se cumple para todo $x \in \mathbb{R}^n$:

$$
f(x) \geq f(x_0) + \nabla f(x_0)^\top (x - x_0).
$$

**Interpretación**: Esto significa que la función $f(x)$ está por encima del plano tangente en el punto $x_0$. Esta es una propiedad fundamental de las funciones convexas y muestra que el plano tangente proporciona una cota inferior de la función.

## Funciones Dos Veces Diferenciables (Usando la Hessiana)

Si una función $f: \mathbb{R}^n \rightarrow \mathbb{R}$ es dos veces diferenciable, podemos considerar la matriz Hessiana $H_f(x_0)$, que es la matriz de las segundas derivadas parciales:

$$
H_f(x_0) = \begin{pmatrix}
\frac{\partial^2 f}{\partial x_1^2}(x_0) & \frac{\partial^2 f}{\partial x_1 \partial x_2}(x_0) & \cdots & \frac{\partial^2 f}{\partial x_1 \partial x_n}(x_0) \\
\frac{\partial^2 f}{\partial x_2 \partial x_1}(x_0) & \frac{\partial^2 f}{\partial x_2^2}(x_0) & \cdots & \frac{\partial^2 f}{\partial x_2 \partial x_n}(x_0) \\
\vdots & \vdots & \ddots & \vdots \\
\frac{\partial^2 f}{\partial x_n \partial x_1}(x_0) & \frac{\partial^2 f}{\partial x_n \partial x_2}(x_0) & \cdots & \frac{\partial^2 f}{\partial x_n^2}(x_0)
\end{pmatrix}.
$$

#### Aproximación de Taylor de Segundo Orden

Para una función dos veces diferenciable, $f(x)$ se puede aproximar mediante una expansión de Taylor de segundo orden alrededor de un punto $x_0$:

$$
f(x) \approx f(x_0) + \nabla f(x_0)^\top (x - x_0) + \frac{1}{2} (x - x_0)^\top H_f(x_0) (x - x_0).
$$

Este término cuadrático refleja la curvatura de la función en torno a $x_0$ y es clave para el análisis de la convexidad.

### Teorema sobre la Convexidad usando la Hessiana

**Teorema**: Una función dos veces diferenciable $f: \mathbb{R}^n \rightarrow \mathbb{R}$ es convexa si y solo si la matriz Hessiana $H_f(x)$ es semidefinida positiva para todo $x \in \mathbb{R}^n$. Esto significa que:

$$
z^\top H_f(x) z \geq 0 \quad \text{para todo } z \in \mathbb{R}^n \text{ y todo } x \in \mathbb{R}^n.
$$

**Interpretación**: La convexidad de una función está relacionada con la curvatura de su gráfico, y la Hessiana describe esta curvatura. Si la Hessiana es semidefinida positiva en todos los puntos, la función no puede curvarse hacia abajo, lo que garantiza que la función sea convexa.

- minimo global
- maximo global
- minimo local
- maximo local
- teorema sobre convexidad y minimo global
- 
