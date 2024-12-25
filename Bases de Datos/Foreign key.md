Agregar una restricción de clave foránea
```postgresql
alter table <nombre_tabla> 
add constraint fk_<campo_tabla> 
foreign key (<campo_tabla>)
references <tabla_referenciada> (<campo_referenciado>)
on delete cascade;
```

- `ON DELETE CASCADE`: Al eliminar la fila en la tabla referenciada, se elimina la fila en la tabla que lo referencia
- `ON DELETE SET NULL`: Si se elimina una fila en la tabla referenciada, el campo que lo referencia en la tabla se vuelve **null**.



