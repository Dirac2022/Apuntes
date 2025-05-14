La indexación hace que las columnas sean más rápidas de consultar al crear punteros a donde se almacenan los datos dentro de una base de datos.


Un índice es una estructura de datos que organiza los registros en disco para optimizar cierto tipo de operaciones de lectura. Un índice permite recuperar eficientemente todos los registros que satisfacen condiciones de búsqueda sobre los campos **clave de búsqueda** del índice.

- El uso de índices en las tablas mejora el tiempo de respuesta de la consulta, pues permiten que las consultas sean mejor procesadas.

- También pueden crearse índices adicionales sobre una colección de registros de datos dada, cada una con una clave de búsqueda diferente para acelerar las operaciones de búsqueda que no están soportadas eficientemente por la organización de archivo utilizada para almacenar los registros.

Hay dos tipos de índices de base de datos:
- Agrupado
- No agrupado.

# Índices agrupados
Los índices agrupados son el índice único por tabla que utiliza la **clave principal** para organizar los datos que se encuentran dentro de la tabla. El índice agrupado garantiza que la clave principal se almacene en orden creciente, que también es el orden en que la tabla se almacena en la memoria. Los índices agrupados deben declararse explícitamente en el caso de Postgres.

**Creación de índices agrupados**
El índice agrupado se creará automáticamente cuando se defina la clave principal:
```sql
create table amigos (
	id int primary key,
	apellidos varchar(50),
	nombres varchar(50),
	distrito varchar(50)
);
```
La tabla creada `amigos`, tendrá un índice agrupado creado automáticamente, organizado alrededor de la clave principal `id` llamada `amigos_pkey`

Al buscar en la tabla por `id`, el orden ascendente de la columna permite realizar búsquedas óptimas. Dado que los números están ordenados, la búsqueda puede navegar por el árbol B, lo que permite que las búsquedas se realicen en tiempo logarítmico.

Sin embargo, para buscar el `nombres` o el `distrito` en la tabla, tendríamos que mirar cada entrada porque estas columnas no tienen índice. Aquí es donde los índices no agrupados se vuelven muy útiles.

# Índices no agrupados
Los índices no agrupados son referencias ordenadas para un campo específico, de la tabla principal, que retienen los punteros a las entradas originales de la tabla. El primer ejemplo que mostramos es un ejemplo de una tabla no agrupada.

Se utilizan para aumentar la velocidad de las consultas en la tabla mediante la creación de columnas que se pueden buscar más fácilmente. Los analistas/desarrolladores de datos pueden crear índices no agrupados después de que se haya creado y llenado una tabla.

Los índices no agrupados apuntan a direcciones de memoria en lugar de almacenar datos en sí mismos. Esto los hace más lentos para consultar que los índices agrupados, pero generalmente mucho más rápidos que una columna no indexada.


# Creación de bases de datos no agrupadas (PostgreSQL)

## Índices parciales
Un índice parcial cubre solo un subconjunto de los datos de una tabla. Es un índice con una
cláusula WHERE. La idea es aumentar la eficiencia del índice reduciendo su tamaño. Un índice más pequeño requiere menos almacenamiento, es más fácil de mantener y es más rápido de escanear.

Por ejemplo, suponga que permite a los usuarios marcar comentarios en su sitio, lo que a su vez establece el booleano marcado como verdadero. A continuación, procesa los comentarios marcados por lotes. Es posible que desee crear un índice como este:
```sql
create index articulos_marcados on articulos (creados_en) where marcado is true;
```
Este índice seguirá siendo bastante pequeño y también se puede usar junto con otros índices en las consultas más complejas que lo requieran.

## Índices de expresión
Los índices de expresión son útiles para consultas que coinciden con alguna función o
modificación de sus datos. Postgres le permite indexar el resultado de esa función para que
las búsquedas sean tan eficientes como la búsqueda por valores de datos sin procesar. 

