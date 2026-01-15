
## 1. Introducción General

Las **variables de entorno** son un componente fundamental en el desarrollo de software moderno. Permiten controlar la configuración y el comportamiento de los programas sin necesidad de modificar su código fuente.

En esta clase estudiaremos qué son, para qué se utilizan, cómo se originaron, cómo se manejan en el sistema operativo, y cómo interactúa Python con ellas mediante el módulo estándar `os` y la librería externa `python-dotenv`.

---

## 2. Fundamentos Teóricos

### 2.1 Definición

Una **variable de entorno** es un **par clave-valor** almacenado en el entorno del sistema operativo. Estas variables contienen información que puede ser utilizada por los programas que se ejecutan dentro de ese entorno.

Ejemplo conceptual:

|Variable|Valor|
|---|---|
|`PATH`|`/usr/local/bin:/usr/bin:/bin`|
|`HOME`|`/home/mitchel`|
|`USER`|`mitchel`|

Cada programa que se ejecuta en el sistema puede acceder a ellas para conocer configuraciones específicas o información del usuario y del sistema.

---

### 2.2 Historia y origen

Las variables de entorno nacen en los sistemas **UNIX** de los años 70 y 80. En aquel entonces, los programas necesitaban conocer información contextual como:

- Dónde estaban los ejecutables.
    
- Qué idioma o configuración regional debía usarse.
    
- Qué usuario estaba ejecutando el proceso.
    

En lugar de incluir esta información en el código (lo cual haría que el programa fuera inflexible), se crearon mecanismos externos llamados **environment variables**.  
De este modo, los programas podían **comportarse de forma diferente** sin necesidad de recompilarse, simplemente cambiando el valor de ciertas variables.

Con el tiempo, este mecanismo fue adoptado por otros sistemas operativos, incluyendo **Windows** y **macOS**, y hoy es un estándar en informática moderna.

---

## 3. Propósito y ventajas

Las variables de entorno permiten que un mismo programa se ejecute en distintos contextos sin modificación del código.  
Esta práctica se basa en el principio de diseño conocido como **Configuration over Code** ("configuración sobre código").

Algunos usos comunes incluyen:

|Caso de uso|Variable de entorno típica|
|---|---|
|Conexión a base de datos|`DATABASE_URL`, `DB_USER`, `DB_PASS`|
|Claves secretas o tokens|`SECRET_KEY`, `API_KEY`|
|Configuración de entorno|`ENV=production`, `ENV=development`|
|Control de nivel de logs|`LOG_LEVEL=DEBUG`|

---

### 3.1 Consecuencias de no usar variables de entorno

Si una aplicación no utiliza variables de entorno y mantiene configuraciones o contraseñas directamente en el código fuente:

- Se **compromete la seguridad**, ya que datos sensibles pueden filtrarse al subir el código a un repositorio público.
    
- Se **reduce la flexibilidad**, ya que cada cambio de entorno (producción, pruebas, desarrollo) requiere modificar el código.
    
- Se **rompe la portabilidad**, haciendo difícil desplegar la aplicación en distintos servidores o plataformas.
    

#### Ejemplo incorrecto:

```python
# ❌ Mal ejemplo: contraseña escrita directamente en el código
DB_PASSWORD = "admin123"
```

Si este código se sube a GitHub, cualquiera puede visualizar esa contraseña, comprometiendo la seguridad del sistema.

---

## 4. Variables de entorno en los sistemas operativos

### 4.1 En Linux / macOS

En estos sistemas, las variables se definen y manipulan mediante comandos en la terminal o en archivos de configuración como `.bashrc` o `.bash_profile`.

```bash
# Definir una variable de entorno
export USER=mitchel

# Ver el valor de una variable
echo $USER
```

### 4.2 En Windows

En Windows, las variables se configuran en el panel de control o mediante la terminal PowerShell.

```powershell
# Mostrar variable de entorno
echo %USERNAME%

# Crear variable de entorno
setx MI_VARIABLE "Hola Mundo"
```

---

## 5. Manejo de variables de entorno en Python

