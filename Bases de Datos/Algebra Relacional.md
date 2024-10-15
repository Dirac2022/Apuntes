
El álgebra relacional es un *lenguaje de consultas procedural*. Consiste en un conjunto de operaciones que toman una o más relaciones como entrada y produce una nueva relación como resultado.

![[Pasted image 20240409095002.png]]

# Operaciones elementales
Las operaciones de `selección`, `proyección` y `renombramiento` son llamadas operaciones **unarias**, puesto que operan en una única relación.

## La operación de selección ($\sigma$)
Selecciona tuplas que satisfacen un predicado dado. El predicado aparece como un subíndice de $\sigma$, el argumento de relación esta en paréntesis después del $\sigma$.

En general, se permiten comparaciones usando $=$, $\neq$, $<$, $\leq$, $>$ y $\geq$ en el operador de selección. Además podemos combinar muchos predicados dentro de un predicado más grande usando los conectores ($\land$) o ($\lor$) y ($\lnot$).

### Ejemplos

*Select those tuples of the instructor relation **where** the instructor is in the “Physics” department*.
$$  \sigma_{name = \text{"Physics"}} \: (instructor) $$

*Find all instructors with salary greater than $90,000*
$$ \sigma_{salary > 90000} \: (instructor) $$
*Find all departments whose name is the same as their building name*
$$ \sigma_{dept\_name = building} \: (department) $$

>[!tip] La operación `select` en Álgebra Relacional corresponde a `where` en **SQL**

## La operación de proyección ($\Pi$)
El operador de proyección es un operador unario que retorna su argumento de relación con ciertos atributos omitidos. Dado que una relación es un conjunto, **filas duplicadas son eliminadas**.  Listamos los atributos que deseamos que aparezcan en el resultado como subíndices a $\Pi$. El argumento de relación se coloca en paréntesis.

$$ \Pi_{ID, \, name, \, salary} \: (instructor)$$

## Composición de operadores relacionales
Como el resultado de un a operación de algebra relacional es del mismo tupo (relación) que su entrada, las operaciones de algebra relacional pueden componerse entre si en una expresión de algebra relacional. Por ejemplo

$$ \Pi_{name} \: ( \sigma_{\text{dept\_name = "Physics"}} \: (instructor)) $$

## La operación de unión ($\cup$)
Por ejemplo consideremos esta consulta: *Find the set of all courses taught in the Fall 2009 semester, the Spring 2010 semester, or both*

$$ \Pi_{course\_id} \: (\sigma_{semester \, = \, \text{"Fall"} \: \land \: year \, = \, 2009} \: (section)) \: \: \cup $$
$$ \Pi_{course\_id} \: (\sigma_{semester \, = \, \text{"Spring"} \: \land \: year \, = \, 2010} \: (section)) $$



En general debemos asegurarnos que las uniones sean realizadas entre relaciones *compatibles*. Para ello requerimos que dos condiciones sean válidas:
1. Las relaciones $r$ y $s$ deben ser de la misma *aridad*, es decir, deben tener el mismo número de atributos
2. Los dominios del i-ésimo atributo de $r$ y el i-ésimo atributo de $s$ deben ser iguales para todo $i$.


## La operación diferencia de conjuntos ($-$)
Nos permite encontrar tuplas que están en una relación pero no en otra. La expresión $r-s$ produce una relación que contiene tuplas en $r$ pero no en $s$. 
Por ejemplo: *Find all the courses taught in the Fall 2009 semester but not in Spring 2010 semester*.
$$ \Pi_{course\_id} \: ( \sigma_{\text{semester = "Fall" } \, \land \, \text{ year = 2009}} \: (section) \, ) \: - $$
$$ \Pi_{course\_id} \: ( \sigma_{\text{semester = "Sptring" } \, \land \, \text{ year = 2010}} \: (section) \, ) $$

**También debemos asegurarnos que las diferencias de conjuntos se tomen entre relaciones *compatibles***.

## La operación producto cartesiano ($\times$)



| nombre1 | nombre2 | nombre3 |
| ------- | ------- | ------- |
| hola    | soy     | grege   |
| gre     | tu      | ui      |

