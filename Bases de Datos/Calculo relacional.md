
El cálculo es un lenguaje de consulta formal donde escribimos una expresión **declarativa** para especificar una solicitud de recuperación.

- Cualquier consulta que pueda ser expresada en el [[Algebra Relacional|algebra relacional]] también puede ser expresada en el cálculo.
- Es un lenguaje de consultas *[[Bases de Datos/Introducción#Lenguajes de base de datos#Data-Manipulation Language (DML)|no procedural]]*. 
# Calculo relacional de tuplas
El **calculo relacional de tuplas** se expresa como
$$ \{ t \: | \: P(t) \}$$
Esto es, el conjunto de todas las tuplas $t$ tal que el predicado $P$ es verdadero para $t$. Usamos $t [ A ]$ para denotar el valor de la tupla $t$ en el atributo $A$, y usamos $t \in r$ para indicar que la tupla $t$ esta en la relación $r$.


![[Pasted image 20240409095002.png]]


## Componentes de una expresión de calculo relacional de tuplas

1. **Una relación R(t)**, equivalente a la clausula *from* de **SQL**.
2. **Una condición o predicado para seleccionar las tuplas**, equivalente a la clausula *where* de **SQL** y *selection* del [[Algebra Relacional|algebra relacional]].
3. **Un conjunto de atributos a ser recuperado**, equivalente a la clausula *select* de **SQL**.

$$ \{ \underbrace{t.nombre, t.apellidos}_{SELECT} \: | \: \underbrace{empleado(t)}_{FROM} \text{ AND } \underbrace{t.salary > 80000}_{WHERE} \} $$
Este ejemplo equivale a la consulta en el [[Algebra Relacional|algebra relacional]]:
$$ 
\Pi_{nombre, \: apellidos} (\sigma_{\text{salario > 80000}} \: (Empleado)
$$

## Cuantificadores

### Cuantificador existencial ( $\exists$ )
- Notación (Silberchatz)
$$ \exists \: t \in C(t) $$
- Notación (Navathe)
$$ (\exists \: t) \: (C) $$
Define una variable acotada (*bound variable*) asociada a una relación $R$ y evalúa una condición $C(t)$ para ella.

### Cuantificador universal ( $\forall$ )
- Notación (Silberchatz)
$$ \forall \: t \in C(t) $$
- Notación (Navathe)
$$ (\forall \: t) \: (C) $$
Es usado para formular consultas que
- Impliquen la asociación con tuplas de relaciones que no van para la respuesta
- Es similar al principio de la **división** del [[Algebra Relacional|algebra relacional]].

## Consultas de ejemplo

### Find the ID, name, dept name, salary for instructors whose salary is greater than $80,000:

- Notación de Silberschatz
$$ \{t | t \in instructor \: \land \: t[salary] > 80000 \} $$
- Notación de Navathe
$$ \{t | \: instructor(t) \text{ AND } t.salary > 80000 \} $$


Si, por ejemplo queremos solo el ID, 

Necesitamos escribir una expresión para la relación en el esquema (ID). **Necesitamos aquellas tuplas en (ID) tal que existe una tupla en *instructor* con el atributo *salary* >80000**. Para ello necesitamos el constructor "existe" de la lógica matemática. La notación 
$$ \exists \: t \in r \: (Q(t))$$
significa, **existe una tupla *t* en la relación *r* tal que el predicado Q(*t*) es cierto**

Con esta notación podemos escribir la consulta “Find the instructor ID for each instructor
with a salary greater than $80,000”
$$ \{ \: t \, | \,  \exists \, s \in instructor \: (t[ID] = s[ID] \land s[salary] > 80000) \} $$
La expresión se lee como **el conjunto de todas las tuplas *t* tal que existe una tupla s en la relación *instructor* para lo cual los valores de *t* y *s*  para el atributo *ID* son iguales y el valor de *s* para el atributo *salary* es mayor que $80,000  **

La variable tupla *t* es definida **solo en el atributo *ID***, dado que es el único atributo que tiene una condición especifica para *t*. Por tanto , el resultado es una relación en *ID*.

- Con la notación de Navathe sería
$$ \{  t.ID \: | \: instructor(t) \text{ AND } t.salary > 8000 \} $$


### Find the names of all instructors whose department is in the Watson building.


- Notación Silberschatz
Esta consulta involucra dos relaciones: *instructor* y *department*. Sin embargo, solo se requieren dos clausulas *existe* en nuestra expresión, conectada por un *y lógico*.
$$ \{ \: t \, | \: \exists \: s \in instructor \: (t[name] = s[name] $$
$$ \land \: \exists \: u \in deparment \: (u[dept\_name] = s[ dept\_name] $$
$$ \land \: u[building] = \text{"Watson"})) \} $$
La variable tupla $u$ esta restringida a los departamentos ubicados en el edificio *Watson*, mientras que la variable tupla $s$ esta restringida a los instructores cuyo *dept_name* coincide con el de la variable tupla $u$.

- Notación Navathe
$$ \{ t.name \: | \: instructor(t) \: AND \: (\exists \: s) (department(s) \: AND \: $$
$$ t[dept\_name] = s[dept\_name]) \: AND \: s[building] = \text{'Watson'} ) \: \} $$



### Find the set of all courses taught in the Fall 2017 semester, the Spring 2018 semester, or both
$$ \{ t \: | \: \exists \: s \in \: section \: (t[course\_id] = s[course\_id] $$
$$ \land \: s[semester] = \text{"Fall"} \: \land s[year] = 2017 ) $$
$$ \lor \: \exists \: u \in section \: (u[course\_id] = t[course\_id] $$
$$ \lor \: u[semester] = \text{"Spring"} \: \lor \: u[year] = 2018 ) \} $$

### Find the set of all courses taught in both the Fall 2017 semester and the Spring 2018 semester

$$ \{ t \: | \: \exists \: s \in \: section \: (t[course\_id] = s[course\_id] $$
$$ \land \: s[semester] = \text{"Fall"} \: \land s[year] = 2017 ) $$
$$ \land \: \exists \: u \in section \: (u[course\_id] = t[course\_id] $$
$$ \lor \: u[semester] = \text{"Spring"} \: \lor \: u[year] = 2018 ) \} $$

### Find all the courses taught in the Fall 2017 semester but not in Spring 2018 semester
$$ \{ t \: | \: \exists \: s \in \: section \: (t[course\_id] = s[course\_id] $$
$$ \land \: s[semester] = \text{"Fall"} \: \land s[year] = 2017 ) $$
$$ \lnot \: \exists \: u \in section \: (u[course\_id] = t[course\_id] $$
$$ \lor \: u[semester] = \text{"Spring"} \: \lor \: u[year] = 2018 ) \} $$
### Find all students who have taken all courses offered in the Biology department.
Para escribir esta consulta introducimos el constructo "para todo", la notación
$$ \forall \: t \in \: r(Q(t)) $$
significa ***Q* es cierto para todas las tuplas *t* en la relación *r***
La expresión para nuestra consulta sería

$$ \{ \: t \: | \: \exists \: r \in student \: (r[ID] = t[ID]) \: \land $$
$$ ( \: \forall \: u \in course \: (u[dept\_name] = \text{"Biology"} \to $$
$$ \exists \: s \in takes \: (t[ID] = s[ID] \: \land s[course\_id] = u[course\_id] \, ) \, ) \, \} $$

Esta expresión se interpreta como: **El conjunto de todos los estudiantes, es decir tuplas *t* (ID), tal que para todas las tuplas *u* en la relación *course*, si el valor de *u* en el atributo *dept_name* es 'Biology' entonces existe una tupla en la relación *takes* que incluye el *ID* y *course_id* del estudiante**

## Expresión general
Con la **notación de Navathe** la expresión general de una consulta de calculo relacional es de la forma
$$ \{ t_1.A_1, t_2.A_2, ... , t_n.A_n \: | \: cond(t_1, t_2, ..., t_n, t_{n+1}, ... t_{n+m}) \} $$
- En $t_1.A_1, t_2.A_2, ... , t_n.A_n$ , $t_i$ son variables de tupla y $A_i$ son un atributo de la relación.
- En $cond(t_1, t_2, ..., t_n, t_{n+1}, ... t_{n+m})$, la relación forma parte de la condición.

## Definición formal
Una expresión del *calculo relacional de tuplas* es de la forma
$$ \{ \: t \: | \: P(t) \: \}$$
donde $P$ es una formula. Muchas tuplas pueden aparecen en una formula. Una variable de tupla se dice que es *free variable* a menos que este cuantificada por $\exists$ o $\forall$. Por ejemplo, en 
$$ t \in instructor \: \land \exists \: s \in department(t[dept\_name] = s[dept\_name] \: ) $$
$t$ es una *free variable*, mientras que la variable de tupla $s$ se dice que es una *bound variable*.

Una formula del calculo relacional de tuplas **se construye a partir de átomos**. Un átomo se compone de las siguientes formas
- $s \in r$, donde $s$ es una variable de tupla y $r$ es una relación (no se permite $\notin$)
- $s[x] \: \Theta  \: s[y]$, donde $s$ y $u$ son variables de tupla, $x$ es un atributo en el cual  $s$ esta definido, $y$ es un atributo en el cual $u$ esta definido, y $\Theta$ es un operador de comparación ($<, \, \leq , \, = , \, \neq , \, > , \, \geq$). **Requerimos que los atributos *x* y *y* tengan dominios cuyos miembros puedan ser comparados**.
- $s[x] \: \Theta \: c$, donde $s$ es una variable de tupla, $x$ es un atributo en el cual esta definido $s$, $\Theta$ es un operador de comparación, y $c$ es una constante en el dominio del atributo $x$.

**Construimos formulas a partir de átomos** usando las siguientes reglas
- Un átomo es una fórmula
- Si $P_1$ es una fórmula, entonces también $\lnot P_1$ y $(P_1)$ 
- Si $P_1$ y $P_2$ son fórmulas, entonces también lo son $P_1 \lor P_2$, $P_1 \land P_2$ y $P_1 \to P_2$
- Si $P_1(s)$ es una fórmula que contiene una variable de tupla *libre* $s$ y $r$ es una relación, entonces $$ \exists \: s \in r \: (P_1(s)) \: \: y \: s \in r(P_1(s)) $$ es también una fórmula.


## Seguridad de expresiones
Una expresión del cálculo relacional de tuplas puede generar una relación infinita. Por ejemplo, tenemos esta expresión
$$ \{ \: t \: | \: \lnot \: (t \in instructor )\} $$
Existe una infinidad de tuplas que no están en *instructor*. La mayoría de estas tuplas contienen valores que **ni siquiera aparecen en la base de datos**. 

Para definir una restricción del cálculo relacional de tuplas introducimos el concepto de **dominio** de una fórmula relacional de tuplas, $P$. El dominio de $P$ ($dom(P)$) es el conjunto de todos los valores **referenciados por P**. Incluye valores mencionado en $P$ mismo, como también valores que aparecen en una tupla de una relación mencionada en $P$. Así, **el dominio de P es el conjunto de todos los valores que aparecen explícitamente en *P* o que aparecen en una o más relaciones cuyos nombres aparecen en *P***. Por ejemplo
$$ dom(t \in instructor \land t[salary] > 80000) $$
En nuestro ejemplo, el dominio de la fórmula es el conjunto de todos los salarios posibles que pueden aparecer en la base de datos.

Decimos que una expresión $\{ t \: | \: P(t) \}$ es *segura* si todos los valores que aparecen en el resultado son valores del dominio de $P$. La expresión $\{ \: t \: | \: \lnot \: (t \in instructor )\}$ **no es segura**, ya que su dominio es el conjunto de todos los valores que aparecen en *instructor*. Sin embargo, es posible hallar una tupla $t$ que no se encuentre en *instructor* que contenga valores que no se encuentren en instructor.


# Calculo relacional de dominios
Utiliza variables de dominio que toman valores de un dominio de atributos en lugar de valores para una tupla completa.

## Definición formal
Una expresión en el calculo relacional de dominios es de la forma
$$ \{ \, <x_1, x_2, ... , x_n> \: | \: P(x_1, x_2, ... , x_n)\,\} $$
donde $x_1, x_2, ... , x_n$ representan variables de dominio. $P$ representa una fórmula compuesta de átomos. Un átomo tiene una de las siguientes formas

- $<x_1, x_2, ... , x_n> \in r$, donde $r$ es una $r$ es una relación en $n$ atributos y $x_1, x_2, ... , x_n$ son variables de dominio o constantes de dominio.
- $x \: \Theta  \: y$, donde $x$ y $y$ son variables de dominio y $\Theta$ es un operador de comparación. **Requerimos que los atributos *x* y *y* tengan dominios cuyos miembros puedan ser comparados**.
- $x \: \Theta \: c$, donde $x$ es una variable de dominio, $\Theta$ es in operador de comparación y $c$ es una constante en el dominio de los atributos para el cual $x$ es una variable de dominio.

**Construimos formulas a partir de átomos** usando las siguientes reglas
- Un átomo es una fórmula
- Si $P_1$ es una fórmula, entonces también $\lnot P_1$ y $(P_1)$ 
- Si $P_1$ y $P_2$ son fórmulas, entonces también lo son $P_1 \lor P_2$, $P_1 \land P_2$ y $P_1 \to P_2$
- Si $P_1(x)$ es una fórmula en $x$, donde $x$ es una variable de dominio *libre*, entonces $$ \exists \: x  \: (P_1(x)) \: \:  y  \: \: \forall \: x \: (P_1(x)) $$ es también una fórmula.

## Consultas de ejemplo

![[Pasted image 20240409095002.png]]
### Find the instructor ID, name, dept name, and salary for instructors whose salary is greater than $80,000
$$ \{ < i, n, d, s > | < i, n, d, s > \: \in instructor ∧ s > 80000 \} $$
### Find all instructor ID for instructors whose salary is greater than $80,000
$$ \{ < i > | \: \exists \: n, d, s \: (< i, n, d, s > \: \in instructor ∧ s > 80000 )\} $$

### Find the names of all instructors in the Physics department together with the course id of all courses they teach
$$ \{ \: <n,c> \: | \exists \: i, \, sec, \, sem, \, y \: (<i,\, c,\, sec,\, sem,\, y> \: \in \: teaches $$
$$ \land \: \exists \: d,\, s \: (<i, n, d, s> \: \in \: instructor \land d = \text{"Physics"}\,)\,)\,\} $$

### Find the set of all courses taught in the Fall 2017 semester, the Spring 2018 semester, or both
$$ \{ \: <c> \: | \: \exists \: sec, \,sem,\, y,\, b,\, r,\, t, \: ( <c, \, sec, \, sem, \, y, \, b, \, r, \, t > \: \in \: section $$
$$ \land \: sem = \text{"Fall"} \: \land \: y = 2017 ) $$
$$  \lor  \: \exists \: sec, \,sem,\, y,\, b,\, r,\, t, \: ( <c, \, sec, \, sem, \, y, \, b, \, r, \, t > \: \in \: section $$
$$  \land \: sem = \text{"Spring"} \: \land \: y = 2018 ) \, \}  $$

### Find all students who have taken all courses offered in the Biology department

$$ \{ \: <i> \: | \: \exists \: n, d, tc \: (<i, n, d, tc> \: \in \: student) \: \land  $$
$$  \forall \: ci, ti, dn, c \: (<ci, ti, dn, c> \: \in \: course \: \land dn = \text{"Biology"} \to  $$
$$ \exists \: sec, \, sem, \, y, g (<i, ci, sec, sem, y, g> \: \in takes \:)\,)\,\} $$

## Seguridad de expresiones
Una expresión como
$$ \{ < i, n, d, s > | \: \lnot \:(< i, n, d, s > \: \in instructor) \} $$
no es segura, porque permite valores en el resultado que **no se encuentran en el dominio de la expresión**.

Para el cálculo relacional de dominios se debe tener en consideración las formulas que lleven los cuantificadores "existe" y "para todo". 

Una expresión
$$ \{ < x_1, x_2,…, x_n > \: | \: P (x_1, x_2, …, x_n)\: \} $$
es segura si se cumplen todas las siguientes condiciones:
1. Todos los valores que aparecen en las tuplas de la expresión son valores del $dom(P)$.
2. Para cada subfórmula de "existe" de la forma $\exists \: x \: (P_1(x))$, la subfórmula es verdadera si y solo si existe un valor $x$ en $dom(P_1)$ tal que $P_1(x)$ es verdadero.
3. Para cada subfórmula "para todo" de la forma $\forall \: x \: (P_1(x))$, la subfórmula es cierta si y solo si $P_1(x)$ es cierta para todos los valores $x$ del dominio del $dom(P_1)$.
