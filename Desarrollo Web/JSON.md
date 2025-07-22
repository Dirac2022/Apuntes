
## Introducción a JSON

JSON (JavaScript Object Notation) es un formato de intercambio de datos ligero, fácil de leer y escribir para humanos, y sencillo de parsear y generar para máquinas. Se utiliza ampliamente en aplicaciones web para transmitir datos entre servidores y clientes.

## Características principales

1. **Ligero**: Ocupa menos espacio que otros formatos como XML
2. **Legible**: Fácil de entender para humanos
3. **Independiente del lenguaje**: Aunque proviene de JavaScript, puede usarse con cualquier lenguaje
4. **Estructura jerárquica**: Permite organizar datos de forma anidada

## Sintaxis Básica

### Estructura general

JSON se compone de dos estructuras principales:
1. **Pares clave-valor** (como objetos)
2. **Listas ordenadas de valores** (como arrays)

### Tipos de datos permitidos

1. **Strings**: Texto entre comillas dobles
   - Ejemplo: `"nombre"`
2. **Numbers**: Números enteros o decimales
   - Ejemplo: `42` o `3.14`
3. **Booleans**: `true` o `false`
4. **null**: Representa un valor nulo
5. **Objects**: Conjuntos de pares clave-valor entre llaves `{}`
6. **Arrays**: Listas ordenadas entre corchetes `[]`

## Sintaxis Detallada

### 1. Objetos JSON

Los objetos se definen entre llaves `{}` y contienen pares clave-valor separados por comas.

```json
{
  "clave1": "valor1",
  "clave2": "valor2",
  "clave3": "valor3"
}
```

**Reglas importantes**:
- Las claves deben ser strings (entre comillas dobles)
- Los valores pueden ser cualquier tipo de dato válido en JSON
- Los pares clave-valor se separan por dos puntos `:`
- No puede haber comas finales después del último elemento

### 2. Arrays JSON

Los arrays se definen entre corchetes `[]` y contienen valores separados por comas.

```json
["valor1", "valor2", "valor3"]
```

Los arrays pueden contener cualquier tipo de dato, incluyendo objetos y otros arrays.

### 3. Strings

- Deben estar entre comillas dobles `""` (no se aceptan comillas simples)
- Caracteres especiales deben escaparse con `\`:
  - `\"` para comillas dobles
  - `\\` para barra invertida
  - `\/` para slash
  - `\b` para backspace
  - `\f` para form feed
  - `\n` para nueva línea
  - `\r` para retorno de carro
  - `\t` para tabulación
- Se pueden usar caracteres Unicode con `\u` seguido de 4 dígitos hexadecimales

### 4. Numbers

- No llevan comillas
- Pueden ser enteros o decimales
- Pueden usar notación exponencial
- Ejemplos válidos:
  - `42`
  - `3.14159`
  - `-273.15`
  - `1.2e10`
  - `1.2E-5`

### 5. Valores booleanos y null

- `true`: valor verdadero
- `false`: valor falso
- `null`: valor nulo o vacío

## Ejemplo Completo

```json
{
  "empleado": {
    "nombre": "Juan Pérez",
    "edad": 35,
    "activo": true,
    "dirección": {
      "calle": "Av. Principal 123",
      "ciudad": "Ciudad de México",
      "códigoPostal": "12345"
    },
    "teléfonos": [
      {
        "tipo": "casa",
        "número": "555-123-4567"
      },
      {
        "tipo": "trabajo",
        "número": "555-987-6543"
      }
    ],
    "hijos": [],
    "puesto": "Desarrollador Senior",
    "salario": 75000.50,
    "skills": ["JavaScript", "Python", "SQL", "JSON"],
    "fechaContratación": "2015-06-15",
    "notas": null
  }
}
```

## Reglas y Buenas Prácticas

1. **Codificación**: JSON debe estar codificado en UTF-8 por defecto
2. **Orden**: Los elementos en objetos JSON no tienen un orden específico
3. **Comillas**: Siempre usar comillas dobles para strings (incluyendo claves de objetos)
4. **Comas finales**: No se permiten comas después del último elemento en objetos o arrays
5. **Comentarios**: JSON no soporta comentarios (aunque algunas implementaciones los permiten como extensión)
6. **Espacios en blanco**: Son opcionales excepto entre tokens
7. **Nombres de claves**: Deben ser únicos dentro de un objeto

## JSON vs JavaScript

Aunque JSON se deriva de la notación de objetos de JavaScript, hay diferencias importantes:

1. En JSON, todas las claves deben estar entre comillas dobles
2. JSON no acepta funciones como valores
3. JSON no acepta comas finales
4. JSON no acepta comentarios

## Validación de JSON

Es importante validar que un archivo JSON esté correctamente formado. Puedes usar:

1. Validadores online como [JSONLint](https://jsonlint.com/)
2. Herramientas de línea de comandos como `jq`
3. Funciones de parseo en tu lenguaje de programación

## Uso en Programación

### JavaScript

```javascript
// Parsear JSON string a objeto JavaScript
const objeto = JSON.parse('{"nombre":"Juan","edad":30}');

// Convertir objeto JavaScript a JSON string
const jsonString = JSON.stringify({nombre: "Juan", edad: 30});
```

### Python

```python
import json

# Parsear JSON string a diccionario Python
objeto = json.loads('{"nombre": "Juan", "edad": 30}')

# Convertir diccionario Python a JSON string
json_string = json.dumps({"nombre": "Juan", "edad": 30})
```

## Errores Comunes

1. **Comas finales**:
   ```json
   {
     "nombre": "Juan",
     "edad": 30,  // ← Esta coma sobra y causará error
   }
   ```

2. **Comillas simples**:
   ```json
   {
     'nombre': 'Juan'  // ← Deben ser comillas dobles
   }
   ```

3. **Comentarios** (no válidos en JSON estándar):
   ```json
   {
     // Esto es un comentario (no válido en JSON)
     "nombre": "Juan"
   }
   ```

4. **Valores no válidos**:
   ```json
   {
     "fecha": new Date()  // ← Funciones no son válidas en JSON
   }
   ```

## Ejercicios Prácticos

1. **Corregir JSON inválido**:
   ```json
   {
     nombre: "Juan",
     'edad': 30,
     "activo": true,
     "dirección": {
       calle: "Av Principal",
       "número": 123,
     },
   }
   ```

   Solución:
   ```json
   {
     "nombre": "Juan",
     "edad": 30,
     "activo": true,
     "dirección": {
       "calle": "Av Principal",
       "número": 123
     }
   }
   ```

2. **Crear un JSON** para representar un libro con:
   - Título
   - Autor (nombre y apellido)
   - Año de publicación
   - Géneros (array)
   - Disponibilidad (booleano)
   - Información de la editorial (objeto con nombre y país)

   Solución posible:
   ```json
   {
     "título": "Cien años de soledad",
     "autor": {
       "nombre": "Gabriel",
       "apellido": "García Márquez"
     },
     "añoPublicación": 1967,
     "géneros": ["Novela", "Realismo mágico", "Ficción"],
     "disponible": true,
     "editorial": {
       "nombre": "Sudamericana",
       "país": "Argentina"
     }
   }
   ```

## Conclusión

JSON es un formato extremadamente útil y versátil para el intercambio de datos. Su simplicidad y legibilidad lo han convertido en el estándar de facto para APIs web y configuración de aplicaciones. Al dominar su sintaxis y reglas, podrás trabajar eficientemente con la mayoría de sistemas modernos de intercambio de datos.