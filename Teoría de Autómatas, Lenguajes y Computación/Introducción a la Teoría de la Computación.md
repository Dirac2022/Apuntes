# Conjuntos
Un conjunto es una colección de objetos.
$$ L = \{a,b, c,d\} $$

$b$ es un elemento o miembro del conjunto.

**Notación:**

- $b \in L$ (b está en L o L contiene a b)
- $z \notin L$

En un conjunto no se repiten los elementos.

$$\{rojo, azul, rojo\} \ \ \text{es el mismo conjunto que} \ \ \{rojo, azul\}$$

El orden de los elementos es irrelevante.

$$\{3, 1, 9\}, \{9, 3, 1\} \ \text{y} \ \{1, 3, 9\} $$
son el mismo conjunto.

> [!important] 
> - Dos conjuntos son iguales si tienen los mismos elementos.
> - Los elementos de un conjunto no necesitan guardar relación entre sí.

**Ejemplo:**

$$\{3, rojo, \{d, azul\}\}$$
es un conjunto formado por tres elementos que no guardan relación entre sí.

## Tipos de conjuntos

### Conjunto unitario
Es aquel formado por un solo elemento.

**Ejemplo:**

$$ U = \{1\}  \ , \quad \quad 1 \neq \{1\} $$

### Conjunto vacío
Conjunto sin elementos.

**Notación**:   $\emptyset, \{\}$

### Conjuntos infinitos
Un conjunto que no es finito es infinito.

$$ \mathbb{N} = \{0, 1, 2, ...\} $$

$$ \mathbb{Z} = \{..., -2, -1, 0, 1, 2, ...\} $$

Podemos especificar algunos conjuntos mediante referencia a otros conjuntos y las propiedades que los elementos puedan o no tener.

Si $F= \{1, 3, 9\}$ y $G = \{3, 9\}$ podemos escribir $G$ como:

$$ G = \{x / x \in F \land x > 2\} $$

En general, si $A$ es un conjunto y $P$ es una propiedad que los elementos de $A$ pueden o no representar, podemos definir:

$B = \{x / x \in A \land x \text{ tiene la propiedad P}\}$

**Ejemplo:**

El conjunto de números naturales impares es:

$$ I = \{x / x \in N \land x \text{ no es divisible por 2}\} $$

## Subconjuntos

$A$ es un subconjunto de $B$ si cada elemento de $A$ también es un elemento de $B$.

**Notación**: $A \subseteq B$

**Ejemplo:**
$$I \subseteq \mathbb{N} $$
$$ A \subseteq A $$

### Subconjunto propio
Si $A$ es un subconjunto de $B$ pero $A$ es diferente de $B$, diremos que $A$ es un subconjunto propio de $B$.

**Notación**: $A \subset B$

Recordar que si $B$ es un conjunto cualquiera entonces $\emptyset \subseteq B$.

> [!tip]
> Para probar que dos conjuntos $A$ y $B$ son iguales, debemos probar que $A \subseteq B$ y $B \subseteq A$.

### Complemento de un conjunto
Para un conjunto $A \subseteq U$, el complemento de $A$, denotado por $\overline{A}$ es:

$$ \overline{A} = \{x / x \in U \land x \notin A\} $$

## Operaciones de conjuntos

### Unión
$$ A \cup B = \{x / x \in A \lor x \in B\} $$

**Ejemplo:**

$$ \{1, 3, 9\} \cup \{3, 5, 7\} = \{1, 3, 5, 7, 9\} $$

### Intersección
$$ A \cap B = \{x / x \in A \land x \in B\} $$

**Ejemplo:**

$$ \{1, 3, 9\} \cap \{3, 5, 7\} = \{3\} $$
$$ \{1, 3, 9\} \cap \{a, b, c, d\} = \emptyset $$

### Diferencia
$$ A - B = \{x / x \in A \land x \notin B\} $$

**Ejemplo:**

$$ \{1, 3, 9\} - \{3, 5, 7\} = \{1, 9\} $$

## Leyes de Teoría de Conjuntos

Si $A$, $B$ y $C$ son conjuntos, se cumplen las siguientes leyes:

1. **Idempotencia:**
$$ A \cup A = A $$
$$ A \cap A = A $$

2. **Conmutatividad:**
$$ A \cup B = B \cup A $$
$$ A \cap B = B \cap A $$

3. **Asociatividad:**
$$ (A \cup B) \cup C = A \cup (B \cup C) $$
$$ (A \cap B) \cap C = A \cap (B \cap C) $$

4. **Distributividad:**
$$ (A \cup B) \cap C = (A \cap C) \cup (B \cap C) $$
$$ (A \cap B) \cup C = (A \cup C) \cap (B \cup C) $$

5. **Absorción:**
$$ (A \cup B) \cap A = A $$
$$ (A \cap B) \cup A = A $$

6. **Leyes de De Morgan:**
$$ \text{(a)} \quad \quad  A \setminus (B \cup C) = (A \setminus B) \ \cap \ (A \setminus C) $$
$$  \text{(b)} \quad \quad A \setminus (B \cap C) = (A \setminus B) \ \cup \ (A \setminus C) $$

**Ejemplo:**

Probaremos (6a):

Sea  $$ I = A \setminus (B \cup C) $$

$$ D = (A \setminus B) \cap (A \setminus C) $$

Probaremos que $I = D$

1. PPQ $I \subseteq D$:

Sea 
$$
\begin{aligned}
x \in I \ &\Rightarrow x \in \ A \quad \text{pero} \quad x \notin B  \quad \text{y} \quad  x \notin C \\ \\
&\Rightarrow x \in A \setminus B  \quad \text{y} \quad x \in A \setminus C \\ \\
&\Rightarrow x \in D
\end{aligned}
$$

Luego $I \subseteq D$

2. PPQ $D \subseteq I$:

Sea 
$$ 
\begin{aligned}
x \in (A \setminus B) \cap (A \setminus C) &\Rightarrow x \in (A \setminus B) \quad \text{y} \quad x \in (A \setminus C) \\ \\
&\Rightarrow x \in A \quad \text{pero} \quad x \notin B \quad \text{y} \quad x \in A \quad \text{pero} \quad x \notin C \\ \\
&\Rightarrow x \in A \quad \text{pero} \quad x \notin B \cup C \\ \\
&\Rightarrow x \in A \setminus (B \cup C) 
\end{aligned}
$$

Luego $D \subseteq I$

$$\therefore I = D $$

## Operaciones generalizadas
1. **Union generalizada**
$$
\bigcup_{i \in I} A_i = \{x / \exists \, i \in I \ , \ x \in A_i \}
$$
2. **Intersección generalizada**
$$
\bigcap_{i \in I} A_i = \{x / x \in A_i \ , \ \forall i \in I \}
$$
1. **Producto cartesiano generalizado**
$$
\begin{aligned}
\bigotimes^n_{i=1} A_i &= \{ x / x = (x_1, \dots , x_n) ,  x_i \in A_i \} \\
A^i &= \bigotimes^n_{i=1} A
\end{aligned}
$$
## Conjuntos disjuntos
	
Dos conjuntos $A$, $B$ son disjuntos si $A \cap B = \emptyset$ (es decir, no tienen elementos en común).

## Intersecciones y uniones de varios conjuntos

Definimos:

$$ \bigcup S = \{x / x \in P \text{ para algún conjunto } P \in S\} $$

**Ejemplo:**

1. Si $S = \{\{a, b\}, \{b, c\}, \{c, d\}\} \Rightarrow \bigcup S = \{a, b, c, d\}$

2. Si $S = \{\{n\} / n \in N\} \Rightarrow \bigcup S = \mathbb{N}$

$$ \bigcap S = \{x / x \in P \text{ para todo } P \in S\} $$

## Conjunto potencia

Dado un conjunto $A$, la colección de todos los subconjuntos de $A$ y ella misma se llama conjunto potencia.

