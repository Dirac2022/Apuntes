# `os`

Biblioteca estándar que proporciona una forma de interactuar con el sistema operativo. Permite realizar operaciones relacionadas con archivos, directorios y otras características del sistema operativo.

```python
import os
```

## Operaciones con directorios

Obtener el directorio de trabajo actual
```python
print(os.getcwd()) # Muestra el directorio en el que se ejecuta el script
```

Cambiar el directorio de trabajo
```python
os.chdir("/ruta") # Cambia el directorio de trabajo

# Ejemplo
os.chdir("..") # Cambia al directorio padre
os.chdir("../..") # Cambia a dos niveles superiores
```



>[!tip]  Este comando no mueve el archivo donde se tiene el script. Solo cambia el directorio en el que Python busca y manipula archivos mientras se ejecuta el programa.

Listar archivos en un directorio
```python
print(os.listdir(".")) # Lista los archivos y carpetas en el directorio actual
```


Crear y eliminar directorios
```python
os.mkdir("nuevo_directorio") # Crea un directorio nuevo
os.makedirs("dir1/dir2/dir3") # Crea múltiples niveles de directorios
os.rmdir("nuevo_directorio") # Elimina un directorio vacio
os.removedirs("dir1/dir2/dir3") # Elimina multiples directorios vacios
```

## Operaciones con archivos

Eliminar un archivo
```python
os.remove("archivo.txr") # Borra un archivo
```

Renombrar un archivo o directorio
```python
os.rename("old_name.txt", "new_name.txt") # Renombra un archivo
```


## Información del sistema

Obtener el nombre del sistema operativo
```python
print(os.name) # 'posix' en Linux/macOs, 'nt' wn Windows
```

Obtener variables de entorno
```python
print(os.environ) # Muestra todas las variables de entorno
print(os.environ.get("HOME")) # Obtiene el directorio HOME del usuario
```

Ejecutar comandos del sistema
```python
os.python("ls") # Ejecuta 'ls'en Linux/macOS o 'dir' en Windows
```





| Función                      | Descripción                                                                 |
|------------------------------|-----------------------------------------------------------------------------|
| `os.name`                    | Retorna el nombre del sistema operativo (por ejemplo, 'posix', 'nt').      |
| `os.getcwd()`                | Obtiene el directorio actual de trabajo.                                   |
| `os.listdir(ruta)`           | Lista todos los elementos en el directorio especificado (archivos y carpetas).|
| `os.mkdir(ruta)`             | Crea un nuevo directorio en la ruta especificada.                          |
| `os.rmdir(ruta)`             | Elimina un directorio vacío.                                               |
| `os.remove(ruta)`            | Elimina un archivo.                                                        |
| `os.rename(origen, destino)` | Renombra un archivo o directorio.                                          |
| `os.path.join(a, b)`         | Une rutas de directorio de forma segura, respetando el sistema operativo.  |
| `os.path.isfile(ruta)`       | Verifica si la ruta corresponde a un archivo.                              |
| `os.path.isdir(ruta)`        | Verifica si la ruta corresponde a un directorio.                           |

## Ejemplos
Cantidad de archivos en una carpeta

```python
import os

# Ruta de la carpeta
carpeta = "/content/imgs"

# Contar los archivos en la carpeta
num_archivos = len([archivo for archivo in os.listdir(carpeta) if os.path.isfile(os.path.join(carpeta, archivo))])

print(f"Número de archivos en la carpeta '{carpeta}': {num_archivos}")
```

- `os.listdir(carpeta)`: Lista todos los elementos (archivos y carpetas) dentro de la carpeta.
- `os.path.isfile()`:  Verifica si el elemento es un archivo (no una carpeta).
- `os.path.join(carpeta, archivo)`: Crea la ruta completa al archivo.

## `os.path`
Permite  manipular rutas de archivos y directorios de manera independiente del sistema operativo.

### `os.path.exists()`
Devuelve `True` si la ruta existe, ya sea un archivo o una carpeta.
```python
import os

ruta = "nueva_carpeta/datos_respaldo.txt"

if os.path.exists(ruta):
	print("La ruta existe")
else:
	print("La ruta no existe")
```


### Verificar si es un archivo o directorio
-  `os.path.isfile(ruta)` : Retorna `True` si es un archivo
- `os.path.isdir(ruta)` : Retorna `True` si es un directorio

Comprueba si la ruta es un archivo
```python
if os.path.isfile(ruta):
	print("📄 Es un archivo")
elif os.path.isdir(ruta):
	print("📂 Es un directorio")
else:
	print("❌ No existe")
```

### `os.path.abspath()`
Convierte una ruta relativa en absoluta

```python
print(os.path.abspath("archivo.txt")) # Devuelve la ruta absoluta del archivo

ruta_relativa = "nueva_carpeta/datos _respaldo.txt"
ruta_absoluta = os.path.abspath(ruta_relativa)
```


### `os.path.basename(path)`
Devuelve el ultimo componente de la ruta
```python
# Devuelve el nombre del archivo
ruta = "/home/usuario/documentos/archivo.txt"
print(os.path.base(ruta)) # Salida: archivo.txt
```

### `os.path.dirname(path)`
Devuelve solo la parte del directorio, eliminando el archivo o la última carpeta
```python
# Obtiene el directorio
ruta = "/home/usuario/documentos/archivo.txt"
print(os.path.dirname(ruta)) # Salida: /home/usuario/documentos
```

### `os.path.split(path)`
Divide la ruta `path` en `(directorio, ultimo_componente)`
```python
# Separar directorio y archivo
ruta = "/home/usuario/documentos/archivo.txt"
directorio, archivo = os.path.split(ruta)
print(f"📂 Directorio: {directorio}") # /home/usuario/documentos
print(f"📄 Archivo: {archivo}") # archivo.txt
```

### `os.path.splitext()`
Separar nombre y extensión
```python
ruta = "/home/usuario/documentos/archivo.txt"
nombre, extension = os.path.splitext(ruta)
print(f"Nombre: {nombre}") # /home/usuario/documentos/archivo
print(f"Extension: {extension}") # .txt
```


### `os.path.join(*paths)`
Une rutas de forma segura. Evita problemas de separadores ( `/` en Linux/macOS, en `\` Windows).

```python
ruta = os.path.join("carpeta", "subcarpeta" "archivo.txt")
print(ruta)
# 'carpeta/subcarpeta/archivo.txt' en Linux/macOS
# 'carpeta\\subcarpeta\\archivo.txt' en Windows
```

>[!info] funcionamiento
>- `os.path.join()` **une partes de una ruta de forma segura** según el sistema operativo. **No mueve ni crea archivos**, solo genera la ruta correcta. 
>- `os.path.join()` no mueve o crea archivos

### `os.path.getsize()`
Obtiene el tamaño de un archivo
```python
size = os.path.getsize("archivo.txt")
print(f"Tamaño del archivo {size} bytes")
```




