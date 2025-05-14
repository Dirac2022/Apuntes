

Las expresiones regulares son patrones que describen conjuntos de cadenas de texto. Se usan para buscar, validar, extraer o manipular texto basándose en esos patrones. Funcionan en casi todos los lenguajes de programación con una sintaxis muy similar.

# Componentes básicos de una expresión regular

**1. Literales**
Son caracteres normales que coinciden con ellos mismos.

- Ejemplo:
    - `/abc/` coincide con la cadena "abc".

**2. Metacaracteres**

Son caracteres con significado especial en regex:

|Metacarácter|Descripción|
|---|---|
|`.`|Coincide con cualquier carácter excepto salto de línea|
|`^`|Inicio de la cadena|
|`$`|Final de la cadena|
|`*`|0 o más repeticiones del elemento anterior|
|`+`|1 o más repeticiones del elemento anterior|
|`?`|0 o 1 repetición del elemento anterior|
|`\`|Escapa un metacarácter para que sea literal|
|`[]`|Define una clase de caracteres|
|`|`|
|`()`|Agrupación y captura|

# Clases de caracteres

- `[abc]` coincide con cualquiera de los caracteres a, b o c.
- `[a-z]` coincide con cualquier letra minúscula.
- `[A-Z]` coincide con cualquier letra mayúscula.
- `[0-9]` coincide con cualquier dígito.
- `[^abc]` coincide con cualquier carácter excepto a, b o c.

# Cuantificadores

Indican cuántas veces debe repetirse un elemento.

- `*` — 0 o más veces.
- `+` — 1 o más veces.
- `?` — 0 o 1 vez.
- `{n}` — Exactamente n veces.
- `{n,}` — Al menos n veces.
- `{n,m}` — Entre n y m veces.

Ejemplo:

- `/a{2,4}/` coincide con "aa", "aaa" o "aaaa".

# Anclas

- `^` — Coincide con el inicio de la cadena.
- `$` — Coincide con el final de la cadena.

Ejemplo:

- `/^Hola/` coincide con cadenas que empiezan con "Hola".
- `/mundo$/` coincide con cadenas que terminan con "mundo".

# Grupos y Capturas

- `(abc)` agrupa los caracteres y captura la coincidencia.
- `(?:abc)` agrupa sin capturar.

Ejemplo:

- `/(\d{3})-(\d{2})-(\d{4})/` puede capturar partes de un número de seguridad social.

# Caracteres especiales predefinidos

|Símbolo|Significado|
|---|---|
|`\d`|Dígito, equivalente a `[0-9]`|
|`\D`|No dígito|
|`\w`|Carácter de palabra (letras, dígitos, guion bajo)|
|`\W`|No carácter de palabra|
|`\s`|Espacio en blanco (tab, espacio, salto de línea)|
|`\S`|No espacio en blanco|

# Modificadores comunes

Estos modificadores cambian el comportamiento de la expresión regular:

| Modificador | Descripción                                                            |
| ----------- | ---------------------------------------------------------------------- |
| `i`         | Ignora mayúsculas y minúsculas                                         |
| `g`         | Búsqueda global (todas las coincidencias)                              |
| `m`         | Multilínea, hace que `^` y `$` coincidan al inicio y fin de cada línea |

Ejemplo en JavaScript:

```js
/abc/i.test("ABC") // true
```
# Ejemplos prácticos

**Validar un correo electrónico simple**

```text
^[a-zA-Z0-9._%-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6}$
```

- `^` inicio de cadena
- `[a-zA-Z0-9._%-]+` uno o más caracteres válidos para usuario
- `@` símbolo arroba literal
- `[a-zA-Z0-9.-]+` dominio
- `\.` punto literal
- `[a-zA-Z]{2,6}` extensión de 2 a 6 letras
- `$` fin de cadena

**Buscar números de teléfono (formato simple)**

```text
^\+?\d{1,3}?[-.\s]?\(?\d{1,4}?\)?[-.\s]?\d{1,4}[-.\s]?\d{1,9}$
```

**Extraer palabras de un texto**

```text
\w+
```

Coincide con cada palabra compuesta por letras, números o guiones bajos.

**Reemplazar espacios múltiples por uno solo**

```text
\s+
```

# Uso general en cualquier lenguaje

- Las expresiones regulares se escriben igual, solo cambia la forma de declararlas y usarlas en cada lenguaje.
- En JavaScript se usan entre barras `/expresion/` o con `RegExp`.
- En Python se usan con el módulo `re` y cadenas raw `r"expresion"`.
- En Java se usan con la clase `Pattern`.

# Resumen

|Concepto|Ejemplo|Descripción|
|---|---|---|
|Literal|`abc`|Coincide con "abc"|
|Punto|`a.c`|"a" seguido de cualquier carácter y "c"|
|Clase de caracteres|`[a-z]`|Cualquier letra minúscula|
|Cuantificador|`a+`|Una o más "a"|
|Ancla|`^Hola`|Empieza con "Hola"|
|Grupo|`(abc)`|Agrupa y captura "abc"|
|Predefinidos|`\d`, `\w`, `\s`|Dígito, palabra, espacio|
|Modificadores|`i`, `g`, `m`|Ignorar mayúsculas, global, multilínea|

