En 1956 Noam Chomsky definió una jerarquía formada por 4 tipos de gramáticas en función de restricciones sobre las reglas.

Estas van de lo más general (**tipo 0**) a lo más específico (**tipo 3**).

1.  Gramáticas sin restricciones (**gramáticas de tipo 0**) 
2. Gramáticas sensibles al contexto (**gramáticas de tipo 1**)
3.  Gramáticas libres del contexto (**gramáticas de tipo 2**)
4. Gramáticas regulares (**gramáticas de tipo 3**)

# Gramaticas regulares
Se les llama también lineales y es el grupo más restringido de gramáticas. Esta restricción consiste en que la parte derecha de la regla tendrá como máximo dos símbolos.

## Clasificación
Hay dos tipos de gramáticas regulares:

### Gramaticas lineales por la derecha (GLD)
Sus reglas son de la forma

$$
\begin{align*}
A &::= a \\ A &::= aB \\ A &::= \varepsilon
\end{align*}
$$
donde $A, B \in \Sigma_N$, $a \in \Sigma_T$.

### Gramaticas lineales por la izquierda (GLI)
Sus reglas son de la forma:

$$
\begin{align*}
A &::= a \\ A &::= Ba \\ A &::= \varepsilon
\end{align*}
$$
donde $A, B \in \Sigma_N$, $a \in \Sigma_T$.

>[!important]
Estos lenguajes son aquellos que pueden ser aceptados por un autómata finito. También esta familia de lenguajes pueden ser obtenidas por medio de expresiones regulares.

## Teorema
La clase de los lenguajes generados por una gramática regular es precisamente la de los lenguajes regulares.

# Procedimiento de conversion de GR a AF

1. Para cada símbolo no terminal de la gramática asociar un estado en el autómata. 
2. Para cada regla de la forma $A ::= bC$ en la gramática se origina una transición $(A, b, C)$ en el autómata. 
3. Para cada regla de la forma $A ::= b$ se tendrán transiciones $(A, b, Z)$ donde $Z$ será el único estado final del autómata.

**Ejemplo**
A partir de la gramática regular $G = (\Sigma_N, \Sigma_T, S, P)$, donde el conjunto $P$ está dado por:

$$ 
\begin{aligned} 
S &::= aA \\ 
S &::= bA \\ A &::= aB \\ 
A &::= bB \\ A &::= a \\ 
B &::= aA \\ 
B &::= bA 
\end{aligned} 
$$

obtener un autómata finito. 

  ![[imgs/conversion GR a AF.png]]



--- 
Para producir una GLI para $L$,
1. Se construye un $AF$ para $L_{rev}$
2. Se obtiene una gramática derecha $G$
3. Se invierten los lados derechos de las producciones obteniendo la gramática izquierda deseada.