**Notación**: $2^A$

**Ejemplo**: Si $A = \{c, d\}$

$$ 2^A = \{\emptyset, \{c\}, \{d\}, \{c, d\}\} $$

## Partición de un conjunto

Sea $A \neq \emptyset$, una partición de $A$ es un subconjunto $\Pi$ de $2^A$ tal que:

1. Cada elemento de $\Pi$ es no vacío. $$ \forall \ X \in \Pi \quad X \neq \emptyset$$
2. Miembros distintos de $\Pi$ son disjuntos. $$ X, Y \ \in \ \Pi \ , \quad X \cap Y = \emptyset $$
3. $\bigcup_{i=0}^{n} X_{i} \in \Pi = A$ 

**Ejemplo:**

1. Sea $A = \{a, b, c, d\}$

	- $\{\{a, b\}, \{c\}, \{d\}\}$ es una partición de $A$
	- $\{\{b,c\}, \{c,d\}\}$ no es una partición de $A$

2. Los conjuntos de números naturales pares e impares forman una partición de $\mathbb{N}$.

## Ejercicios

1. Probar que $\overline{A \cup B} = \overline{A} \cap \overline{B}$

Prueba.  Sea $x \in U$. entonces

(a) 
$$
\begin{aligned}
x \in \overline{A \cup B} &\Rightarrow x \notin A \cup B  \\ \\
&\Rightarrow x \notin A \wedge x \notin B \\ \\ 
&\Rightarrow x \in \overline{A} \wedge x \in \overline{B} \\ \\
&\Rightarrow x \in \overline{A} \ \cap \ \overline{B} \\ \\
\end{aligned}
$$

Luego $\overline{A \cup B} \ \subseteq \overline{A} \cap \overline{B}$.

(b) 
$$
\begin{aligned}
x \in \overline{A} \cap \overline{B} &\Rightarrow x \in \overline{A} \wedge x \in \overline{B} \\ \\ 
&\Rightarrow x \notin A \wedge x \notin B \\ \\ 
&\Rightarrow x \notin A \cup B \\ \\
&\Rightarrow x \in \overline{A \cup B}
\end{aligned}
$$

Luego $A \cup B \subseteq \overline{A \cup B}$


2. Probar que $A \cap (B \cup C) = (A \cap B) \cup (A \cap C)$

Para cada $x \in \bigcup$,

$$
\begin{aligned}
x \in A \cap (B \cup C) &\Leftrightarrow (x \in A) \wedge (x \in B \cup C) \\ \\ &\Leftrightarrow (x \in A) \wedge (x \in B \ \vee \ x \in C) \\ \\
&\Leftrightarrow (x \in A \wedge x \in B) \vee (x \in A \wedge x \in C) \\ \\
&\Leftrightarrow (x \in A \cap B) \vee (x \in A \cap C) \\ \\
&\Leftrightarrow x \in (A \cap B) \cup (A \cap C)
\end{aligned}
$$

3. Probar que $A \cup (B \cap C) = (A \cup B) \cap (A \cup C)$

	- (a) Sea 
$$
\begin{aligned}
x \in A \cup (B \cap C) &\Rightarrow x \in A \vee (x \in B \cap C) \\ \\ 
&\Rightarrow x \in A \vee (x \in B \wedge x \in C) \\ \\ 
&\Rightarrow (x \in A \vee x \in B) \wedge (x \in A \vee x \in C) \\ \\ 
&\Rightarrow x \in (A \cup B) \wedge x \in (A \cup C) \\ \\
&\Rightarrow x \in (A \cup B) \cap (A \cup C)
\end{aligned}
$$

	- (b) Sea 
$$\begin{aligned}
x \in (A \cup B) \cap (A \cup C) &\Rightarrow x \in (A \cup B) \wedge x \in (A \cup C) \\ \\
&\Rightarrow (x \in A \vee x \in B) \wedge (x \in A \vee x \in C) \\ \\
&\Rightarrow x \in A \vee (x \in B \wedge x \in C) \\ \\ 
&\Rightarrow (x \in A) \vee (x \in B \cap C) \\ \\ 
&\Rightarrow x \in A \cup (B \cap C)
\end{aligned}
$$


# Relaciones

### Par ordenado
Para agrupar objetos utilizaremos un dispositivo llamado par ordenado (p.o.)

**Notación**: $(a, b)$ $a$  y  $b$  se dirán componentes del par ordenado. 
**Observación**: $(a, b) \neq \{a, b\}$

1. El orden de los componentes es relevante $(a, b) \neq (b, a)$.
2. Los dos componentes de un par ordenado no necesitan ser distintos.
3. $(a, b)$ es igual a $(c, d)$ si y solo si  $a=c$  $\wedge$  $b=d$.

## Producto Cartesiano

El **producto cartesiano** de dos conjuntos $A$ y $B$ se define como el conjunto de todos los pares ordenados posibles donde el primer elemento pertenece a $A$ y el segundo a $B$:
$$
A \times B = \{ (a, b) \mid a \in A, b \in B \}
$$

**Ejemplo**:
$$
\{1, 3, 9\} \times \{b, c, d\} = \{(1, b), (1, c), (1, d), (3, b), (3, c), (3, d), (9, b), (9, c), (9, d)\}
$$

## Relación Binaria
Una **relación binaria** es un subconjunto del producto cartesiano $A \times B$.

Ejemplos:
1. Si $A = \{1, 3, 9\}$ y $B = \{b, c, d\}$, entonces:
$$
R1 = \{(1, b), (1, c), (3, d), (9, d)\} \subseteq A \times B
$$

2. $R2 = \{(i, j) \mid i, j \in \mathbb{N} \land i < j\}$, entonces:
$$
R2 \subseteq \mathbb{N} \times \mathbb{N}
$$

## Tupla Ordenada

Sea $n \in \mathbb{N}$, una **tupla ordenada** es una secuencia de elementos de longitud $n$:
$$
(a_1, a_2, \ldots, a_n)
$$
donde $a_i$ es el $i$-ésimo componente $\forall \ i = 1, \dots , n$.
Dos tuplas ordenadas $(a_1, a_2, \ldots, a_n)$ y $(b_1, b_2, \ldots, b_m)$ son iguales si y solo si $m = n$ y $a_i = b_i$ para todo $i = 1, \ldots, n$.

**Ejemplos**:
$$
(4, 4), \quad (4, 4, 4), \quad ((4, 4), 4), \quad (4, (4, 4))
$$
son todos diferentes entre sí.

## Secuencia

Una **secuencia** es una $n$-tupla para algún $n$ no especificado (conocido como longitud de la secuencia).

## Producto Cartesiano Múltiplo

Sean $A_1, A_2, \ldots, A_n$ conjuntos cualesquiera, entonces el producto cartesiano múltiplo de nivel $n$ es:
$$
A_1 \times A_2 \times \cdots \times A_n = \{ (a_1, a_2, \ldots, a_n)  \mid a_i \in A_i \ \forall \ i = 1, \ldots, n \}
$$

Si $A_1 = A_2 = \dots = A_n = A$, se puede escribir $A^n$.

**Ejemplo**:
$$
\mathbb{N}^2 = \{(a, b) \mid a \in \mathbb{N}, b \in \mathbb{N} \}
$$

## Relación $n$-aria

Una **relación $n$-aria** es un subconjunto de $A_1 \times A_2 \times \dots \times A_n$.

## Tipos Especiales de Relaciones Binarias

Sea $A$ un conjunto y $R \subseteq A \times A$ una relación en $A$. La relación $R$ pueden representarse mediante un **grafo dirigido** donde cada elemento de $A$ es un vértice y cada par $(a, b) \in R$ es una arista dirigida de $a$ a $b$.

