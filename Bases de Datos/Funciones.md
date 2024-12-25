
# Requisitos
`create function` requiere la siguiente información
- Nombre de la función
- Número de argumentos de la función
- Tipo de datos de cada argumento
- Tipo de retorno de la función
- Acción de la función
- Lenguaje usado por la función acción

# Sintaxis

```
create [or replace] function Nombre ([parametros])
	returns tipo_retorno as delimitador
	instruction1;
	...
	instructionN;
	delimitador LANGUAGE nombre_lenguaje;
```


>[!warning]
>Solo es posible sobre escribir una función si el tipo de retorno es el mismo que el original. 


# Funciones SQL
- Las funciones SQL le permiten nombrar las consultas y almacenarlas en la base de datos para su posterior acceso.
- Ejecutan una lista de instrucciones SQL y devuelven el resultado de la última consulta de esa lista.
- En el caso simple, la primera fila de la última consulta será el valor de retorno. Si la última consulta no retorna ninguna fila, se devolverá un valor `NULL`

## Eliminación de funciones
Permite eliminar una función:
```sql
drop function nombre_funcion();
```

## Funciones de retorno No Nulo
Las funciones pueden retornar una tupla o un conjunto de tuplas. En los casos en que el retorno no es un conjunto, la primera fila del resultado de la última consulta pasa a ser el retorno de la función, así tenga más filas.

### Ejemplo
Elabore una función que retorne la unión de dos cadenas
```plsql
create function concatena (text, text)
	return text as $$
		select $1 || ' ' || $2
$$ language SQL;
```
#### Ejecución
```
select concatena('hola', 'mundo');
```
#### Explicación
   - `CREATE FUNCTION`: Esta cláusula indica que estamos creando una nueva función.
   - `concatena`: Este es el nombre de la función. Puedes llamarla como prefieras.
   - `(text, text)`: Estos son los parámetros que la función acepta. En este caso, la función toma dos argumentos de tipo `text`.
   - `RETURNS text`: Esto especifica que la función devolverá un valor de tipo `text`.
   - `AS $$ ... $$`: Esta parte encierra el cuerpo de la función. Todo lo que está entre los delimitadores `$$` es el cuerpo de la función.
   - `SELECT $1 || ' ' || $2`: Esta es la instrucción SQL que se ejecutará cuando se llame a la función.
   - `$1` y `$2`: Representan los parámetros de entrada de la función. `$1` es el primer parámetro y `$2` es el segundo.
   - `||`: Es el operador de concatenación en SQL.
- `' '` (espacio): Es un espacio en blanco que se coloca entre los dos textos concatenados.
   - `LANGUAGE SQL`: Esto indica que el cuerpo de la función está escrito en SQL. 


> [!tip]
> En SQL, el operador `||` se utiliza para concatenar cadenas de texto. Cuando se usan dos o más cadenas con el operador `||`, se unen para formar una sola cadena.

### Ejemplo
```plsql
create function IGV (numeric)
	returns numeric as $$
		select ($1 * 0.18 :: numeric(8, 2) :: numeric(8,2));
$$ language SQL;
```

#### Ejecución
```sql
select IGV(100);
```

#### Explicación
Vamos a revisar y explicar la función `IGV` en SQL paso a paso. También corregiremos cualquier posible error que pueda tener.
  - `$1` se refiere al primer y único parámetro de la función.
  - `0.18` es la tasa del IGV.
  - `:: numeric(8, 2)` está intentando convertir el resultado a un tipo de dato `numeric` con una precisión de 8 dígitos y 2 decimales.

### Aplicación

```plsql
create table repuestos (
	id int,
	nombre varchar(60),
	costo numeric(8, 2),
	peso float
);
```


| id  | nombre   | costo | peso |
| --- | -------- | ----- | ---- |
| 637 | Cable    | 14.29 | 5    |
| 638 | Martillo | 25.46 | 8    |
| 639 | Focos    | 7.35  | 32   |
```sql
select id, nombre, costo, IGV(costo), costo + IGV as total
from repuestos
order by id;
```

