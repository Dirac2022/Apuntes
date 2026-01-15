
## 📘 Patrón de Ingesta de Datos: CSV a PostgreSQL (ETL)

Este flujo está diseñado para ser agnóstico al proyecto. Úsalo siempre que necesites mover datos de archivos planos (CSV/Excel) a una base de datos relacional robusta.

### 1. Filosofía del Diseño: ¿Por qué usar una tabla de Staging?

No cargamos directamente a la tabla final por tres razones de confiabilidad:

* **Aislamiento de Errores:** Si el CSV tiene un formato roto, el error ocurre en una tabla temporal, no en tu tabla de producción.
* **Flexibilidad de Mapeo:** Tu base de datos puede tener una estructura (ej. UUIDs, relaciones) que el CSV no tiene.
* **Limpieza de Datos:** Permite transformar datos "sucios" (como el texto `'NaN'`) en valores reales (`NULL`) antes de que toquen el sistema.

---

### 2. El "Sandbox": Creación de la Tabla Temporal

La tabla de staging debe ser **permisiva**. Usamos el tipo `TEXT` para todo, evitando que la base de datos rechace filas por errores de formato menores.

```sql
-- Creamos una tabla que solo vive durante la conexión actual (Sesión)
CREATE TEMP TABLE staging_raw_data (
    col1 TEXT,
    col2 TEXT,
    col3 TEXT  -- Añadir tantas columnas como tenga el archivo físico
);

```

**Explicación técnica:**

* **`CREATE TEMP TABLE`**: Esta tabla reside en la memoria/disco temporal del motor. Se destruye automáticamente al cerrar la sesión (`psql`), lo que garantiza un entorno **seguro y limpio**.
* **`TEXT`**: Al definir todo como texto, delegamos la validación de tipos al paso final, asegurando que el comando de copia no falle a mitad de camino.

---

### 3. La Transferencia: El comando `\copy`

Es vital distinguir entre `COPY` (comando SQL del servidor) y `\copy` (meta-comando del cliente psql).

```bash
-- Ejecutado desde la terminal del cliente (psql)
\copy staging_raw_data FROM '/ruta/al/archivo.csv' WITH (
    FORMAT CSV, 
    HEADER TRUE, 
    ENCODING 'LATIN1', 
    DELIMITER ','
);

```

**Explicación de parámetros cruciales:**

* **`\copy`**: Corre en tu máquina local (Ubuntu). Lee el archivo de tu disco y lo "empuja" hacia el servidor remoto (Neon). `COPY` normal fallaría porque el servidor no tiene acceso a tus archivos de `/home/dirac/`.
* **`ENCODING 'LATIN1'`**: Vital para el español. Si el archivo fue guardado con codificación Windows/Excel, el UTF-8 fallará con acentos y eñes.
* **`HEADER TRUE`**: Instruye al motor a ignorar la primera fila de metadatos.

---

### 4. La Consolidación: Mapeo y Transformación

Este es el paso de **carga final**. Aquí es donde aplicamos la lógica de negocio y la integridad referencial.

```sql
INSERT INTO tabla_final (col_uuid, col_negocio, col_limpia, tenant_id)
SELECT 
    gen_random_uuid(),            -- Generación automática de IDs
    col1,                         -- Mapeo directo
    NULLIF(col2, 'NaN'),          -- Transformación de 'NaN' a NULL real
    'ID_FIJO'::UUID               -- Inyección de llaves foráneas (Contexto)
FROM staging_raw_data;

```

**Análisis de expresiones complejas:**

* **`NULLIF(A, B)`**: Retorna `NULL` si `A == B`. Es la forma más limpia de sanitizar datos que vienen de Python/Pandas o Excel donde los vacíos se marcan como "NaN".
* **`::UUID` (Type Casting)**: Fuerza a PostgreSQL a tratar un string como un objeto de tipo UUID. Sin esto, la base de datos rechazaría la inserción por incompatibilidad de tipos.
* **Atocimidad**: Al usar un `INSERT INTO ... SELECT`, Postgres garantiza que o se insertan las 273 filas o ninguna. Esto mantiene la **consistencia** del sistema ante fallos de red.

---

### 5. Resumen de comandos de supervivencia (Cheat Sheet)

| Acción | Comando | Por qué es útil |
| --- | --- | --- |
| **Borrar staging** | `DROP TABLE staging_raw_data;` | Libera recursos si la sesión es larga. |
| **Validar carga** | `SELECT COUNT(*) FROM staging_raw_data;` | Confirmar que el `\copy` leyó todas las filas. |
| **Check de Nulos** | `SELECT * FROM final WHERE col IS NULL;` | Verificar que la limpieza `NULLIF` funcionó. |
| **Ver Encodings** | `SHOW client_encoding;` | Saber qué formato de texto espera tu terminal actual. |

---