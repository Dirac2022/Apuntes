
# Dominios, relaciones y llaves
I. CREACIÓN DE DOMINIOS, RELACIONES Y LLAVES: Se evaluará la integridad
de la información buscando que las tuplas reflejen lo mejor posible la realidad del
modelo del negocio.
a) Definición de dominios: 4 como mínimo.
b) Claves Primarias: 4 como mínimo.
c) Claves Únicas: 4 como mínimo.
d) Claves Foráneas: 4 como mínimo.
## Dominios

Definición de dominios

### Misiones
fecha

```sql
create domain fecha_valida as date
check (value >= '1960-01-10' and value <= '2500-12-31');
```

Par id_mision
```sql
create domain id_mision_dom as varchar(5)
check (value ~ '^[0-9]{2}[A-Z]$');
```


### Vehiculo

tipo vehiculo
```sql
create domain tipo_vehiculo_dom as varchar(50) check (value in ('Orbitador', 'Rover', 'Sonda', 'Aterrizador', 'Sonda/Aterrizador'));
```

id_vehiculo
```sql
create domain id_vehiculo_dom as varchar(5)
check (value ~ '^[0-9]{5}$');
```
### Otros

Una medida, un valor que no es negativo.
```sql
create domain medida as numeric not null
check (value >=0);
```

Para nombres de misiones, cientificos, etc.
```sql
create domain nombre_valido as varchar(50) not null;
```



## Claves primarias

En mision: id_mision

En cientifico: id_cientifico

En cohete: id_cohete

En comunicación: id_comunicacion

En experimento: id_experimento

En instrumento: id_instrumento

En vehiculo: id_vechiculo

## Claves únicas

En Mision
nombre
```sql
nombre nombre_valido unique;
```

(lugar_aterri, fecha_aterri)
```sql
lugar_aterri nombre_valido,
fecha_aterri fecha_valida,
unique (lugar_aterri, fecha_aterri)
```

En cohete
(nombre, id_mision)
```sql
nombre nombre_valido,
id_mision id_mision_dom
unique (nombre, id_mision)
```

En vehiculo
(nombre, tipo)
```sql
nombre nombre_valido, 
tipo varchar(50)
unique (nombre, tipo)
```


## Claves foráneas
Podemos fácilmente hallar las claves foráneas a partir del diagrama E-R presentado en la fase 1. Este nos mostraba las relaciones entre entidades.

Un cohete se relaciona con una misión y también con un vehículo de exploración.
```sql
vehiculo_id id_vehiculo_dom, 
id_mision id_mision_dom,
foreign key (vehiculo_id) references vehiculo(id_vehiculo),
foreign key (id_mision) references mision(id_mision),
```

Una comunicación se relaciona con una misión
```sql
id_mision id_mision_dom,
foreign key (id_mision) references mision(id_mision)
```

Un experimento se relaciona tanto con una misión, un científico que la encabeza y un instrumento
```sql
id_mision id_mision_dom,
id_cientifico varchar(5), 
id_instrumento varchar(5),
foreign key (id_mision) references mision(id_mision),
foreign key (id_cientifico) references cientifico(id_cientifico),
foreign key (id_instrumento) references instrumento(id_instrumento)
```


# Vistas
Deberá formular el enunciado, la consulta y una captura del resultado:
a) Vista que utilice una operación de conjuntos(union, intersection, etc) : 2 como mínimo


Una vista que nos muestre los nombres de las misiones y los cohetes:
```sql
create view misiones_cohetes as 
select nombre, 'Mision' as tipo from mision union 
select nombre, 'Cohete' as tipo from cohete;
```


Una vista que nos muestre las misiones que tengan tanto comunicaciones como experimentos asociados:
```sql
create view misiones_comunicaciones_experimentos as
select m.id_mision, m.nombre
from mision m join comunicacion c on m.id_mision=c.id_mision
intersect
select m.id_mision, m.nombre
from mision m join experimento e on m.id_mision = e.id_mision;
```

b) Vista cuyo origen de datos sean dos tablas, una por cada tipo de JOIN incluyendo una
condición WHERE: 3 como mínimo.

Una vista que muestre los vehículos y sus misiones asociadas para las misiones en estado activo:
```sql
create view vehiculos_misiones as
select v.nombre as vechiculo, m.nombre as mision
from vehiculo v inner join cohete c on v.id_vehiculo=c.vehiculo_id
inner join mision m on c.id_mision=m.id_mision
where m.estado = 'activo';
```

Una vista que muestre a científicos y los experimentos que encabezan, además de la misión a la que pertenece el experimento y el estado del experimento:
```sql
create view cientificos_experimentos as
select c.nombre as cientifico, m.nombre as nombre_mision, e.nombre_experimento, e.estado as estado_experimento
from cientifico c left join experimento e on c.id_cientifico=e.id_cientifico
inner join mision m on e.id_mision=m.id_mision
where e.estado is not null;
```
![[Pasted image 20240627145136.png]]

Una vista que muestre las misiones y las comunicaciones de estas:
```sql
create view misiones_comunicaciones as
select m.id_mision, m.nombre as mision, c.mensaje as tipo, c.respuesta as mensaje
from mision m right join comunicacion c on m.id_mision=c.id_mision
where c.mensaje is not null;
```
![[Pasted image 20240627145200.png]]

c) Vista cuyo origen de datos sea otra vista: 2 como mínimo.

A partir de la vista `misiones_comunicaciones` podemos obtener una vista que nos muestre las misiones por lanzar:
```sql
create view misiones_por_lanzar as
select mision, mensaje
from misiones_comunicaciones
where tipo = 'estado' and mensaje != 'Lanzamiento exitoso';
```


Si deseamos saber que experimentos se están llevando en misiones activas, podemos hacer uso de la vista  `cientificos_experimentos` la cual junto con la relación `mision` nos permite obtener una nueva vista:
```sql
create view cientificos_experimentos_misiones as
select ce.cientifico, ce.nombre_mision, ce.nombre_experimento, me.fecha_lanz
from cientificos_experimentos ce join mision me on ce.nombre_mision = me.nombre
where me.estado = 'activo';
```