```plsql
create function cargo(numeric)
	returns numeric as $$
		select case
			when $1 < 2 then cast (3.00 as numeric(8, 2))
			when $1 >= 2 and 1 < 4 then cast (5.00 as numeric(8, 2))
			when $1 >= 4 then cast (6.00 as numeric(8, 2))
		end;
	$$
	language SQL;
```

#### Ejecución

```plsql
select id, nombre, costo, IGV(costo), costo + IGV(costo) as subtotal, cargo(peso), costo+IGV(costo)+cargo(peso) as total
from repuestos
order by id;
```

## Funciones que retornan conjuntos
- Aunque la mayoría de funciones retornan un único valor, las funciones SQL pueden retornar múltiples valores usando `SETOF.

- Se debe especificar el retorno como ``SETOF tipo``, donde tipo puede ser una tabla. Luego, se devolverán todas las filas del resultado.

- Las acciones de la función pueden también contener ``INSERT``, ``UPDATE`` y ``DELETE`` así como múltiples consultas separadas por puntos y coma.

### Ejemplo
Elabore una función que demuestre el uso de `SETOF`

```plsql
create function prueba (text)
	returns setof empleados as $$
		select * from empleados
		where dept = $1
$$ language SQL;
```

#### Ejecución
```sql
select nombre from prueba('TA');
```

#### Explicación
- `RETURNS SETOF empleados` Esta línea especifica que la función devolverá un conjunto de registros (filas) de la tabla `empleados`. Esto significa que la función puede devolver múltiples filas, no solo un único valor.
- `SELECT * FROM empleados`: Selecciona todas las columnas de la tabla `empleados`.
- `WHERE dept = $1`: Filtra las filas para que solo se devuelvan aquellas donde la columna `dept` (departamento) coincide con el valor del primer parámetro de la función `$1`.


> [!tip]
> La ultima declaración de una función debe ser un `select`, la cual servirá como retorno, a menos que su retorno sea declarado del tipo `void`.

### Ejemplo
Suponga que se tiene la tabla `empleado` con el esquema;
```
empleado = (codemp, nombres, apellidos, salario)
```

Elabore una función para eliminar a los empleados con salario negativo.

```plsql
create function eliminaEmp()
	returns void as $$
		delete from empleado
		where salario < 0;
$$ language SQL;
```

#### Ejecución
```plsql
select eliminaEmp();
```

### Ejemplo
Suponga que se tiene la tabla `cuentas` cuyo esquema es:
```
cuentas = (nrocuenta, saldo)
```
Elabore una función que permita realizar un retiro de una cuenta.
```plsql
create function retiro(integer, numeric)
	returns numeric as $$
		update cuenta
		set saldo = saldo - $2
		where nrocuenta = $1;
		select saldo from cuenta
		where nrocuenta = $1;