Por ejemplo, puede solicitar a los usuarios que almacenen sus direcciones de correo electrónico para iniciar sesión, pero desea una autenticación que no distinga entre mayúsculas y minúsculas. En ese caso, es posible almacenar la dirección de correo electrónico tal como está, pero realice búsquedas `WHERE LOWER(email) = 'correo minuscula'`. La única forma de usar un índice en una consulta de este tipo es con un índice de expresión como este:
```sql
create index usuarios_correo_minuscula on usuarios (lower(email));
```

Otro ejemplo común es para encontrar filas para una fecha determinada, donde hemos
almacenado marcas de tiempo en un campo de fecha y hora pero queremos encontrarlas por un valor de fecha emitido. Un índice como
```sql
create index articulos_dia on articulos (date(publicado_en));
```
puede ser usado por una consulta que contenga:
```sql
where date(articulos.publicados_en) = date('03-07-2021');
```


## Índices únicos
Un índice único garantiza que la tabla no tendrá más de una fila con el mismo valor. Es
ventajoso crear índices únicos por dos razones: la integridad de los datos y el rendimiento.
Las búsquedas en un índice único generalmente son muy rápidas.

En términos de integridad de datos, el uso de una validación de unicidad realmente no
garantiza la unicidad porque puede haber y habrá usuarios simultáneos que crean registros
no válidos. Por lo tanto, siempre debe crear la restricción en el nivel de la base de datos, ya
sea con un índice o una restricción única.

Hay poca distinción entre índices únicos y restricciones únicas. Los índices únicos se pueden
considerar como de nivel inferior, ya que los índices de expresión y los índices parciales no se pueden crear como restricciones únicas. Incluso son posibles índices únicos parciales en
expresiones.

## Índices de varias columnas
Si bien Postgres tiene la capacidad de crear índices de varias columnas, es importante
comprender cuándo tiene sentido hacerlo. El planificador de consultas de Postgres tiene la
capacidad de combinar y utilizar varios índices de una sola columna en una consulta de varias columnas mediante la realización de un escaneo de índice de mapa de bits. En general, puede crear un índice en cada columna que cubra las condiciones de consulta y, en la mayoría de los casos, Postgres lo utilizará, así que asegúrese de comparar y justificar la creación de un índice de varias columnas antes de crear uno. Como siempre, los índices tienen un costo, y los índices de varias columnas solo pueden optimizar las consultas que hacen referencia a las columnas del índice en el mismo orden, mientras que varios índices de una sola columna brindan mejoras de rendimiento a una mayor cantidad de consultas.

Sin embargo, hay casos en los que un índice de varias columnas claramente tiene sentido. Un índice en las columnas (a, b) puede ser usado por consultas que contienen ``WHERE a = x AND b = y``, o consultas que usan ``WHERE a = x`` solamente, pero no lo usará una consulta que use ``WHERE b = y``. Entonces, si esto coincide con los patrones de consulta de su aplicación, vale la pena considerar el enfoque de índice de varias columnas. También tenga en cuenta que, en este caso, crear un índice solo en a sería redundante.
# Beneficios
- Cuando una tabla no tiene índices, sus registros son desordenados y una consulta tendrá que recorrer todos los registros.
- El uso de índices puede aún ser todavía más valioso en consultas en las que involucran joins o múltiples tablas.
# Sintaxis
```sql
create [unique] index nombre_indice on tabla ([lista de atributos]);
```

Al crear claves primarias, automáticamente se crea un índice.
El parámetro `unique` hace que cada columna indexada solo acepte valores únicos. Sin embargo si la tabla ya tuviera valores duplicados en la columna deseada no será posible crear el índice como `unique`.

# Estructura de índices en PostgreSQL

## B-Tree
Son árboles de búsqueda balanceada desarrollados para trabajar en dispositivos de almacenamiento de acceso directo en memoria secundaria. El índice **B-Tree** es una implementación de los árboles **B** de alta concurrencia propuestas por *Lehman* y *Yao*.

