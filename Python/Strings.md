

### `capitalize()`

Convierte el primer carácter de la cadena en mayúscula y los demás en minúsculas.

```python
str.capitalize()
```

- No recibe parámetros
    
- Retorna: nueva cadena con formato capitalizado
    
- Ejemplo:
    

```python
"hola MUNDO".capitalize()  # 'Hola mundo'
```

---

### `casefold()`

Convierte todos los caracteres a minúsculas de forma más agresiva (útil para comparaciones).

```python
str.casefold()
```

- No recibe parámetros
    
- Retorna: nueva cadena en minúsculas
    
- Ejemplo:
    

```python
"Straße".casefold()  # 'strasse'
```

---

### `center(width[, fillchar])`

Centra la cadena en un ancho determinado, rellenando con un carácter si es necesario.

```python
str.center(width[, fillchar])
```

- `width`: ancho total deseado
    
- `[fillchar]`: carácter de relleno (por defecto: espacio `' '`)
    
- Retorna: nueva cadena centrada
    
- Ejemplo:
    

```python
"python".center(10, "*")  # '**python**'
```

---

### `count(sub[, start[, end]])`

Cuenta cuántas veces aparece una subcadena en un rango opcional.

```python
str.count(sub[, start[, end]])
```

- `sub`: subcadena a buscar
    
- `[start]`: índice donde comenzar
    
- `[end]`: índice donde terminar
    
- Retorna: número entero
    
- Ejemplo:
    

```python
"banana".count("an")  # 2
```

---

### `encode([encoding[, errors]])`

Codifica la cadena a bytes usando una codificación específica.

```python
str.encode([encoding[, errors]])
```

- `[encoding]`: tipo de codificación (por defecto: `'utf-8'`)
    
- `[errors]`: estrategia de manejo de errores (`'strict'`, `'ignore'`, `'replace'`, etc.)
    
- Retorna: objeto `bytes`
    
- Ejemplo:
    

```python
"café".encode("utf-8")  # b'caf\xc3\xa9'
```

---

### `endswith(suffix[, start[, end]])`

Comprueba si la cadena termina con una subcadena.

```python
str.endswith(suffix[, start[, end]])
```

- `suffix`: subcadena o tupla de subcadenas
    
- `[start]`: índice de inicio
    
- `[end]`: índice final
    
- Retorna: `True` o `False`
    
- Ejemplo:
    

```python
"archivo.txt".endswith(".txt")  # True
```

---

### `expandtabs([tabsize])`

Reemplaza los tabuladores (`\t`) por espacios.

```python
str.expandtabs([tabsize])
```

- `[tabsize]`: número de espacios por tabulación (por defecto: 8)
    
- Retorna: nueva cadena con tabs expandidos
    
- Ejemplo:
    

```python
"uno\tdos".expandtabs(4)  # 'uno dos'
```

---

### `find(sub[, start[, end]])`

Devuelve el índice de la primera aparición de `sub`, o `-1` si no se encuentra.

```python
str.find(sub[, start[, end]])
```

- `sub`: subcadena a buscar
    
- `[start]`: índice de inicio
    
- `[end]`: índice final
    
- Retorna: índice o `-1`
    
- Ejemplo:
    

```python
"buscar aquí".find("aquí")  # 7
```

---

### `format(*args, **kwargs)`

Formatea una cadena con valores posicionales o nombrados.

```python
str.format(*args, **kwargs)
```

- `*args`: valores posicionales
    
- `**kwargs`: valores con nombre
    
- Retorna: nueva cadena formateada
    
- Ejemplo:
    

```python
"Hola, {nombre}".format(nombre="Ana")  # 'Hola, Ana'
```

---

### `index(sub[, start[, end]])`

Como `find()`, pero lanza `ValueError` si no encuentra `sub`.

```python
str.index(sub[, start[, end]])
```

- `sub`: subcadena a buscar
    
- `[start]`: índice inicial
    
- `[end]`: índice final
    
- Retorna: índice (entero)
    
- Ejemplo:
    

```python
"python".index("th")  # 2
```

---

### `isalnum()`

Comprueba si todos los caracteres son alfanuméricos.

```python
str.isalnum()
```

- No recibe parámetros
    
- Retorna: `True` o `False`
    
- Ejemplo:
    

```python
"abc123".isalnum()  # True
```

---

### `isalpha()`

Comprueba si todos los caracteres son letras.

```python
str.isalpha()
```

- No recibe parámetros
    
- Retorna: `True` o `False`
    
- Ejemplo:
    

```python
"Python".isalpha()  # True
```

---

### `isdigit()`

Comprueba si todos los caracteres son dígitos.

```python
str.isdigit()
```

- No recibe parámetros
    
- Retorna: `True` o `False`
    
- Ejemplo:
    

```python
"1234".isdigit()  # True
```

---

### `islower()`

Verifica si todos los caracteres alfabéticos están en minúsculas.

```python
str.islower()
```

- No recibe parámetros
    
- Retorna: `True` o `False`
    
- Ejemplo:
    

```python
"hola".islower()  # True
```

---

### `isupper()`

Verifica si todos los caracteres alfabéticos están en mayúsculas.

```python
str.isupper()
```

- No recibe parámetros
    
- Retorna: `True` o `False`
    
- Ejemplo:
    

```python
"PYTHON".isupper()  # True
```

---

### `isspace()`

