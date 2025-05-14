
Las gramáticas son un formalismo diseñado para la definición de lenguajes. Estas son un medio para generar las cadenas que pertenecen a un lenguaje.

El elemento fundamental de las gramáticas es la regla.


### Definición (Regla)
 Dado un alfabeto $\Sigma$ , una regla definida sobre $\Sigma$ (producción) es una par ordenado de cadenas (x,y) donde $x$, $y$ $\in \Sigma^*$ Aquí $x$ se dirá parte izquierda de la producción, $y$ se dirá parte derecha.

**Notación** $x := y$

### Definición (Regla compresora)
Una regla se llamará compresora si la longitud de su parte derecha es menor que la de la parte izquierda.

### Definición (Derivación directa)
Dado un alfabeto $\Sigma$ un conjunto de producciones $P$ sobre $\Sigma$ donde:
$$
P = 
\begin{cases}
x_1 := y_1 \\
x_2 := y_2 \\
\vdots \\
x_n := y_n
\end{cases}
$$
y $v, w \in \Sigma^*$.

Diremos que $w$ **deriva directamente** de $v$ si $\exists t,u \in \Sigma^*$ y una producción $x_i := y_i$ tal que $v = tx_i u$ y $w = t y_i u$.

**Notación:** $v \rightarrow w$ se lee $v$ produce directamente $w$.

### Definición (Derivación)
Dado un alfabeto $\Sigma$, un conjunto de producciones sobre $\Sigma$ y $v, w \in \Sigma^*$.

Se dice que $w$ **deriva** de $v$ si $\exists \ w_0, w_1, \dots, w_m \in \Sigma^*$ tales que:
$$
\begin{align*}
v = w_0 &\rightarrow w_1 \\
w_1 &\rightarrow w_2 \\
&\vdots \\
 w_{m-1} &\rightarrow w_m = w
\end{align*}
$$

**Notación:** $v \overset{*}{\rightarrow} w$ se lee $v$ produce a $w$.

### Ejemplos
**Ejemplo 1**: 
Defina un conjunto de reglas que nos permita evaluar la correcta formación de frases. Así, “el atleta corre velozmente” es correcta.

**Solución**:

$$
\begin{align*}
R1 <\text{oracion}>&:=<\text{sujeto}><\text{predicado}> \\
R2 <\text{sujeto}>&:=<\text{articulo}><\text{nombre}> \\
R3 <\text{predicado}>&:=<\text{verbo}><\text{complemento}> \\
R4 <\text{predicado}>&:=<\text{verbo}>\\
R5 <\text{articulo}>&:=\text{el} \\
R6 <\text{articulo}>&:=\text{la} \\
R8 <\text{nombre}>&:=\text{atleta} \\
R8 <\text{nombre}>&:=\text{voleibolista} \\
R9 <\text{verbo}>&:=\text{corre} \\
R10 <\text{verbo}>&:=\text{salta} \\
R11 <\text{complemento}>&:=\text{velozmente} \\
R12 <\text{complemento}>&:=\text{mucho} \\
\end{align*}
$$
Utilizando el conjunto $\mathcal{P}$ y partiendo del item podemos obtener frases como: 
- “**el atleta corre velozmente**” 
- “**la voleibolista salta mucho**” 
- “**la voleibolista salta**” 
- Sin embargo, nunca podríamos formar la frase "**mucho velozmente atleta**".

**Ejemplo 2**: 
Defina un conjunto de reglas que describa como son las instrucciones que permiten asignar el valor de una expresión a una variable en un Lenguaje de Programación.

**Solución**

$$
\begin{align*}
R1 <\text{asignacion}>&:=<\text{variable}>'='<\text{expresion}> \\
R2 <\text{expresion}>&:=<\text{numero}> \\
R3 <\text{expresion}>&:=<\text{variable}> \\
R4 <\text{expresion}>&:=<\text{expresion}>'+'<\text{expresion}> \\
R5 <\text{expresion}>&:=<\text{expresion}>'*'<\text{expresion}> \\


\end{align*}
$$


Luego, si asumimos que `A`, `B` y `C` pueden ser considerados como `<variable>` y `3`, `6` pueden ser considerados como `<numero>`, obtendremos instrucciones como:

$$
\begin{align*}
A &= B + C  \\
B &= B * 3  \\
C &= C + 6  \\
\end{align*}
$$

Pero no podremos construir instrucciones como:
$$
\begin{align*}
A &= +2 * / +4   \\
4 &= A \\
\end{align*}
$$

#### Resumen
- Se observa que el objetivo es llegar a tener una secuencia correcta de símbolos.
- Los símbolos  en el **Ejemplo 1** son el, la atleta, voleibolista, etc
- Los símbolos en el **Ejemplo 2** son A, B, C, +, \*, 3, 6 
- Se parte de un símbolo inicial (<oración> para el **Ejemplo 1**, <asignación> para el **Ejemplo 2** )
- Se utilizan algunas producciones.
### Definición (Gramática formal)
Una gramática formal definida sobre un alfabeto $\Sigma$ es una cuádrupla 
$$G = (\Sigma_T, \Sigma_N, S, P)$$ donde:

- $\Sigma_T$: alfabeto de símbolos terminados.
- $\Sigma_N$: alfabeto de símbolos no terminales.
- $S$: es el símbolo inicial de la gramática.
- $P$: es el conjunto de reglas.

Además, se cumple que:
1. $S \in \Sigma_N$
2. $\Sigma_N \cap \Sigma_T = \emptyset$
3. $\Sigma = \Sigma_N \cup \Sigma_T$

### Definición
La relación $\overset{n}{\rightarrow}$ se define recursivamente mediante:

1. $x \overset{0}{\rightarrow} x \quad \forall x \in \Sigma^*$,
2. $w \overset{n}{\rightarrow} xuy \wedge u \rightarrow v \implies w \overset{n+1}{\rightarrow} xvy \quad \forall x, y, w \in \Sigma^*, n \geq 0$.

Cuando $x \overset{n}{\rightarrow} y$, se dice que $y$ **se deriva de $x$ en $n$ pasos**.

**Observación**Se utilizarán las notaciones:

1. $x \overset{*}{\rightarrow} y$ si existe $n \geq 0$ tal que $x \overset{n}{\rightarrow} y$ (se deriva de $x$ en $0$ o más pasos).
2. $x \overset{+}{\rightarrow} y$ si existe $n \geq 1$ tal que $x \overset{n}{\rightarrow} y$ (se deriva de $x$ en $1$ o más pasos).



### Forma Normal de Backus-Naur (BNF)
Es una manera estandarizada de enunciar la composición de una gramática. En la BNF:

1. Los símbolos no terminales empiezan con “<” y terminan en “>”.
2. La regla $(S, T)$ se expresa $S ::= T$.
3. Las reglas de la forma:
$$
S ::= T_1, \ S ::= T_2, \dots, S ::= T_n
$$

   pueden combinarse como: $S ::= T_1 \mid T_2 \mid \dots \mid T_n$  
   donde la barra $\mid$ se lee *o*.

---

### Definición (Lenguaje Generado por una Gramática)

Dada una gramática $G = (\Sigma_T, \Sigma_N, S, P)$, llamamos **lenguaje generado por $G$** al conjunto de palabras de símbolos terminales derivables a partir de su símbolo inicial:

$$
L(G) = \{ w \in \Sigma_T^* \mid S \overset{*}{\rightarrow} w \}
$$

---

### Definición(Recursividad)
Una gramática es **recursiva** si tiene alguna derivación recursiva, es decir:  
si $A \overset{*}{\rightarrow} xAy$ donde $A \in \Sigma_N$, $x, y \in \Sigma^*$.

1. Si $x = \varepsilon$, se dice que la gramática es **recursiva por la izquierda**.  
2. Si $y = \varepsilon$, se dice que la gramática es **recursiva por la derecha**.

Si una gramática tiene producciones recursivas, es decir, producciones de la forma $A ::= xAy$, entonces es recursiva.

#### Teorema
Un lenguaje es infinito si y sólo si existe una gramática recursiva que lo genera.

---

# Equivalencia de Gramáticas
En muchas ocasiones es recomendable simplificar ciertas gramáticas eliminando símbolos o reglas no deseadas. Para esto definiremos una gramática equivalente a la primera pero que no tenga esos elementos indeseables.

**Un mismo lenguaje puede ser generado por varias gramáticas.**