## R-Tree
Utiliza el algoritmo de **partición cuadrática de Guttman**, es utilizada para indexar estructuras de datos multidimensionales cuya implementación está limitada a datos con hasta 8Kbytes, siendo bastante limitada para datos geográficos reales. Utilizado normalmente con datos del tipo box, circle, point y otros.

## Hash
Los índices Hash son estructuras de datos utilizadas para optimizar la velocidad de recuperación de datos en bases de datos. Funcionan muy bien para operaciones de búsqueda exacta, donde el objetivo es encontrar un valor específico.
### Ventajas de los Índices Hash
**Rápidos para Comparaciones de Igualdad**:
Cuando necesitas encontrar filas que coincidan exactamente con un valor específico, los índices Hash son muy eficientes. Por ejemplo: Si tienes una tabla de usuarios y quieres encontrar al usuario con un ID específico, un índice Hash puede localizar rápidamente la fila correspondiente.

### Limitaciones de los Índices Hash
**No Aptos para Consultas de Rango**:
Consultas de rango son aquellas que buscan valores dentro de un intervalo específico. Ejemplo: Encontrar todos los usuarios cuyo ID esté entre 100 y 200.   Los índices Hash no son adecuados para esto porque están diseñados para buscar valores exactos, no rangos. No tienen un orden natural que permita recorrer fácilmente un rango de valores.

**No Aptos para Operaciones de Clasificación**:
Las operaciones de clasificación (ordenamiento) requieren comparar y ordenar todos los valores en un índice.  Ejemplo: Ordenar una lista de usuarios por su nombre. Los índices Hash no pueden ayudar aquí porque no mantienen los datos en un orden secuencial. Simplemente permiten acceder rápidamente a un valor específico, sin proporcionar una forma eficiente de recorrer todos los valores en un orden determinado.

### Sintaxis
```sql
create index my_hash_index on my_table using hash (my_column);
```

El índice hash es una implementación de las dispersiones lineales de *Litwin*.
El la propia documentación de PostgerSQL está presente la nota:

> [!quote]
> “Las pruebas muestran que los índices hash del Postgres tiene un desempeño semejante
o más lento que los índices BTree y que el tamaño y el tiempo de construcción de
los índices hash son peores. Los índices hash también poseen un débil
desempeño sobre la alta concurrencia”.

## Gist
Los índices GIST (árbol de búsqueda generalizada) son realmente versátiles y le permiten crear árboles de búsqueda personalizados según sus necesidades específicas. Son excelentes cuando se trata de tipos de datos geométricos  y de texto.


## GIN
Índice invertido generalizado. Si esta trabajando con valores compuestos donde los elementos dentro de estos valores deben buscarse con frecuencia, los índices GIN podrían ser justo lo que necesita.
Son útiles cuando un índice debe asignar muchos valores a una fila. Los GIN son buenos para indexar valores de arrays, así como para implementar búsquedas de texto completo.


# Indexación en PostgreSQL

```sql
create index nombre_indice on nombre_tabla (columna_nombre);
```

De forma predeterminada, al crear un índice en PostgreSQL, si no se especifica su tipo, utiliza la estructura B-Tree. Sin embargo, puede ser que elija otro tipo, dependiendo de los operadores de comparación inmersos:


| Tipo   | Operadores                |
| ------ | ------------------------- |
| B-Tree | <, <=, =, >=, >           |
| R-Tree | <<, &<, &>, >>, @, ~=, && |
| Hash   | =                         |
Para escoger el tipo de índice se debe añadir al final de comando la palabra `using`, especificando el tipo deseado:
- `create index nombre on tabla using hash (columna)`;
- `create index nombre on tabla using btree (columna)`;
- `create index nombre on tabla using rtree (columna)`;
- `create index nombre on tabla using gist (columna)`;

Cuando se utiliza más de una columna, el índice se organiza de acuerdo con la primera columna especificada en la declaración, siendo la segunda utilizada solo cuando la primera columna tiene varios valores iguales. Por lo tanto, la segunda columna se utiliza como una segunda opción de clasificación.

```sql
create index columna1_columna2_tabla_idx on tabla (columna1, columna2);
```

