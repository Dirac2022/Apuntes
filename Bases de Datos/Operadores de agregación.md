Los operadores de agregación son funciones que toman una colección de valores como entrada y retornan un valor simple.

**Comportamiento de un Operador de Agregación**
- **Opera** en una sola columna 
- **Retorna** un solo valor. 
- Usado solo en la lista `SELECT` y en la cláusula `HAVING`.
- Acepta
	- ``DISTINCT``, considera solo valores distintos del argumento de la expresión.
	- ``ALL``, considera todos los valores incluyendo todos los duplicados.

Ejemplo:

```SQL
select count(distinct nombre_columna);
```
# Tipos de operadores de agregación

- ``SUM`` y ``AVG``: opera solo en una colección de números.
- ``MIN``, ``MAX`` y ``COUNT``: opera sobre una colección de tipos de datos numéricos y no numéricos.

Cada función **elimina** valores *NULL* y opera sobre valores *No-NULL*.



### Tabla ``empleado``

| numEmp | nombre | apellido | salario  | posicion           |
| ------ | ------ | -------- | -------- | ------------------ |
| SL100  | John   | White    | 30000.00 | Administrador      |
| SL101  | Susan  | Brand    | 24000.00 | Administrador      |
| SL102  | David  | Ford     | 12000.00 | Gestor de Proyecto |
| SL103  | Ann    | Beech    | 12000.00 | Gestor de Proyecto |
| SL104  | Mary   | Howe     | 9000.00  | Gestor de Proyecto |

## ``SUM()``
Retorna la suma de los valores en una columna específica.
**Ejemplo:** Recupere la suma total de los salarios de Administradores [[#Tabla ``empleado``|empleado]]
```sql
select sum(salario) as sum_salario
from empleado
where empleado.posicion = 'Administrador';
```

| sum_salario |
| ----------- |
| 54000.00    |

## `AVG()`
Retorna el promedio de los valores en una column especifica.
**Ejemplo:** Obtenga el promedio del salario de los gestores del proyecto. [[#Tabla ``empleado``|empleado]]
```sql
select avg(distinct salario) as media_salario
from empleado
where empleado.posicion='Gestor del Proyecto';
```

| media_salario |
| ------------- |
| 10500.00      |
**Al usar ``distinct`` no se toman en cuenta los salarios duplicados**


## ``MIN()``  y ``MAX()``
Retorna el valor más pequeño y más grande de una columna.
**Ejemplo:** Obtenga el salario mínimo y máximo de los empleados. [[#Tabla ``empleado``|empleado]]
```sql
select min(salario) as salario_min, max(salario) as salario_max
from empleado;
```

| salario_min | salario_max |
| ----------- | ----------- |
| 9000.00     | 30000.00    |
## ``COUNT()``
Retorna el numero de valores en la columna especificada
**Ejemplo:** Contabilice el numero de empleados que son Administradores [[#Tabla ``empleado``|empleado]]

```sql
select count(numEmp) as cuenta_numEmp
from empleado
where empleado.posicion='Administrador';
```

| cuenta_numEmp |
| ------------- |
| 2             |

## Uso de COUNT() y SUM()
**Ejemplo:** Halla el número total de Administrador y la suma de sus salarios. [[#Tabla ``empleado``|empleado]]
```sql
select count(numEmp) as cont_emp, sum(salario) as suma_salario
from empleado
where empleado.posicion='Administrador';
```

| cont_emp | suma_salario |
| -------- | ------------ |
| 2        | 54000.00     |

## ``COUNT(*)``
No hay entrada para esta función. Retorna todas las filas de una tabla, independientemente de si se producen valores nulos o duplicados. [[#Tabla ``empleado``|empleado]]

**Ejemplo:** ¿Cuántos Gestores de Proyecto tienen salario superior a 9000.00?
```sql
select count(*) as cuenta_salarioGP
from empleado.posicion='Gestor de Proyecto' and empleado.salario > 9000.00
```

| cuenta_salarioGP |
| ---------------- |
| 2                |

# Uso de operadores de agregación

### Tabla ``empleado``

| area | numEmp | nombre | apellido | salario  | posicion           |
| ---- | ------ | ------ | -------- | -------- | ------------------ |
| B3   | SL100  | John   | White    | 30000.00 | Administrador      |
| B5   | SL101  | Susan  | Brand    | 24000.00 | Administrador      |
| B3   | SL102  | David  | Ford     | 12000.00 | Gestor de Proyecto |
| B5   | SL103  | Ann    | Beech    | 12000.00 | Gestor de Proyecto |
| B7   | SL104  | Mary   | Howe     | 9000.00  | Gestor de Proyecto |

## GROUP BY
Agrupa los datos de la tabla en una consulta `select` y produce una única fila de resumen para cada grupo.

**Cuando usar `GROUP BY`**:
1. Cada elemento de la lista `SELECT` debe tener un solo valor por grupo.
2. La cláusula `SELECT` solo puede contener:
	- Nombres de Columnas
	- Operador de Agregación
	- Constante
	- Una expresión que contiene combinaciones de las anteriores
3. Todos los nombres de columna en la lista `SELECT` deben aparecer en la cláusula `GROUP BY` a menos que el nombre se use sólo en la función agregada.

**Ejemplo:** Encuentre el número de empleados que trabajan en cada área y la suman de sus salarios. [[#Uso de operadores de agregación#Tabla ``empleado``|empleado]] 
```sql
select area, count(numEmp) as cuenta, sum(salario) as suma
from empleado
group by area
order by area;
```

| area | cuenta | suma     |
| ---- | ------ | -------- |
| B3   | 2      | 42000.00 |
| B5   | 2      | 36000.00 |
| B7   | 1      | 9000.00  |

## HAVING
Esta diseñada para ser usada con `GROUP BY` de tal forma que puedan restringir los grupos que aparecen en la tabla resultado final.

**Ejemplo:** Para cada área con más de un empleado, hallar la cantidad de empleados que trabajan en cada área así como la suma de sus salarios. [[#Uso de operadores de agregación#Tabla ``empleado``|empleado]] 

```sql
select area, count(numEmp) as cuenta, sum(salario) as suma
from empleado
group by area
having count(numEmp) > 1
order by area;
```

Tabla resultado después de realizar la cláusula `GROUP BY` area.

| area | count | sum      |
| ---- | ----- | -------- |
| B3   | 2     | 42000.00 |
| B5   | 2     | 36000.00 |
| B7   | 1     | 9000.00  |

Tabla resultado final luego de realizar `HAVING COUNT(numEmp) > 1 ORDER BY area;`

| area | count | sum      |
| ---- | ----- | -------- |
| B3   | 2     | 42000.00 |
| B5   | 2     | 36000.00 |