$$ language SQL;
```

#### Ejecución
```sql
select retiro(35, 1000.0)
```

#### Explicación
- La función `retiro` primero actualiza el saldo de la cuenta restando el monto especificado (`$2`).
- Luego, selecciona y devuelve el nuevo saldo actualizado después del retiro.

## Funciones con parámetros del tipo OUT

### Ejemplo
Calcula la suma de dos números enteros y devuelve el resultado como un parámetro de salida. 
```plsql
create function una_salida(in x int, in y int, out suma int)
as $$
select $1 + $2;
$$ language SQL;
```

#### Explicación
- `in x int, in y int`: Son parámetros de entrada (`x` e `y`) de tipo entero (`int`).
- `out suma int`: Es el parámetro de salida (`suma`), que también es de tipo entero (`int`) y contendrá el resultado de la suma.
- `select $1 + $2;`: Realiza la operación de suma entre los parámetros de entrada `$1` y `$2`.
- `$1` y `$2` corresponden a los primeros y segundos parámetros de entrada (`x` e `y`, respectivamente).

#### Ejecución
```plsql
select una_salida(3, 7);
```

### Ejemplo
Calcula tanto la suma como el producto de dos números enteros
```plsql
create function dos_salidas(x int, y int, out s int, out p int)
as $$
select $1 + $2, $1 * $2;
$$ language SQL;
```

#### Explicación
- `x int, y int`: Son parámetros de entrada (`x` e `y`) de tipo entero (`int`).
- `out s int, out p int`: Son parámetros de salida (`s` y `p`), también de tipo entero (`int`), que contendrán la suma (`s`) y el producto (`p`) de `x` e `y`.
- No es necesario usar explícitamente `in` en los parámetros de ingreso.
- `select $1 + $2, $1 * $2;`: Realiza dos operaciones en una sola consulta SQL.
	- `$1 + $2`: Calcula la suma de los parámetros de entrada (`x` e `y`).
	- `$1 * $2`: Calcula el producto de los parámetros de entrada (`x` e `y`).

#### Ejecución
```sql
select dos_salidas(11, 42);
```



# Funciones en PL/pgSQL
Las funciones en lenguajes procedurales en PostgreSQL, como el PL / pgSQL corresponden a lo que comúnmente se conoce como Stored Procedures.

De forma predeterminada, PostgreSQL sólo trae soporte para funciones en el lenguaje SQL.

El PL / pgSQL es el lenguaje de procedimientos almacenados más utilizado en PostgreSQL, por ser más maduro y con más recursos.

PL / pgSQL es otro lenguaje destinado a funciones de servidor. Este es un verdadero lenguaje de programación.

Mientras que las funciones de SQL permiten solo sustituir argumentos, PL / pgSQL incluye características tales como variables, evaluación condicional y bucles.

## Características
Alguna de las características del PL / pgSQL
- **DECLARE**: Define variables que se usarán en la función.
- **SELECT INTO**: Es una forma especial de ``SELECT`` que permite que los resultados de la consulta sean almacenados en variables. No debería confundirse con la instrucción ``SELECT * INTO``
- **RETURN**: Termina y devuelve un valor desde la función.

### Ejemplo
Función que retorna la suma de los parámetros de entrada
```plsql
create or replace function sumar(int, int)
returns int as $$
declare
	i alias for $1;
	j alias fro $2;
	s int
begin
	s := i + j;
	return s;
end
$$ language plpgsql;
```

#### Explicación
- `create or replace function sumar(int, int)`: Esta línea declara la función `sumar`, que toma dos parámetros de tipo entero.
- `return int`: Especifica que la función retornará un valor de tipo entero.
- `as $$`: Aquí comienza el bloque de código de la función, delimitado por `$$`
- `declare`: Esta sección es opcional y se usa para declarar variables locales que se utilizarán dentro del cuerpo de la función.
- `i alias for $1;`: Declara la variable `i` como un alias para el primer parámetro de la función (`$1`).
- `j alias for $2;`: Declara la variable `j` como un alias para el segundo parámetro de la función (`$2`).
- `s int;`: Declara una variable `s` de tipo entero.
- `begin`: Indica el inicio del bloque de código ejecutable de la función.
- `s := i + j;`: Asigna a la variable `s` la suma de `i` y `j`.
- `return s;`: Retorna el valor de `s`, que es la suma de los dos parámetros de entrada.
- `end`: Finaliza el bloque de código de la función.
- `$$`: Finaliza el bloque de código de la función.
- `language plpgsql;`: Especifica que el lenguaje utilizado para definir esta función es PL/pgSQL.

#### Ejecución
```
select sumar(23, 19);
```

## Estructura If
### If Else
```plsql
if boolean-expression then
	statements
else
	statements
end if
```

### If Anidado
```plsql
if boolean-expression then
	statements
[ elseif boolean-expression then
	statements
[ elseif boolean-expression the
	statements ...]]
[ else
	statements]
end if;
```

### Ejemplo
```plsql
create or replace function par (i int)
returns boolean as $$
declare
	temp int;
begin
	temp := i % 2;
	if temp=0 then return true;
	else return false;
	end if;
end;
$$ language plpgsql;
```

#### Ejecución
```sql
select par(23), par(18);
```


## Estructuras repetitivas

### For
```
for name in [reverse] expression ... expression [by expression] loop
	statements
end loop[label];
```

### Clausulas
```
exit [label] [when boolean-expression];
continua [label] [when boolean-expression];
```


### Ejemplo
```plsql
create or replace function factorial(i numeric)
returns numeric as $$
declare
	i int;
	f numeric;
begin
	f := 1;
	for i in 1..i loop
		f = f*i;
	end loop;
	return f;
