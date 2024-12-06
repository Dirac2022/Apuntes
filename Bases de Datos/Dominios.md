Para crear un dominio en PostgreSQL para un campo de fecha, puedes definir un dominio que asegure que los valores sean válidos y, si lo deseas, agregar restricciones adicionales como límites de rango. A continuación se muestra cómo puedes hacerlo:

### Paso 1: Crear el Dominio

Vamos a crear un dominio llamado `fecha_valida` que solo acepte fechas válidas dentro de un rango específico.

```sql
CREATE DOMAIN fecha_valida AS DATE
CHECK (VALUE >= '1900-01-01' AND VALUE <= '2100-12-31');
```

### Explicación

- **CREATE DOMAIN**: Inicia la creación de un nuevo dominio.
- **fecha_valida**: El nombre del dominio.
- **AS DATE**: Especifica que el dominio es de tipo `DATE`.
- **CHECK (VALUE >= '1900-01-01' AND VALUE <= '2100-12-31')**: Define una restricción que asegura que el valor de la fecha está dentro del rango entre el 1 de enero de 1900 y el 31 de diciembre de 2100.

### Paso 2: Usar el Dominio en una Tabla

Una vez creado el dominio, puedes usarlo en tus tablas para asegurar que las fechas cumplan con las restricciones definidas.

```sql
CREATE TABLE eventos (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(100),
    fecha fecha_valida
);
```

### Explicación

- **fecha fecha_valida**: Define que la columna `fecha` debe cumplir con las restricciones del dominio `fecha_valida`.

### Paso 3: Insertar Datos

Al intentar insertar datos en la tabla, PostgreSQL verificará que las fechas cumplan con las restricciones del dominio.

```sql
INSERT INTO eventos (nombre, fecha) VALUES ('Conferencia', '2022-05-15'); -- Esto funcionará
INSERT INTO eventos (nombre, fecha) VALUES ('Conferencia', '1800-05-15'); -- Esto fallará
```

### Paso 4: Modificar el Dominio (Opcional)

Si necesitas ajustar las restricciones del dominio, puedes modificarlo con el comando `ALTER DOMAIN`.

```sql
ALTER DOMAIN fecha_valida ADD CONSTRAINT chk_future CHECK (VALUE <= CURRENT_DATE);
```

#### Forma general
1. Primero, debes identificar el nombre de la restricción actual en el dominio y eliminarla. Si no conoces el nombre de la restricción, puedes verlo con:
```postgresql
select conname
from pg_constraint
where connamespace = 'public'::regnamespace
and conrelid = 0
and contypid = 'nombre_dominio'::regtype;
```

Después de identificar el nombre de la restricción, usa el siguiente comando para eliminarla:
```postgresql
alter domain sex_dom drop constraint nombre_restriccion
```

2. Agregar una nueva restricción al dominio
```postgresql
alter domain sex_dom
add constraint nombre_restriccion check ... ;
```
### Paso 5: Eliminar el Dominio

Si ya no necesitas el dominio, puedes eliminarlo con el siguiente comando:

```sql
DROP DOMAIN fecha_valida;
```


### Ver dominios
Para ver los dominios creados en PostgreSQL, puedes utilizar la consulta siguiente en el terminal de psql:

```sql
SELECT domain_name, data_type 
FROM information_schema.domains 
WHERE domain_schema = 'public';
```

### Ver detalle de un dominio
```postgresql
\dD nombre_dominio
```
#### Explicación

- **`information_schema.domains`**: Es una vista en PostgreSQL que contiene información sobre todos los dominios definidos en la base de datos.
- **`domain_name`**: El nombre del dominio.
- **`data_type`**: El tipo de datos del dominio.
- **`WHERE domain_schema = 'public'`**: Filtra los dominios que están en el esquema `public`, que es el esquema por defecto en PostgreSQL.

Esta consulta te mostrará todos los dominios que has creado en el esquema público de tu base de datos. Puedes modificar el filtro `domain_schema` si tus dominios están en un esquema diferente.
### Conclusión

Definir un dominio para un campo de fecha en PostgreSQL te permite asegurar que las fechas ingresadas en tus tablas cumplan con ciertas restricciones, mejorando la integridad y consistencia de los datos en tu base de datos.

