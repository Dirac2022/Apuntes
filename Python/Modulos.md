
# `os`

Biblioteca estándar que proporciona una forma de interactuar con el sistema operativo. Permite realizar operaciones relacionadas con archivos, directorios y otras características del sistema operativo.

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


# `pickle`

## Serialización
En Python, la **serialización** se refiere al proceso de convertir un objeto en una secuencia de bytes que puede ser almacenada en un archivo, transmitida por la red, o guardada en una base de datos. Este proceso es esencial cuando se necesita guardar el estado de un objeto para su posterior recuperación.
## Pickle en el Contexto de Python y Serialización
El módulo de Python que facilita la serialización y deserialización de objetos se llama **`pickle`**.
Este es un módulo estándar de Python que proporciona la capacidad de serializar y deserializar estructuras complejas de datos en Python. Al "serializar" un objeto, `pickle` convierte ese objeto en una cadena de bytes (llamado *stream* o *byte stream*), que puede ser fácilmente almacenada o transmitida. La "deserialización" convierte esa secuencia de bytes de vuelta al objeto original.

## Funciones Principales de `pickle`

1. **`pickle.dump(obj, file)`**
   - Serializa el objeto `data` y lo escribe en el archivo `file`.
   - Ejemplo:
   ```python
   import pickle

   data = {"nombre": "Juan", "edad": 30}
   with open("datos.pkl", "wb") as file:
       pickle.dump(data, file)
   ```

2. **`pickle.load(file)`**
   - Lee un archivo `datos.pkl` que contiene un objeto serializado y lo deserializa, reconstruyendo el objeto original en memoria.
   - Ejemplo:
   ```python
   import pickle

   with open("datos.pkl", "rb") as file:
       data = pickle.load(file)
       print(data)  # Salida: {'nombre': 'Juan', 'edad': 30}
   ```

3. **`pickle.dumps(obj)`**
   - Serializa el objeto `data` y devuelve la representación en bytes (sin necesidad de escribirlo en un archivo).
   - Ejemplo:
   ```python
   import pickle

   data = {"nombre": "Juan", "edad": 30}
   bytes_data = pickle.dumps(data)
   print(bytes_data)
   ```

4. **`pickle.loads(bytes)`**
   - Deserializa un objeto desde una secuencia de bytes previamente serializada con `dumps`.
   - Ejemplo:
   ```python
   import pickle

   bytes_data = b'\x80\x04\x95...\x94.'
   data = pickle.loads(bytes_data)
   print(data)  # Salida: {'nombre': 'Juan', 'edad': 30}
   ```

### Ventajas y Desventajas de `pickle`

#### Ventajas:
- **Versatilidad:** Puede manejar una amplia gama de tipos de datos de Python, incluyendo listas, diccionarios, objetos de clases personalizadas, etc.
- **Fácil de usar:** La interfaz de `pickle` es simple y directa, lo que facilita su uso para la serialización de objetos.

#### Desventajas:
- **Compatibilidad:** Los objetos serializados con `pickle` pueden no ser compatibles entre diferentes versiones de Python. Esto significa que un objeto serializado en Python 3.9 puede no ser deserializable en Python 3.8.
- **Seguridad:** Deserializar datos de fuentes no confiables usando `pickle` es peligroso, ya que puede ejecutar código arbitrario. Es crucial usar `pickle` solo con datos de fuentes confiables.
- **Portabilidad:** Los archivos generados por `pickle` están diseñados específicamente para Python y no son fácilmente portables a otros lenguajes de programación.