| campo1 | campo2 |
| ------ | ------ |
| no     | corras |
| tr     | bt     |



| nombre1 | nombre2 | nombre3 | campo1 | campo2 |
| ------- | ------- | ------- | ------ | ------ |
| hola    | soy     | grege   | no     | corras |
| gre     | tu      | ui      | no     | corras |
|         |         |         |        |        |


Nos permite combinar información de dos relaciones cualesquiera.
Dado que un nombre de atributo puede aparecer en ambas relaciones, necesitamos idear un esquema de nombres para distinguir entre estos atributos. Lo hacemos aquí adjuntando al atributo el nombre de la relación de la cual proviene originalmente el atributo. Por ejemplo, el esquema de relación para $r = instructor \times teaches$ es
$$ (\textit{ instructor.ID, instructor.name, instructor.dept\_name, instructor.salary}  $$
$$ \textit{teaches.ID, teaches.course\_id, teaches.sec\_id, teaches.semester, teaches.year ) } $$
Con este esquema, podemos distinguir $instructor.ID$ de $teaches.ID$. Para aquellos atributos que aparecen en solo uno de los dos esquemas omitimos el prefijo del nombre de la relación.

La relación de esquema para $r$ nos queda como
$$ (\textit{instructor.ID, name, dept\_name, salary, } $$
$$ { teaches.ID, course\_id, sec\_id, semester, year} ) $$

Esta convención de nombres requiere que las relaciones que son los argumentos de la operación de producto cartesiano tengan nombres distintos. Esta exigencia provoca problemas en algunos casos, como cuando se desea el producto cartesiano de una relación consigo misma. Un problema similar surge si utilizamos el resultado de una expresión de álgebra relacional en un producto cartesiano, ya que necesitaremos un nombre para la relación para poder referirnos a los atributos de la relación. 

Ejemplo: *Find the names of all instructors in the Physics department together with the course id of all courses they taught*




Si escribimos 
$$ \sigma_{\text{dept\_name = "Physics"}} \: (instructor \times teaches) $$
Sin embargo la columna *course_id* pueden tener información acerca de cursos que no fueron impartidos por el instructor correspondiente. Si escribimos

