
Su objetivo es **asegurar la integridad de datos**. Para ello los SGBD ofrecen el mecanismo de **restricciones de integridad.
- Una restricción de integridad es una regla de consistencia de datos que está garantizada por mismo SGBD.
- Requiere ser probada cuando un registro es incluido, modificado o excluido de la base de datos.
- Las restricciones que cambios hechos en la base de datos por usuarios autorizados no resulten en pérdida de la consistencia de los datos.

## Restricciones de integridad básicas
Restricciones garantizadas por el SGBD (lo que implica que el programador no se preocupa por estas restricciones):
- Restricción de nulidad.
- Restricciones de dominio.
- Restricciones de clave primaria

Otras restricciones
- Restricciones de Check.
- Desencadenantes.
- Aserciones.

## Restricciones de integridad semántica.
Hay muchas restricciones de integridad que no encajan en las categorías básicas, estas restricciones reciben el nombre de **restricciones semánticas** o reglas de negocio.

**Ejemplos**:
- Un empleado del departamento "Legal" no puede tener la categoría funcional "Ingeniero".
- Un empleado no puede tener un salario mayor que su superior inmediato.

# Restricciones de valor nulo

- Hay columnas en las cuales **nos on admitidos valores nulos** llamadas columnas **obligatorias**.
- Hay columnas en las cuales **pueden aparecer valores vacíos** llamadas **columnas opcionales**.

**Ejemplo**:

| Matricula | Nombre | direccion |
| --------- | ------ | --------- |
| 548       |        | Av Life   |
| 549       | Pedro  | Av Death  |
- El cliente 548 no tiene nombre.
- Un cliente anónimo no tiene mucho sentido en la base de datos.
- Se desea prohibir los valores nulos. Para ello restringimos el dominio del atributo nombre por `not null`