Cuando se utilizan varias columnas en un índice, el optimizador de consultas puede utilizar todas las columnas especificadas o solo una o algunas, de acuerdo con su decisión. Esto dependerá de si las columnas son consecutivas.

Por ejemplo, un índice que incluye (col_1, col_2, col_3) se puede utilizar en consultas que involucran col_1, col_2 y col_3, o en consultas que involucran col_1 y col_2, o en consultas que implican solo col_1, pero no en otras combinaciones. (En un a consulta que implica col_1y  col_3, el optimizador puede decidir utilizar un índice para solo col_1, tratando a col_3 como una columna común, no indexada).

**Ejemplo**. Dada la creación del índice:
```sql
create index anio_credito_cliente_idx on clientes using btree (anio_nac, credito);
```

Considere las consultas siguientes:
```sql
select nombre from clientes where anio_nac > 1973 and credito < 1750;

select nombre from clientes where anio_nac > 1973 or credito < 1750;
```

En el ejemplo, solo la primera consulta utiliza el índice. Por definición, PostgreSQL utiliza solo el índice  con más de una columna cuando las columnas se unen en una cláusula `where` por `and`, en otros casos el índice se utilizará solo en la columna que se estableció por primera vez en la creación del índice.

**Ejemplo**. Dada la creación del índice:
```sql
create index anio_credito_cliente_idx on clientes using btree (anio_nac, credito);
```

Considere las consultas siguientes:
```sql
select nombre from clientes where anio_nac > 1973 and credito 1750;

select nombre from clientes where anio_nac > 1973 or credito < 1750;
```

En la segunda consulta, el índice `anio_credito_cliente_idx` se utilizará solo en la búsqueda de los clientes nacidos después de 1973, por se `anio_nac` su columna principal.

El comando:
```sql
select * from pg_stat_all_indexes;
```
trae información sobre los índices contenidos en la base de datos, así como el número total de exploraciones que utilizó un determinado índice y el número de líneas leídas por el índice.

El comando
```sql
select * from pg_indexes where schemaname = 'public';
```
contiene la información sobre todos los índices en la base de datos.

- La indexación es una herramienta importante para el aumento del desempeño de las consultas.
- Use indexación como la primera alternativa para obtener una ganancia de rendimiento y luego evaluar que otras técnicas pueden ser útiles.
- Cuando una consulta tarda en completarse, normalmente las tablas implicadas no tienen índices o se han creado incorrectamente. La adecuación o creación de los índices necesarios resuelve el problema en la gran mayoría de las veces.



# Activar tiempo de consulta
De forma predeterminada el tiempo de los resultados de la consulta no está disponible, pero podemos activarlo usando el siguiente comando: `\timing` .Esto mostrará el tiempo de consulta en milisegundos. Puede usar `\timing` solo con el cliente de línea de comandos psql, ya que este es un comando psql.  Es un interruptor que activa o desactiva el tiempo de ejecución de informes.

# Plan de ejecución en PostgreSQL
Postgres tiene una gran capacidad para mostrarle como ejecutará una consulta. Esto se conoce como  un **plan de ejecución** y se utiliza el comando `explain`.

Comprender esto le dice cómo puede optimizar su base de datos con índices para mejorar el rendimiento. La parte difícil para la mayoría de los usuarios es comprender el resultado de estos.

Comúnmente, `explain` se ejecuta en las instrucciones `select`. Sin embargo, también puede usarlo en:
```sql
insert / update / delete / execute /  declare
```

**Usando explain**
Dada una consulta:
```sql
select las_name from employees where salary >= 50000;
```

Podemos inspeccionar cómo Postgres lo ejecutará con:
```sql
explain select last_name from employees where salary >= 50000;
```

Podemos ejecutar la consulta e inspeccionar la ruta / tiempo que tomó con:
```sql
explain analyze select last_name from employees where salary >= 50000;
```

# Como crear un índice en PostgreSQL - Guía

