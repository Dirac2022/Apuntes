
# Vistas

Dos objetivos principales de las vistas:
- Simplificar consultas.
- Autorización de acceso (seguridad).

## Concepto
- **Vista**: es un medio de proveer al usuario un *modelo personalizado* de base de datos.
- Es una relación que no almacena datos, compuesta dinámicamente por una *consulta* que es previamente analizada y optimizada.

## Vista
- Un SGBD puede dar soporte a un gran número de vistas sobre cualquier conjunto de relaciones.
- El SGBD almacena la definición de la vista, más es instanciada cuando una consulta sobre esta fuera ejecutada.
	- Toda vista puede ser consulta pero no toda vista puede ser actualizada.

# Creación y consulta en vistas

### En SQL una vista está definida como
```sql
create view nombreDeVista <expresion de consulta>
```
Donde < expresion de consulta> es cualquier expresión de consulta válida en SQL.

- Proyecto (codProy, tipo, descripcion)
- ProyectoEmpleado (codProy, codEmp, fechaInicial, fechaFinal)
- Empleado (codEmp, nombre, categoria, salario)

```sql
create view vSalariosAltos as
select codEmp, nombre, salario
from empleado  -- Tabla base
where salario > 10000
```

Esta vista tendrá los atributos especificados en la consulta.

**Para ver todas las vistas creadas**
```sql
select viewname
from pg_views
where schemaname = 'public';
```

## Vistas sobre una relación
### Otra forma
```sql
create view vSalarios (a, b, c) as
select codEmp, nombre, salario
from empleado
where salario > 10000
```

Esta vista tendrá los atributos a, b, c, que serán instanciados con los respectivos valores recuperados por la consulta (codEmp, nombre, salario)

## Vistas con varias relaciones
### Proyectos de alto nivel (nivel con varias tablas)
- Proyecto (<u>codProy</u>, tipo, descripcion)
- ProyectoEmpleado (<u>codProy</u>, <u>codEmp</u>, fechaInicial, fechaFinal)
- Empleado (<u>codEmp</u>, nombre, categoria, salario)

```sql
create view vProyectoAltoNivel as
select e.codEmp, e.nombre, e.salario p.descripcion
from empleado e, proyecto p, proyectoEmpleado pe
where e.salario > 10000 AND e.codEmp=pe.codEmp AND pe.codProy=p.codProy
```

## Vista: recursividad (vista sobre vista)
### Proyectos de alto nivel (vista sobre vista)
- Proyecto (<u>codProy</u>, tipo, descripcion)
- ProyectoEmpleado (<u>codProy</u>, <u>codEmp</u>, fechaInicial, fechaFinal)
- Empleado (<u>codEmp</u>, nombre, categoria, salario)
- vAltoNivel(codEmp, nombre, salario)

```sql
create view vProyectosAltoNivel as
select e.codEmp, a.nombre, a.salario, p.descripcion
from vAltoNivel a, proyecto p, proyectoEmpleado pe
where a.codEmp=pe.codEmp AND pe.codProy=p.codProy
```


## Consultas en Vistas
### Consultas SQL pueden ser específicas sobre la vista
```sql
select nombre
from vProyectosAltoNivel
where descripcion="Proyecto A"
```

- Una vista está siempre actualizada: al modificar tuplas en las tablas implicadas en la vista, la vista automáticamente refleja los cambios.
- Los resultados no se aprecian cuando se crea la vista, sino cuando ejecutamos una consulta sobre esta.

### Eliminación de vistas
Cuando una vista no se necesita más la podemos eliminar usando el comando `drop view`:
```sql
drop view nombreDeLaVista;
```

# Laboratorio 15

## Restauración de bd walmart

1. Descargar el archivo *walmart.backup* y copiarlo en el escritorio.
2. Ingresar a psql:
```bash
sudo su
su posgres
psql -U postgres -d postgres
```
3. Crear la base de datos *walmart*:
```sql
create database walmart;
```
4. Cerrar sesión en postgres:
```sql
exit
```
4. Dirigirse al escritorio

5. Una vez ubicado en el escritorio (o en la carpeta donde se encuentre el backup) realizar la restauración:
```bash
psql -U postgres -d walmart -f walmart.backup
```

## Laboratorio

1. Crear vista

```sql
create view vista_00 as
select 'Bienvenido al diseño de Vistas';
```

Ver la vista:
```sql
select * from vista_00;
```
SELECT * FROM vista_00,

>Para mostrar las vistas creadas
```sql
\dv
```


2. Borrar la vista 
```sql
drop view vista_00;
```


3. Crear vista
```sql
create view vista_00 as
select text 'Bienvenido al diseño de Vistas' as mensaje;
```
Ver vista:
```sql
select * from vista_00;
```

4. Clientes
```sql
create view vista_01 (codigo, nombrecia, direccion, pais) as
select idcliente, nombrecia, direccion, pais
from clientes;
```

5. Consulta de vistas:

```sql
select * from vista_01;
```

```sql
select codigo, nombrecia, pais from vista_01;
```

6. Crear vista_002
```sql
create view vista_02 (CodigoProducto, NombreProducto, PrecioTotal) as
select idproducto, nombreproducto, preciounidad*unidadesenexistencia
as preciototal
from productos;
```

7. Consulta
```sql
select * from vista_02;
```

8. Crear vista_03
```sql
create view vista_03 as
select * from clientes
where pais='Brasil';
```

9. Consulta a vista_03
```sql
select idcliente, nombrecia, ciudad, pais
from vista_03;
```


10. Crear vista
```sql
create view ClientesProveedoresCiudad as
select ciudad, nombrecia, nombrecontacto, 'CLIENTE' as tipo
from clientes union
select ciudad, nombrecia, nombrecontacto, 'PROVEEDOR' as tipo
from proveedores;
```

- Se añade una columna adicional llamada *tipo* con el valor *CLIENTE* para cada fila seleccionada de la tabla *clientes*.
- Se añade una columna adicional llamada *tipo* con el valor *PROVEEDOR* para cada fila seleccionada de la tabla *proveedores*.


11. Ver vista
```sql
select ciudad, nombrecia, tipo from ClientesProveedoresCiudad;
```

```sql
select * from ClientesProveedoresCiudad;
```

12. Crear vista ListaAlfabertica_ProductosCategoria
```sql
create view ListaAlfabetica_ProductosCategorias as
select idproducto, nombreproducto, categoria
from productos inner join categorias
on productos.idcategoria=categorias.idcategoria
order by categoria, nombreproducto;
```

13. Ver vista
```sql
select * from ListaAlfabetica_ProductosCategorias;
```

14. Crear vista ProductosPorCategoria
```sql
create view ProductosPorCategoria as
select categoria, nombreproducto, cantidadporunidad, unidadesenexistencia
from productos inner join categorias
on productos.idcategoria=categorias.idcategoria
order by categoria, nombreproducto;
```

15. Ver vista
```sql
select categoria, nombreproducto, unidadesenexistencia
from ProductosPorCategoria;
```


16. Crear vista SubTotalPedidos
```sql
create view SubtotalPedidos as
select idpedido, sum(preciounidad*cantidad*(1-descuento)) as subtotal
from detallesdepedidos
group by idpedido
order by idpedido;
```

```sql
select * from SubTotalPedidos;
```


17.  Crear una vista sobre una vista
```sql
create view sumapedidosanuales as
select fechaenvio, p.idpedido, subtotal
from pedidos p inner join subtotalpedidos s
on p.idpedido=s.idpedido
where fechaenvio is not null;
```

```sql
select * from sumapedidosanuales;
```





