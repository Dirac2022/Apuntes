# Proposición
Es una frase de la cual se puede determinar si es verdadera o falsa, es decir tiene un valor de verdad.

**Ejemplos**
Son proposiciones:
- $3+2$ es $7$
- $3 > \sqrt{7}$
- $13$ es un número primo

**No son proposiciones**:
Buen día
ven a mi cumpleaños
qué hora tienes?

## Proposiciones equivalentes
Dos proposiciones $P$ y $Q$ son equivalentes si para todos los casos tienen el mismo valor de verdad.
- $P : 3 < 7$ y $Q : \pi$ es irracional son equivalentes
- $P : 1/3$ es un entero y $Q : 7 < 5$ son equivalentes

## Negación de una proposición
Si P es una proposición, $\lnot P$ es su negación.

**Ejemplos**
- $P : 8 < 5$ , $\lnot P : 8 ≥ 5$

### Tabla de verdad
| $P$ | $\lnot P$ |
| --- | --------- |
| $V$ | $F$       |
| $F$ | $V$       |

# Conjunción
Una conjunción implica que ambas afirmaciones son verdaderas. Con una conjunción, las declaraciones están conectadas por la palabra "y".
## Tabla de verdad
| $P$ | $Q$ | $P \wedge Q$ |
| --- | --- | ------------ |
| $V$ | $V$ | $V$          |
| $V$ | $F$ | $F$          |
| $F$ | $V$ | $F$          |
| $F$ | $F$ | $F$          |

# Disyunción débil
La disyunción implica que al menos una armación es verdadera. En la disyunción las declaraciones están conectadas por la palabra "o".
## Tabla de verdad
| $P$ | $Q$ | $P \vee Q$ |
| --- | --- | ---------- |
| $V$ | $V$ | $V$        |
| $V$ | $F$ | $V$        |
| $F$ | $V$ | $V$        |
| $F$ | $F$ | $F$        |

# Condicional
Un enunciado condicional nos dice que si el antecedente es verdadero, el consecuente no puede ser falso. Por tanto, un enunciado condicional sólo es falso cuando un antecedente
verdadero implica un consecuente falso.
## Tabla de verdad
| $P$ | $Q$ | $P \to Q$ |
| --- | --- | --------- |
| $V$ | $V$ | $V$       |
| $V$ | $F$ | $F$       |
| $F$ | $V$ | $V$       |
| $F$ | $F$ | $V$       |
- $P$ : hipótesis, antecedente
- $Q$ : conclusión, consecuente
Para $P \to Q$ su recíproca es $Q \to P$
la contrapuesta es $\lnot Q \to \lnot P$

# Bicondicional
Un enunciado bicondicional es verdadero cuando ambos enunciados son verdaderos o ambos son falsos.
$P \leftrightarrow Q$ es equivalente a $P \to Q \wedge Q \to P$
## Tabla de verdad
| $P$ | $Q$ | $P \leftrightarrow Q$ |
| --- | --- | --------------------- |
| $V$ | $V$ | $V$                   |
| $V$ | $F$ | $F$                   |
| $F$ | $V$ | $F$                   |
| $F$ | $F$ | $V$                   |

# Disyunción Exclusiva
Una disyunción exclusiva solamente es verdadera cuando ambas frases tienen valores diferentes y es falsa si las dos frases son ambas verdaderas o ambas falsas.
## Tabla de verdad
| $P$ | $Q$ | $P \Delta Q$ |
| --- | --- | ------------ |
| $V$ | $V$ | $F$          |
| $V$ | $F$ | $V$          |
| $F$ | $V$ | $V$          |
| $F$ | $F$ | $F$          |
$P \Delta Q \equiv \lnot \ (P \leftrightarrow Q)$

# Combinación de valores veritativos
Si se tienen $n$ proposiciones, el número de combinaciones es $2^n$ el cual es el número de filas de la tabla de verdad.

# Tautología y contradicción

**Definición**
Una proposición es una tautología si es siempre verdadera.
- Si la proposición condicional es una tautología se denota $P \Rightarrow Q$
- Si la proposición bicondicional es una tautología se denota $P \Leftrightarrow Q$

**Definición**
Una contradicción es una proposición que siempre es falsa.

# Frase abierta

Una frase abierta o función proposicional es una proposición que contiene una variable.
**Ejemplo**
- $x^2 + 2x + 16 = 0$  Notación P(x)
- $x$ fue el primer presidente del Perú

# Conjunto de significados
El conjunto de significados de una variable es la colección de objetos que pueden ser sustituidos por una variable en una frase abierta. Llamaremos **conjunto de verdad de la frase abierta** al conjunto de objetos del conjunto de significados para los cuales la frase abierta
se convierte en una proposición verdadera al sustituir la variable por ellos.

**Ejemplo**
Sea la frase abierta $x^2 + 2x + 16 = 0$  y el conjunto de significados es el de números reales
Determine el conjunto de verdad.

**Ejemplo**
Sea la frase abierta $x^2 + 2x + 16 = 0$ y el conjunto de significados es los números complejos
Determine el conjunto de verdad.

En una contingencia la proposición resultante es $V$ o $F$.

# Frase universalmente cuantificada
Es una frase de la forma $\forall \ x$, $P(x)$ para todo $x$ del conjunto de significados $P(x)$
**Ejemplo**
Si $P(x)$ es la frase abierta $x + 1 > x$ y el conjunto de significados la colección de todos los reales $\forall \ x$, $P(x)$ es una proposición verdadera.

# Frase cuantificada existencialmente
Es una frase de la forma $\exists \ x$ , $P(x)$ se lee: "existe un $x$ tal que $P(x)$"
Esto indica que algún elemento del conjunto de significados es un valor que, al sustituir a $x$, hace que $P(x)$ sea verdadera.

# Leyes del álgebra proposicional
1. **Ley de Idempotencia**
	- $p \wedge p \equiv p$
	- $p \vee p \equiv p$
2. **Ley Conmutativa**
	- $p \wedge q \equiv q \wedge p$
	- $p \vee q \equiv q \vee p$
	- $p \leftrightarrow q \equiv q \leftrightarrow p$
	- $p \, \Delta \, q \equiv q \, \Delta \, p$
3. **Ley de Absorción**
	- $p \wedge (p \vee q) \equiv p$
	- $p \wedge (\lnot p \vee q) \equiv p \wedge q$
	- $p \vee (p \wedge q) \equiv p$
	- $p \vee (\lnot p \wedge q) \equiv p \vee q$
4. **Ley de De Morgan**
	- $\lnot \, (p \wedge q) \equiv \lnot \, p \vee \lnot \, q$
	- $\lnot \, (p \vee q) \equiv \lnot \, p \wedge \lnot \, q$
5. **Leyes de uso frecuente**
	- $p \to q \equiv \lnot \, p \vee q$
	- $p \to q \equiv\lnot q \to \lnot \, p$
	- $p \leftrightarrow q \equiv (p \to q) \wedge (q \to p)$
	- $p \leftrightarrow q \equiv (p \wedge q) \vee (\lnot \, p\wedge \lnot \, q)$
	- $p \, \Delta \, q \equiv \lnot \, (p \leftrightarrow q)$
	- $p \, \Delta  \, q \equiv (p \vee q) \wedge (\lnot \, p \vee \lnot \, q)$

