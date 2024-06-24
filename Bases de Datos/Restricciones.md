

# Restricciones de valor nulo

- Hay columnas en las cuales **nos on admitidos valores nulos** llamadas columnas **obligatorias**.
- Hay columnas en las cuales **pueden aparecer valores vacíos** llamadas **columnas opcionales**.

## Ejemplo

Creamos una tabla y añadimos restricciones not null
```
postgres=# \c bdconstraints
You are now connected to database "bdconstraints" as user "postgres".
bdconstraints=# 
bdconstraints=# create table trabajador(
        codigo integer not null,
        nombre varchar(30) not null,
        telefono varchar(20)
);
```


- Intentamos insertar una tupla con el nombre vacío
- Intentamos insertar una tupla con el código vacío
```
bdconstraints=# insert into trabajador values(100, null, '997654321');
ERROR:  null value in column "nombre" of relation "trabajador" violates not-null constraint
DETAIL:  Failing row contains (100, null, 997654321).
bdconstraints=# insert into trabajador values(null, 'Juan Perez', '997654321');
ERROR:  null value in column "codigo" of relation "trabajador" violates not-null constraint
DETAIL:  Failing row contains (null, Juan Perez, 997654321).

bdconstraints=# select * from trabajador;
 codigo | nombre | telefono 
--------+--------+----------
(0 rows)
```

Insertamos una tupla con el código no vacío y el nombre no vacío
```
bdconstraints=# insert into trabajador values(120, 'Juan Perez', '997654321');
INSERT 0 1
bdconstraints=# select * from trabajador;
 codigo |   nombre   | telefono  
--------+------------+-----------
    120 | Juan Perez | 997654321
(1 row)

```


# Restricciones de dominio
Se refiere al dominio de un atributo


# Restricciones de clave 


## Restricciones de clave primaria

- Restringe que cada fila de una tabla debe ser identificada por un valor único.
- Puede ser simple o compuesta.


## Restricciones de clave candidata
Restricciones *Unique* aseguran que los datos contenidos en una columna o un grupo de columnas es único en relación a todas las filas de la tabla.

### Clausula unique
En PostgreSQL, la cláusula `UNIQUE` se utiliza en la definición de una tabla para especificar que una o más columnas deben contener valores únicos en todas las filas de la tabla. Esto significa que no puede haber duplicados en esas columnas dentro de la tabla.


# Restricciones de integridad referencial

Es la garantía de que un valor que aparece en una relación $R1$



# Restricciones semánticas

## Check constraints





# Aplicacion

## Dominio
Un dominio es un nuevo nombre para un tipo de datos. En un dominio también puede declararse un valor por omisión