### Equivalencia de gramáticas
Dos gramáticas $G^1$ y $G^2$ definidas ambas sobre $\Sigma_T$ son equivalentes si generan el mismo lenguaje, esto es $L(G^1) = L(G^2)$.


## Elementos Indeseables en Gramáticas

### Regla innecesaria
Una **regla innecesaria** es una producción de la forma:

$$
A ::= A
$$

### Variable útil
Sea $G = (\Sigma_T, \Sigma_N, S, P)$ una GLC. Una variable $X \in \Sigma_N$ se llama **variable útil** si y sólo si existen $u, v \in \Sigma^*$ tales que:

$$
S \overset{*}{\rightarrow} u X v \quad \text{y existe} \ w \in \Sigma_T^* \ \text{tal que} \ u X v \overset{*}{\rightarrow} w
$$

Decimos que un símbolo $X$ es útil para una gramática $G = (\Sigma_T, \Sigma_N, S, P)$ si existe alguna derivación de la forma $S \overset{*}{\rightarrow}  \alpha X \beta \ \overset{*}{\rightarrow} w$, donde $W$ pertenece a $\Sigma_T$.
Si $X$ no es útil, decimos que es **inútil*

El método para eliminar los símbolos inútiles identifica en primer lugar las dos cosas que un símbolo tiene que cumplir para resultar útil.

1. Decimos que $X$ es generador si $X \overset{*}{\rightarrow} w$  para alguna cadena terminal $w$.
2. Decimos que $X$ es alcanzable si existe una derivación $S \overset{*}{\rightarrow} \alpha X \beta$ para algún $\alpha$ y $\beta$.


>[!tip] Todo símbolo terminal es generador, ya que $w$ puede ser ese mismo símbolo terminal, el cual se obtiene en cero pasos.

Un símbolo que es útil será generador y alcanzable. Si eliminamos los símbolos que no son generadores en primer lugar y luego eliminamos de la gramática resultante aquellos símbolos que no son alcanzables, tendremos sólo los símbolos útiles, como demostraremos.

### Símbolo inaccesible o inútil
Llamaremos **símbolo inaccesible o inútil** a aquel símbolo no terminal que no aparece en ninguna cadena de símbolos que pueda derivarse a partir del símbolo inicial de la gramática.

### Definición (Símbolo no generativo)
Denominaremos **símbolo no generativo** a aquel símbolo no terminal a partir del cual no puede derivarse ninguna cadena de símbolos terminales.

---

Sea $G^1 = (\Sigma_N^1, \Sigma_T, S, P^1)$ una GLC. Transformaremos $G^1$ en $G^2 = (\Sigma_N^2, \Sigma_T, S, P^2)$ de modo que $L(G^1) = L(G^2)$ y para todo $A \in \Sigma_N^2$ se obtenga:

$$
A \overset{*}{\rightarrow} w \quad \text{para algún} \ w \in \Sigma_T^*
$$

---

### Algoritmo

1. **Inicializar** $\Sigma_N^2$ con las variables $A$ para los que $A \rightarrow w$ es una regla de $G^1$ con $w \in \Sigma_T^*$.

2. **Inicializar** $P^2$ con todas las reglas $A \rightarrow w$ para las cuales $A \in \Sigma_N^2$ y $w \in \Sigma_T^*$.

3. **Repetir**:  
   Añadir a $\Sigma_N^2$ todos los símbolos no terminales $A$ para los cuales $A \rightarrow w$, para algún $w \in (\Sigma_N^2 \cup \Sigma_T)^*$ que sea una producción de $P^1$, y añadirla a $P^2$.

   **Hasta que** no se puedan añadir más variables a $\Sigma_N^2$.

### Producción $\varepsilon$
Denominamos producción $\varepsilon$ a una regla de la forma:
$$
A \rightarrow \varepsilon
$$

### Variable anulable
Una variable $A \in \Sigma_N$ en una $GLC$ se dirá anulable si $A \overset{*}{\rightarrow} \varepsilon$ 

**Notación**
El conjunto de todos los símbolos no terminales anulables en una $GLC$ se denotará por $\mathcal{N}$ 

### Algoritmo
Algoritmo para determinar el conjunto de las variables anulables en una $GLC$

