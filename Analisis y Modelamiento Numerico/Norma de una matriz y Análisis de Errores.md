
# Norma vectorial
Dado un espacio vectorial $V$, una normal es una función $\| \cdot \|$ de $V$ en $[ 0, \infty )$, que satisface

1. $\| x\| > 0 \, , \quad x \neq 0, x \in V$
2. $\| \lambda x\| = |\lambda|\| x\| \, , \quad \lambda \in \mathbb{R} \, , x \in V$
3. $\| x + y \| \leq \| x \| + \| y \| \: , \quad x \, , y \in V$

Algunas normas:

- $\|x\|_2 = \left( \sum_{i=1}^{n} x_{i}^2 \right)^{1/2}$
- $\|x\|_{\infty} = \max_{1\leq i \leq n} |x_i|$
- $\|x\|_{1} = \sum_{i=1}^{n} |x_i|$
- $\|x\|_{p} = \left( \sum_{i=1}^{n} |x_{i}|^{p} \right)^{1/p}, \quad p \geq 1$


## Bola unitaria
Una bola unitaria en $\mathbb{R}^2$ se define como el conjunto $\{x : x \in \mathbb{R}^2 \, , \|x\| \leq 1\}$

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Analisis y Modelamiento Numerico\imgs\bolas unitarias.png">
    <figcaption></figcaption>
    </figure>
</div>


## Convergencia de vectores
Una sucesión $\{x^{(k)}\}$ de vectores en $\mathbb{R}^n$ se dice convergente a $x$ respecto a la norma $\|\cdot\|$ si para 
$$\epsilon> 0 \: \exists N : \|x^{(k)} - x\| < \epsilon \, , \quad \forall k\geq N $$

## Teorema
La sucesión $\{x^{(k)}\}$ converge a $x$ en $\mathbb{R}^n$ respecto a $\| \cdot \|_{\infty}$ si y solo si $$ \lim_{k \to \infty} x^{(k)}_i = x_i \quad \text{para todo } i = 1, 2, \ldots, n. $$

Por  ejemplo, $x^{(k)} =(1,2 + \frac{1}{k},\frac{3}{k^2}, e^{-k} \sin k)$ converge a $x = (1,2,0,0)^T$ respecto a la norma $\| \cdot \|_{\infty}$

## Teorema
Si $x \in \mathbb{R}^n$: $$ \|x\|_{\infty} \leq \|x\|_2 \leq \sqrt{n} \|x\|_{\infty} $$ $$ \|x\|_2 \leq \|x\|_1 \leq \sqrt{n} \|x\|_2 $$ $$ \|x\|_{\infty} \leq \|x\|_1 \leq \sqrt{n} \|x\|_{\infty} $$

# Normal matricial subordinada
Si se ha especificado una norma vectorial $\|\cdot\|$ , la **norma matricial subordinada** esta *definida* como
$$ \|A\| = sup \{ \|Au\|\ : u \in \mathbb{R}^n, \|u\| = 1  \}$$
También se le llama la norma matricial **asociada** con la norma vectorial dada. Se entiende que $A$ es una matriz de $n \times n$.

## Teorema de la norma matricial subordinada
Si $\|\cdot\|$ es cualquier norma en $\mathbb{R}^n$, entonces la ecuación
$$  \|A\| = \underset{\|u\|= 1}{sup} = \{ \|Au\| : u \in \mathbb{R}^n \} $$
define una norma en el espacio lineal de todas las matrices $n\times n$

### Prueba
Para propiedad 1:Si $A \neq 0$, existe $A^{(j)} \neq 0$. Sea el vector $x = e_j$, y $v = x / \|x\|$. De la definición de $\|A\|$ 
$$ \|A\| \geq \|Av\| = \frac{\|Ax\|}{x} = \frac{\|A^{(j)}\|}{\|x\|} \geq 0 $$
Para propiedad 2: $$\|\lambda A\| = sup\{\|\lambda A u\| : \|u\| = 1\} = |\lambda|sup{\|Au\| : \|u\| = 1} = |\lambda|\|A\| $$
Para propiedad 3: 
$$ \|A + B\| = sup\{\|(A + B)u\| : \|u\| = 1\}$$
$$  \leq sup\{\|A u\| + \|B u\| : \|u\| = 1\}  $$
$$  \leq sup\{\|A u\| : \|u\| = 1\} + sup\{\|B u\| : \|u\| = 1\}  $$
$$  = \|A\| + \|B\| $$


Una consecuencia importante de la definición de **norma matricial subordinada** es que
$$ \|Ax\| \leq \|A\|\|x\| $$
Además, si $A = I$, entonces
$$ \|I\| = sup \{ \|Ix\| : \|x\| = 1 \} = 1 $$



## Algunas normas matriciales

### Norma de Frobenius
$$ \|A\|_F = \sqrt{\sum_{i=1}^{n}\sum_{j=1}^{n} |a_{ij}|^2} $$
La norma de frobenius **no es una norma matricial subordinada**, $\|I\|_F \neq 1$

### Norma $\infty$

$$ \|A\|_{\infty} =  \underset{1 \leq i \leq n}{max} \sum_{j=1}^{n} |a_{ij}| $$
Es la fila que tiene la suma maxima de los valores absolutos de sus elementos.

### Norma 1
$$ \|A\|_1 = \underset{1 \leq j \leq n}{max} \sum_{i=1}^{n} |a_{ij}| $$
Es la columna que tiene la suma máxima de los valores absolutos de sus elementos.