Ejemplo de relación representada como grafo dirigido:
$$
R = \{(a, b), (b, a), (a, d), (d, c), (c, c), (c, a)\}
$$
Grafo correspondiente:

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Teoría de Autómatas, Lenguajes y Computación\imgs\grafo G1.png" width=400>
    <figcaption></figcaption>
    </figure>
</div>



**Utilidad de Grafos**
- Tráfico
- Redes de comunicación
- Estructuras y procesos computacionales

- No se permiten “flechas paralelas”.
- No hay ninguna distinción formal entre relaciones binarias sobre un conjunto A y grafos dirigidos cuyos nodos son elementos de A.

Usaremos el término grafo dirigido cuando necesitemos enfatizar que el conjunto sobre el cual la relación es definida no tiene ningún interés especial para nosotros fuera del contexto de la relación particular considerada.

**Ejemplo**:
Dibuje el grafo dirigido para la relación $\leq$ "menor o igual" definida sobre los números naturales.

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Teoría de Autómatas, Lenguajes y Computación\imgs\grafo G2.png">
    <figcaption></figcaption>
    </figure>
</div>

## Relación Reflexiva
Una relación $R \subseteq A \times A$ es **reflexiva** si $(a, a) \in R \ \ \forall \ a \in A$. Los grafos dirigidos que representan relaciones reflexivas tienen un lazo en cada vértice.

$$
G_2 \ \text{ representa una relación reflexiva }. G_1 \ \ \text{no.}
$$

## Relación Simétrica
Una relación $R \subseteq A \times A$ es **simétrica** si $(a, b) \in R \Rightarrow (b, a) \in R$.

Ejemplo: Dibuje una relación de amistad entre 6 personas usando un grafo no dirigido.

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Teoría de Autómatas, Lenguajes y Computación\imgs\grafo G3.png" width=400>
    <figcaption></figcaption>
    </figure>
</div>

> [!info]  Una relación simétrica sin pares de la forma (a, a) acostumbra representarse en la forma de un grafo no dirigido o simplemente grafo.

Los grafos se dibujan sin flechas y representan la combinación de pares de fechas que van en sentido contrarios entre los nodos.

**Ejemplo**: La relación anterior puede ser representada también mediante un grafo

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Teoría de Autómatas, Lenguajes y Computación\imgs\grafo G3_.png" width=400>
    <figcaption></figcaption>
    </figure>
</div>


## Relación Anti-Simétrica

Una **relación antisimétrica** se define como aquella en la que si $(a, b) \in R$ y $a \neq b$, entonces $(b, a) \notin R$.

Ejemplo:
$$
P = \{x \mid x \text{ es persona}\}
$$
$$
R = \{(a, b) \mid a, b \in P \land a \text{ es el padre de } b\}
$$
Esta relación es antisimétrica porque si $a$ es el padre de $b$, entonces $b$ no puede ser el padre de $a$.

>[!info] Una relación puede no ser simétrica ni antisimétrica

**Ejemplo**: La relación
$$
R = \{ (a, b) \mid a, b \in P \ \wedge \ a \ \text{ le gusta } \ b \}
$$

## Relación Transitiva
Una **relación transitiva** es aquella en la que si $(a, b) \in R$ y $(b, c) \in R$, entonces $(a, c) \in R$.

Ejemplo:
$$
R = \{(a, b) \mid a, b \in P \land a \text{ es un ancestro de } b\}
$$
Esta relación es transitiva porque si $a$ es ancestro de $b$ y $b$ es ancestro de $c$, entonces $a$ es ancestro de $c$.

**Ejemplo**: La relación "$\leq$"

>[!info] En términos de grafos dirigidos: si hay una secuencia de flechas que conducen de $a$ hasta $z$, habrá una flecha que apunte directamente de $a$ hasta $z$.


<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Teoría de Autómatas, Lenguajes y Computación\imgs\grafo G4.png" width=400>
    <figcaption>Este grafo representa una relación transitiva</figcaption>
    </figure>
</div>