1. Inicializar $\mathcal{N}$ con todos los $A \in \Sigma_N / A \rightarrow \varepsilon$ 
2. Repetir
	1. Si $B \rightarrow w$  para $w \in \Sigma^*$ y todos los símbolos de $w$ están en $\mathcal{N}$, añadir $B$ a $\mathcal{N}$
	Hasta que no se puedan añadir más variables a $\mathcal{N}$

### Algoritmo
Algoritmo para la eliminación de reglas $\varepsilon$

Sea $G^1 = (\Sigma_N, \Sigma_T, S, P^1)$ una GLC.  
Se obtendrá una gramática equivalente $G^2 = (\Sigma_N, \Sigma_T, S, P^2)$ sin reglas $\varepsilon$, excepto $S \to \varepsilon$.


1. Obtener $\mathcal{N}$
2. $P^2 \leftarrow \emptyset$
3. Para cada regla $X \to w \in P^1$ hacer:
	Para cada representación de $w$ como $x_1 \psi_1 x_2 \dots \psi_n x_{n+1}$ con $\psi_1, \dots, \psi_n \in \mathcal{N}$:
            $$
            P^2 \leftarrow P^2 \cup \{ X \to x_1 x_2 \dots x_{n+1} \}
            $$
    Fin\_Para
4. Devolver $G^2 = (\Sigma_N, \Sigma_T, S, P^2 - \{ X \to \varepsilon \mid X \neq P \})$

#### Resumen
Para eliminar las producciones $\varepsilon$ sin cambiar el lenguaje generado por la gramática, se siguen los siguientes pasos:
1. **Identificar los símbolos anulables**: Un símbolo no terminal es anulable si puede derivar la cadena vacía $\varepsilon$.
2. **Reescribir las reglas**: Para cada regla, agregamos nuevas producciones donde se eliminan los símbolos anulables, en **todas las combinaciones posibles**.


### Ejemplo
La gramática original es:

$$
\begin{align*}
S &\rightarrow AaB \mid aaB \\   
A &\rightarrow \varepsilon \\
B &\rightarrow bbA \mid \varepsilon \\
\end{align*}
$$


#### Paso 1: Identificar los símbolos anulables

- $A \to \varepsilon$ : A es anulable.
- $B \to \varepsilon$: B es anulable.

Por lo tanto, los símbolos anulables son $A$ y $B$.
#### Paso 2: Generar nuevas producciones

Ahora, reescribimos las reglas eliminando los símbolos anulables en todas las combinaciones posibles:

1. **Regla $S \to AaB$ :**
    
    - $A \to \varepsilon$ y $B \to \varepsilon$, entonces:
        - Si A se elimina: $S \to aB$.
        - Si B se elimina: $S \to Aa$.
        - Si ambos se eliminan: $S \to a$.
    
    Producciones resultantes:
    $$
    S \to AaB \mid aB \mid Aa \mid a
    $$
1. **Regla $S \to aaB$ :**
    
    - $B \to \varepsilon$, entonces:
        - Si B se elimina: $S \to aa$.
    
    Producciones resultantes:
    $$
    S \to aaB \mid aa
    $$
1. **Regla $A \to \varepsilon$ :**  
    Eliminamos la producción $A \to \varepsilon$.
    
4. **Regla $B \to bbA \mid \varepsilon$ :**
    
    - $A \to \varepsilon$, entonces:
        - Si $A$ se elimina: $B \to bb$.
    
    Producciones resultantes:
    $$
    B \to bbA \mid bb
    $$

---

#### Gramática sin producciones épsilon

La gramática simplificada es:

$$
\begin{align*}
S &\to AaB \mid aB \mid Aa \mid a \mid aaB \mid aa \\
B &\to bbA \mid bb
\end{align*}
$$



A partir de una producción $\mathcal{P}^1$
$$
B \rightarrow X_1X_2 \dots X_n
$$
se pueden conseguir nuevas producciones en $\mathcal{P}^2$


### Producción unitaria
Una regla se llama producción unitaria o no generativa si es de la forma:

$$
A \to B \quad \text{con} \ A \, , \ B \in \Sigma_N 
$$

Las producciones unitarias hacen que la $GLC$ se vuelva compleja.