end;
$$ language plpgsql;
```
==este código esta mal==
#### Explicación
- `declare`: Esta sección es opcional y se usa para declarar variables locales que se utilizarán dentro del cuerpo de la función.
- `i int;`: Declara una variable `i` de tipo entero. Sin embargo, hay un conflicto con el parámetro `i` que se pasa a la función.
- `f numeric;`: Declara una variable `f` de tipo numérico.
- `begin`: Indica el inicio del bloque de código ejecutable de la función.
- `f := 1;`: Inicializa la variable `f` con el valor 1.
- `for i in 1..i loop`: Aquí hay un error lógico, ya que el parámetro `i` es redefinido dentro del bucle. Debería ser `for i in 1..$1 loop` para evitar el conflicto.
    - `for i in 1..$1 loop`: Itera desde 1 hasta el valor del parámetro `i`.
- `f := f * i;`: Multiplica el valor actual de `f` por `i` en cada iteración.
- `end loop;`: Termina el bucle.
- `return f;`: Retorna el valor de `f`, que contiene el factorial del número.
- `end;`: Finaliza el bloque de código de la función.

## Estructuras repetitivas
### Loop
```
loop
	statements
end loop;
```


### While
```
while boolean-expression loop
	statements
end loop;
```

### Ejemplo
```plsql
create or replace function factorialb(n numeric)
returns numeric as $$
declare
	i int;
	f numeric;
begin
	i := 1;
	f := 1;
	while i <= n loop
		f := f * i;
		i := i + 1;
	end loop;
	return f;
end;
$$ language plpgsql;
```

#### Ejecución
```plsql
select factorialb(6);
```

## Recursividad
### Ejemplo
```plsql
create or replace function factorialc(n numeric)
returns numeric as $$
declare
	i int;
	f numeric;
begin
	if i=0 then
		return 1;
	else if i=1 then
		return 1;
	else
		return n * factorialc(n-1);
	end if;
end;
$$ language plsql;
```

## Tipos Record

>[!info]
>En PL/pgSQL, los tipos `RECORD` son tipos de datos especiales que permiten almacenar una fila de datos, sin necesidad de definir una estructura específica para las columnas de antemano. Los tipos `RECORD` son muy útiles cuando no se conoce la estructura exacta de la fila de antemano o cuando se desea manejar filas de diferentes tablas con diferentes estructuras.

### Ejemplo
```plsql
create or replace function formato()
returns text as $$
declare
	temp record;
begin
	select into temp 1+1 as a, 2+2 as b;
	return 'a=' || temp.a || '; b=' || temp.b;
end;
$$ language plpgsql;
```

#### Explicación
- `temp record;`: Declara una variable `temp` de tipo `record`. Esta variable puede almacenar una fila de datos con cualquier estructura.
- `begin`: Indica el inicio del bloque de código ejecutable de la función.
- `select into temp 1+1 as a, 2+2 as b;`: Ejecuta una consulta `SELECT` que calcula `1+1` y `2+2`, y almacena los resultados en la variable `temp`. Los resultados se almacenan con los nombres de columna `a` y `b`.
- `return 'a=' || temp.a || ';b=' || temp.b;`: Construye una cadena de texto concatenando las cadenas `'a='`, el valor de `temp.a`, la cadena `';b='`, y el valor de `temp.b`. Esta cadena es la que será retornada por la función.
- `end;`: Finaliza el bloque de código de la función.
- `$$`: Finaliza el bloque de código de la función.
- `language plpgsql;`: Especifica que el lenguaje utilizado para definir esta función es PL/pgSQL

#### Ejecución
```plsql
select formato();
```

## Búsqueda a partir de un código
```plsql
create function retornaNombreDep(text)
returns text as $$
declare
	nomdep text;
begin
	select into nomdep cast(nombre as text)
	from departamentos
	where coddeo = $1;
	return nomdep;