## Relación de Equivalencia
Una **relación de equivalencia** es aquella que es [[#Relaciones#Relación Reflexiva|reflexiva]], [[#Relación Simétrica|simétrica]] y [[#Relación Transitiva|transitiva]].

La representación de una relación de equivalencia mediante un grafo no dirigido se compone de un cierto conjunto de *clusters*. Un *cluster* está formado por un conjunto máximo de nodos interconectados por arcos. En cada par de nodos existe una arista entre estos.


<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Teoría de Autómatas, Lenguajes y Computación\imgs\relacion eq cluster.png">
    <figcaption>Representación de una relación de equivalencia mediante clusters</figcaption>
    </figure>
</div>


### Clases de Equivalencia
Los *clusters* de una relación de equivalencia se denominan **clases de equivalencia**.

**Notación**:
- $[a]$ se leerá la clase de equivalencia que contiene al elemento $a$.
- $[a] = \{b \mid (a, b) \in R\} = \{b \mid (b, a) \in R\}$


#### Teorema
Dado un conjunto $A$. Las clases de equivalencia tienen las siguientes propiedades
1. Si $z \in [x]$ , entonces $[z] = [x]$.
2. Si $[x] \neq [y]$ , entonces $[x] \cap [y] = \emptyset$.
3. $A = \underset{x \in A}{\bigcup}  [x]$  unión disjunta.

##### Demostración
1. Sea $z \in [x]$. Si $z' \in [z]$ , entonces $z' \sim z$ . Como $z \in [x]$, resulta $z \sim x$, luego por transitividad $z' \sim x$. Así $z' \in [x]$. Por tanto $[z] \subset [x]$. Recíprocamente, si $x' \in [x]$ , entonces $x' \sim x$. Por hipótesis $x \sim z$ y como $x' \sim x$, por transitividad resulta que $x' \sim z$. Así $x' \in [z]$ .Por tanto $[x] \subset [z]$.

2. Si $z \in [x] \cap [z]$ , entonces $[x] = [y] = [z]$ por (1). Lo cual genera una contradicción, por tanto $[x] \cap [y] = \emptyset$.

3. Para todo $x \in A$ ,  $x \in [x] \subset \underset{x \in A}{\bigcup \ [x]}$ . Luego es claro que $A = \underset{x \in A}{\bigcup \ [x]}$ . Además esta unión es disjunta, por (2). 

#### Teorema
Sea $R$ una relación de equivalencia sobre un conjunto $A \neq \emptyset$. Entonces, las clases de equivalencia de $R$ constituyen una [[#Partición de un conjunto|partición]] de $A$.

Ejemplo:
$$
R = \{(a, b) \mid a \land b \text{ son personas y } a \land b \text{ tienen los mismos padres}\}
$$

> [!info] A partir de cualquier partición $\Pi$, podemos construir la correspondiente relación de equivalencia:
$$
R = \{(a, b) \mid a \land b \text{ pertenecen al mismo conjunto de } \Pi\}
$$
es una relación de equivalencia.
Así, existe un isomorfismo natural entre el conjunto de relaciones de equivalencia sobre un conjunto $A$ y el conjunto de particiones de $A$. 
## Relación de Orden Parcial
Una **relación de orden parcial** es aquella que es [[#Relación Reflexiva|reflexiva]], [[#Relación Anti-Simétrica|antisimétrica]] y [[#Relación Transitiva|transitiva]].

**Ejemplo**:
$$
R_a = \{(a, b) \mid a \land b \text{ son personas y } a \text{ es un ancestro de } b\}
$$
(considerando que cada persona es ancestro de sí misma).

## Elemento Mínimo
Sea $R \subseteq A \times A$ una relación de orden parcial; $a \in A$ es mínimo si se cumple:
$$
(b, a) \in R \text{ solamente si } a = b
$$

Ejemplo: Los únicos elementos mínimos de $R_a$ son Adán y Eva.

**Nota**:
- Una relación de orden parcial **finita** debe tener, por lo menos, un elemento mínimo.
- En una relación de orden parcial **infinita** esto no ocurre necesariamente.

## Relación de Orden Total
Una relación de orden parcial $R \subseteq A \times A$ se dirá que es una **relación de orden total** si:
$$
\forall \ a, b \in A \quad (a, b) \in R \quad \text{o} \quad (b, a) \in R
$$

Ejemplo:
1. La relación $R$ no es una relación de orden total.
2. ¿La relación menor o igual será una relación de orden total?

**Nota**: Una relación de orden total no puede tener más de un elemento mínimo.

## Camino
Un **camino** en una relación binaria $R$ es una secuencia $(a_1, a_2, \ldots, a_n)$ para algún $n \geq 1$ tal que $(a_i, a_{i+1}) \in R$ para $i = 1, \dots, n-1$. Esta ruta se dice que es un camino de $a_1$ hacia $a_n$.

## Longitud de un Camino
En un camino $(a_1, \ldots, a_n)$, su longitud es $n$.

>[!warning] ¿No sería de $n-1$?
## Ciclo
El camino $(a_1, \ldots, a_n)$ es un **ciclo** si todos los $a_i$ son distintos y también $(a_n, a_1) \in R$.

# Funciones

Un conjunto $f \subseteq A \times B$ es una función si:
1. $Dom(f) = A$
2. Si $(x, y), (x, z) \in f \Rightarrow y = z$

Esto significa que para todo elemento $x$ de $A$ existe un único $y$ tal que $(x, y) \in f$.

**Notación**:
$$ f: A \rightarrow B $$
$$ y = f(x) \quad \text{donde} \ (x, y) \in f $$
>[!info]
>Una función de estas características la llamaremos **función total**.
### Teorema
Sean las funciones $f: A \rightarrow B$ y $g: A \rightarrow B$, entonces $f = g$  si y solo si $f(x) = g(x) \ \forall x \in A$.

#### Prueba
$\Rightarrow )$ Supongamos que $f = g$
Sea $x \in A$. Si $y=f(x) \Rightarrow (x, y) \in f = g \Rightarrow (x, y) \in g \Rightarrow y = g(x)$
Luego $f(x) = g(x)$  $\forall \ x \in A$.

$\Leftarrow)$ Supongamos que $f(x) = g(x) \ \forall \ x \in A$

1. $f \subseteq g$
	Sea $(x, y) \in f$ arbitrario.
	Entonces $y = f(x) = g(x)$. Luego $$ (x, y) \in g \ \text{y} \ f \subseteq g $$
2. $g \subseteq f$
	Sea $(x, y) \in g$ arbitrario.
	Entonces $y = g(x) = f(x)$. Luego $$ (x, y) \in f \ \text{y} \ g \subseteq f $$
## Función Parcial
Una relación $f \subseteq A \times B$ se dirá función parcial si:
1. $Dom(f) \subseteq A$
2. Si $(x, y), (x, z) \in f \Rightarrow y = z$

## Imagen
Sea $f: A \rightarrow B$ una función. Si $X \subseteq A$, se dice que la imagen de $X$ bajo $f$ es:
$$
f(X) = \{y \in B \mid y = f(x) \ \text{para algún} \ x \in X\}
$$

## Imagen Inversa

Si $Y \subseteq B$, la imagen inversa de $Y$ bajo $f$ es:
$$
f^{-1}(Y) = \{x \in A \mid f(x) = y \ \text{para algún} \ y \in Y\}
$$

### Teorema
Sea $f: A \rightarrow B$ una función.

1. $f(\emptyset) = \emptyset$.  La imagen de un conjunto nulo bajo $f$ es el conjunto nulo.
2. $f(\{x\}) = \{f(x)\} \ \forall x \in A$
3. Si $X \subseteq Y \subseteq A$ entonces $f(X) \subseteq f(Y)$
4. Si $X \subseteq Y \subseteq B$ entonces $f^{-1}(X) \subseteq f^{-1}(Y)$
5. Si $X$ e $Y$ son subconjuntos de $B$, entonces:
$$
f^{-1}(X - Y) = f^{-1}(X) - f^{-1}(Y)
$$

## Tipos Especiales de Funciones

### Función Inyectiva
Una función $f: A \rightarrow B$ es inyectiva si:
$$
\forall (x, z) \in f \ \text{y} \ (y, z) \in f \Rightarrow x = y \\
\ \text{ i.e } \ f(x) = f(y) \Rightarrow x = y
$$

### Función Sobreyectiva
Una función $f: A \rightarrow B$ es sobreyectiva si:
$$
\forall \ y \in B \ \ \exists \ x \in A \mid f(x) = y
$$

### Ejemplo
En las siguientes funciones, indique si son inyectivas o sobreyectivas:
1. Sea $f: \mathbb{N} \rightarrow \mathbb{N} / f(n) = n$
	- $f$ es a la vez inyectiva y sobreyectiva.
1. La función $g: \mathbb{N} \rightarrow \mathbb{N} / g(n) = n + 1$
	- $g$ es inyectiva.
	- $g$ no es sobreyectiva pues no existe $x \in \mathbb{N}$ tal que $x + 1 = 0$.
1. La función $h: \mathbb{R} \rightarrow \mathbb{R} / h(x) = x^2$
	- $h$ no es inyectiva.
	- $h$ no es sobreyectiva.

### Función Biyectiva
Una función $f: A \rightarrow B$ es biyectiva o correspondencia uno a uno si es a la vez inyectiva y sobreyectiva.

- Si $f: A \rightarrow B$ es sobreyectiva, entonces $f^{-1}(\{b\}) \neq \emptyset \quad  \forall \ b \ \in B$.  Es decir, si $f$ es sobreyectiva, para todo $y \in B$ existe al menos un elemento $x \in A$ tal que $f(x) = y$.  

- Si $f$ es una biyección, entonces $\forall \ b \in B \ f^{-1}(\{b\})$ es un conjunto con un único elemento. Por tanto, cuando $f$ es una biyección, $f^{-1}: B \rightarrow A$ es una función.

## Composición de Relaciones
Sean $R \subset A \times B$ y $S \subset B \times C$. Definimos la composición de $R$ y $S$ como:
$$
S \circ R = \{(a, c) \in A \times C \mid (a, b) \in R \ y \ (b, c) \in S \ \text{para algún} \ b \in B\}
$$

### Ejemplo
Sean $R = \{(0, 1), (0, 2), (1, 1)\}$ y $S = \{(1, a), (2, b)\}$. Hallar $S \circ R$ y $R \circ S$.

Solución:
$$
\begin{aligned}
S \circ R &= \{(0, a), (0, b), (1, a)\} \\
R \circ S &= \emptyset
\end{aligned}
$$

Conclusión: En general $S \circ R \neq R \circ S$.

## Composición de Funciones
$$
g \circ f = \{(a, b) \mid f(a) = y \ \text{ y } \ b = g(y) \ \ \text{para algún} \ y \in \text{ Dom}(g) \ \wedge  y \in \text{ Ran}(f) \}
$$


### Propiedades
- La composición de funciones es **asociativa**, es decir, si $f$ ,  $g$  y $h$ son funciones, entonces
$$ f \circ ( g \circ h) = (f \circ g) \circ h $$
- La composición de funciones en general **no es conmutativa**
$$ g \circ f \neq f \circ g $$
- El **elemento neutro** y también asociado a la composición de funciones es la **función identidad**.
- La **inversa** de la composición de dos funciones es
$$ (g \circ f)^{-1} = f^{-1} \circ g^{-1} $$

>[!tip] Para demostrar la inversa de la composición, se puede partir de que $(g \circ f) \circ f^{-1} \circ g^{-1}$ es la función identidad.  

### Ejemplo

Sea $f: \mathbb{R} \rightarrow \mathbb{R} / f(x) = x + 1$ y $g: \mathbb{R} \rightarrow \mathbb{R} / g(x) = x^2$. Hallar $g \circ f$ y $f \circ g$.

Solución:
1. $g \circ f(x) = g(f(x)) = g(x + 1) = (x + 1)^2$
2. $f \circ g(x) = f(g(x)) = f(x^2) = x^2 + 1$


### Ejemplo
Sean $A$ y $B$ conjuntos definidos por:

$$
A = \{0, 1, 2, 3\}
$$
$$
B = \{-1, 0, \frac{1}{2}, 1, \frac{3}{2}, 2, 3, 4\}
$$

Determine si las siguientes relaciones califican como funciones totales, funciones parciales o no son funciones:


| Relación                                                     | Descripción            |
| ------------------------------------------------------------ | ---------------------- |
| $f = \{(0, 1), (1, 2), (2, 3), (3, 4)\}$                     | Es una función total   |
| $f = \{(0, 0), (1, \frac{1}{2}), (2, 1), (3, \frac{3}{2})\}$ | Es una función total   |
| $f = \{(0, 0), (1, 1), (1, -1), (2, 3)\}$                    | No es una función      |
| $f = \{(0, 0), (1, 3), (2, 2)\}$                             | Es una función parcial |
| $f = \{(0, 0)\}$                                             | Es una función parcial |
 

### Ejemplo 2
Sea $f: \{0, 1, 2, 3, 4\} \rightarrow \{0, 1, 2, 3, 4\}$ definida por:

| $n$ | $f(n)$ |
| --- | ------ |
| 0   | 1      |
| 1   | 2      |
| 2   | 3      |
| 3   | 4      |
| 4   | 0      |

Si $Z_m = \{0, 1, 2, \ldots, m-1\}$, $f$ se puede escribir como $f: Z_5 \rightarrow Z_5$.

### Ejemplo 3
Sea la función $g: Z_4 \times Z_4 \rightarrow Z_4$ dada por:

| $g$ | 0 | 1 | 2 | 3 |
| --- | --- | --- | --- | --- |
| 0 | 0 | 1 | 2 | 3 |
| 1 | 1 | 2 | 3 | 0 |
| 2 | 2 | 3 | 0 | 1 |
| 3 | 3 | 0 | 1 | 2 |

$g$ es la función adición módulo 4.

## Definición de $Z_i$

Dado $m$ se define $Z_i$ como:

$$
Z_i = \{x \mid x \in \mathbb{Z} \ \text{y} \ x - i = km \ \text{para algún entero} \ k\}
$$

### Ejemplo
Si $m = 3$, hallar $\mathbb{Z}_0, \ \mathbb{Z}_1, \ \mathbb{Z}_2$:

$$
\begin{aligned}
\mathbb{Z}_0 &= \{0, \pm3, \pm6, \pm9, \ldots\} \\ \\
\mathbb{Z}_1 &= \{\ldots, -5, -2, 1, 4, 7, \ldots\} \\ \\
\mathbb{Z}_2 &= \{\ldots, -4, -1, 2, 5, 8, \ldots\}
\end{aligned}
$$


## Funciones
Una función de un conjunto $A$ a un conjunto $B$ es una relación binaria $R$ sobre $A$ y $B$ con la siguiente propiedad:
$$
\forall a \in A \ \text{hay exactamente un par ordenado en} \ R \ \text{cuya primera componente es} \ a
$$

**Ejemplo**

Dado:
- $C = \{c \mid c \text{ es ciudad de Perú}\}$
- $D = \{d \mid d \text{ es departamento de Perú}\}$

Sean:
$R1 = \{(x, y) \mid x \in C, y \in D \ \land \ x \ \text{es una ciudad del departamento} \ y\}$
$R2 = \{(x, y) \mid x \in D, y \in C \ \land \ y \ \text{es una ciudad del departamento} \ x\}$

- $R1$ es una función porque cada ciudad está en uno y solo un departamento.
- $R2$ no es una función ya que algunos departamentos tienen más de una ciudad.

**Convención**
Usaremos $f, g, h$ para representar funciones.

**Notación**
$$
f: A \rightarrow B
$$

- $A$ es el dominio de $f$. 
- Si $(a, b) \in f$, denotaremos $b = f(a)$. 
- Al objeto $f(a)$ se le conoce como la imagen de $a$ bajo $f$.
- Si $f: A \rightarrow B$ y $A_1$ es un subconjunto de $A$ entonces:
$$
f[A1] = \{f(a) \mid a \in A_1\} \ \text{ó} \ \{b \mid b = f(a), a \in A_1\}
$$

Denotaremos $f[A_1]$ a la imagen de $A_1$ bajo $f$. El rango de $f$ es la imagen de su dominio.

**Observación**: Si el dominio de una función es un producto cartesiano, se acostumbra eliminar un par de paréntesis

**Ejemplo**
$$
f: \mathbb{N} \times \mathbb{N} \rightarrow \mathbb{N} / f((m, n)) = m + n
$$
Por conveniencia notacional, se escribe $f(m, n) = m + n$.

Si $f: A_1 \times A_2 \times \cdots \times A_n \rightarrow B$ es una función y
$$
f(a_1, \ldots, a_n) = b \ \text{donde} \ a_i \in A_i \ \text{para} \ i = 1, \ldots, n; \ b \in B
$$

Entonces $a_1, \ldots, a_n$ se llaman argumentos de $f$ y $b$ el valor correspondiente de $f$. $f$ puede ser especificado indicando su valor para cada n-tupla de argumentos.

## Tipos Especiales de Funciones

### Función Inyectiva
Una función $f: A \rightarrow B$ se dice inyectiva si $\forall \ a_1, a_2 \in A \ a_1 \neq a_2 \Rightarrow f(a_1) \neq f(a_2)$.

#### Ejemplo

$C = \{c \mid c \text{ es ciudad del Perú}\}$
$D = \{d \mid d \text{ es departamento del Perú}\}$

Si la función $g: D \rightarrow C$ fuera especificada por:
$$
g(d) = \text{la capital del departamento} \ d \ \forall d \in D
$$

Entonces $g$ es inyectiva porque ningún par de departamentos tiene la misma capital.

### Función Sobreyectiva
Una función $f: A \rightarrow B$ se dice sobreyectiva si cada elemento de $B$ fuera la imagen, bajo $f$, de alguno de los elementos de $A$.

#### Ejemplo

- La función anterior $g$ no es sobreyectiva.
- La función $R_1$ es sobreyectiva, ya que cada departamento contiene, al menos, una ciudad.

### Función Biyectiva
Una función $f: A \rightarrow B$ se dice una biyección entre $A$ y $B$ si es inyectiva y sobreyectiva simultáneamente.

#### Ejemplo
Si $C_0$ es el conjunto de las ciudades que son capitales de departamento, entonces la función $g: D \rightarrow C_0$
$$
g(d) = \text{la capital del departamento} \ d
$$
es una biyección entre $D$ y $C_0$.

## Inversa de Relación Binaria
Sea $R \subset A \times B$ una relación. La relación inversa de $R$ es $R^{-1} \subset B \times A$:
$$
R^{-1} = \{(b, a) \mid (a, b) \in R\}
$$

### Ejemplo
La relación inversa de $R_1$ es $R_2$ , $R_1^{-1} = R_2$. La inversa de una función no necesariamente es una función. La inversa de $R_1$ no es una función porque algunos departamentos tienen más de una ciudad. Hay ciudades distintas $C_1$ y $C_2$ tales que $R_1(C_1) = R_1(C_2)$.

### Nota
1. Una función $f: A \rightarrow B$ no tiene inversa si hay algún elemento $b \in B$ tal que $f(a) \neq b \ \forall a \in A$.
2. Si $f: A \rightarrow B$ es una biyección, se tiene que $f^{-1}$ es una biyección entre $B$ y $A$. Además:
$$
\begin{aligned}
f^{-1}(f(a)) &= a \ , \quad \forall a \in A \\ \\
f(f^{-1}(b)) &= b \ , \quad \forall b \in B
\end{aligned}
$$

**Ejemplo**
Para tres conjuntos cualesquiera $A, B, C$ hay un isomorfismo natural de $A \times B \times C$ a $(A \times B) \times C$:
$$
f(a, b, c) = ((a, b), c) \ \forall a \in A, b \in B, c \in C
$$

**Ejemplo**
Para dos conjuntos $A$ y $B$ hay un isomorfismo natural $\phi$ de $2^{A \times B}$, es decir, el conjunto de todas las relaciones binarias en $A$ y $B$, al conjunto:
$$
\{f \mid f \ \text{es una función de} \ A \ \text{a} \ 2^B\}
$$

A saber, para cualquier relación $R \subseteq A \times B$, sea $\phi(R)$ una función $f:A \to 2^B$ tal que:
$$ f(a) = \{b \mid b \in B \ \wedge \ (a, b) \in \mathbb{R} \} $$

Por ejemplo, si $D$ es el conjunto de departamentos y $R \subset D \times D$ contiene cualquier par ordenado de departamentos con una frontera común, entonces la función asociada naturalmente $f: D \rightarrow 2^D$ está especificada por:
$$
f(d) = \{d_1 \mid d_1 \in D \ \text{y} \ d_1 \ \text{comparte una frontera con} \ d\}
$$

**Ejemplo** 
A veces consideramos la inversa de una función $f: A \to B$ como si fuera una función aún cuando $f$ no es una biyección. La idea es considerar $f^{-1} \subseteq B \times A$ como una función de $B$ a $2^A$ usando el isomorfismo natural descrito anteriormente. Así, $f^{-1}(b)$ es $\forall \ b \in B$ el conjunto de todos los $a \in A$ tal que $f(a) = b$.

**Ejemplo** 
Si $R1$ es la función que asigna a cada ciudad el departamento en el cual está localizado, entonces: 

$$ R_1^{-1} (d) = \{ c \mid c \text{ es cuidad del departamento} \} $$
i.e. el conjunto de todas las ciudades de este departamento.

# Operaciones binarias
Una operación binaria es aquella operación matemática que necesita un operador y dos operandos (argumentos) para que se calcule un valor. En esta sección nos centraremos en el estudio de las operaciones binarias internas.

Sea $A$ un conjunto. Una operación binaria en $A$ es una función $f : A \times A \to A$.

### Propiedades

1. $\text{Dom}(f) = A \times A$
2. Solo un elemento de $A$ se asigna a cada par ordenado $(a,b)$.

### Convención
Usaremos $\ast$ en lugar de $f$ y $a \ast b$ en lugar de $\ast(a,b)$.

**Ejemplos:**
En los siguientes ejemplos consideraremos:

- $Z$ el conjunto de enteros: $\{0, +1, -1, +2, -2, \ldots\}$
- $Z^+$ el conjunto de enteros positivos: $\{+1, +2, +3, \ldots\}$
- $R$ el conjunto de los números reales.

1. Sea $A = \mathbb{Z}$. Definiendo $a \ast b = a + b$, $\ast$ es una operación binaria en $\mathbb{Z}$.
2. Sea $A = \mathbb{R}$. Se define $a \ast b = a/b$, $\ast$ no es una operación binaria en $\mathbb{R}$.
3. Sea $A = \mathbb{Z}^+$. Se define $a \ast b = a - b$, $\ast$ no es una operación binaria.
4. Sea $A = \mathbb{Z}$. Se define $a \ast b = \max(a,b)$, $\ast$ es una operación binaria.
5. Sea $A = \mathcal{P}{(S)}$, para algún conjunto $S$. Si $V$ y $W$ son subconjuntos de $S$, se define $V \ast W = V \cup W$, $\ast$ es una operación binaria en $A$.

Podemos definir una operación binaria para un conjunto finito $A = \{a_1, a_2, \ldots, a_n\}$ por medio de una tabla:

| $\ast$ | $a_1$ | $a_2$ | $\cdots$ | $a_j$ | $\cdots$ | $a_n$ |
|-------|-------|-------|----------|-------|----------|-------|
| $a_1$ |       |       |          |       |          |       |
| $\vdots$|     |       | $a_i \ast a_j$ |       |          |       |
| $a_n$ |       |       |          |       |          |       |

**Ejemplo:** Sea $A = \{0, 1\}$. Podemos representar las operaciones binarias $\lor$ y $\land$ mediante:

- $\lor$ (OR lógico)

| $\lor$ | 0 | 1 |
|-------|---|---|
| 0     | 0 | 1 |
| 1     | 1 | 1 |

- $\land$ (AND lógico)

| $\land$ | 0 | 1 |
|--------|---|---|
| 0      | 0 | 0 |
| 1      | 0 | 1 |

## Propiedades de las Operaciones Binarias

Una operación binaria en el conjunto $A$ es conmutativa si $a \ast b \ = \ b \ast a \ \ , \quad \forall \ a, b \in A$.

**Ejemplo:**

1. $a \ast b = a + b$ es conmutativo en $A = \mathbb{Z}$.
2. $a \ast b = a - b$ no es conmutativo en $A = \mathbb{Z}$.
3. ¿Cuál de las siguientes operaciones binarias en $A = \{a, b, c, d\}$ son conmutativas?

(a) $\ast$

| $\ast$  | **$a$** | **$b$** | **$c$** | **$d$** |
| ------- | ------- | ------- | ------- | ------- |
| **$a$** | $a$     | $c$     | $b$     | $d$     |
| **$b$** | $b$     | $c$     | $b$     | $a$     |
| **$c$** | $c$     | $d$     | $b$     | $c$     |
| **$d$** | $a$     | $a$     | $b$     | $b$     |

(b) $\ast$

| $\ast$ | **$a$** | **$b$** | **$c$** | **$d$** |
| ------ | ------- | ------- | ------- | ------- |
| **$a$**    | $a$     | $c$     | $b$     | $d$     |
| **$b$**    | $c$     | $d$     | $b$     | $a$     |
| **$c$**    | $b$     | $b$     | $a$     | $c$     |
| **$d$**    | $d$     | $a$     | $c$     | $b$     |

(a) no es conmutativa, pues $a \ast b \neq b \ast a$.

(b) es conmutativa, pues las componentes de la tabla son simétricas respecto a la diagonal principal.

Una operación binaria $\ast$ en un conjunto $A$ es asociativa si $a \ast (b \ast c) = (a \ast b) \ast c \ , \ \ \forall \ a, b, c \in A$.

**Ejemplo:**

1. $a \ast b = a + b$ es asociativa en $A = \mathbb{Z}$.
2. $a \ast b = a - b$ no es asociativa en $A = \mathbb{Z}$.

# Semigrupo
Un semigrupo es un conjunto no vacío $S$ junto a una [[#Operaciones binarias|operación binaria]] **asociativa** $\ast$ definida en $S$.

**Notación**: Denotaremos un semigrupo por $(S, \ast)$.

Un semigrupo $(S, \ast)$ es conmutativo si $\ast$ es una operación conmutativa. Se cumple que $a \ast b = b \ast a \ , \ \ \forall \ a, b \in S$.

**Ejemplo**
1. $(\mathbb{Z}, +)$ es un semigrupo conmutativo.
2. $(\mathbb{Z}, -)$ no es semigrupo, ya que la sustracción no es asociativa.
3. $(\mathcal{P}{(S)}, \cup)$ es un semigrupo conmutativo, donde $S$ es un conjunto.
4. Sea $S$ un conjunto fijo no vacío y sea $S^S$ el conjunto de todas las funciones $h : S \to S$. Si $f, g \in S^S$, definimos $f \ast g = f \circ g$. $\ast$ es una operación binaria en $S^S$ y es asociativa. Luego, $(S^S, \ast)$ es un semigrupo. Sin embargo, no es conmutativo.

### Elemento identidad
A un elemento $e$ en un semigrupo $(S, \ast)$ se le llama identidad (o elemento neutro) si $e \ast a = a \ast e = a \ , \ \ \forall \ a \in S$.

**Ejemplos:**
1. El número 0 es una identidad en el semigrupo $(Z, +)$.
2. El semigrupo $(Z^+, +)$ no tiene elementos identidad.


### Teorema
Si un semigrupo $(S, \ast)$ tiene un elemento identidad, éste es único.

#### Prueba
Supongamos que $e_1$ y $e_2$ son elementos identidad en $S$.

Como $e_1$ es una identidad:
$$ e_1 \ast e_2 = e_2 $$

Como $e_2$ es una identidad:
$$ e_1 \ast e_2 = e_1 $$

De $e_1 \ast e_2 = e_2$ y $e_1 \ast e_2 = e_1$ se deduce que:
$$ e_1 = e_2 $$


### Subsemigrupo
Sea $(S, \ast)$ un semigrupo y sea $T \subset S$. Si $T$ es cerrado bajo la operación $\ast$ (i.e., $a \ast b \in T$ siempre que $a, b \in T$) entonces a $(T, \ast)$ se le llama **subsemigrupo** de $(S, \ast)$.

**Ejemplo**
- Si $(S, \ast)$ es un semigrupo entonces $(S, \ast)$ es un subsemigrupo de $(S, \ast)$.

Supóngase que $(S, \ast)$ es un semigrupo y sea $a \in S$. Para $n \in \mathbb{Z}^+$, se definen las potencias de $a^n$ recursivamente como sigue:
$$ a^1 = a, a^2 = a \ast a, a^n = a^{n-1} \ast a \, \text{para } n \geq 2 $$


# Monoide
Un monoide es un [[#Semigrupo|semigrupo]] $(S, \ast)$ que tiene una identidad.

**Ejemplos**

1. El semigrupo $(\mathcal{P}{(S)}, \ast)$ tiene como identidad a $\emptyset$, ya que 
	$$ \emptyset \ast A = \emptyset \cup A = A \cup \emptyset = A \, \forall A \in P(S)
	$$
	Luego, $(P(S), \ast)$ es un monoide.
	
2. El semigrupo $(S^S, \ast)$ tiene a la identidad $1_S$, ya que 
	$$ 1_S \ast f = 1_S \circ f = f = f \circ 1_S \, \forall f \in S^S $$
	De aquí, $(S^S, \ast)$ es un monoide.



### Submonoide
Sea $(S, \ast)$ un monoide con identidad $e$ y sea $\emptyset \neq T \subset S$. Si $T$ es cerrado bajo la operación $\ast$ y $e \in T$, entonces a $(T, \ast)$ se le denomina **submonoide** de $(S, \ast)$.


**Ejemplo**
- Sea $(S, \ast)$ un monoide. Entonces $(S, \ast)$ es un submonoide de $(S, \ast)$. Si $T = \{e\}$, $(T, \ast)$ es también un submonoide de $(S, \ast)$.

Si $(S, \ast)$ es un monoide, se define $a^0 = e$.
Si $m$ y $n$ son enteros no negativos, se cumple:
$$ a^m \ast a^n = a^{m+n} $$

# Isomorfismo y Homomorfismo

## Isomorfismo
Sean $(S, \ast)$ y $(T, \ast')$ dos semigrupos.
A la función $f : S \to T$ se le llama isomorfismo de $(S, \ast)$ en $(T, \ast')$ si es inyectiva, suprayectiva y si:
$$ f(a \ast b) = f(a) \ast' f(b) \, \forall a, b \in S $$

Notación: Si los semigrupos $(S, \ast)$ y $(T, \ast')$ son isomorfos se denotará $S \cong T$.

### Método para demostrar un isomorfismo
Para demostrar que los semigrupos $(S, \ast)$ y $(T, \ast')$ son isomorfos, se deberá usar el siguiente procedimiento:

1. Defínase una función $f : S \to T$.
2. Demuéstrese que $f$ es inyectiva.
3. Demuéstrese que $f$ es suprayectiva.
4. Demuéstrese que $f(a \ast b) = f(a) \ast' f(b)$.

**Ejemplo:** Sea $T$ el conjunto de todos los enteros pares. Demuéstrese que los semigrupos $(\mathbb{Z}, +)$ y $(T, +)$ son isomorfos.

**Solución:**

1. Se define $f : \mathbb{Z} \to T$ por $f(a) = 2a, \forall a \in \mathbb{Z}$.
2. Veamos si es inyectiva. Supongamos que:
	$$ f(a_1) = f(a_2) \implies 2a_1 = 2a_2 \implies a_1 = a_2 $$
	Luego, $f$ es inyectiva.
3. Veamos si es suprayectiva. Sea $b \in T$ cualquiera, luego $b$ es par $\implies b = 2a \ , \ \ a \in \mathbb{Z}$
	$$ f(a) = f\left(\frac{b}{2}\right) = 2\left(\frac{b}{2}\right) = b $$
	Luego, $f$ es suprayectiva.
4. Probemos que $f(a \ast b) = f(a) \ast' f(b)$:
	$$ f(a + b) = 2(a + b) = 2a + 2b = f(a) + f(b) $$
De aquí, $(\mathbb{Z}, +)$ y $(T, +)$ son isomorfos. 

$$ \mathbb{Z} \cong T $$

### Representación de un isomorfismo
Si $S$ y $T$ son semigrupos finitos, sus operaciones binarias respectivas se pueden expresar por medio de tablas. Entonces, $S$ y $T$ son isomorfos si es posible reordenar y etiquetar los elementos de $S$ para que su tabla sea idéntica a la de $T$.

**Ejemplo:** Sean $S = \{a, b, c\}$ y $T = \{x, y, z\}$ con las tablas respectivas:

| $\ast$ | $a$ | $b$ | $c$ |
| ------ | --- | --- | --- |
| $a$    | $a$ | $b$ | $c$ |
| $b$    | $b$ | $c$ | $a$ |
| $c$    | $c$ | $a$ | $b$ |

$\ast'$

| $\ast'$ | $x$ | $y$ | $z$ |
|--------|-----|-----|-----|
| $x$    | $z$ | $x$ | $y$ |
| $y$    | $x$ | $y$ | $z$ |
| $z$    | $y$ | $z$ | $x$ |

Haciendo:
$$ f(a) = y \, \ \ f(b) = x \, \ \ f(c) = z $$

Reemplazando los elementos en $S$ por sus imágenes y reordenando la tabla se concluye que $(S, \ast)$ y $(T, \ast')$ son isomorfos.

$$ S \cong T $$


### Teorema
Sean $(S, \ast)$ y $(T, \ast')$ monoides con identidades respectivas $e$ y $e'$. Sea $f$ un isomorfismo. Entonces $f(e) = e'$.

#### Prueba
Sea $b$ cualquier elemento de $T$. Como $f$ es suprayectiva, $\exists a \in S$ tal que $f(a) = b$.

$$
\begin{aligned}
a &= a \ast e \\
b &= f(a) = f(a \ast e) = f(a) \ast' f(e) \\
b &= b \ast' f(e) 
\end{aligned}
$$

Como $e'$ es el único elemento en $T$ tal que $b *' e' = b$, entonces  $f(e) = e'$.


### Teorema
Si $(S, \ast)$ y $(T, \ast')$ son semigrupos tales que $S$ tiene un idéntico y $T$ no, se sigue que $(S, \ast)$ y $(T, \ast')$ no pueden ser isomorfos.

**Ejemplo:** Sea $T$ el conjunto de todos los enteros pares y sea $\times$ la multiplicación ordinaria.

Luego, los semigrupos $(\mathbb{Z}, \times)$ y $(T, \times)$ no son isomorfos ya que $\mathbb{Z}$ tiene una identidad y $T$ no.

$$
e = 1 \quad e' \text{ no puede ser } 1 \notin T
$$

## Homomorfismo
Sean $(S, \ast)$ y $(T, \ast')$ dos semigrupos. A una función $f : S \to T$ se le llama homomorfismo de $(S, \ast)$ a $(T, \ast')$ si
$$
f(a \ast b) = f(a) \ast' f(b) \quad \forall a, b \in S
$$

Si $f$ también es suprayectiva, se dice que $T$ es la imagen homomorfa de $S$.

> [!tip] Diferencia entre homomorfismo e isomorfismo
> Un homomorfismo es una función que preserva la operación del semigrupo, mientras que un isomorfismo es un homomorfismo que es además una biyección, estableciendo una equivalencia entre dos semigrupos.



# Teoría de Grupos

## Grupo

### Definición de grupo
Un **grupo** $(G, \ast)$ es un [[#Monoide|monoide]] que satisface los siguientes axiomas:

1. **Asociatividad:** $(a \ast b) \ast c = a \ast (b \ast c) \quad \forall a,b, c \in G$
2. **Existencia de elemento neutro:** Existe un elemento único $e \in G$ tal que $a \ast e = e \ast a = a \ , \quad \forall a \in G$
3. **Existencia de elemento inverso:** $\forall a \in G$ existe un elemento $a' \in G$ al que se le llama inverso de $a$, tal que $a \ast a' = a' \ast a = e$

Si $G$ es un grupo y $\ast$ es una operación binaria, $G$ deberá ser cerrada bajo $\ast$, es decir:

$$a \ast b \in G \quad \forall a,b \in G$$
### Grupo abeliano
Un [[#Definición de grupo|grupo]] $G$ es **abeliano** o **conmutativo** si se cumple:
$$a \ast b = b \ast a \quad \forall a,b \in G$$

### Ejemplos

- $(\mathbb{Z}, +)$ es un grupo abeliano. Si $a \in \mathbb{Z}$, entonces el inverso de $a$ es $-a$.
- $(\mathbb{Z}^+, \cdot)$ no es un grupo. El elemento $2 \in \mathbb{Z}^+$ no tiene inverso.
- $(\mathbb{R} - \{0\}, \cdot)$ es un grupo. Un inverso de $a \neq 0$ es $1/a$.



<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Teoría de Autómatas, Lenguajes y Computación\imgs\esquema grupos.png">
    <figcaption></figcaption>
    </figure>
</div>

### Teoremas

Sea $G$ un grupo y sean $a$ y $b$ elementos de $G$. Entonces:

1. La ecuación $ax = b$ tiene una solución única en $G$.
2. La ecuación $ya = b$ tiene una solución única en $G$.


### Ejemplo
Sea $G$ el conjunto de los reales sin el cero y sea:

$$a \ast b = \frac{ab}{2}$$

Demuestre que $(G, \ast)$ es un grupo abeliano.

#### Demostración
Verificaremos que $\ast$ es una operación binaria:
Si $a$ y $b \in G \rightarrow a \ast b = \frac{ab}{2}$ está en $G$

**Verificando su propiedad asociativa:**

$$(a \ast b) \ast c = \left(\frac{ab}{2}\right) \ast c = \frac{(ab)c}{4}$$

$$a \ast (b \ast c) = a \ast \left(\frac{bc}{2}\right) = \frac{a(bc)}{4} = \frac{(ab)c}{4}$$

Así, $\ast$ es asociativa.

**El elemento $2$ es la identidad en $G$**

Si $a \in G$:

$$a \ast 2 = \frac{a(2)}{2} = a = \frac{(2)a}{2} = 2 \ast a$$

**Si $a \in G$, $a^0 = \frac{4}{a}$ es un inverso de $a$:**

$$a \ast a^0 = a \ast \frac{4}{a} = \frac{a(4/a)}{2} = 2 = \frac{4}{a} \ast a = a^0 \ast a$$

$G$ es abeliano pues $a \ast b = b \ast a \ \forall \ a, b \in G$

### Más Teoremas

- Sea $G$ un grupo. Cada elemento $a \in G$ tiene un inverso único en $G$.
- Sea $G$ un grupo y sean $a, b$ y $c$ elementos en $G$. Entonces:

$$
\begin{align*}
ab &= ac \Rightarrow b = c \quad (\text{propiedad de cancelación izquierda}) \\
ba &= ca \Rightarrow b = c \quad (\text{propiedad de cancelación derecha})
\end{align*}
$$

- Sea $G$ un grupo y sean $a$ y $b$ elementos en $G$. Entonces:

$$
\begin{align*}
(a^{-1})^{-1} &= a \\
(ab)^{-1} &= b^{-1}a^{-1}
\end{align*}
$$

## Grupos Finito
Si un grupo $G$ tiene un número finito de elementos, su operación binaria $\ast$ puede representarse por una tabla de multiplicación. La tabla de multiplicación de $G = \{a_1,a_2, ...,a_n\}$ bajo $\ast$ debe satisfacer:

1. La fila etiquetada por $e$ deberá contener los elementos $a_1,a_2, ...,a_n$.
2. Cada elemento $b$ en el grupo deberá aparecer exactamente una vez en cada fila y en cada columna de la tabla. Cada columna y cada fila es una permutación de los elementos $a_1,a_2, ...,a_n$ de $G$.
3. El orden de $G$ es el número de elementos y se denota por $|G|$

### Ejemplos de Tablas de Multiplicación

#### Orden 1
Si $G$ es un grupo de orden 1, entonces $G = \{e\}$ y $e \ast e = e$.

#### Orden 2
Sea $G = \{e,a\}$ un grupo de orden 2 y su tabla es:

|     | e   | a   |
| --- | --- | --- |
| e   | e   | a   |
| a   | a   | e   |
donde $a' = a$ 
#### Orden 3
Sea $G = \{e,a,b\}$ un grupo de orden 3 y su tabla es:

|   | e | a | b |
|---|---|---|---|
| e | e | a | b |
| a | a | b | e |
| b | b | e | a |

#### Orden 4
Sea $G = \{e,a,b,c\}$ un grupo de orden 4. Existen 4 posibles tablas de multiplicación para un grupo de orden 4:

|   | e | a | b | c |
|---|---|---|---|---|
| e | e | a | b | c |
| a | a | e | c | b |
| b | b | c | e | a |
| c | c | b | a | e |

|   | e | a | b | c |
|---|---|---|---|---|
| e | e | a | b | c |
| a | a | e | c | b |
| b | b | c | a | e |
| c | c | b | e | a |

|   | e | a | b | c |
|---|---|---|---|---|
| e | e | a | b | c |
| a | a | b | c | e |
| b | b | c | e | a |
| c | c | e | a | b |

|   | e | a | b | c |
|---|---|---|---|---|
| e | e | a | b | c |
| a | a | c | e | b |
| b | b | e | c | a |
| c | c | b | a | e |

#### Ejemplo de Grupo

Sea $B = \{0, 1\}$ y sea $+$ la operación definida en $B$ como sigue:

| + | 0 | 1 |
|---|---|---|
| 0 | 0 | 1 |
| 1 | 1 | 0 |

Entonces $B$ es un grupo. En él cada elemento es su propio inverso.

## Demostración de Teorema

El elemento $x = a^{-1} \ast b$ es una solución de la ecuación $ax = b$ pues:

$$a \ast (a^{-1} \ast b) = (a \ast a^{-1}) \ast b = e \ast b = b$$

Supongamos que $x_1$ y $x_2$ sean dos soluciones $a \ast x = b$. Entonces:

$$a \ast x_1 = b \quad \text{y} \quad a \ast x_2 = b$$

De aquí,

$$a \ast x_1 = a \ast x_2$$

Por un teorema anterior esto implica que $x_1 = x_2$.




