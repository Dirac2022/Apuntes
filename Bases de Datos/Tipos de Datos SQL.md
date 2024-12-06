

# VARCHAR
- **Definición**: Tipo de dato para almacenar cadenas de texto de longitud variable. Se especifica un tamaño máximo `n` y la longitud real de la cadena se ajusta al contenido almacenado.
- **Formato típico**: `VARCHAR(n)` (e.g., `VARCHAR(100)`).
- **Uso**: Se usa cuando se necesita almacenar texto cuya longitud varía, como nombres, direcciones, descripciones, etc. Es ideal para casos en los que las cadenas pueden tener tamaños diferentes.

# CHAR
- **Definición**: Tipo de dato para almacenar cadenas de texto de longitud fija. Si la cadena almacenada es menor que el tamaño especificado, se rellena con espacios.
- **Formato típico**: `CHAR(n)` (e.g., `CHAR(10)`).
- **Uso**: Se utiliza cuando se necesita una cadena de longitud fija, como códigos de identificación o códigos de país. Es más eficiente en comparación y alineación si todas las cadenas tienen la misma longitud.

# TEXT
- **Definición**: Tipo de dato que almacena solo la parte de la hora, sin la fecha.
- **Formato típico**: `TIME` (e.g., `14:30:00`).
- **Uso**: Se usa para representar horas en casos donde la fecha no es importante, como horarios de atención.

# INTEGER
- **Definición**: Tipo de dato para almacenar números enteros, sin decimales.
- **Formato típico**: `INTEGER` (e.g., `123`, `-456`).
- **Uso**: Se usa para contar elementos o representar valores enteros, como la cantidad de productos, IDs de usuarios, etc.


# SMALLINT
- **Definición**: Tipo de dato para almacenar números enteros más pequeños. Ocupa menos espacio que `INTEGER`.
- **Formato típico**: `SMALLINT` (e.g., `1000`, `-500`).
- **Uso**: Se utiliza cuando necesitas almacenar números enteros de un rango menor, como edades o cantidades pequeñas.

# BIGINT
- **Definición**: Tipo de dato para almacenar números enteros grandes. Útil para valores que superan el rango de `INTEGER`.
- **Formato típico**: `BIGINT` (e.g., `123456789012345`, `-987654321`).
- **Uso**: Se usa en situaciones donde es necesario manejar grandes números, como registros contables o grandes identificadores numéricos.

# DECIMAL
- **Definición**: Tipo de dato que almacena números con una precisión exacta y permite definir el número total de dígitos (`p`) y la cantidad de decimales (`s`).
- **Formato típico**: `DECIMAL(p, s)` (e.g., `DECIMAL(10, 2)` para valores como `12345.67`).
- **Uso**: Se utiliza principalmente para almacenar cantidades monetarias, precios o datos financieros donde la precisión es crucial. Se asegura de que no haya errores de redondeo, manteniendo exactitud en los cálculos.
# NUMERIC
- **Definición**: Tipo de dato sinónimo de `DECIMAL` y con la misma funcionalidad. Ambos se utilizan para almacenar números con precisión exacta y permiten especificar la cantidad de dígitos y decimales.
- **Formato típico**: `NUMERIC(p, s)` (e.g., `NUMERIC(12, 4)` para valores como `123456.7890`).
- **Uso**: Ideal para situaciones donde la precisión es necesaria, como en cálculos contables, tasas de interés, etc. `NUMERIC` es preferido por algunos estándares SQL para indicar precisión exacta.

# FLOAT
- **Definición**: Tipo de dato que almacena números en punto flotante. Permite representar números con un rango amplio pero con una precisión variable, lo que puede llevar a errores de redondeo.
- **Formato típico**: `FLOAT` (e.g., `FLOAT` o `FLOAT(53)` para una mayor precisión).
- **Uso**: Se utiliza en aplicaciones donde no es crucial mantener una precisión exacta, como cálculos científicos, estadísticas y gráficos, donde la flexibilidad y la representación de números muy grandes o pequeños es más importante que la precisión.

# REAL
- **Definición**: Tipo de dato de punto flotante similar a `FLOAT`, pero con una precisión menor. Generalmente, ocupa menos espacio y es menos preciso que `FLOAT`.
- **Formato típico**: `REAL` (e.g., `12345.6789`).
- **Uso**: Se usa en aplicaciones donde la precisión exacta no es fundamental y donde se requiere una representación de punto flotante más ligera. Es útil para cálculos de aproximación y tareas donde el rendimiento es más importante que la precisión.

# TIMESTAMP
- **Definición**: El tipo de dato `TIMESTAMP` se usa para almacenar fechas y horas completas, incluyendo la información de año, mes, día, hora, minuto, segundo y, en algunos casos, fracciones de segundo.
- **Formato típico**: `YYYY-MM-DD HH:MM:SS` (e.g., `2024-11-12 14:30:00`)
- **Zona horaria**: Por lo general, `TIMESTAMP` se almacena en formato UTC y puede convertir automáticamente las fechas y horas a diferentes zonas horarias al momento de consultarlas

# DATE
- **Definición**: El tipo de dato `DATE` solo almacena la parte de la fecha (año, mes y día), sin incluir la hora.
- **Formato típico**: `YYYY-MM-DD` (e.g., `2024-11-12`)
- **Uso**: Se utiliza cuando solo necesitas registrar la fecha, sin preocuparte por la hora exacta.

# TIME
- **Definición**: Tipo de dato que almacena solo la parte de la hora, sin la fecha.
- **Formato típico**: `TIME` (e.g., `14:30:00`).
- **Uso**: Se usa para representar horas en casos donde la fecha no es importante, como horarios de atención.

5084
Av Los pergaminos Jr Las azucenas calle Rios La Rotonda 463 Area3 Departamento 452 Interior 63