end;
$$ language plpgsql;
```

#### Explicación
- `nomdep text;`: Declara una variable `nomdep` de tipo `text` que se utilizará para almacenar el nombre del departamento.
- `begin`: Indica el inicio del bloque de código ejecutable de la función.
- `select into nomdep cast(nombre as text) from departamentos where coddeo = $1;`: Ejecuta una consulta `SELECT` que obtiene el valor de la columna `nombre` de la tabla `departamentos` donde `coddeo` coincide con el primer parámetro de la función (`$1`). El resultado se almacena en la variable `nomdep`.
    - `cast(nombre as text)`: Asegura que el valor de `nombre` se convierte a tipo `text`, aunque ya debería ser `text`.
- `return nomdep;`: Retorna el valor almacenado en `nomdep`.
- `end;`: Finaliza el bloque de código de la función.

#### Ejecución
```plsql
select retornaNombreDep("UCA");
```

>[!info]
> En el contexto de funciones SQL y PL/pgSQL, `END` se utiliza para señalar el final de un bloque de código. Su uso varía dependiendo de si estás trabajando con una función simple SQL o con una función más compleja en PL/pgSQL.
> En las funciones PL/pgSQL, `END` se utiliza para cerrar el bloque de código de la función, el cual comienza con `BEGIN`. Aquí, `END` indica el final de la lógica de la función.

# Listar las funciones creadas
```sql
SELECT proname AS function_name
FROM pg_proc
JOIN pg_namespace ON pg_namespace.oid = pg_proc.pronamespace
WHERE pg_namespace.nspname NOT IN ('pg_catalog', 'information_schema')
ORDER BY function_name;drop 
```

# Laboratorio

## Datos
```sql
--Carga de datos bdcomercial
CREATE TABLE departamentos(
        coddep smallint not null,
        nomdep  varchar(60)  not null
);


INSERT INTO departamentos
VALUES
(10,'CUZCO'),
(11,'LIMA'),
(12,'AREQUIPA'),
(13,'TRUJILLO'),
(14,'LORETO');



select * from cliente


DROP TABLE cliente

CREATE TABLE Cliente(
        Cod_Cli smallint not null,
        Nombre_Cli  varchar(60)  not null,
        Ingreso_Cli  numeric(8,2)  not null
)

INSERT INTO cliente
VALUES
(1,'Williams Suarez',        2500.00),
(2,'Nestor Bautista',        3500.00),
(3,'Margarita Mondragon',        2000.00),
(4,'Miguel Chuquispuma',        4500.00),
(5,'Rita Paz',        4100.00),
(6,'Eduardo Yauri',2800.00),
(7,'Cesar Diez',3350.00),
(8,'Angela Perez',2650.00),
(9,'Arturo Rojas',5200.00),
(10,'Dante Antiporta',6500.00),
(11,'Hector Bedon',7200.00);

DELETE FROM cliente

select * from cliente


CREATE TABLE Conyuge(
    Cod_Cli smallint not null,
    Nombre_Cony varchar(60)  not null,
    Ingreso_Cony numeric(8,2)  not null,
    Edad_Cony smallint not null
)


delete from conyuge


select * from conyuge


INSERT INTO conyuge VALUES
(1        ,'Alicia Galvez'        ,2250.00,        28),
(2        ,'Patricia Micha',1950.00,        49),
(3        ,'Bryan Caballero'        ,1800.00,        29),
(8        ,'Miguel Chuquispuma',2500.00,        27),
(9        ,'Karina Huarache',1450.00,        28),
(10        ,'Julita Inca'        ,1900.00,        36),
(11        ,'Esther Campos',3300.00,        37)



CREATE TABLE Pedido(
        Num_Ped smallint not null,
        Cod_Cli smallint not null,
        Fecha_Ped  date not null,
    Val_Ped numeric(8,2)  not null
)



DELETE FROM pedido


INSERT INTO Pedido VALUES 
(1,        1,        '2019-09-12'        ,285.00),
(2,        7,        '2019-09-13'        ,3270.00),
(3,        5,        '2019-09-14'        ,3485.00),
(4,        6,        '2019-09-14'        ,957.00),
(5,        3,        '2019-09-15'        ,1785.00),
(6,        11,        '2019-09-15'        ,4270.00),
(7,        2,        '2019-09-15'        ,687.00),
(8,        9,        '2019-09-16'        ,4567.00)



SELECT * FROM pedido




