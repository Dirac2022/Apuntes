
# Como definir una función

Estas son las partes clave necesarias para definir una función

- La función necesita un nombre para que puedas llamarla más tarde.
- También puede requerir algunas entradas o información que se debe proporcionar cuando se la llama. La función usa estas entradas para lograr su propósito. Requerir entradas es opcional, algunas funciones no las necesitan.
- La función también tiene un cuerpo que contiene las instrucciones para realizar la tarea.


El código Kotlin, usa la siguiente sintaxis, o formato, para definir una función. El orden de estos elementos es importante.

```kotlin
fun name ( inputs ) {
	body
} 

// Ejemplo
fun main() {
	println("Hello world")
}
```

- La definición de la función comienza con la palabra `fun`.
- Luego, el nombre de la función es `main`


# Entradas de funciones

- Observa que el nombre de la función siempre va seguido de paréntesis. Entre estos paréntesis, se enumeran las entradas de la función.
- Una entrada es un dato que necesita una función para cumplir su propósito. Cuando defines una función, puedes solicitar que se pasen ciertas entradas en el momento en que se la llama. Si una función no tiene entradas, los paréntesis aparecen vacíos en ().

```kotlin
fun name (<inputs>) {
	body
}
```


# Guía de estilo de Kotlin

A continuación, se incluyen algunas de las recomendaciones de la guía de estilo para lo que aprendiste en Kotlin hasta el momento

- Los nombres de las funciones deben seguir la convención de mayúsculas y minúsculas, y deben ser verbos o frases verbales.
- Cada sentencia debe estar en su propia línea.
- La llave de apertura debe aparecer al final de la línea donde comienza la función.
- Debe haber un espacio antes de la llave de apertura.
- EL cuerpo de la función debe tener una sangría de 4 espacios. No uses caracteres de tabulación para aplicar sangría a l código.
- La llave de cierre se encuentra en su propia línea después de la última línea de código del cuerpo de la función. La llave de cierre debe alinearse con la palabra clave fun al comienzo de la función.

[Guía de estilo de Kotlin  |  Android Developers](https://developer.android.com/kotlin/style-guide?hl=es-419)



# Tipos de datos y variables


| Tipos de datos de Kotlin | Qué tipo de datos puede contener                                                     | Ejemplos de valores literales |
| ------------------------ | ------------------------------------------------------------------------------------ | ----------------------------- |
| String                   | Texto                                                                                | "Add contact"                 |
| Int                      | Número entero                                                                        | 32, 123491, -4561             |
| Double                   | Número racional                                                                      | 2.0, -31723.9999              |
| Float                    | Número decimal (menos preciso que un Double). Tiene un `f` o `F` al final del número | 5.0f, -1650.45F               |
| Boolean                  | `true` o `false`                                                                     |                               |


**Ejemplo**

```kotlin
val <name>: <data type> = <initial value>

# Ejemplo
val count: Int = 2
```


# Declaración variable

- Kotlin utiliza dos palabras clave diferentes para declarar variables: `val` y `var`.
- Usa `val` para una variable cuyo valor no cambia nunca.
- Utiliza `var` para una variable cuyo valor puede cambiar.
- En el siguiente ejemplo,  `count` es una variable de tipo `Int` asignada a un valor inicial de 10:

```kotlin
val count: Int = 10
```

- Usando `var`

```kotlin
var count: Int = 10
count = 15
```

Sin embargo, algunos valores no se pueden cambiar. Tomemos como ejemplo un objeto `String` llamado ``languageName``. Si quieres asegurarte de que ``languageName`` siempre retenga un valor de "Kotlin", puedes declarar ``languageName`` mediante la palabra clave `val`:

```kotlin
val `languageName`: String = "Kotlin"
```

# Inferencia de tipo

Continuando con el ejemplo anterior, cuando asignas un valor inicial a `languageName`, el compilador de Kotlin puede inferir el tipo en función del tipo del valor asignado. 

Debido a que el valor de "Kotlin" es de tipo String, el compilador infiere que `languageName` también es String. Ten en cuenta que Kotlin es un lenguaje de tipo estático. Eso quiere decir que el tipo se resuelve en el tiempo de compilación y no cambia nunca. 

En el siguiente ejemplo, `languageName` se infiere como String, de manera que no puedes llamar a ninguna de las funciones que no forman parte de la clase de String:

```kotlin
val languageName = "Kotlin"
val upperCaseName = languageName.toUpperCase()
```

# Seguridad nula

En algunos ejemplos, se puede declarar una variable de tipo de referencia sin proporcionar un valor explícito inicial. En estos casos, por lo general, la variable contiene un valor nulo. Las variables de Kotlin no pueden retener valores nulos de manera predeterminada. Por lo tanto, el siguiente fragmento no es válido:

```kotlin
// Fails to compile
val languageName: String = null
```


Para que una variable retenga un valor nulo, debe ser de tipo anulable. Si deseas especificar que una variable es anulable, puedes agregar un sufijo a su tipo mediante `?`, como se muestra en el siguiente ejemplo:

```kotlin
val languageName: String? = null
```


Mediante el tipo `String?`, puedes asignar un valor `String` o `null` a `languageName`.

Debes manejar las variables anulables con cuidado o podrías obtener un `NullPointerException` no deseado. En Java, por ejemplo, tu programa falla si intentas invocar un método en una variable nula

# Operadores de incremento y disminución

- `varaible ++` equivale a `variable = variable + 1`
- `variable --` equivale a `variable = variable - 1`

# Condicionales

Kotlin cuenta con varios mecanismos para implementar la lógica condicional. El más común es la declaración "if-else". Si una expresión entre paréntesis junto a una palabra clave `if` evalúa `true`, se ejecuta el código dentro de esa rama (es decir, el código que siga inmediatamente después del código entre paréntesis). De lo contrario, se ejecuta el código dentro de la rama de else.

```kotlin
if (count == 42) {
	println("I have the answer.")
} else {
	println("The answer eludes me.")
}
```



Puedes representar varias condiciones mediante `else if`. De esta manera, puedes representar una lógica más detallada y compleja dentro de un solo enunciado condicional, como se muestra en el siguiente ejemplo:

```kotlin
if (count == 42) {
	println("I have the answer.")
} else if (count > 35) {
	println("The answer is close.")
} else {
	println("The answer eludes me.")
}
```

Las declaraciones condicionales son útiles para representar lógica de estado, aunque podría resultarte repetitivo escribirlas. En el ejemplo anterior, imprimes un objeto String en cada rama. Para evitar esta repetición Kotlin ofrece expresiones condicionales. El último ejemplo se puede volver a escribir de la siguiente manera:

```kotlin
val answerString: String = if (cont == 42) {
	"I have the answer."
} else if (count > 35) {
	"The answer is close."
} else {
	"The answer eludes me."
}

println(answerString)
```

A medida que aumenta la complejidad de tu declaración condicional quizá te convenga reemplazar la expresión `if-else` con una expresión `when`, como se muestra en le siguiente ejemplo:

```kotlin
val answerString = when {
	count == 42 -> "I have the answer."
	count > 35 -> "The answer is close."
	else -> "The answer eludes me."
}

println(answerString)
```