# Ejemplos

```postgresql
create domain sex_dom as varchar(10)
check (value in ('hombre', 'mujer'));
```


## Correo electrónico
```postgresql
create domain email_dom as varchar(100)
check (value ~* '^[A-Za-z0-9._-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$');
```

### Desglose detallado:

`~*`: Operador que realiza una comparación de expresión regular que no distingue entre mayúsculas y minúsculas.

1. **`^`**: Este es el **ancla de inicio**. Indica que la validación debe comenzar desde el inicio de la cadena, asegurando que toda la cadena cumpla con el patrón desde el principio.
    
2. **`[A-Za-z0-9._%+-]`**:
    
    - **`[ ]`**: Define una **clase de caracteres**, lo que significa que cualquier carácter incluido dentro de estos corchetes es válido en esa parte de la cadena.
    - **`A-Z`**: Cualquier letra mayúscula del alfabeto (de la `A` a la `Z`).
    - **`a-z`**: Cualquier letra minúscula del alfabeto (de la `a` a la `z`).
    - **`0-9`**: Cualquier dígito numérico (del `0` al `9`).
    - **`._%+-`**: Los caracteres especiales `.` (punto), `_` (guion bajo), `%` (signo de porcentaje), `+` (signo de suma), y `-` (guion). Estos caracteres son comunes en direcciones de correo electrónico y permiten nombres como `nombre.apellido+etiqueta@example.com`.
3. **`+`**:
    
    - Es un **modificador de cuantificación** que significa "uno o más". Aplica a la clase de caracteres anterior (`[A-Za-z0-9._%+-]`). Por lo tanto, la expresión requiere que haya al menos un carácter de esta clase al inicio de la cadena (por ejemplo, `nombre`, `usuario123`, `test%user`).
4. **`@`**:
    
    - Representa el **símbolo de arroba** literal, que es obligatorio en todas las direcciones de correo electrónico. Solo debe aparecer una vez y separa el nombre de usuario del dominio.
5. **`[A-Za-z0-9.-]`**:
    
    - Similar a la clase de caracteres anterior, pero aplicada al dominio:
        - **`A-Z`** y **`a-z`**: Letras mayúsculas y minúsculas.
        - **`0-9`**: Dígitos numéricos.
        - **`.`**: Punto, que es común en dominios para separar subdominios (por ejemplo, `mail.google`).
        - **`-`**: Guion, que es válido en nombres de dominio.
6. **`+`**:
    
    - Igual que antes, significa "uno o más", aplicándose a la clase de caracteres `[A-Za-z0-9.-]`. Esto asegura que la parte del dominio tenga al menos un carácter.