CREATE TABLE Items(
        Num_Ped smallint not null,
        Cod_Prod char(3) not null,
        Cant_Prod smallint not null
)





DELETE FROM items



INSERT INTO items VALUES 
(1,        '005',        8),
(1,        '007',        12),
(1,        '004',        6),
(2,        '001',        72),
(2,        '007',        8),
(2,        '004',        15),
(3,        '003',        12),
(3,        '010',        14),
(4,        '009',        6),
(4,        '006',        9),
(4,        '002',        12),
(4,        '005',        13),
(5,        '001',        20),
(5,        '008',        18),
(6,        '001',        17),
(7,        '001',        10),
(7,        '004',        26),
(8,        '001',        6),
(8,        '007',        14)



SELECT * FROM items;


﻿CREATE TABLE Producto(
        Cod_Prod char(3) not null,
        Nombre_Prod char(3) not null,
        Cant_Prod smallint not null,
    Val_Prod numeric(8,2)  not null
);


DELETE from producto


INSERT INTO producto VALUES 
('001'        ,'ACEITE VEGETAL PRIMOR'                                   ,        28,        14.20),
('002'        ,'ARROZ EXTRA PAISANA'                                     ,        33,        19.80),
('003'        ,'AVENA CON CEREAL TRES OSITOS'                            ,        18,        2.30),
('004'        ,'AZUCAR RUBIA CARTAVIO'                                   ,        19,        14.49),
('005'        ,'CAFE NESCAFE TRADICION'                                  ,        25,        21.90),
('006'        ,'CAJA DE FOSFOROS INTI CHICA'                             ,        45,        2.20),
('007'        ,'FILETE DE ATUN FANNY'                                    ,        95,        9.50),
('008'        ,'AGUA MINERAL EVIAN'                                      ,        50,        7.90),
('009'        ,'JUGO DE DURAZNO PULPIN'                                  ,        63,        6.90),
('010'        ,'QUESO FUNDIDO BONLE SACHET'                              ,        100,1.80),
('011'        ,'YOGURT DE FRESA LAIVE 1 LITRO'                           ,        100,9.00),
('012'        ,'QUINUA AVENA 3 OSITOS'                                   ,    250,1.30)


select * from producto

CREATE TABLE repuestos(
id int,
nombre varchar(60),
costo numeric(8,2),
peso numeric(8,2)
);



INSERT INTO repuestos VALUES
(637,'Cable', 14.29 , 5),
(638,'Martillo', 25.46 , 8),
(639,'Focos', 7.35 , 32);


create table empleados
(codemp char(5),
nombres varchar(20),
apellidos varchar(20),
salario numeric(8,2),
posicion varchar(20),
area char(2),
dept char(2));



insert into empleados values
('SL100','Juan','Gonzales',30000,'Administrador','B3','TA'),
('SL101','Marlon','Brandes',24000,'Administrador','B5','AN'),
('SL102','Rayan','Figueroa',12000,'Gestor de Proyecto','B3','TA'),
('SL103','Jesus','Mendez',12000,'Gestor de Proyecto','B5','AR'),
('SL104','Luz','Marquez',9000,'Gestor de Proyecto','B7','CU'),
('SL105','Leonela','Tacure',-2500,'Gestor de Proyecto','B3','PI');


CREATE TABLE cuentas(
id int generated by default as identity,
titular varchar(100) not null,
saldo numeric(8,2)
);



INSERT INTO cuentas (titular,saldo) VALUES
('MIGUEL', 13520.75),
('BRYAN', 8745.70),
('ALONSO', 23645.25),
('JORGE', 57234.16);

