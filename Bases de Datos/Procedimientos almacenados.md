
# Laboratorio en clase

Crear la base de datos donde se hará el laboratorio

```sql
create database bdsp;
```

Creamos el primer procedimiento para cambiar a mayúsculas un texto
```sql
create procedure aMayus(INOUT string text)
LANGUAGE plpgsql
AS $$
BEGIN
string := upper(string);
END
$$;
```

```sql
call aMayus('Hola mundo');
```

Crea las tablas pedidos y facturas e ingresa los valores para la tabla pedidos.
```
CREATE DATABASE bdsp;

CREATE TABLE facturas (
numfac SERIAL PRIMARY KEY,
cliente TEXT NOT NULL,
monto_total NUMERIC NOT NULL,
fechafac DATE NOT NULL,
cancelada BOOLEAN DEFAULT FALSE
);

CREATE TABLE pedidos (
idped SERIAL PRIMARY KEY,
idcliente INT NOT NULL,
fechaped DATE NOT NULL,
monto_total NUMERIC NOT NULL
);

INSERT INTO pedidos (idcliente,fechaped,monto_total)	
VALUES
(1,'01/06/2024',150.0),
(2,'02/06/2024',75.50),
(1,'03/06/2024',2000.0),
(3,'04/06/2024',50.0),
(2,'05/06/2024',120.75);
 
select * from pedidos;
```

>[!tip]
No es necesario colocar el nombre del campo, es suficiente colocar los tipos

Crear un procedimiento para crear una factura, que recibe como parámetros el número de cliente, el monto total y la fecha
```sql
create procedure crea_factura(
in  pcliente text, 
in ptotal numeric, 
in pfecha date)
language plpgsql
as $$
begin
	insert into facturas (cliente, monto_total, fechafac)
	values (pcliente, ptotal, pfecha);
end;
$$;
```

Los parámetros de texto o fecha deben estar en comillas simples

```sql
call crea_factura('MARTIN', 3500, '25-06-2024');
```

```sql
call crea_factura('GERALDINE', 2750, '24-06-2024');
```

Para eliminar un procedimiento
```sql
DROP PROCEDURE crea_factura(text, numeric, date);
```


Procedimiento para cancelar una factura, recibe como parámetro el número de factura
```sql
create procedure cancela_factura(
in pnumfac integer
)
language plpgsql
as $$
begin
	update facturas set cancelada=true
	where numfac=pnumfac;
end;
$$;
```


Procedimiento para calcular el monto total de los pedidos de un cliente.
```sql
create procedure monto_TotalporCliente(in pidcliente int)
language plpgsql
as $$
declare
	vtotal numeric := 0;
begin
	select sum(monto_total) into vtotal
	from pedidos
	where idcliente=pidcliente;
	raise notice 'Total gastado por el cliente de id % : %' , pidcliente, vtotal;
	exception
		when others then
		raise exception 'Error al calcular el monto total por idcliente %', pidcliente;
end;
$$;
```

```sql
call monto_TotalporCliente(1);
```
