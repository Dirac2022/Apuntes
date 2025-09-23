
`re` es la biblioteca estándar para trabajar con expresiones regulares en Python. Provee funciones de alto nivel (por ejemplo `re.search`) y la capacidad de compilar patrones en objetos `Pattern` para reutilizar. 
## Uso de strings de patrón: raw strings

Siempre que escribas patrones, usa `r'...'` (raw string) para evitar que Python interprete `\` como secuencia de escape de cadena.
Ejemplo:

```python
pat = r"\d+\.\d+"   # encuentra números con punto decimal
```

Explicación: sin `r` tendrías que escribir `"\\d+\\.\\d+"`, lo que complica la lectura.

## Tipos de retorno claves (resumen antes de entrar a funciones)

Cuando uses `re` verás estos tipos de retorno frecuentemente:

* `Match` o `None`: resultado de `re.search()`, `re.match()`, `re.fullmatch()` (objeto `re.Match` si hay coincidencia, `None` si no).
* `list[str]` o `list[tuple]`: resultado de `re.findall()` (lista de cadenas; si hay grupos de captura, devuelve lista de tuplas).
* `iterator` de `Match`: `re.finditer()` devuelve un iterador que produce objetos `Match`.
* `str`: resultado transformado por `re.sub()`.
* `(str, int)`: `re.subn()` devuelve la cadena resultante y el número de sustituciones.
* `list[str]`: `re.split()` (similar a `str.split`, pero soportando regex), puede devolver elementos que incluyan los separadores si el patrón tiene grupos de captura.
* `Pattern` (objeto): `re.compile()` devuelve un objeto con métodos que replican las funciones de módulo.

Ahora vemos cada función con ejemplos y explicaciones.

---

## `re.compile(pattern, flags=0)`

Crea y devuelve un objeto `Pattern` compilado. `Pattern` tiene atributos útiles (`pattern`, `flags`, `groups`, `groupindex`) y métodos (`search`, `match`, `findall`, `finditer`, `sub`, `subn`, `split`, `fullmatch`), que son equivalentes a las funciones del módulo pero ligados al patrón compilado. Usar `compile` mejora rendimiento cuando reutilizas el mismo patrón muchas veces. ([Python documentation][1])

Qué devuelve: `re.Pattern` (objeto).

Ejemplos:

```python
import re
p = re.compile(r"\b\w+\b")
print(p.findall("hola mundo"))  # ['hola','mundo']
```

Explicación: `p` es reutilizable y más eficiente si llamas repetidamente.

```python
pat = re.compile(r"(\w+)@(\w+\.\w+)")
for email in ["a@x.com","b@y.org"]:
    m = pat.search(email)
    print(m.groups())   # ('a', 'x.com')  luego ('b','y.org')
