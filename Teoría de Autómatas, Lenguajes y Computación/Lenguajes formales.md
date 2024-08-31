Un lenguaje formal consiste en un conjunto de símbolos y algunas reglas de formación por los que estos símbolos se pueden combinar en entidades que se llaman oraciones.

>[!info]
>Un lenguaje formal es el conjunto de todas las cadenas permitidas por las reglas de formación.


# Simbolo
Un símbolo es un objeto indivisible, es una entidad abstracta.

**Ejemplo:** 
- Las letras del alfabeto: $a, b, c, \dots$
- Los dígitos: $0, 1, \dots, 9$
- Otros caracteres: $\$, \#, \%, \$

# Alfabeto
Un alfabeto es un conjunto no vacío finito de símbolos.

**Notación:** Usaremos $\Sigma$ para denotar a un alfabeto.

**Ejemplo:** 
- $\Sigma = \{0, 1\}$ alfabeto binario
- $\Sigma = \{a, b, \dots, z\}$ alfabeto romano
- $\Sigma = \{a, b, \dots, z, A, \dots, Z, \$, \%, \#, \dots\}$ alfabeto ASCII

# Cadena
Una cadena (palabra, frase) es una secuencia finita de símbolos tomados a partir de un alfabeto $\Sigma$.

**Ejemplo:** 
- Para el alfabeto romano: $abc, def, hzw$
- Para el alfabeto binario: $0, 1, 01, 001, 1010, \dots$

**Notación:** Se usa generalmente $w$ para denotar una cadena.

## Longitud de cadena
Sea $w = a_1a_2 \dots a_k$ una cadena sobre $\Sigma$ tal que $a_i \in \Sigma$ con $i = 1, \dots, k$, la longitud de $w$ es el número de símbolos de la cadena. Diremos que
$$|w| = k \iff w = a_1 \dots a_k \text{ con } a_i \in \Sigma \text{ para } i = 1, \dots, k$$

**Ejemplo:** $\Sigma = \{A, C, 2, 3, 4\}; |CC342A| = 6 = |w|$, $w$ cadena sobre $\Sigma$.

$$| \cdot |: \Sigma^* \rightarrow \mathbb{N}$$

$$|HOY| = 3$$
## Cadena nula o vacía
A la cadena que no contiene símbolos se le llama cadena nula o cadena vacía.

**Notación:** $\epsilon$, donde $|\epsilon| = 0$


>[!important]
>El metasímbolo (ni palabra, ni símbolo) $\epsilon$, nunca puede ser considerado como un símbolo del alfabeto $\Sigma$.

# Potencia de un alfabeto
- **Definición:** Para un alfabeto $\Sigma$, definiremos $\Sigma^0 = \{\epsilon\}$.

- **Definición:** Si $\Sigma$ es un alfabeto y $n \in \mathbb{Z}^+$, definimos las potencias de $\Sigma$ recursivamente como sigue:
	1. $\Sigma^1 = \Sigma$
	2. $\Sigma^{n+1} = \{xy/x \in \Sigma, y \in \Sigma^n\}$ donde $xy$ denota la yuxtaposición de $x$ e $y$.

**Ejemplo:** Sea $\Sigma$ un alfabeto.

- Si $n = 2$ entonces $\Sigma^2 = \{xy/x,y \in \Sigma\}$, digamos si $\Sigma = \{0, 1\} \Rightarrow \Sigma^2 = \{00, 01, 10, 11\}$
- Si $n = 3$ y $\Sigma = \{a, b, c, d, e\}$, $\Sigma^3$ podría contener $5^3 = 125$ cadenas de longitud $3$, entre ellas $aaa, acb, aea, cdd, eda$.

En general, $\forall n \in \mathbb{Z}^+$ se cumple que $|\Sigma^n| = |\Sigma|^n$ ya que estamos tratando con ordenaciones de tamaño $n$, donde se puede repetir cualquiera de los objetos de $\Sigma$.

**Notación:** Sea un alfabeto $\Sigma$, denotaremos:

$$\Sigma^+ = \bigcup_{i=1}^{\infty} \Sigma^i = \bigcup_{i \in \mathbb{Z}^+} \Sigma^i$$

$$\Sigma^* = \bigcup_{i=0}^{\infty} \Sigma^i$$

Se verifica que $\Sigma^* = \Sigma^+ \cup \Sigma^0$.

Para $\Sigma = \{0, 1, 2\}$ encontraremos cadenas como $0, 01, 102, 1112$ tanto en $\Sigma^+$ como en $\Sigma^*$.

Al conjunto $\Sigma^*$ se le conoce como la estrella o cerradura de Kleene, en honor a Stephen Kleene, lógico matemático.

Si $\Sigma = \{0, 1\} \Rightarrow \Sigma^* = \{ \epsilon, 0, 1, 01, 00, 10, 11, 000, \dots \}$.

Aquí tienes el texto extraído de la imagen, con la notación matemática adecuada:

---

### 5.1 Operaciones con cadenas

**Definición:** La concatenación es la operación básica entre cadenas. Es una operación binaria en $\Sigma^*$.

$$
\cdot : \Sigma^* \times \Sigma^* \rightarrow \Sigma^*
$$

Si $x = a_1a_2 \dots a_i$ y $z = b_1b_2 \dots b_j$ entonces:

$$
w = x \cdot z = a_1a_2 \dots a_i b_1 \dots b_j
$$

A veces se suele suprimir el operador $\cdot$, escribiendo directamente $w = xz$.

**Definición:** Una cadena $z$ se dirá subcadena de otra cadena $w$ si existen cadenas $x, y \in \Sigma^*$ tal que:

$$
w = xzy
$$

**Definición:** Sea una cadena $w = xz$. Entonces:

- $x$ es un prefijo de $w$.
- $x$ se dirá prefijo propio de $w$ si $z \neq \epsilon$.
- $z$ es un sufijo de $w$.
- $z$ es un sufijo propio de $w$ si $x \neq \epsilon$.

$$
\text{Prefijo}(w) = \{x \in \Sigma^* / \exists z \in \Sigma^* : w = xz\}
$$

$$
\text{Sufijo}(w) = \{x \in \Sigma^* / \exists z \in \Sigma^* : w = zx\}
$$

### Propiedades de la concatenación

- **P1 [Cerradura]** $\forall v, w \in \Sigma^*$, $v \cdot w \in \Sigma^*$.
- **P2 [Asociatividad]** $\forall u, v, w \in \Sigma^*$, $(uv)w = u(vw)$.
- **P3 [Identidad]** Para $w \in \Sigma^*$: $w\epsilon = \epsilon w = w$.
- **P4 [Longitud]** Para $u, w \in \Sigma^*$: $|uw| = |u| + |w|$.

Además, la concatenación no necesariamente es conmutativa.

**Definición:** Sea $w$ una cadena, donde $w = a_1a_2 \dots a_n$. La reversa de $w$ se denota por $w^R$ y se define mediante:

$$
w^R = a_n a_{n-1} \dots a_2 a_1
$$

Se puede definir recursivamente mediante:

$$
\epsilon^R = \epsilon
$$

$$
(vw)^R = w^R v^R
$$

### Propiedades

$$
(w^R)^R = w
$$

$$
(uv)^R = v^R u^R
$$

**Notación:** $w^k = \underbrace{ww \dots w}_{k \text{ veces}}$.