```

## Funciones

### Funciones en SQL
1. Crear la función `escribe` que exhiba un número real en la salida.
```plsql
create function escribe()
returns numeric
as $body$
select 13.0
$body$
language sql;
```

2. Invoque a la función `escribe`
```plsql
select escribe();
```

3. Desarrolle una función que reciba como argumentos dos números enteros y retorne su suma
```plsql
create function suma(n1 int, n2 int)
returns int
as $body$
select n1 + n2
$body$
language sql;
```

4. Sume 350 y 750 invocando la función anterior
```plsql
select suma(350, 750);
```

5. Elabore una función para convertir grados Fahrenheit a Centígrados
```plsql
create function convertir(real)
returns real
as $body$
select ($1-32) *(5.0/9)
$body$
language sql;
```

6. Averigüe a cuanto equivale 77° Fahrenheit
```plsql
select convertir(77);
```

### Funciones con tablas como parámetros

7. Crear la relación temporal trabajador con atributos: nombre, sueldo y edad

```sql
create temp table trabajador(
	nombre text,
	sueldo numeric,
	edad int
);
```

>[!info]
> `CREATE TEMP TABLE`: Esta parte del comando indica que se va a crear una tabla temporal.
> Una tabla temporal es una tabla que existe solo durante la sesión de base de datos en la que se creó. Las tablas temporales se utilizan para almacenar datos temporales que no necesitan ser retenidos permanentemente.


8. Insertar las tuplas
	- ('Marisol', 2400, 21)
	- ('Paloma', 4200, 30)

```sql
insert into trabajador values
('Marisol', 2400, 21),
('Paloma', 4200, 30);
```

9. Elabore una función que duplique el sueldo de los trabajadores
```plsql
create function duplica_sueldo(trabajador)
returns numeric
as $body$
select $1.sueldo * 2 as nuevoSueldo
$body$
language sql;
```
- **Observación**: esta función no modifica los valores de los sueldos en las tablas.


10. Presente el nombre con los sueldos duplicados para los trabajadores mayores de 25 años

```plsql
select nombre, duplica_sueldo(trabajador.*) from trabajador
where edad > 25;
```
- `duplica_sueldo(trabajador.*)`: Llama a la función `duplica_sueldo` pasando toda la fila de `trabajador` como argumento. El operador `.*` indica que se pasa toda la fila como un registro.


11. Liste a los trabajadores con un aumento del 10% sobre el sueldo duplicado

```sql
select nombre, duplica_sueldo(trabajador.*) * 1.1 as aumento_duplicado from trabajador;
```
También
```plsql
select nombre, duplica_sueldo(row(nombre, sueldo*1.1, edad)) from trabajador;
```
El uso de `row` crea una fila (registro) con los valores especificados. En este caso, crea una fila con:
- `nombre`: El valor de la columna `nombre` de la tabla `trabajador`.
- `sueldo * 1.1`: El valor de la columna `sueldo` multiplicado por 1.1 (aumentando el sueldo en un 10%).
- `edad`: El valor de la columna `edad` de la tabla `trabajador`

### Funciones PL/PGSQL

12. Elabore la función `obtenerDepa` que permita recuperar el nombre del departamento dado su código

```sql
CREATE TABLE departamentos(
        coddep smallint not null,
        nomdep  varchar(60)  not null
);


INSERT INTO departamentos
VALUES
(10,'CUZCO'),
(11,'LIMA'),
(12,'AREQUIPA'),
(13,'TRUJILLO'),
(14,'LORETO');
```

```plsql
create or replace function obtenerDepa(codigo smallint)
returns varchar(60) 
as $body$
declare
	nombre_depa varchar(60);
begin
	select nomdep into nombre_depa 
	from departamentos
	where coddep=codigo;
	return nombre_depa;
end;
$body$ language plpgsql;
```

```sql
select obtenerDepa(11::smallint);
```


13. Exhiba el nombre del cliente y su departamento de origen
```sql
CREATE TABLE Cliente(
        Cod_Cli smallint not null,
        Nombre_Cli  varchar(60)  not null,
        Ingreso_Cli  numeric(8,2)  not null
);

INSERT INTO cliente
VALUES
(1,'Williams Suarez', 2500.00),
(2,'Nestor Bautista', 3500.00),
(3,'Margarita Mondragon', 2000.00),
(4,'Miguel Chuquispuma', 4500.00),
(5,'Rita Paz', 4100.00),
(6,'Eduardo Yauri',2800.00),
(7,'Cesar Diez',3350.00),
(8,'Angela Perez',2650.00),
(9,'Arturo Rojas',5200.00),
(10,'Dante Antiporta',6500.00),
(11,'Hector Bedon',7200.00);
```

```plsql
create or replace function nombre_depa(codigo smallint)
returns 
```