### Unit(A)
Sea $G$ una $GLC$. Para un símbolo $A \in \Sigma_N$ se define:
$$
\text{Unit}(A) = \{ B \in \Sigma_N \mid A \overset{*}{\to} B \text{ usando solo producciones unitarias}\}
$$
**Observación**
$A \in \text{Unit}(A)$ ya que $A \overset{*}{\to} A$ en o producciones unitarias.


### Par unitario
Sean $A$, $B \in \Sigma_N$. Nos referimos a $(A, B)$ como el par unitario si verifica $A \overset{*}{\to} B$ empleando sólo producciones unitarias.

#### Método de Eliminación de Producciones unitarias
Sea $G^1 = (\Sigma_N, \Sigma_T, S, P^1)$ una $GLC$ con producciones unitarias.  
Construiremos una GLC $G^2 = (\Sigma_N, \Sigma_T, S, P^2)$ sin producciones unitarias mediante:


1. Hállese $\Sigma_N$.
2. Para cada $A \in \Sigma_N$, determine $\text{Unit}(A)$.
3. Para cada par unitario $(A, B)$, añada a $P^2$ todas las producciones $A \to w$, donde $B \to w$ es una producción no unitaria de $P^1$.
	Observe que $A = B$ es posible, luego $P^2$ contiene todas las producciones no unitarias de $P^1$.
4. Elimine todas las producciones unitarias de $P^1$.


 **Ejemplo**
 Sea $G$ la GLC dada por:
$$
\begin{align*}
S &\to A \mid Aa \\
A &\to B \\
B &\to C \mid b \\
C &\to D \mid ab \\
D &\to b
\end{align*}
$$

Eliminar todas las producciones unitarias de $G$ y dar la gramática equivalente.

**Solución**


1. $\Sigma_N = \{S, A, B, C, D\}$.

 2. 
$$
    \begin{aligned}
    \text{Unit}(S) &= \{S, A, B, C, D\} \\
    \text{Unit}(A) &= \{A, B, C, D\} \\
    \text{Unit}(B) &= \{B, C, D\} \\
    \text{Unit}(C) &= \{C, D\} \\
    \text{Unit}(D) &= \{D\}
    \end{aligned}
    $$
3.  $$
    \begin{array}{|c|c|}
    \hline
    \text{Par Unitario} & \text{Producción no Unitaria} \\ \hline
    (S, S) & S \to Aa \\ \hline
    (S, A) & - \\ \hline
    (S, B) & S \to b \\ \hline
    (S, C) & S \to ab \\ \hline
    (S, D) & S \to b \\ \hline
    (A, A) & - \\ \hline
    (A, B) & A \to b \\ \hline
    (A, C) & A \to ab \\ \hline
    (A, D) & A \to b \\ \hline
    (B, B) & B \to b \\ \hline
    (B, C) & B \to ab \\ \hline
    (B, D) & B \to b \\ \hline
    (C, C) & C \to ab \\ \hline
    (C, D) & C \to b \\ \hline
    (D, D) & Db \\ \hline
    \end{array}
    $$
4. Eliminamos las Producciones Unitarias de $\mathcal{P^1}$:
$$
S \to A, \quad A \to B, \quad B \to C, \quad C \to D
$$

5. La gramática $G^2$ resultante es:
    $$
    P^2 = 
    \begin{cases}
    S \to b \mid ab \mid Aa \\
    A \to b \mid ab \\
    B \to ab \mid b \\
    C \to b \mid ab \\
    D \to b
    \end{cases}
    $$


# Forma Normal de Chomsky
La forma de las gramáticas libres de contexto es extremadamente general. Surge naturalmente una pregunta: ¿hay alguna forma en la que podamos restringir la sintaxis de las gramáticas libres de contexto sin reducir su poder expresivo?.

La forma normal de Chomsky presenta la gramática de una ma nera muy restringida, lo que facilita considerablemente ciertas pruebas sobre el lenguaje generado.


## Forma Normal de Chomsky

Todas las producciones son de la forma:
$$
\begin{align*}
S \to \varepsilon \quad &\text{ si } \varepsilon \in L(G) \\
A \to BC \quad &\text{ donde } B, C \in \Sigma_N \\
A \to \sigma \quad &\text{ donde } \sigma \in \Sigma_T
\end{align*}
$$