7. **`\.`**:
    
    - **`\.`** representa un punto literal. Se usa `\` (barra invertida) para escapar al punto, ya que en las expresiones regulares, el punto `.` tiene un significado especial (representa cualquier carácter). Con `\.` se asegura que el carácter específico en esa posición sea un punto, como el que separa el nombre de dominio de la extensión (`.com`, `.org`, etc.).
8. **`[A-Za-z]{2,}`**:
    
    - Esta parte representa la **extensión del dominio**.
        - **`[A-Za-z]`**: Solo permite letras, tanto mayúsculas como minúsculas.
        - **`{2,}`**: Es un cuantificador que indica "al menos 2 caracteres". Esto asegura que la extensión tenga una longitud mínima de 2 caracteres, como `.com`, `.net`, etc., y puede ser más larga, como `.info`, `.museum`.
9. **`$`**:
    
    - Es el **ancla de fin**. Indica que la validación debe terminar al final de la cadena, asegurando que no haya caracteres adicionales después de la parte de la extensión.
### Uso de los caracteres:

- **`%` (porcentaje)**: Aunque es raro, a veces se utiliza en correos electrónicos como parte de direcciones especiales en sistemas antiguos o como alias. Sin embargo, es poco común en los correos electrónicos actuales.
- **`+` (suma)**: Este carácter es más común y se usa para añadir etiquetas a direcciones de correo, una práctica llamada _plus addressing_ o _subaddressing_. Por ejemplo, `usuario+noticias@gmail.com` permite a los usuarios filtrar correos entrantes basándose en estas etiquetas.


## Número de teléfono

```postgresql
create domain telefono_cel_dom as varchar(15)
check ( value ~ '^\+?[0-9]{10,15}$')
```

- `CHECK (VALUE ~ '^\+?[0-9]{10,15}$')`: Valida el formato del número de teléfono usando una expresión regular.

### Desglose de la expresión regular:

- **`^`**: Ancla de inicio que asegura que la validación comience desde el inicio de la cadena.
- **`\+?`**: Indica que el signo `+` es opcional. Se utiliza al comienzo de un número de teléfono internacional, como `+1234567890`.
- **`[0-9]`**: Permite solo dígitos numéricos del `0` al `9`.
- **`{10,15}`**: Es un cuantificador que indica que debe haber entre 10 y 15 dígitos. Esto asegura que el número tenga un mínimo de 10 dígitos (típico de números locales) y un máximo de 15 dígitos (típico de números internacionales).


## Contraseñas

Al menos 8 caracteres alfanuméricos

```postgresql
create domain password_dom as varchar(50)
check (value ~ '^(?=.*[A-Za-z])(?=.*[0-9])[A-Za-z0-9]{8,}$');
```


- **`^`**: Ancla de inicio que asegura que la validación comience desde el inicio de la cadena.
- **`(?=.*[A-Za-z])`**: Asegura que haya al menos una letra en la cadena. Es un **lookahead** que verifica que en algún lugar de la cadena exista al menos un carácter alfabético (mayúscula o minúscula).
- **`(?=.*[0-9])`**: Asegura que haya al menos un número en la cadena. Es otro **lookahead** que verifica que haya al menos un dígito.
- **`[A-Za-z0-9]{8,}`**:
    - **`[A-Za-z0-9]`**: Permite solo letras (mayúsculas y minúsculas) y dígitos.
    - **`{8,}`**: Indica que la longitud de la cadena debe ser de al menos 8 caracteres.
- **`$`**: Ancla de fin que asegura que la validación termine al final de la cadena.


## Código de seguridad de tarjeta de crédito/debito

```postgresql
create domain cod_seguridad_dom as char(3)
check (value ~ '^\d{3}$');
```

### Explicación detallada

1. **`CHAR(3)
    
    - **`CHAR(3)`**: Es un tipo de dato de longitud fija que siempre almacena exactamente 3 caracteres. Si el valor es menor de 3 caracteres, se completa con espacios. Se usa aquí porque queremos asegurarnos de que la columna `cod_seguridad` siempre tenga exactamente 3 caracteres, sin variación en la longitud.
    
2. **`CHECK (VALUE ~ '^\d{3}$')`**:
    
    - Esta es una condición que utiliza una expresión regular para validar que el valor cumpla ciertos criterios.
    - **`~`**: Es el operador de coincidencia de expresión regular en PostgreSQL.
    
    **Explicación de la expresión regular `^\d{3}$`**:
    
    - **`^`**: Indica el inicio de la cadena. La validación debe empezar desde el primer carácter del valor.
    - **`\d`**: Representa un dígito numérico (equivalente a `[0-9]`).
    - **`{3}`**: Significa que la expresión anterior (`\d`) debe repetirse exactamente 3 veces. Esto asegura que el valor tenga exactamente 3 dígitos.
    - **`$`**: Indica el final de la cadena. La validación debe terminar en el último carácter del valor.


## Fecha de vencimiento de tarjeta
Podemos definir un dominio que valide que el valor ingresado tenga el formato `YY-MM`, comenzando desde el año `25` (que representaría 2025 en adelante) y el mes entre `01` y `12`
```postgresql
create domain dom_fecha_ven as char(5)
check (value ~ '^(2[5-9]|[3-9][0-9])-(0[1-9]|1[0-2])$');
```

### Explicación de la expresión regular:

- **`^`**: Indica el inicio de la cadena.
- **`2[5-9]`**: Representa los años `25`, `26`, `27`, `28`, y `29`.
- **`|`**: Alternativa lógica (o).
- **`[3-9][0-9]`**: Representa cualquier año de `30` a `99`.
- **`-`**: Un guion separador entre el año y el mes.
- **`(0[1-9]|1[0-2])`**: El mes debe ser un número entre `01` y `12`.
- **`$`**: Indica el final de la cadena.