Python incluye el módulo **`os`**, que permite acceder a las variables del sistema operativo a través del objeto `os.environ`.

### 5.1 Acceder a variables existentes

```python
import os

# Obtener el valor de la variable "USER"
usuario = os.environ.get("USER")
print(usuario)  # Ejemplo de salida en Linux: mitchel
```

- `os.environ` actúa como un **diccionario** que contiene todas las variables de entorno disponibles.
    
- `os.environ.get("USER")` busca una clave llamada `"USER"` y devuelve su valor.
    
- Si la variable no existe, se devuelve `None`.
    

---

### 5.2 Establecer variables de entorno dentro del programa

```python
import os

# Crear o modificar una variable de entorno dentro del proceso actual
os.environ["MY_VAR"] = "Hola Mundo"

# Verificar su valor
print(os.environ["MY_VAR"])  # Hola Mundo
```

Estas variables solo existen **mientras el proceso de Python esté en ejecución**.  
Una vez que el programa termina, la variable desaparece, ya que no se guarda permanentemente en el sistema operativo.

---

### 5.3 Asignar valores por defecto (fallback)

```python
import os

# Si la variable no existe, se usará un valor por defecto
db_name = os.environ.get("DB_NAME", "default_db")
print(db_name)
```

Esto permite asegurar que el programa tenga un valor funcional incluso si la variable no fue definida externamente.

---

### 5.4 Listar todas las variables de entorno disponibles

```python
import os

# Iterar sobre todas las variables del entorno actual
for key, value in os.environ.items():
    print(f"{key}: {value}")
```

Este código mostrará todas las variables disponibles que Python heredó del sistema operativo.

---

### 5.5 Definir variables temporalmente en la terminal

#### En Linux o macOS:

```bash
export PRUEBA="Estoy en el sistema operativo"
python script.py
```

#### En el script Python:

```python
import os
print(os.environ.get("PRUEBA"))
```

#### Salida esperada:

```
Estoy en el sistema operativo
```

Esto demuestra que Python hereda las variables directamente del entorno del sistema.

---

## 6. Archivo `.env` y librería `python-dotenv`

### 6.1 Motivación

Definir variables manualmente cada vez es tedioso. Para evitar esto, se creó la librería **`python-dotenv`**, que permite almacenar variables en un archivo `.env` y cargarlas automáticamente al entorno de Python.

---

### 6.2 Instalación

```bash
pip install python-dotenv
```

---

### 6.3 Estructura de un archivo `.env`

El archivo `.env` es un simple texto con pares clave-valor:

```bash
DB_USER=admin
DB_PASS=1234
DB_NAME=mi_base_de_datos
```

---

### 6.4 Ejemplo completo con `load_dotenv()`

```python
from dotenv import load_dotenv  # Función para cargar variables desde el archivo .env
import os

# Cargar las variables de entorno del archivo .env
load_dotenv()

# Acceder a las variables cargadas
user = os.environ.get("DB_USER")
password = os.environ.get("DB_PASS")
database = os.environ.get("DB_NAME")

print(f"Usuario: {user}")
print(f"Contraseña: {password}")
print(f"Base de datos: {database}")
```

#### Salida esperada:

```
Usuario: admin
Contraseña: 1234
Base de datos: mi_base_de_datos
```

---

1. Busca un archivo `.env` en el directorio actual.
    
2. Lee todas las líneas con formato `CLAVE=VALOR`.
    
3. Inserta esos valores dentro de `os.environ`, de modo que el programa puede acceder a ellas como si vinieran del sistema operativo.
    

---

### 6.5 Parámetros útiles de `load_dotenv()`

#### Especificar la ruta del archivo `.env`

```python
from dotenv import load_dotenv
load_dotenv(dotenv_path="/ruta/a/mi/archivo.env")
```

#### Sobrescribir variables ya definidas

```python
load_dotenv(override=True)
```

Por defecto, `python-dotenv` no reemplaza variables ya existentes.  
Si se usa `override=True`, las sobrescribirá.

---

### 6.6 Buenas prácticas con `.env`

