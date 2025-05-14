
# Tipo sql
	En línea de comandos o power shell
```bash
pg_dump -U <usuario> -d <nombre-BD> -f "ruta\nombre" o nombre
```

Ejemplo
```bash
pg_dump -U postgres -d sigepat -f "C:\Users\mitch\Documents\sigepat_backup.sql"

```


# Tipo backup

Ejecuta el siguiente comando desde la terminal o desde una sesión de `psql`:
```bash
pg_dump -U postgres -F c -d sigepat -f /ruta/donde/guardar/sigepat.backup
```

## Explicación de los parámetros
- `-U postgres`: Usuario propietario de la base de datos (puedes cambiarlo si es necesario).
- `-F c`: Indica el formato de salida **custom** (binario compatible con pgAdmin).
- `-d sigepat`: Nombre de la base de datos que deseas respaldar.
- `-f /ruta/donde/guardar/sigepat.backup`: Ruta completa y nombre del archivo de respaldo

Ejemplo
```shell
pg_dump -U postgres -F c -d sigepat -f sigepat_backup.backup
```



# Restaurar achivo sql en bd creada en neon:

Ejecutar el comando psql en un terminal:
```shell
psql "postgresql://sigepat-bd_owner:Ulxwnb3rj8Rz@ep-orange-bird-a5o6nkrk.us-east-2.aws.neon.tech/sigepat-bd?sslmode=require" -f "C:\Users\mitch\Documents\sigepat_backup.sql"
```
