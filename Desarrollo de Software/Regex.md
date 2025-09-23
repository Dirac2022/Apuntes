
Perfecto, entiendo lo que quieres: no solo una lista rápida de definiciones, sino **una explicación rica en teoría, contexto, ejemplos y matices**, para que incluso un principiante pueda interiorizar el concepto y un futuro experto sepa aplicarlo en escenarios reales.

Voy a rehacer la clase de regex **sin enumeraciones**, pero con explicaciones extensas, ejemplos variados y comentarios que conecten la teoría con el uso profesional.
Voy a desarrollar cada tema con más detalle, como si fuera una **clase universitaria** donde no solo te digo *qué es*, sino *por qué es así*, *qué errores evitar*, *cómo se usa en la práctica* y *qué variaciones existen entre Python y JavaScript*.

---

# 📚 Clase Magistral de Expresiones Regulares (Regex)

## Introducción

Las expresiones regulares, o *regex*, son un **mini lenguaje especializado** para describir patrones dentro de texto.
Si lo piensas, una regex es como una "plantilla de búsqueda" muy flexible que no se limita a letras exactas, sino que describe **formas y estructuras** de texto.

Por ejemplo, si buscas un número de teléfono, puedes describirlo como:

* Tres dígitos
* Un guion
* Otros tres dígitos
* Otro guion
* Y finalmente cuatro dígitos

Con regex, eso sería algo como:

```
\d{3}-\d{3}-\d{4}
```

y podría encontrar `123-456-7890` en medio de un texto, sin importar qué más haya alrededor.

Lo poderoso de regex es que puedes:

* Buscar patrones complejos sin escribir bucles.
* Validar que un texto cumpla un formato.
* Extraer datos muy específicos de grandes volúmenes de texto.
* Reemplazar partes de un texto de forma masiva y controlada.

En Python, las regex se trabajan con el módulo `re`, y en JavaScript con el objeto `RegExp`. La sintaxis base es muy similar en ambos, aunque hay diferencias sutiles que veremos más adelante.

Ejemplo en Python:

```python
import re
re.findall(r"\d+", "Tengo 2 gatos y 14 peces")  
# ['2', '14']
```

Ejemplo equivalente en JavaScript:

```javascript
console.log("Tengo 2 gatos y 14 peces".match(/\d+/g)); // ["2", "14"]
```

En ambos casos `\d+` significa: "uno o más dígitos".

---

## Metacaracteres y caracteres especiales

En regex, hay símbolos con significado especial llamados **metacaracteres**. Son como "palabras clave" en un lenguaje de programación, pero aquí indican *cómo* buscar.

Ejemplos importantes:

* `.` → Cualquier carácter excepto salto de línea.
* `\d` → Un dígito (0-9).
* `\w` → Un carácter de palabra: letras, dígitos o guion bajo.
* `\s` → Un espacio en blanco (incluye tabs y saltos de línea).

