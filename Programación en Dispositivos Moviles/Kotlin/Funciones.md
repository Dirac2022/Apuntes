
# Sintaxis


**Sintaxis básica**
```kotlin
fun <name> () {
	<body>
}
```

**Sintaxis con retorno**
```kotlin
fun <name> (): <return type> {
	<body>
	<return statement>
}
```

**Sintaxis con retorno y parámetros de entrada**
Cada parámetro consta de un nombre y un tipo de datos, separados por dos puntos y un espacio, si hay varios parámetros, se separan con una coma
```kotlin
fun <name> (<parameters>): <return type> {
	<body>
	<return statement>
}
```


> [!info] Diferencia entre parámetro y argumento
> Los parámetros son las variables a las que puede acceder la función, como una variable, mientras que los argumentos son los valores reales que se pasan a la función.

> [!warning] Los parámetros en Kotlin son inmutables

> [!tip] Firma de una función
> Es el nombre y la entrada (los parámetros) de una función.


# Argumentos de una función
## Argumentos con nombre
Se puede especificar el orden de entrada de los parámetros colocando el nombre del parámetro y su valor.

## Argumentos predeterminados
Los parámetros de la función también pueden especificar argumentos predeterminados. Esto se hace en la declaración de la función, asignando un valor predeterminado: `parameter_name: typo = default`
# El tipo unit
El tipo `unit` es análogo a `void` en lenguajes como Java o C++ Es el tipo de datos de retorno por defecto. **Cualquier función que no muestre un valor muestra `unit` de forma implícita**. En este caso no necesitas incluir una sentencia `return`


# funcion let
En Kotlin, la función **`let`** es una **función de alcance** (scope function) que se utiliza para ejecutar un bloque de código en el contexto de un objeto. El principal propósito de **`let`** es evitar referencias nulas y hacer que el código sea más limpio y legible.

### ¿Cómo funciona **`let`**?

- **`let`** toma un objeto y lo pasa como argumento dentro de un bloque de código. Este objeto puede ser una variable o una propiedad.
- El objeto pasado a **`let`** se accede a través de la palabra clave **`it`** (aunque puedes renombrarlo si lo prefieres).
- Después de ejecutar el bloque de código, **`let`** devuelve el resultado del último valor en el bloque (si es necesario).

### ¿Para qué se usa **`let`**?

1. **Evitar valores nulos** (manejo de null safety).
2. **Ejecutar un bloque de código solo si el valor no es nulo**.
3. **Simplificar operaciones** sobre variables que necesitan ser usadas en un contexto temporal.

### Ejemplo básico:

```kotlin
val nombre: String? = "André"

nombre?.let {
    println("El nombre no es nulo: $it")  // it se refiere a 'nombre'
}
```

#### Explicación:

1. **`nombre?.let`**: Usamos el **operador seguro (`?.`)** para asegurarnos de que solo si `nombre` no es nulo, se ejecute el bloque de código dentro de **`let`**.
2. **`it`**: Dentro del bloque, **`it`** representa el valor de `nombre`. En este caso, **`it`** será `"André"` si `nombre` no es nulo.
3. **Salida**: Si `nombre` no es nulo, imprime `"El nombre no es nulo: André"`. Si `nombre` es nulo, no se ejecuta nada.

### Otro ejemplo: evitar un valor nulo y realizar una operación

```kotlin
val numero: Int? = 5

numero?.let {
    val resultado = it * 2
    println("El número multiplicado por 2 es: $resultado")
}
```

En este caso:
- Si `numero` no es nulo, se ejecuta el bloque de código y se multiplica por 2.
- Si `numero` es nulo, el bloque **no se ejecuta**.

### Renombrar `it` en **`let`**:

Por defecto, **`let`** usa la variable **`it`** para referirse al objeto dentro del bloque de código. Sin embargo, puedes renombrarla para hacer el código más legible:

```kotlin
val nombre: String? = "André"

nombre?.let { valorNoNulo ->
    println("El nombre no es nulo: $valorNoNulo")
}
```

Aquí, en lugar de usar **`it`**, se renombra a **`valorNoNulo`**, lo que puede ser más claro en algunos contextos.

### Casos de uso comunes de **`let`**:

#### 1. **Evitar referencias nulas (null safety)**:
La función **`let`** es muy útil cuando necesitas ejecutar código solo si una variable no es nula.

```kotlin
val email: String? = obtenerEmail()

email?.let {
    enviarEmail(it)  // Solo se ejecuta si 'email' no es nulo
}
```

En este caso, **`let`** garantiza que **`enviarEmail(it)`** solo se ejecutará si **`email`** no es nulo.

#### 2. **Encadenar operaciones**:
Puedes encadenar varias operaciones utilizando **`let`** para realizar transformaciones u operaciones de manera concisa.

```kotlin
val longitud: Int? = nombre?.let {
    println("El nombre no es nulo y tiene longitud: ${it.length}")
    it.length
}
```

Aquí, **`let`** se usa para imprimir la longitud del nombre si no es nulo, y también devuelve esa longitud para asignarla a `longitud`.

#### 3. **Hacer que el código sea más limpio**:
Si necesitas usar una variable temporalmente y deseas limitar su alcance, puedes usar **`let`** en lugar de crear una variable adicional.

```kotlin
val resultado = "Hola Mundo".let {
    it.uppercase()  // Convierte "Hola Mundo" a mayúsculas
}
println(resultado)  // Imprime: HOLA MUNDO
```

### ¿Cuándo usar **`let`**?

- **Cuando quieres ejecutar código solo si un valor es no nulo**.
- **Cuando necesitas transformar o trabajar temporalmente con un objeto** y no necesitas crear variables adicionales.
- **Cuando quieres simplificar el código** y evitar largas verificaciones de nulos como `if (variable != null)`.

### Resumen:

- **`let`** es una **función de alcance** en Kotlin que te permite ejecutar un bloque de código en el contexto de un objeto.
- Es útil para el **manejo seguro de nulos** y para **hacer el código más limpio y legible**.
- El objeto pasado a **`let`** se accede a través de la palabra clave **`it`**, aunque puedes renombrarla para mayor legibilidad.
- **`let`** devuelve el resultado de la última línea de su bloque de código.

Si tienes más dudas sobre **`let`** o sobre otras funciones de alcance en Kotlin, ¡no dudes en preguntar!