```

Explicación: compilar el patrón con grupos facilita reusarlo en varias cadenas.

`Pattern` tiene atributos informativos:

* `p.pattern` (str), `p.flags` (int), `p.groups` (número de grupos) y `p.groupindex` (dict de nombres a índices).

Ejemplo:

```python
p = re.compile(r"(?P<name>\w+)@(\w+)", re.I)
print(p.pattern, p.groups, p.groupindex)  # muestra patrón, count de grupos, {'name':1}
```

---

## `re.match(pattern, string, flags=0)`

Busca una coincidencia **solo al inicio** de la cadena. Devuelve `Match` o `None`. Útil para validar prefijos o formatos que deben comenzar al principio.

Ejemplos:

```python
m = re.match(r"\d+", "123abc")
print(bool(m), m.group())  # True, '123'
```

Explicación: coincide porque la cadena empieza por dígitos.

```python
m = re.match(r"\d+", "abc123")
print(m)  # None
```

Explicación: no coincide porque los dígitos no están al inicio.

Consejo: si quieres forzar coincidencia desde inicio pero siendo explícito, puedes usar `\A` en un `search`.

---

## `re.search(pattern, string, flags=0)`

Busca la primera **coincidencia en cualquier parte** de la cadena. Devuelve `Match` o `None`. Es la función más usada cuando quieres localizar un patrón sin importar su posición.

Ejemplos:

```python
m = re.search(r"error: (\d+)", "log: error: 42 en módulo X")
print(m.group(1))  # '42'
```

Explicación: `search` encuentra la primera aparición y puedes acceder a grupos.

```python
m = re.search(r"@(\w+)", "usuario: @maria, otro: @juan")
print(m.group())  # '@maria' (solo la primera)
```

Explicación: `search` devuelve la primera coincidencia; si quieres todas, usa `findall` o `finditer`.

---

## `re.fullmatch(pattern, string, flags=0)`

Coincide solo si **toda** la cadena coincide con el patrón. Devuelve `Match` o `None`. Muy útil para validación estricta (formato exacto de una fecha, email, código, etc.). `fullmatch` apareció para evitar combinaciones con `^` y `\Z`. ([Python documentation][1])

Ejemplos:

```python
re.fullmatch(r"\d{4}-\d{2}-\d{2}", "2025-08-10")  # Match
re.fullmatch(r"\d{4}-\d{2}-\d{2}", "Fecha 2025-08-10")  # None
```

---

## `re.findall(pattern, string, flags=0)`

Devuelve una lista con todas las coincidencias. Si el patrón no tiene grupos, la lista contiene strings con las coincidencias completas. Si el patrón tiene grupos, devuelve una lista de tuplas con las partes capturadas. Es ideal para extraer múltiples fragmentos. Devuelve siempre una `list`.

Ejemplos:

```python
re.findall(r"\d+", "a1b22c333")  # ['1','22','333']
```

Explicación: sin grupos, devuelve substrings coincidentes.

```python
re.findall(r"(\w+)@(\w+\.\w+)", "a@x.com b@y.org")
# [('a','x.com'),('b','y.org')]
```

Explicación: con grupos, devuelve tuplas por cada match.

Consejo: si necesitas posiciones (indices), `findall` no las da; usa `finditer`.

---

## `re.finditer(pattern, string, flags=0)`

Devuelve un iterador que produce objetos `Match`. Es eficiente en memoria para textos grandes y te permite acceder a `start()`/`end()` y grupos. Tipo de retorno: iterator sobre `Match` (p. ej. generador).

Ejemplo:

```python
for m in re.finditer(r"\d+", "a1b22c333"):
    print(m.group(), m.start(), m.end())
