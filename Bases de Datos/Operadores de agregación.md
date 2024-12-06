Los operadores de agregación son funciones que toman una colección de valores como entrada y retornan un valor simple.

**Comportamiento de un Operador de Agregación**
- **Opera** en una sola columna 
- **Retorna** un solo valor. 
- Usado solo en la lista *SELECT* y en la cláusula *HAVING*.
- Acepta
	- *DISTINCT*, considera solo valores distintos del argumento de la expresión.
	- *ALL*, considera todos los valores incluyendo todos los duplicados.

Ejemplo:
> SELECT COUNT (DISTINCT nombre_columna);

# Tipos de operadores de agregación

- *SUM* y *AVG*: opera solo en una colección de números.
- *MIN*, *MAX* y *COUNT*: opera sobre una colección de tipos de datos numéricos y no numéricos.

Cada función **elimina** valores *NULL* y opera sobre valores *No-NULL*.

![[Pasted image 20240514094321.png]]


| enum  | nombre | apellido | salario | posicion      | area |
| ----- | ------ | -------- | ------- | ------------- | ---- |
| SL100 | John   | White    | 30000   | Administrador | B3   |
| SL101 | Susan  | Brand    | 24000   |               |      |
| SL102 | David  | Ford     | 12000   |               |      |
| SL103 | Ann    | Beech    | 12000   |               |      |
| SL104 | Mary   | Howe     | 9000    |               |      |
## SUM
Retorna la suma de los valores en una columna específica.

Ejemplo: Recupere la suma total de los salarios de Administradores