- Hay columnas en las cuales **no son admitidos los valores nulos**, estas se llaman **columnas obligatorias**.
- Hay columnas en las que pueden aparecer **valores vacíos**, estas se llaman **columnas opcionales.
- Todas las columnas que componen la  [[Modelo Relacional#Clave primaria (Primary Key PK)|llave primaria]] **deben ser obligatorias*.
- Las demás llaves pueden contener columnas opcionales (Revisar esta afirmación).

## Ejemplo
Para este y los posteriores ejemplos crearemos una base de datos `restricciones`
```sql
create database restricciones
\c restricciones
```

Creamos una tabla y añadimos restricciones  `not null 
```sql
create table trabajador(
        codigo integer not null,
        nombre varchar(30) not null,
        telefono varchar(20)
);
```

- Intentamos insertar una tupla con el nombre vacío
```sql
insert into trabajador values(100, null, '997654321');
```
	Vemos que nos sale un error de violación not-null para el nombre

- Intentamos insertar una tupla con el código vacío
```sql
insert into trabajador values(100, null, '997654321');
```
	Obtenemos un error similar para el codigo

- Si insertamos una tupla con el código no vacío y el nombre no vacío tendremos un error similar. 
- Para una correcta inserción, los valores con restricciones `not-null` no deben estar vacías.


# Restricciones de dominio
El dominio de un atributo es el conjunto de valores que pueden aparecer en una columna. Se requiere que este conjunto de valores sean válidos para la columna.

- Las restricciones de dominio son las más elementales, estas son fácilmente verificadas por el sistema.
- **Ejemplo**: el atributo `edad` es numérico, requiere ser de dominio **entero** y no del tipo caracter, como el caso del atributo **nombre**.

```sql
create table trabajador(
        codigo integer not null,
        nombre varchar(30) not null,
        edad integer,
        telefono varchar(20)
);
```
- Si ingresamos un atributo que no corresponda al dominio definido en la tabla, tendremos un error de sintaxis.

# Restricciones de clave 

## Restricciones de clave primaria

- Restringe que cada fila de una tabla debe ser identificada por un valor único.
- Puede ser simple o compuesta.

**Ejemplo de llave simple**
```sql
create table medico(
	codigoM integer primary key,
	nombre varchar(80),
	direccion varchar(100)
);
```
O también:
```sql
create table medico(
	codigoM integer,
	nombre varchar(80),
	direccion varchar(100),
	primary key (codigoM)
);
```
Con cualquiera de las dos opciones el SGBD no nos permitirá ingresar un valor nulo en el atributo definido como llave primaria.

**Ejemplo de llave compuesta**
```sql
create table consulta(
	codigoMedico integer not null,
	codigoPaciente integer not null,
	fecha date not null,
	primary key (codigoMedico, codigoPaciente, fecha));
```

## Restricciones de clave candidata
Son restricciones `unique`, es decir, aseguran que los datos contenidos en una columna o un grupo de columnas es único en relación a todas las filas de la tabla.

> [!info]
> En PostgreSQL, la cláusula `UNIQUE` se utiliza en la definición de una tabla para especificar que una o más columnas deben contener valores únicos en todas las filas de la tabla. Esto significa que no puede haber duplicados en esas columnas dentro de la tabla.



Existen dos formas de hacer una restricción `unique`
```sql
create table producto (
	nroProducto integer unique,
	nombre varchar(30), 
	precio real
);
```
O también
```sql
create table producto (
	nroProducto integer,
	nombre varchar(30), 
	precio real,
	unique (nroProducto)
);
```

**Ejemplo**:
```sql
create table alumno(
	codIngreso varchar(5),
	seguroSoc varchar(4) unique,
	dni varchar(8) unique,
	nombre varchar(60),
	primary key (codIngreso)
	);
```
Al tratar de registrar dos tuplas en la tabla `alumno` si estas comparten el atributo `seguroSoc` o `dni` tendremos un error de restricción `unique constraint` .


# Restricciones de integridad referencial
Es la garantía de que un valor que aparece en una relación $R_1$, para un conjunto de atributos, debe obligatoriamente corresponder a valores de un conjunto de atributos en una relación $R_2$. Con esto, los valores de atributos que son una [[Modelo Relacional#Clave foránea (Foreign Key FK)|llave foránea]] en una relación $R_1$ posee valores correspondientes en **llaves primarias** de la tabla referenciada $R_2$.

**Ejemplos**:

```sql
create table ciudad(
	codigociudad integer not null primary key,
	descripcion varchar(35),
	departamento varchar(2)
);
```
Insertemos dos tuplas:
```
insert into ciudad values
(1, 'Huacho', 'LI'),
(2, 'Cañete', 'LI');
```

```sql
create table cliente(
	codigoCliente integer primary key,
	nombre varchar(80) not null,
	codciudad integer,
	foreign key(codciudad) references ciudad(codigociudad)
);
```
Si deseamos ingresar las tuplas `(548, 'Maria', 1)` y  `(549, 'Pedro', 5)` solo tendremos éxito con la primera, ya que la segunda viola una restricción de llave foránea al no existir un `codciudad` igual a 5.

La restricción de integridad es probada es tres casos.
- **Inclusión**. Si una tupla $t_2$ es insertada en una relación $r_2$, el sistema necesita asegurar que existe una tupla $t_1$ en una relación $r_1$ tal que $t_1[r_1=t_2[r_2]$
- **Exclusión**. Una llave primaria referenciada es **removida**: `on delete`.
- **Actualización**. Una llave primaria referenciada es modificada: `on update`.
### Acciones
- No permite actualización o exclusión, es decir, no permite la exclusión/alteración mientras haya dependencia. Por ejemplo, solo permitiría excluir una ciudad cuando ningún cliente referencie a esa ciudad.
- `SET DEFAULT`: si hubiera un valor default para la columna de la llave foránea, ella recibe este valor.
- `CASCADE`: propaga la exclusión/alteración.
- `SET NULL`: asigna el valor nulo.

### Inclusión
Al insertar un nuevo cliente, es necesario asegurar que el código de la ciudad en la tabla `cliente` exista en la tabla `ciudad`. Para asegurar esto, se crea la tabla de clientes con la llave foránea `codCiudad`.
Lo que hicimos líneas arriba:
```sql
create table cliente(
	codigoCliente integer primary key,
	nombre varchar(80) not null,
	codciudad integer,
	foreign key(codciudad) references ciudad(codigociudad)
);
```

### Exclusión
Al excluir una ciudad de la tabla ciudad el SGBD requiere asegurar que no exista ningún cliente en la tabla `cliente` referenciando a esta ciudad. Tenemos varias opciones:

- Fijar a nulo el código de la ciudad en la tabla `cliente`.
```sql
create table cliente(
	codigoCliente integer primary key,
	nombre varchar(80) not null,
	codciudad integer,
	foreign key(codciudad) references ciudad(codigociudad) on delete set null
);
```

- Asumir un valor `default`.
```sql
create table cliente(
	codigoCliente integer primary key,
	nombre varchar(80) not null,
	codciudad integer,
	foreign key(codciudad) references ciudad(codigociudad) on delete set default
);
```

- No permitir la exclusión de la ciudad 1 porque tiene clientes habitando en esta ciudad. La ciudad 3 puede ser excluida.
```sql
create table cliente(
	codigoCliente integer primary key,
	nombre varchar(80) not null,
	codciudad integer,
	foreign key(codciudad) references ciudad(codigociudad) on delete restrict
);
```

- Remueve las referencias (remueve la ciudad y todos los clientes de la ciudad)
```sql
create table cliente(
	codigoCliente integer primary key,
	nombre varchar(80) not null,
	codciudad integer,
	foreign key(codciudad) references ciudad(codigociudad) on delete cascade
);
```
Sin embargo, esto no esta permitido en este contexto: ya que al remover la ciudad, se estaría removiendo también el cliente.

>[!tip]
>`on delete cascade` es útil cuando se requiere que al eliminar un atributo, se desea que los items que lo referencian también sean removidos.


# Restricciones semánticas

## Check constraints

Por ejemplo
```sql
create table productos (
	producto_nro integer,
	nombre text,
	precio integer check (precio > 2)
);
```
Al ingresar, por ejemplo, la tupla `(1, 'teste', 0`, obtenemos un error `check constraint`.

Otro ejemplo:
```sql
create table productos (
producto_nro integer,
nombre text,
precio numeric check (precio > 2),
precio_descuento numeric check (precio_descuento > 0),
check (precio > precio_descuento)
);
```
Tendremos los mismos errores que en el ejemplo anterior si los valores de `precio` y `precio_descuento` no son mayores a 2 y a 0 respectivamente. Además existe una restricción que no permite que `precio_descuento` sea mayor o igual al precio del producto.

# Aplicación

## Dominio
Un dominio es un nuevo nombre para un tipo de datos. En un dominio también puede declararse un valor por omisión
