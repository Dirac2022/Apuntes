
# `Path`

`Path` es una clase del módulo estándar `pathlib` de Python que permite **trabajar con rutas de archivos y directorios de forma orientada a objetos**, en lugar de manejar simples strings.  
Su gran ventaja es que abstrae las diferencias entre sistemas operativos (Windows usa `\`, Linux/Mac `/`).

```python
from pathlib import Path
```


## Creación de objetos `Path`

Un `Path` representa una ruta en el sistema de archivos. Puede apuntar a un archivo o a un directorio.

```python
Path(path_string)
```

- `path_string`: (str o Path-like) ruta absoluta o relativa.
- Retorno: objeto `Path`.

**Ejemplo**

```python
p1 = Path("mi_carpeta/archivo.txt")   # ruta relativa
p2 = Path("/home/usuario")           # ruta absoluta
print(p1, type(p1))  # mi_carpeta/archivo.txt <class 'pathlib.PosixPath'>
```

---

## `exists()`

Verifica si la ruta existe en el sistema.

```python
Path.exists()
```

- Parámetros: ninguno.
- Retorno: `bool`.

**Ejemplo:**

```python
p = Path("mi_carpeta")
print(p.exists())  # True si existe, False si no
```


## `is_file()` y `is_dir()`

Verifican si la ruta es un archivo o un directorio.

```python
Path.is_file()
Path.is_dir()
```

- Parámetros: ninguno.
- Retorno: `bool`.

**Ejemplo:**

```python
archivo = Path("mi_carpeta/archivo.txt")
print(archivo.is_file())  # True si es archivo

carpeta = Path("mi_carpeta")
print(carpeta.is_dir())   # True si es carpeta
```


## `mkdir()`

Crear carpetas

```python
Path.mkdir(parents=False, exist_ok=False)
```

- `parents`: (bool) crea directorios intermedios si no existen.
- `exist_ok`: (bool) no lanza error si ya existe.
- Retorno: `None`.

**Ejemplo:**

```python
p = Path("nueva_carpeta")
p.mkdir(exist_ok=True)  # crea carpeta si no existe
```


## `touch()`

Crear archivos

```python
Path.touch(exist_ok=True)
```

- `exist_ok`: (bool) evita error si ya existe.
- Retorno: `None`.

**Ejemplo:**

```python
f = Path("nueva_carpeta/archivo.txt")
f.touch()  # crea archivo vacío
```


## `rename()`

Renombrar

```python
Path.rename(target)
```

- `target`: (str o Path) nuevo nombre o ruta destino.
- Retorno: nuevo objeto `Path`.

**Ejemplo:**

```python
f = Path("nueva_carpeta/archivo.txt")
f.rename("nueva_carpeta/renombrado.txt")
```

### `replace()`

Mover

```python
Path.replace(target)
```

- `target`: (str o Path) ruta destino.
- Retorno: nuevo objeto `Path`.

**Ejemplo:**

```python
f = Path("nueva_carpeta/renombrado.txt")
f.replace("otra_carpeta/renombrado.txt")  # mueve el archivo
```


## Copiar archivos (indirecto con `shutil.copy`)

`Path` no tiene un método `copy`, se usa `shutil`.

**Ejemplo:**

```python
import shutil

src = Path("otra_carpeta/renombrado.txt")
dst = Path("copia_carpeta/renombrado.txt")

shutil.copy(src, dst)  # copia archivo
```

Para copiar carpetas:

```python
shutil.copytree("carpeta_original", "carpeta_copia", dirs_exist_ok=True)
```

---

## Borrar archivos y carpetas

- **Archivos:** `Path.unlink()`
- **Carpetas vacías:** `Path.rmdir()`
- **Carpetas con contenido:** `shutil.rmtree()`

**Ejemplo:**

```python
f = Path("otra_carpeta/renombrado.txt")
if f.exists():
    f.unlink()  # elimina archivo
```

---

## Leer y escribir archivos

- `read_text()` → devuelve contenido como `str`.
- `write_text(data)` → escribe texto en archivo.

**Firma:**

```python
Path.read_text(encoding=None)
Path.write_text(data, encoding=None)
```

- `data`: (str) texto a escribir.
- `encoding`: (str) como `"utf-8"`.
- Retorno: `str` en lectura, `int` en escritura (número de caracteres).

**Ejemplo:**

```python
f = Path("nueva_carpeta/datos.txt")
f.write_text("Hola Mundo", encoding="utf-8")
print(f.read_text(encoding="utf-8"))
```

---

## Ejemplo

Supongamos que queremos:

1. Crear una carpeta de trabajo.
2. Crear un archivo dentro.
3. Escribirle contenido.
4. Copiarlo a otra carpeta.
5. Renombrar el archivo copiado.
6. Borrarlo.

```python
from pathlib import Path
import shutil

# 1. Crear carpeta principal
work_dir = Path("proyecto")
work_dir.mkdir(exist_ok=True)

# 2. Crear archivo
archivo = work_dir / "reporte.txt"
archivo.touch()

# 3. Escribir contenido
archivo.write_text("Este es mi reporte.", encoding="utf-8")

# 4. Copiar archivo a otra carpeta
backup_dir = Path("backup")
backup_dir.mkdir(exist_ok=True)
shutil.copy(archivo, backup_dir / "reporte.txt")

# 5. Renombrar archivo copiado
copia = backup_dir / "reporte.txt"
copia.rename(backup_dir / "reporte_final.txt")

# 6. Borrar archivo renombrado
(backup_dir / "reporte_final.txt").unlink()
```