Los índices ayudan a acelerar la recuperación de datos al proporcionar rutas rápidas hacia las filas necesarias. Por ejemplo
```sql
create index idx_name on tbl_employee (name);
```
En este caso, hemos creado un índice llamado `idx_name` en la columna de nombre de nuestra tabla `tbl_employee`. ==Esto significa que cualquier consulta de búsqueda futura relacionada con los nombre de los empleados ahora será más rápida de nunca==.

Sin embargo, no es beneficioso usar en exceso los índices, ya que pueden ralentizar ligeramente las operaciones de escritura.

> [!info]
> La mejor práctica suele ser indexar columnas que los usuarios buscan u ordenan con frecuencia.

Uso incorrecto
```sql
create index idx_wrong on tbl_employee (*);
```

Uso correcto:
```sql
create index idx_right on tbl_employee (frequent_column);
```

La importancia de los índices en PostgreSQL radica en su capacidad para aumentar drásticamente el rendimiento de las consultas.

## Mejores prácticas para usar índices en PostgreSQL
>[!Tip]
>Un índice no siempre es la solución.

La indexación excesiva puede ralentizar sus operaciones, especialmente aquellas que involucran modificación de datos como **actualizar** e **insertar**.

Por ejemplo
```sql
create index idx_name on table_name (column_name)
```
Si `column_name` rara vez aparece en su cláusula `where` o no participa con frecuencia en operaciones `join`, dicho índice podría ser excesivo.

También es importante elegir el tipo correcto de índice. PostgreSQL ofrece varios tipos de índices, incluidos B-Tree, Hash, GiST, SP-GiST y GIN. Cada uno con sus propias fortalezas y debilidades.
- B-Tree es perfecto para manejar consultas de igualdad y rango.
- GIN se adapta a los casos en los que existen varios valores en una sola columna.

Por último: ¡mantenga sus índices ajustados! Evite indexar columnas innecesarias. En su lugar, céntrese en las columnas ordenadas o buscadas con frecuencia.

Algunos errores al utilizar indices:
- **Sobreindexación**: demasiados índices pueden ralentizar las modificaciones de datos.
- **Subindexación**: no tener suficientes índices podría llevar a escaneos completos de la tabla, lo que perjudica el rendimiento.
- **Tipo de índice incorrecto**: no todos los índices se crean de la misma manera. Elegir el tipo incorrecto para sus datos y consultas puede generar operaciones ineficientes.


## Cuando usar índices
Los índices están destinados a acelerar el rendimiento de una base de datos, así que use la
indexación siempre que mejore significativamente el rendimiento de su base de datos. A
medida que su base de datos se vuelve más y más grande, es más probable que vea los
beneficios de la indexación.

## Cuando no usar índices
Cuando los datos se escriben en la base de datos, la tabla original (el índice agrupado) se
actualiza primero y luego se actualizan todos los índices fuera de esa tabla. Cada vez que se
realiza una escritura en la base de datos, los índices no se pueden utilizar hasta que se hayan actualizado. Si la base de datos recibe escrituras constantemente, los índices nunca se podrán utilizar. Esta es la razón por la que los índices generalmente se aplican a las bases de datos en los almacenes de datos que obtienen nuevos datos actualizados de forma programada (horas de menor actividad) y no a las bases de datos de producción que pueden recibir nuevas escrituras todo el tiempo.

# Pruebas de rendimiento del índice
Para probar si los índices comenzarán a disminuir los tiempos de consulta, puede ejecutar un conjunto de consultas en su base de datos, registrar el tiempo que tardan en finalizar esas consultas y luego comenzar a crear índices y volver a ejecutar sus pruebas.

Para hace esto, intente usar la clausula `explain analyze` en PostgreSQL:
```sql
explain analyze select * from amigos where nombres='Iris';
```
Este resultado le indicará qué método de búsqueda del plan de consulta se eligió y cuánto tiempo tomó la planificación y ejecución de la consulta.

**Para eliminar un índice** use el comando `drop index`
```sql
drop index amigos_nombres_asc;
```