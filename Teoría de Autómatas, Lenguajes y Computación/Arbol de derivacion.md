
A veces es útil realizar un gráfico de la derivación que indique de qué manera ha contribuido cada símbolo no terminal a formar la cadena final de símbolos terminales. Tal gráfico tiene forma de árbol y se llama árbol de derivación (o árbol de análisis).

**Reglas**

1. La raíz se etiqueta con un símbolo inicial.
 2. Los hijos de la raíz son aquellos símbolos que aparecen al lado derecho de la composición usada para reemplazar el símbolo inicial
 3. Todo nodo etiquetado con un símbolo no terminal tiene unos nodos hijos etiquetados con los símbolos del lado derecho de la producción usada para sustituir ese símbolo no terminal.
 4. Los nodos que no tienen hijos (hojas) deben ser etiquetados con símbolos terminales.

# Arbol de derivación
Sea $G = (\Sigma_N, \Sigma_T, S, P)$ una GLC. Un árbol de derivación (AD) es un árbol ordenado construido recursivamente como sigue:

1. Un árbol sin aristas cuyo único vértice tiene etiqueta $S$ es un AD de $S$.

2. Si $X \in \Sigma_N$ es etiqueta de una hoja $h$ de un árbol de derivación $A$, entonces:
    - Si $X \to \varepsilon \in P$, entonces el árbol obtenido incrementando a $A$ un vértice $v$ con etiqueta $\varepsilon$ y una arista $\{h, v\}$ es un AD.
    - Si $X \to X_1 X_2 \cdots X_n \in P$, donde $X_1, X_2, \dots, X_n \in \Sigma_T \cup \Sigma_N$ entonces el árbol obtenido incrementando a $A$ $n$ vértices $v_1, v_2, \dots, v_n$ con etiquetas $x_1, x_2, \dots, x_n$, en ese orden y con $n$ aristas $\{h, v_1\}, \{h, v_2\}, \dots, \{h, v_n\}$ es un AD.

Si la secuencia de los rótulos de la frontera del AD es la forma sentencial $w$, se dice que $AD$ es un árbol de derivación de $w$.

**Ejemplo**
Sea $G$ una GLC donde $P$ está dado por:
$$
\begin{aligned}
E &\to E + T \mid T \\
T &\to T * F \mid F \\
F &\to (E) \mid t
\end{aligned}
$$

Obtener el árbol de derivación para $t * (t + t)$ partiendo de $E$.

**Solución**
Se tiene:
$$
\begin{aligned}
E &\to T && R2 \\
&\to T * F && R3 \\
&\to T * (E) && R5 \\
&\to T * (E + T) && R1 \\
&\to T * (T + T) && R2 \\
&\to F * (T + T) && R4 \\
&\to F * (F + T) && R4 \\
&\to F * (F + F) && R4 \\
&\to t * (F + F) && R6 \\
&\to t * (t + F) && R6 \\
&\to t * (t + t) && R6
\end{aligned}
$$

![[arbol derivacion ejem1.png]]

El número de pasos de cualquier derivación que lleva a un \( AD \, X \) es el número de vértices internos de \( X \), ya que a cada vértice interno le corresponde la aplicación de una regla.

Cada nodo interno del árbol será un símbolo no terminal de la gramática mientras que las hojas serán los símbolos terminales.

Una regla \( A ::= X_1 \dots X_n \) se representará como un subárbol cuyo nodo padre es \( A \) siendo sus hijos \( X_1, \dots, X_n \).


### Lenguaje inherentemente ambiguo
Un lenguaje libre de contexto se dice inherentemente ambiguo si todas las gramáticas libres de contexto para $L$ son ambiguas.

### Derivación a la izquierda
Una derivación se dirá a la izquierda si en cada paso se expande la variable más a la izquierda.

### Derivación a la derecha
Una derivación se dirá derivación por la derecha si en cada paso se expande el no terminal más a la derecha.

>[!tip] Una gramática ambigua se caracteriza por tener dos o más derivaciones por la izquierda para la misma cadena