```

Explicación: cada `m` es un objeto con información de posición y grupos.

---

## `re.split(pattern, string, maxsplit=0)`

Divide la cadena alrededor de las ocurrencias del patrón. Devuelve `list[str]`. Si el patrón tiene grupos de captura, las subcadenas capturadas también se incluyen en la lista resultante.

Ejemplo:

```python
re.split(r"[;,\s]+", "uno, dos; tres  cuatro")
# ['uno','dos','tres','cuatro']
```

Ejemplo mostrando grupos incluidos:

```python
re.split(r"(-)", "a-b-c")
# ['a','-','b','-','c']
```

Explicación: el carácter separador `-` se incluye porque el patrón tiene un grupo de captura.

`maxsplit` limita el número de divisiones (igual que `str.split`).

---

## `re.sub(pattern, repl, string, count=0, flags=0)`

Reemplaza ocurrencias del patrón por `repl`. `repl` puede ser una cadena o una función que recibe un `Match` y devuelve la cadena de reemplazo. Devuelve `str`.

Ejemplos básicos:

```python
re.sub(r"\d+", "#", "A1B22C333")  # 'A#B#C#'
```

Ejemplo con función (útil si el nuevo texto depende del match):

```python
def doblar(m): return str(int(m.group())*2)
re.sub(r"\d+", doblar, "tengo 3 perros y 4 gatos")  # 'tengo 6 perros y 8 gatos'
```

Explicación: la función recibe el `Match` y puede usar `group()` para construir la sustitución.

Importante: en la cadena `repl` puedes usar backreferences `\1` o la forma recomendada `\g<1>` o `\g<name>` (evita ambigüedades). Ejemplo:

```python
re.sub(r"(\w+) (\w+)", r"\2, \1", "Juan Pérez")  # 'Pérez, Juan'
```

---

## `re.subn(pattern, repl, string, count=0, flags=0)`

Hace lo mismo que `sub` pero además devuelve una tupla `(new_string, number_of_subs)`. Útil cuando quieres saber cuántas sustituciones se hicieron. Devuelve `(str, int)`.

Ejemplo:

```python
re.subn(r"foo", "bar", "foo and foo")  # ('bar and bar', 2)
```

---

## `re.escape(string)`

Escapa todos los caracteres especiales en `string`, de modo que puedan buscarse literalmente en un patrón. Devuelve `str`. Muy útil cuando el patrón incluye texto proveniente de usuarios.

Ejemplo:

```python
re.escape("www.example.com?x=1")  # 'www\\.example\\.com\\?x=1'
```

Explicación: luego puedes usar el resultado en un patrón seguro.

---

## `re.purge()`

Limpia la caché interna de patrones compilados. Normalmente no es necesario, pero existe para control fino.

---

## Objetos `Match`: atributos y métodos importantes

Cuando obtenemos un `Match` (por `search`, `match`, `fullmatch` o `finditer`), ese objeto tiene datos y métodos muy útiles:

* `m.group()` o `m.group(0)`: la coincidencia completa (str).
* `m.group(i)` para `i`≥1: el contenido del i-ésimo grupo de captura.
* `m.groups()`: tupla con todos los grupos (o `()` si no hay).
* `m.groupdict()`: diccionario `{nombre: valor}` para grupos nombrados.
* `m.start(i)`, `m.end(i)`, `m.span(i)`: índices de inicio, fin y tupla `(start,end)` para la i-ésima captura. `m.start()` equivale a `m.start(0)`.
* `m.re`: referencia al objeto `Pattern` usado.
* `m.string`: la cadena original buscada.
* `m.pos`, `m.endpos`: los límites de búsqueda usados cuando el `Pattern` fue aplicado con límites.
* `m.lastindex`: índice (int) del último grupo capturado que participa en la coincidencia (o `None`).
* `m.lastgroup`: nombre del último grupo capturado (si hay nombres).

Ejemplos:

```python
m = re.search(r"(\d+)-(?P<name>\w+)", "123-abc")
print(m.group(1), m.group('name'))  # '123' 'abc'
print(m.span())  # (0,7)
print(m.groupdict())  # {'name': 'abc'}
```

`Match.expand(template)` devuelve una cadena donde referencias `\1`, `\g<1>` o `\g<name>` son reemplazadas por los grupos correspondientes; útil para plantillas complejas.

---

## Flags (banderas) y su efecto

Puedes pasar flags como argumentos a funciones (`re.I`, `re.M`, `re.S`, `re.X`, `re.A`) o incluirlos inline en el patrón con `(?i)` o `(?im)` etc. Algunas banderas importantes:

* `re.I` / `re.IGNORECASE`: ignora mayúsculas/minúsculas.
* `re.M` / `re.MULTILINE`: `^` y `$` funcionan por línea (no solo para toda la cadena).
* `re.S` / `re.DOTALL`: hace que `.` incluya saltos de línea.
* `re.X` / `re.VERBOSE`: permite escribir regex con espacios y comentarios para legibilidad.
* `re.A` / `re.ASCII`: limita `\w`, `\b`, `\d` a ASCII (en vez del comportamiento Unicode por defecto en Python 3).

Ejemplos:

```python
re.findall(r"^foo", "foo\nbar", re.M)  # ['foo']  (multilínea)
re.search(r"(?i)hola", "HOLA amigo")   # match con inline flag
```

Usar `re.VERBOSE` para patrones complejos mejora la mantenibilidad:

```python
pattern = re.compile(r"""
    ^            # inicio
    (\d{4})-     # año-
    (\d{2})-     # mes-
    (\d{2})$     # día
""", re.X)
```

Explicación: comentarios y separaciones hacen el patrón legible.

---

## Errores comunes y excepciones

Si el patrón es inválido, `re.error` (subclase de `Exception`) se lanza al compilar o al usar funciones con patrones inválidos. Siempre maneja (o revisa) excepciones si el patrón viene de entrada no confiable.

---

## Lookarounds (lookahead / lookbehind) en `re`

`re` soporta lookahead positivo `(?=...)`, lookahead negativo `(?!...)`, lookbehind positivo `(?<=...)` y lookbehind negativo `(?<!...)`. Son **assertions** de ancho cero que **no consumen** caracteres: solo verifican contexto. Muy potentes para extracción sin capturar el texto del contexto.

Importante y práctico: el contenido de los lookbehinds en el módulo `re` debe ser de **longitud fija** (el patrón dentro del `(?<=...)` debe poder coincidir solo con cadenas de una longitud conocida). Esta limitación viene del motor de `re`. Si necesitas lookbehinds de longitud variable, considera el paquete `regex` (tercero). ([Python documentation][1], [PyPI][3])

Ejemplo lookahead:

```python
re.findall(r"\d+(?= euros)", "10 euros y 5 dólares")  # ['10']
```

Explicación: devuelve el número si está seguido por " euros" pero no incluye la palabra.

Ejemplo lookbehind (longitud fija):

```python
re.search(r"(?<=#)\w+", "Comentario: #TODO listo").group()  # 'TODO'
```

Explicación: busca una palabra que esté precedida por el carácter `#`.