Un detalle importante:
Si quieres buscar un carácter que normalmente es un metacaracter (como un punto `.` literal), debes **escaparlo** con `\`.
Por ejemplo, `\.` busca un punto real, no cualquier carácter.

Esto es útil porque, por ejemplo, `www.example.com` con regex `www\.example\.com` asegura que buscas exactamente esa dirección, no algo como `wwwXexampleXcom`.

---

## Cuantificadores y rangos

Los cuantificadores indican **cuántas veces** debe aparecer algo.

Ejemplos:

* `+` → Una o más veces.
* `*` → Cero o más veces.
* `?` → Cero o una vez.
* `{n}` → Exactamente n veces.
* `{n,}` → Al menos n veces.
* `{n,m}` → Entre n y m veces.

Los rangos permiten especificar un conjunto de caracteres aceptables:

* `[abc]` → a, b o c.
* `[0-9]` → cualquier dígito.
* `[A-Za-z]` → cualquier letra.

En la práctica:

```python
import re
re.findall(r"[A-Z]{2}\d{4}", "AB1234, XY9999, C123")
# ['AB1234', 'XY9999']
```

Aquí buscamos dos letras mayúsculas seguidas de cuatro dígitos.

En JavaScript:

```javascript
console.log("AB1234 XY9999 C123".match(/[A-Z]{2}\d{4}/g));
// ["AB1234", "XY9999"]
```

---

## Grupos y subgrupos

Los paréntesis `()` son fundamentales porque permiten:

* **Agrupar** partes de un patrón para aplicarle cuantificadores a todo el grupo.
* **Capturar** la parte encontrada para usarla después.

Ejemplo simple:

```python
m = re.search(r"(\d{4})-(\d{2})-(\d{2})", "Fecha: 2025-08-10")
print(m.groups())  # ('2025', '08', '10')
```

Aquí extraemos año, mes y día por separado.

También existen:

* **Grupos sin captura** `(?:...)` → útiles cuando quieres agrupar pero no guardar.
* **Grupos con nombre** `(?P<nombre>...)` en Python, `(?<nombre>...)` en JavaScript → permiten referirte a partes del patrón por nombre.

Ejemplo con nombre en JavaScript:

```javascript
let m = "2025-08-10".match(/(?<año>\d{4})-(?<mes>\d{2})-(?<día>\d{2})/);
console.log(m.groups.año); // 2025
```

---

## Alternancia

El operador `|` indica que cualquiera de las opciones es válida.

```python
re.findall(r"gato|perro", "Tengo un perro y un gato")
# ['perro', 'gato']
```

Esto es equivalente a decir: "busca 'gato' o 'perro'".

---

## Anclas

Las anclas no representan caracteres, sino **posiciones**:

* `^` → Inicio de la cadena.
* `$` → Fin de la cadena.
* `\b` → Límite de palabra (entre un carácter de palabra y un no-caracter de palabra).
* `\B` → No-límite de palabra.

Ejemplo:

```javascript
console.log(/^Hola/.test("Hola mundo")); // true
console.log(/^Hola/.test("Adiós Hola")); // false
```

Aquí `^Hola` solo es verdadero si "Hola" está al inicio.

---

## Lookaheads y lookbehinds

Aquí viene uno de los conceptos más potentes y menos entendidos.

Los **lookaheads** y **lookbehinds** son *assertions* que dicen "esto debe (o no) estar aquí", pero **no consumen caracteres**.
Es decir, no forman parte del resultado, solo imponen una condición.

Tipos:

* **Lookahead positivo** `(?=...)` → asegura que después de lo que llevamos debe venir el patrón.
* **Lookahead negativo** `(?!...)` → asegura que después **no** venga el patrón.
* **Lookbehind positivo** `(?<=...)` → asegura que antes de lo que llevamos estaba el patrón.
* **Lookbehind negativo** `(?<!...)` → asegura que antes **no** estaba el patrón.

Ejemplo lookahead positivo:

```python
re.findall(r"\d+(?= euros)", "10 euros y 5 dólares")
# ['10']
```

Aquí encontramos el número solo si va seguido de la palabra " euros".

Ejemplo lookbehind positivo:

```javascript
console.log("abc123".match(/(?<=abc)\d+/)); // ["123"]
```

Aquí el número se devuelve solo si está precedido por "abc".

**Aplicación profesional:**
Se usan mucho para extracción precisa de datos. Por ejemplo, si tienes un log donde quieres todos los errores con código que empieza en "ERR" pero sin capturar el texto "ERR", un lookbehind sería perfecto.

---

## Flags

Los flags modifican el comportamiento:

* `i` → Ignora mayúsculas/minúsculas.
* `m` → Multilínea: `^` y `$` se aplican a cada línea, no solo al inicio/fin del texto.
* `s` → Hace que `.` incluya saltos de línea.
* `g` (JavaScript) → Encuentra todas las coincidencias.

Ejemplo en Python:

```python
re.findall(r"hola", "Hola HOLA hola", re.I)
# ['Hola', 'HOLA', 'hola']
```

Ejemplo en JavaScript:

```javascript
console.log("Hola hola".match(/hola/gi)); // ["Hola", "hola"]
```

---

## Patrones avanzados y optimización

* Usa grupos no capturantes `(?:...)` si no necesitas almacenar coincidencias.
* Especifica límites para evitar que `.*` capture demasiado.
* Escapa metacaracteres si quieres usarlos literalmente.

Ejemplo optimizado en Python:

```python
re.findall(r"(?:http|https)://\S+", "Visita https://example.com y http://test.com")
```

---

## Buenas prácticas

* Empieza con patrones simples y prueba.
* Usa `re.compile()` para rendimiento en Python cuando reutilices un patrón.
* Testea patrones en [regex101.com](https://regex101.com).
* No abuses de patrones demasiado generales.

---