Comprueba si todos los caracteres son espacios, tabs o saltos de línea.

```python
str.isspace()
```

- No recibe parámetros
    
- Retorna: `True` o `False`
    
- Ejemplo:
    

```python
" \t\n".isspace()  # True
```

---

### `istitle()`

Verifica si la cadena está en formato título.

```python
str.istitle()
```

- No recibe parámetros
    
- Retorna: `True` o `False`
    
- Ejemplo:
    

```python
"Hola Mundo".istitle()  # True
```

---

### `join(iterable)`

Une los elementos del iterable con la cadena como separador.

```python
str.join(iterable)
```

- `iterable`: secuencia de strings
    
- Retorna: nueva cadena unida
    
- Ejemplo:
    

```python
"-".join(["uno", "dos", "tres"])  # 'uno-dos-tres'
```

---

### `lower()`

Convierte todos los caracteres alfabéticos a minúsculas.

```python
str.lower()
```

- No recibe parámetros
    
- Retorna: nueva cadena
    
- Ejemplo:
    

```python
"HELLO".lower()  # 'hello'
```

---

### `upper()`

Convierte todos los caracteres alfabéticos a mayúsculas.

```python
str.upper()
```

- No recibe parámetros
    
- Retorna: nueva cadena
    
- Ejemplo:
    

```python
"hola".upper()  # 'HOLA'
```


---

### `lstrip([chars])`

Elimina espacios en blanco (u otros caracteres especificados) desde el inicio de la cadena.

```python
str.lstrip([chars])
```

- `[chars]`: caracteres a eliminar (por defecto: espacios en blanco)
    
- Retorna: nueva cadena sin los caracteres al inicio
    
- Ejemplo:
    

```python
"   hola".lstrip()  # 'hola'
```

---

### `rstrip([chars])`

Elimina espacios en blanco (u otros caracteres) desde el final de la cadena.

```python
str.rstrip([chars])
```

- `[chars]`: caracteres a eliminar (por defecto: espacios en blanco)
    
- Retorna: nueva cadena sin los caracteres al final
    
- Ejemplo:
    

```python
"hola   ".rstrip()  # 'hola'
```

---

### `strip([chars])`

Elimina espacios en blanco (u otros caracteres) al inicio y al final de la cadena.

```python
str.strip([chars])
```

- `[chars]`: caracteres a eliminar (por defecto: espacios en blanco)
    
- Retorna: nueva cadena sin los caracteres alrededor
    
- Ejemplo:
    

```python
"  hola  ".strip()  # 'hola'
```

---

### `partition(sep)`

Divide la cadena en una tupla de tres elementos: antes, separador, después.

```python
str.partition(sep)
```

- `sep`: subcadena separadora obligatoria
    
- Retorna: tupla `(antes, sep, después)`
    
- Ejemplo:
    

```python
"clave=valor".partition("=")  # ('clave', '=', 'valor')
```

---

### `replace(old, new[, count])`

Reemplaza todas (o algunas) ocurrencias de una subcadena por otra.

```python
str.replace(old, new[, count])
```

- `old`: subcadena a reemplazar
    
- `new`: subcadena nueva
    
- `[count]`: máximo de reemplazos (por defecto: todos)
    
- Retorna: nueva cadena con reemplazos
    
- Ejemplo:
    

```python
"banana".replace("a", "o", 2)  # 'bonona'
```

---

### `split([sep[, maxsplit]])`

Divide la cadena en una lista, usando un separador (espacios por defecto).

```python
str.split([sep[, maxsplit]])
```

- `[sep]`: separador (por defecto: espacios)
    
- `[maxsplit]`: número máximo de divisiones
    
- Retorna: lista de subcadenas
    
- Ejemplo:
    

```python
"uno,dos,tres".split(",")  # ['uno', 'dos', 'tres']
```

---

### `rsplit([sep[, maxsplit]])`

Igual que `split()`, pero comienza desde el final de la cadena.

```python
str.rsplit([sep[, maxsplit]])
```

- `[sep]`: separador
    
- `[maxsplit]`: máximo de divisiones (desde la derecha)
    
- Retorna: lista de subcadenas
    
- Ejemplo:
    

```python
"uno,dos,tres".rsplit(",", 1)  # ['uno,dos', 'tres']
```

---

### `splitlines([keepends])`

Divide una cadena en líneas, separando por saltos de línea.

```python
str.splitlines([keepends])
```

- `[keepends]`: si `True`, conserva los saltos de línea
    
- Retorna: lista de líneas
    
- Ejemplo:
    

```python
"línea1\nlínea2".splitlines()  # ['línea1', 'línea2']
```

---

### `startswith(prefix[, start[, end]])`

Verifica si la cadena comienza con una subcadena.

```python
str.startswith(prefix[, start[, end]])
```

- `prefix`: subcadena o tupla de subcadenas
    
- `[start]`: índice de inicio
    
- `[end]`: índice de fin
    
- Retorna: `True` o `False`
    
- Ejemplo:
    

```python
"hola mundo".startswith("hola")  # True
```

---

### `zfill(width)`

Rellena la cadena con ceros a la izquierda hasta alcanzar el ancho `width`.

```python
str.zfill(width)
```

- `width`: ancho mínimo deseado de la cadena
    
- Retorna: nueva cadena con ceros agregados al principio
    
- Ejemplo:
    

```python
"42".zfill(5)  # '00042'
```

---