**Norma Inducida**
Una norma matricial inducida es un tipo específico de norma matricial que surge al aplicar una norma vectorial a los vectores resultantes de la multiplicación de la matriz por un vector normado. Esto significa que la norma matricial inducida se define a partir de una norma vectorial preexistente.

Dada una norma vectorial $\| \cdot \|$ para vectores en un espacio vectorial normado, la norma matricial inducida de una matriz \( A \), denotada como $ \| A \|$, se define como:

$$ \| A \| = \sup_{\| x \| \neq 0} \frac{\| A x \|}{\| x \|} $$

Esta definición es similar a la norma matricial subordinada que te mencioné anteriormente, pero la diferencia clave radica en cómo se interpreta la norma vectorial utilizada. En el caso de la norma matricial inducida, la norma vectorial utilizada para medir la magnitud de los vectores resultantes de $A x$ es la norma euclidiana, también conocida como norma $l^2$.

La norma matricial inducida es muy utilizada en el ámbito del análisis numérico y la teoría de matrices. Algunos ejemplos de normas matriciales inducidas comunes son:

1. Norma matricial inducida $\| A  \|_1$ (norma del máximo de las columnas).
2. Norma matricial inducida $\| A \|_\infty$ (norma del máximo de las filas).
3. Norma matricial inducida $\| A \|_2$ (norma de Frobenius).

Estas normas matriciales inducidas se utilizan para medir la magnitud de las matrices en relación con vectores normados según la norma euclidiana.

la principal diferencia radica en la norma vectorial utilizada: la norma matricial subordinada puede basarse en cualquier norma vectorial, mientras que la norma matricial inducida se basa específicamente en la norma euclidiana $l^2$.


## El radio espectral
Si $A$ es una matriz simétrica real $n\times n$ entonces es diagonalizable con valores propios no negativos y sus vectores propios forman una base de $\mathbb{R}^n$. Definimos el radio espectral como
$$ \rho(M) = max \{ |\lambda|: 
Av = \lambda v, v \neq 0 \} $$
El radio espectral de una matriz $M$ es el máximo valor absoluto de sus valores propios.

### Propiedad
La norma de una matriz esta relacionada con su radio espectral de la siguiente manera
$$
\frac{1}{\sqrt{n}} \cdot \|A\|_2 \leq \rho(A) \leq \|A\|_F \leq \|A\|_2 \leq \|A\|_\infty
$$

### Norma 2
Se define como
$$ \|A\|_2 = \underset{\|x\|_2 = 1}{sup} \|ax\|_2 $$
Se puede probar que 
$$ \|A\|_2 = \underset{1 \leq i \leq n}{max} |\sigma_i| $$
donde $\sigma_i$ son los **valores singulares** de A (raíces cuadradas de los valores propios positivos de la matriz $AA^T$ o $A^TA$). Si $\sigma_1 \geq \sigma_2 \geq ... \geq \sigma_n \geq 0$, entonces se puede demostrar que la *norma 2* se define como
$$ \|A\|_2 = \sqrt{\rho(A^T A)} $$

### Propiedades
- Si $A$ es simétrica, entonces $\|A\|_2 = \rho(A)$
- $\|A\|_2 = \|A^T\|_2$
- $\|A^TA\|_2 = \|AA^T\|_2 = \|A\|^2_2$
- $\|A^{-1}\|_2 = \frac{1}{\delta_{min}}$ donde $\delta_{min}$ es el mínimo valor propio de $A^TA$


## Numero de Condición
Si resolvemos un sistema de ecuaciones
$$ Ax = b $$
numéricamente, no obtenemos la solución exacta $x$ pero una aproximación $\hat{x}$. Uno puede probar $\hat{x}$ formando $A\hat{x}$ para ver si esta cerca de $b$. Así obtenemos el **vector residual**
$$ r = b - A\hat{x} $$
La diferencia entre la solución exacta $x$ y la solución aproximada $\hat{x}$ es llamada el **vector error**
$$ e = x - \hat{x} $$

La siguiente relación
$$
Ae = r 
$$
entre el vector error y el vector residual es de suma importancia.
Note que $\hat{x}$ es la solución exacta del sistema lineal $A\hat{x} = \hat{b}$, donde $\hat{b} = b - r$. Ahora establezcamos relaciones entre los errores relativos en $x$ y $b$, es decir $\|\ x - \hat{x} \|\  / \| x \|$ y $\|\ b - \hat{b} \|\  / \| b \| = \| r \| / \| b \|$.  

### Teorema sobre límites que involucra el número de condición
En la resolución de ecuaciones $ax=b$, el número de condición $\kappa(A)$, el vector residual $r$ y el vector error $e$ satisfacen la siguiente desigualdad
$$ \frac{1}{\kappa (A)} \frac{\|r\|}{\|b\|} \leq \frac{\|e\|}{\|x\|} \leq \kappa(A) \frac{\|r\|}{\|b\|} $$


## Matrices convergentes
LLamamos **convergente** a una matriz $A_{n \times n}$ si
$$ \lim_{k \to \infty} (A^k)_{ij} = 0 $$
para cada $i=1, 2, \dots, n$ y $j=1, 2, \dots, n$.

### Teorema
Las siguientes declaraciones son equivalentes

1. $A$ es una matriz convergente
2. $\lim_{n \to \infty} \|A^n\| = 0$, para alguna norma inducida
3. $\lim_{n \to \infty} \|A^n\| = 0$, para alguna toda norma inducida
4. $\rho(A) < 1$
5. $\lim_{n \to \infty} A^nx = 0$, para todo $x$
