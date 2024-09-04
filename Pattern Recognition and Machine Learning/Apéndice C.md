
En este apéndice, reunimos algunas propiedades e identidades útiles que involucran matrices y determinantes. No se pretende que sea un tutorial introductorio, y se asume que el lector ya está familiarizado con el álgebra lineal básica. Para algunos resultados, indicamos cómo demostrarlos, mientras que en casos más complejos dejamos que el lector interesado consulte libros de texto estándar sobre el tema. En todos los casos, asumimos que existen inversas y que las dimensiones de las matrices son tales que las fórmulas están correctamente definidas. Una discusión exhaustiva sobre álgebra lineal se puede encontrar en Golub y Van Loan (1996), y una extensa colección de propiedades de matrices está dada por Lütkepohl (1996). Las derivadas de matrices se discuten en Magnus y Neudecker (1999).

# Identidades Básicas de Matrices

Una matriz $A$ tiene elementos $A_{ij}$ donde $i$ indexa las filas, y $j$ indexa las columnas. Usamos $I_N$ para denotar la matriz identidad de $N \times N$ (también llamada matriz unitaria), y donde no hay ambigüedad sobre la dimensionalidad, simplemente usamos $I$. La matriz transpuesta $A^\top$ tiene elementos $(A^\top)_{ij} = A_{ji}$. A partir de la definición de transpuesta, tenemos:

$$
(AB)^\top = B^\top A^\top \tag{C.1}
$$

lo cual se puede verificar escribiendo los índices. La inversa de $A$, denotada $A^{-1}$, satisface:

$$
AA^{-1} = A^{-1}A = I. \tag{C.2}
$$

Debido a que $ABB^{-1}A^{-1} = I$, tenemos:

$$
(AB)^{-1} = B^{-1}A^{-1}. \tag{C.3}
$$

También tenemos:

$$
(A^\top)^{-1} = (A^{-1})^\top \tag{C.4}
$$

lo cual se prueba fácilmente tomando la transpuesta de $(C.2)$ y aplicando $(C.1)$. 

Una identidad útil que involucra inversas de matrices es la siguiente:

$$
(P^{-1} + B^\top R^{-1} B)^{-1}B^\top R^{-1} = P B^\top (B P B^\top + R)^{-1}. \tag{C.5}
$$

lo cual se verifica fácilmente multiplicando ambos lados por $(B P B^\top + R)$. Supongamos que $P$ tiene dimensionalidad $N \times N$ mientras que $R$ tiene dimensionalidad $M \times M$, de modo que $B$ es $M \times N$. Entonces, si $M \leq N$, será mucho más barato evaluar el lado derecho de $(C.5)$ que el lado izquierdo. Un caso especial que a veces surge es:

$$
(I + AB)^{-1}A = A(I + BA)^{-1}. \tag{C.6}
$$

Otra identidad útil que involucra inversas es la siguiente:

$$
(A + B D^{-1} C)^{-1} = A^{-1} - A^{-1} B(D + C A^{-1} B)^{-1} C A^{-1} \tag{C.7}
$$

que se conoce como la identidad de Woodbury y que se puede verificar multiplicando ambos lados por $(A + B D^{-1} C)$. Esto es útil, por ejemplo, cuando $A$ es grande y diagonal, y por lo tanto fácil de invertir, mientras que $B$ tiene muchas filas pero pocas columnas (y viceversa para $C$), de modo que el lado derecho es mucho más barato de evaluar que el lado izquierdo.

Un conjunto de vectores $\{a_1, \dots, a_N\}$ se dice que es linealmente independiente si la relación $\sum_n \alpha_n a_n = 0$ se cumple solo si todos los $\alpha_n = 0$. Esto implica que ninguno de los vectores puede expresarse como una combinación lineal de los restantes. El rango de una matriz es el número máximo de filas linealmente independientes (o, equivalentemente, el número máximo de columnas linealmente independientes).

# Trazas y Determinantes

La traza y el determinante se aplican a matrices cuadradas. La traza $\text{Tr}(A)$ de una matriz $A$ se define como la suma de los elementos en la diagonal principal. Escribiendo los índices, vemos que:

$$
\text{Tr}(AB) = \text{Tr}(BA). \tag{C.8}
$$

Aplicando esta fórmula varias veces al producto de tres matrices, vemos que:

$$
\text{Tr}(ABC) = \text{Tr}(CAB) = \text{Tr}(BCA) \tag{C.9}
$$

lo que se conoce como la propiedad cíclica del operador traza y que claramente se extiende al producto de cualquier número de matrices. El determinante $|A|$ de una matriz $N \times N$ $A$ se define por:

$$
|A| = \sum (\pm1)A_{1i_1} A_{2i_2} \cdots A_{Ni_N} \tag{C.10}
$$

en el cual la suma se toma sobre todos los productos que consisten en precisamente un elemento de cada fila y un elemento de cada columna, con un coeficiente de $+1$ o $-1$ según si la permutación $i_1 i_2 \dots i_N$ es par o impar, respectivamente. Nótese que $|I| = 1$. Así, para una matriz $2 \times 2$, el determinante toma la forma:

$$
|A| = \begin{vmatrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{vmatrix} = a_{11}a_{22} - a_{12}a_{21}. \tag{C.11}
$$

El determinante de un producto de dos matrices se da por:

$$
|AB| = |A||B| \tag{C.12}
$$

como se puede demostrar a partir de $(C.10)$. Además, el determinante de una matriz inversa se da por:

$$
|A^{-1}| = \frac{1}{|A|} \tag{C.13}
$$

lo cual se puede demostrar tomando el determinante de $(C.2)$ y aplicando $(C.12)$. Si $A$ y $B$ son matrices de tamaño $N \times M$, entonces:

$$
|I_N + AB^\top| = |I_M + A^\top B|. \tag{C.14}
$$

Un caso especial útil es:

$$
|I_N + ab^\top| = 1 + a^\top b \tag{C.15}
$$

donde $a$ y $b$ son vectores columna de dimensión $N$.
# Derivadas de Matrices

A veces necesitamos considerar derivadas de vectores y matrices con respecto a escalares. La derivada de un vector $\mathbf{a}$ con respecto a un escalar $x$ es en sí misma un vector cuyos componentes están dados por:

$$
\left(\frac{\partial \mathbf{a}}{\partial x}\right)_i = \frac{\partial a_i}{\partial x} \tag{C.16}
$$

con una definición análoga para la derivada de una matriz. También se pueden definir derivadas con respecto a vectores y matrices, por ejemplo:

$$
\left(\frac{\partial x}{\partial \mathbf{a}}\right)_i = \frac{\partial x}{\partial a_i} \tag{C.17}
$$

y de manera similar:

$$
\left(\frac{\partial \mathbf{a}}{\partial \mathbf{b}}\right)_{ij} = \frac{\partial a_i}{\partial b_j}. \tag{C.18}
$$

Lo siguiente se puede demostrar fácilmente escribiendo los componentes:

$$
\frac{\partial}{\partial x} \left(\mathbf{x}^\top \mathbf{a}\right) = \frac{\partial}{\partial x} \left(\mathbf{a}^\top \mathbf{x}\right) = \mathbf{a}. \tag{C.19}
$$

De manera similar:

$$
\frac{\partial}{\partial x} (AB) = \frac{\partial A}{\partial x} B + A \frac{\partial B}{\partial x}. \tag{C.20}
$$

La derivada de la inversa de una matriz se puede expresar como:

$$
\frac{\partial}{\partial x} \left(A^{-1}\right) = -A^{-1} \frac{\partial A}{\partial x} A^{-1} \tag{C.21}
$$

como se puede demostrar diferenciando la ecuación $A^{-1}A = I$ usando $(C.20)$ y luego multiplicando por la derecha con $A^{-1}$. Además:

$$
\frac{\partial}{\partial x} \ln |A| = \text{Tr} \left(A^{-1} \frac{\partial A}{\partial x}\right) \tag{C.22}
$$

lo cual probaremos más adelante. Si elegimos $x$ como uno de los elementos de $A$, tenemos:

$$
\frac{\partial}{\partial A_{ij}} \text{Tr} (AB) = B_{ji} \tag{C.23}
$$

como se puede ver escribiendo las matrices usando notación de índices. Podemos escribir este resultado de manera más compacta en la forma:

$$
\frac{\partial}{\partial A} \text{Tr} (AB) = B^\top. \tag{C.24}
$$

Con esta notación, tenemos las siguientes propiedades:

$$
\frac{\partial}{\partial A} \text{Tr} \left(A^\top B\right) = B \tag{C.25}
$$

$$
\frac{\partial}{\partial A} \text{Tr}(A) = I \tag{C.26}
$$

$$
\frac{\partial}{\partial A} \text{Tr}(AB A^\top) = A(B + B^\top) \tag{C.27}
$$

lo cual se puede demostrar nuevamente escribiendo los índices de la matriz. También tenemos:

$$
\frac{\partial}{\partial A} \ln |A| = \left(A^{-1}\right)^\top \tag{C.28}
$$

lo cual se sigue de $(C.22)$ y $(C.26)$.