|Práctica|Descripción|
|---|---|
|No subir `.env` a repositorios|Contiene información sensible.|
|Crear un archivo `.env.example`|Muestra qué variables se deben definir sin revelar valores reales.|
|Usar nombres en mayúsculas|Convención estándar (`API_KEY`, `SECRET_KEY`, etc.).|
|Cargar `.env` al inicio del programa|Evita errores por variables no inicializadas.|

---

### 6.7 Ejemplo de uso en una aplicación FastAPI

#### Estructura del proyecto

```
app/
 ├── main.py
 ├── .env
 └── requirements.txt
```

#### Contenido de `.env`

```bash
DATABASE_URL=postgresql://user:pass@localhost:5432/mydb
SECRET_KEY=mi_clave_super_secreta
ENV=development
```

#### Código de `main.py`

```python
from dotenv import load_dotenv
import os
from fastapi import FastAPI

# Cargar variables de entorno al iniciar la aplicación
load_dotenv()

app = FastAPI()

@app.get("/config")
def config():
    # Acceder a las variables de entorno dentro del endpoint
    return {
        "env": os.environ.get("ENV"),
        "db_url": os.environ.get("DATABASE_URL"),
    }
```

De este modo, la aplicación puede cambiar de entorno simplemente modificando las variables del archivo `.env` o configurándolas directamente en el servidor.

---

## 7. Comparación entre `os.environ` y `python-dotenv`

|Característica|`os.environ`|`python-dotenv`|
|---|---|---|
|Origen|Lee las variables del sistema operativo.|Carga variables desde un archivo `.env`.|
|Requiere instalación|No|Sí|
|Persistencia|Temporal al proceso.|Temporal también, pero más práctico para desarrollo.|
|Ideal para|Producción y servidores.|Desarrollo local o entornos de prueba.|

---

## 8. Representación conceptual

```
+----------------------------------------------+
|               Sistema Operativo              |
|----------------------------------------------|
| PATH=/usr/bin:/bin                           |
| HOME=/home/mitchel                           |
| USER=mitchel                                 |
| ENV=production                               |
| API_KEY=xyz123                               |
+--------------------┬-------------------------+
                     │
              Python Script
                     │
                     ▼
         os.environ["API_KEY"]  →  "xyz123"
```

Cuando se usa `load_dotenv()`, el flujo incluye un paso adicional:

```
          ┌─────────────────────────────┐
          │          .env file          │
          │ DB_USER=admin               │
          │ DB_PASS=1234                │
          └────────────┬────────────────┘
                       │ load_dotenv()
                       ▼
             ┌──────────────────────┐
             │ os.environ["DB_USER"]│ → "admin"
             │ os.environ["DB_PASS"]│ → "1234"
             └──────────────────────┘
```

---

## 9. Conclusiones

1. Las **variables de entorno** son una herramienta esencial para mantener la configuración separada del código fuente.
    
2. Permiten que los programas sean **seguros**, **portátiles** y **flexibles**.
    
3. En Python, se acceden a través del módulo **`os`** y pueden gestionarse fácilmente con **`python-dotenv`** durante el desarrollo.
    
4. Su uso adecuado garantiza buenas prácticas en desarrollo de software, especialmente en entornos de despliegue (DevOps, CI/CD, contenedores, etc.).
    

---

## 10. Recomendaciones finales

- Usa `os.environ.get()` en lugar de `os.environ["VAR"]` para evitar errores si una variable no existe.
    
- Mantén el archivo `.env` fuera del control de versiones.
    
- Crea un archivo `.env.example` con las claves necesarias pero sin valores sensibles.
    
- Carga las variables al inicio del programa con `load_dotenv()`.
    
- Utiliza mayúsculas y nombres descriptivos para tus variables.
    

---

**En resumen:**  
El manejo correcto de variables de entorno es una práctica profesional imprescindible en cualquier proyecto de software moderno. En Python, dominar `os.environ` y `python-dotenv` te permitirá construir aplicaciones seguras, configurables y listas para escalar en cualquier entorno.