$$ \sigma_{\text{instructor.ID = teaches.ID}} \: (\sigma_{\text{dept\_name = "Physics}} \: (instructor \times teaches)) $$
obtenemos solo aquellas tuplas de $instructor \times teaches$ que pertenecen a *instructors* en *Physics* y los cursos que impartieron.
Finalmente, dado que solo queremos los nombres de todos los *instructors* en el departamento de física con el *couse_id* de todos los cursos que impartieron, hacemos una proyección:
$$ \Pi_{\text{name, course\_id}} \: (\sigma_{\text{instructor.ID = teaches.ID}} (\sigma_{\text{dept\_name = "Physics"}} \: (instructor \times teaches))) $$


## La operación de renombrar ($\rho$)
Los resultados en las expresiones de álgebra relacional no tienen un nombre que podemos usar para referenciarlos. Es útil poder darles nombres. Dada una expresión de álgebra relacional $E$, la expresión

$$ \rho_x \: (E) $$
retorna el resultado de la expresión $E$ bajo el nombre $x$
También podemos aplicar la operación de renombrar a una relación $r$ para obtener la misma relación bajo un nuevo nombre.

Supongamos que una expresión de álgebra relacional $E$ tiene aridad $n$, entonces la expresión
$$ \rho_{x(A_1, A_2, ... ,  A_n)} \: (E) $$
retorna el resultado de la expresión E bajo el nombre $x$, y con los atributos renombrados a $A_1, A_2, ..., A_n$

Ejemplo: *Find the highest salary in the university*

 Nuestra estrategia es (1) calcular primero una relación temporal que consista en aquellos salarios que no son los más altos y (2) tomar la diferencia entre la relación salario (instructor) y la relación temporal recién calculada, para obtener el resultado.

 
**Paso 1**: Para calcular la relación temporal, necesitamos comparar los valores de todos los salarios. Hacemos esta comparación calculando el producto cartesiano instructor × instructor y formando una selección para comparar el valor de cualquier par de salarios que aparezcan en una tupla. Primero, necesitamos idear un mecanismo para distinguir entre los dos atributos de salario. Usaremos la operación de renombrar para renombrar una referencia a la relación instructor; de esta manera, podemos hacer referencia a la relación dos veces sin ambigüedad.

Ahora podemos escribir la relación temporal que consiste en los salarios que no son los más grandes
$$ \Pi_{instructor.salary} \: (\sigma_{\text{instructor.salary < d.salary}} \: (instructor \times \rho_d \: (instructor))) $$
El resultado contiene todos los salarios *excepto el más grande*.

**Paso 2**: La consulta para encontrar el salario más grande en la universidad se puede escribir como:
$$ \Pi_{salary} \: (instructor) \: - $$
$$ \Pi_{instructor.salary} \: (\sigma_{\text{instructor.salary < d.salary}} \: (instructor \times \rho_d \: (instructor))) $$

# Definición formal del álgebra relacional

Una expresión básica en el álgebra relacional consiste en cualquiera de los siguientes

- Una relación en la base de datos
- Una relación constante, por ejemplo {(2222, Einstein, Physics, 95000), (76543, Singh, Finance, 80000)}

Una expresión general en el álgebra relacional es construido de pequeñas subexpresiones.  Sean $E_1$ y $E_2$ expresiones en el álgebra relacional, entonces las siguientes expresiones son todas expresiones de álgebra relacional

- $E_1 \cup  E_2$
- $E_1 - E_2$
- $E_1 \times  E_2$
- $\sigma_P \: (E_1)$, donde $P$ es un predicado sobre los atributos en $E_1$
- $\Pi_S \: (E_1)$, donde $S$ es una lista que consiste en algunos de los atributos en $E_1$
- $\rho_x \: (E_1)$, donde $x$ es el nuevo nombre para el resultado de $E_1$


# Operaciones adicionales de algebra relacional

## La operación intersección de conjuntos ($\cap$)
*Find the set of all courses taught in both the Fall 2009 and the Spring 2010 semesters*
$$ \Pi_{course\_id} \: (\sigma_{\text{semester = "Fall" } \land \text{ year = 2009}} \: (section)) \: \cap $$
$$ \Pi_{course\_id} \: (\sigma_{\text{semester = "Sptring" } \land \text{ year = 2010}} \: (section)) $$


## La operación natural-join ($\Join$)
La unión natural es una operación binaria que nos permite combinar ciertas selecciones y un producto cartesiano en una sola operación. La operación de unión natural forma un producto cartesiano de sus dos argumentos, **realiza una selección forzando la igualdad en aquellos atributos que aparecen en ambos esquemas de relación**, y finalmente elimina atributos duplicados.

Retomemos el ejemplo anterior de producto cartesiano: *Find the names of all instructors together with the course id of all courses they taught*
$$ \Pi_{\text{name, course\_id}} \: (instructor \Join teaches) $$

Como los esquemas para *instructor* y *teaches* **tienen el atributo *ID* en común**, la operación de unión natural considera solo pares de tuplas que tienen el mismo valor en ID. Combina cada par de tuplas de esta manera en una sola tupla en la unión de los dos esquemas; es decir, ($ID, name, dept\_name, salary, course\_id$)

Consideremos dos esquemas de relaciones $R$ y $S$, que son, por supuesto, listas de nombres de atributos. Si consideramos que los esquemas son conjuntos en lugar de listas, podemos denotar los nombres de atributos que aparecen en ambos $R$ y $S$ por $R \cap S$, análogamente para $R \cup S$, $R - S$. Ten en cuenta que las operaciones de unión, intersección y diferencia aquí se aplican a conjuntos de atributos, en lugar de relaciones.

Ahora estamos listos para una definición formal de la unión natural. Considera dos relaciones $r \: (R)$ y $s \:  (S)$. La unión natural de $r$ y $s$, denotada por $r \Join s$, es una relación en el esquema $R ∪ S$ definida formalmente de la siguiente manera:
$$ r \Join s = \Pi_{R \, \cup \, S} \: (\sigma_{r.A_1 \, = \, s.A_1 \: \land r.A_2 \, = \, s.A_2 \: \land \: ... \: \land r.A_n \, = \, s.A_n} \: (r \times s) ) $$
Donde $R \cap S = \{ A_1, A_2, ... A_n\}$

Consideremos otro ejemplo: *Find the names of all instructors in the Comp. Sci. department together with the course titles of all the courses that the instructors teach*

$$ \Pi_{\textit{name, title}} \: (\sigma_{\textit{dept\_name = "Comp. Sci"}} \: ( instructor \Join teaches \Join course)) $$

**La unión natural es asociativa** por lo cual $((instructor \Join teaches) \Join course)$  es lo mismo que $(instructor \Join (teaches \Join course))$ 

![[Pasted image 20240510164234.png]]
### La operación theta join ($\Join_{\theta}$)
Es una variante de la operación *natural join* que nos permite combinar una selección y un producto cartesiano en una única operación. Considera las relaciones $r\:(R)$ y $s\:(S)$ y sea $\theta$ un predicado sobre atributos en el esquema $R\cup S$. La operación *theta join* se define como
$$ r \Join_{\theta} s = \sigma_{\theta} \: (r \times s) $$
![[Pasted image 20240510164324.png]]

## La operación de asignación ($\leftarrow$)
La operación de asignación funciona de manera similar a la asignación en un lenguaje de programación. Para ilustrar esta operación, consideremos la definición de la operación de unión natural. Podríamos escribir $r \Join s$ como:
1. $temp1 \leftarrow R \times S$
2. $temp2 \leftarrow \sigma_{r.A_1 \, = \, s.A_1 \: \land r.A_2 \, = \, s.A_2 \: \land \: ... \: \land r.A_n \, = \, s.A_n} \: (temp1)$
3. $resultado = \Pi_{R \, \cup \, S} \: (temp2)$

**La evaluación de una asignación no resulta en la visualización de ninguna relación para el usuario.**


## Operaciones de unión externa (Outer join operations)
La operación de *outer join* funciona de manera similar a la operación de unión natural, pero preserva esas tuplas que se perderían en una unión creando tuplas en el resultado que contienen valores nulos. Existen 3 formas de la operación *outer join*.

### The left outer join  (⟕)
Toma todas las tuplas en la relación izquierda que no coinciden con ninguna tupla en la relación derecha, completa las tuplas con valores nulos para todos los demás atributos de la relación derecha, y las agrega al resultado de la unión natural. Toda la información de la relación izquierda está presente en el resultado de la *left outer join*.


Course

| course_ID | nombre        |
| --------- | ------------- |
| 2         | Base de datos |
| 5         | Concurrente   |

Instructor

| ID  | Nombre  |
| --- | ------- |
| 456 | Melchor |
| 356 | Yuri    |
| 756 |         |



| ID  | course_ID |
| --- | --------- |
| 456 | 2         |
| 356 | 1         |
|     |           |

Intructor ⟕ Teaches 

| Intructor.ID | Nombre  | Teaches.ID | course_ID |
| ------------ | ------- | ---------- | --------- |
| 456          | Melchor | 456        | 2         |
| 456          | Melchor | 356        | 1         |
| 356          | Yuri    | 356        | 1         |
| 356          | Yuri    | 456        | 2         |



### The right outer join (⟖)
Es simétrico con el *left outer join*: rellena las tuplas de la relación derecha que no coinciden con ninguna de la relación izquierda con nulos y las agrega al resultado de la unión natural. Por lo tanto, toda la información de la relación derecha está presente en el resultado del *right outer join*.

### Full outer join (⟗)
Realiza tanto las operaciones de *left outer join* como de *right outer join*, rellenando las tuplas de la relación izquierda que no coinciden con ninguna de la relación derecha, así como las tuplas de la relación derecha que no coinciden con ninguna de la relación izquierda, y las agrega al resultado de la unión.

## División
![[Pasted image 20240510173921.png]]
![[Pasted image 20240510173934.png]]
![[Pasted image 20240510174432.png]]


# Agregación
![[Pasted image 20240510174527.png]]