Advertencia práctica: si intentas algo como `(?<=\w+)X` con `\w+` variable dentro del lookbehind, `re` dará error "look-behind requires fixed-width". Plan B: reescribir con capture groups o usar `regex`. ([Python documentation][1], [learnbyexample.github.io][4])

---

## Rendimiento y backtracking

Las regex con cuantificadores ambiciosos y alternancias mal planteadas pueden producir "catastrophic backtracking", que congela o ralentiza tu programa. Recomendaciones prácticas:

* Prefiere especificidad sobre `.*` cuando sea posible.
* Usa cuantificadores no-greedy `*?`, `+?` con cuidado.
* Compila patrones si los vas a reutilizar intensamente.
* Si necesitas características avanzadas (atomic groups, possessive quantifiers, overlapped matches), mira el paquete `regex`. ([PyPI][3])

Ejemplo de peligro:

```python
re.match(r"^(a+)+b", "a"*30 + "c")  # puede provocar backtracking costoso
```

---

## Herramientas útiles del módulo y prácticas

`re.DEBUG` como flag al compilar imprime información de depuración del patrón; útil cuando estás depurando una regex compleja. `re.escape()` para literalizar entradas de usuarios. `re.purge()` si por alguna razón quieres limpiar la caché interna.

---

## Ejemplos prácticos combinando funciones (recetas)

Normalizar espacios y extraer correos de texto grande:

```python
import re
text = "Contactos: A@X.com;  B@y.org ,, C@Z.net"
emails = re.findall(r"[\w\.-]+@[\w\.-]+\.\w+", text)
cleaned = re.sub(r"\s+", " ", text.strip())
```

Explicación: `findall` extrae todos los correos; `sub` normaliza espacios.

Reemplazo condicional usando función:

```python
import re
def mask(m): return "***" + m.group(0)[-4:]
re.sub(r"\b\d{8,16}\b", mask, "Tarjeta 1234567890123456")  
# 'Tarjeta ***23456' (ejemplo de máscara)
```

Contar ocurrencias y obtener la nueva cadena:

```python
s, n = re.subn(r"foo", "bar", "foo foo baz")
# s='bar bar baz', n=2
```

Extraer palabras y posiciones (finditer):

```python
for m in re.finditer(r"\b\w{4}\b", "Esta lista tiene cuatro letras ok"):
    print(m.group(), m.span())
```

Separar por múltiples delimitadores y conservar separadores:

```python
re.split(r"(\s+|,|;)", "a, b;  c d")  
# devuelve lista que incluye los separadores
```

Validar con `fullmatch`:

```python
def es_fecha(s):
    return bool(re.fullmatch(r"\d{4}-\d{2}-\d{2}", s))
```

---

## Diferencias entre funciones de módulo y métodos de `Pattern`

Las funciones en `re` (`re.search`, `re.findall`, etc.) aceptan un `pattern` que se compila internamente (y se guarda en caché). `Pattern` (resultado de `re.compile`) te deja invocar `p.search(text)` y pasar flags en la compilación, lo que es más claro y eficiente si vas a usar muchas veces el mismo patrón. ([Python documentation][1])

---

## Errores y debugging

Si obtienes `re.error` revisa el patrón (paréntesis desequilibrados, escapes mal colocados, lookbehind variable). Usa `re.DEBUG` o escribe el patrón con `re.VERBOSE` y pequeños tests con `re.search` y `re.finditer`.

---
