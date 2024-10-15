


# Tipos de datos



| Tipo    | Dato               | Ejemplo                      |
| ------- | ------------------ | ---------------------------- |
| String  | Texto              | "Va entre comillas"          |
| Byte    | Entero de 8 bits   | -128, 127                    |
| Short   | Entero de 16 bits  | -32768, 32767                |
| Int     | Entero de 32 bits  | -2147483648, 2147483647      |
| Long    | Entero             | Va de $-2^{63}$ a $2^{63}-1$ |
| Double  | Decimal de 64 bits | 2.0,  -31.9999               |
| Float   | Decimal de 32 bits | 5.45f                        |
| Boolean | Booleano           | true, false                  |

# Contantes y variables
- Usamos la palabra reservada  `val` para definir constantes.
- Usamos la palabra reservada `var` para definir variables

> [!important] En Kotlin, se recomienda usar la palabra clave `val` en lugar de `var` cuando sea posible


## Sintaxis
```kotlin
val name: data_type = initial_value
```

## Ejemplos
```kotlin
val age:Int = 30  
  
val longExample:Long = 30  
  
val floatExample:Float = 30.5f  
  
val doubleExample:Double = 3241.321654  
  
val charExample1:Char = 'e'  
val charExample2:Char = '@'  
  
val stringExample:String = "My pain is self chosen"  
 
val booleanExample:Boolean = true
```

> [!tip] Inferencia de tipos
> No es necesario añadir el tipo de variable en la declaración ya que el compilador de Kotlin lo puede determinar. La sintaxis quedaría como: `val name = initial_value`

> [!important] Si no proporcionas un valor inicial cuando declaras una variable, debes especificar el tipo

> [!info] Cuando existen operaciones con variables que son distintos tipos (Int y Long, Int y Float) la operación se realiza con el tipo más general


## Plantilla de Strings
Una expresión de plantilla es una expresión que se evalúa como un valor y que luego se sustituye en el string.

Para referenciar un valor de una variable dentro de una cadena de texto usamos el signo dolar `$`
```kotlin
val stringExample2 = "4"

var stringConcatenada:String = "Hola, Mitchel $stringExample2"  

println(stringConcatenada)
```

Si son varios valores debes encerrarlos entre llaves, por ejemplo si queremos referenciar la suma de dos variables numéricas:  `${variable1 + variable2}

## Operadores de incremento y decremento
`++` para incrementar en 1 y `--` para decrementar en 1



# Estructuras de control

## when
La estructura **`when`** en Kotlin es una alternativa más poderosa y flexible al tradicional `switch` que existe en lenguajes como Java o C. Se utiliza para ejecutar diferentes bloques de código en función del valor de una expresión. Es más versátil que `switch` porque puede evaluar no solo números o constantes, sino también cualquier tipo de expresión, como variables, tipos de datos o incluso rangos.

### Sintaxis básica de `when`

La estructura básica de `when` es la siguiente:

```kotlin
when (expresión) {
    valor1 -> {
        // Bloque de código para valor1
    }
    valor2 -> {
        // Bloque de código para valor2
    }
    else -> {
        // Bloque de código por defecto si ninguno de los valores coincide
    }
}
```

- **`expresión`**: Es el valor o la variable que se evalúa.
- **`valor1`, `valor2`**: Son los posibles valores con los que se compara la expresión.
- **`else`**: Es opcional y actúa como el caso por defecto, ejecutándose si ninguna de las condiciones anteriores se cumple.

### Ejemplo básico:

```kotlin
val day = 2

when (day) {
    1 -> println("Lunes")
    2 -> println("Martes")
    3 -> println("Miércoles")
    else -> println("Día no válido")
}
```

En este ejemplo, la variable `day` se evalúa y, si su valor es `2`, se ejecuta el bloque que imprime "Martes". Si `day` tiene un valor diferente que no está listado (por ejemplo, `4`), se ejecutará el bloque de `else`, que imprime "Día no válido".

### Funcionalidades avanzadas de `when`

A diferencia de `switch`, la estructura `when` de Kotlin es mucho más versátil. Veamos algunos casos avanzados:

#### 1. **Comparar múltiples valores en una sola línea**:
Puedes agrupar varias condiciones en un solo bloque.

```kotlin
val day = 1

when (day) {
    1, 7 -> println("Fin de semana")
    2, 3, 4, 5, 6 -> println("Día laboral")
    else -> println("Día no válido")
}
```

Aquí, si `day` es `1` o `7`, se imprimirá "Fin de semana". Si es `2` a `6`, se imprimirá "Día laboral".

#### 2. **Rangos (Ranges)**:
Puedes usar rangos para verificar si un valor cae dentro de un cierto intervalo.

```kotlin
val age = 25

when (age) {
    in 0..12 -> println("Niño")
    in 13..19 -> println("Adolescente")
    in 20..64 -> println("Adulto")
    else -> println("Senior")
}
```

Este código verifica en qué rango cae la edad (`age`). Si está entre `20` y `64`, se imprimirá "Adulto".

#### 3. **Verificar el tipo de dato (`is`)**:
`when` puede evaluar el tipo de una variable utilizando el operador `is`.

```kotlin
val obj: Any = "Kotlin"

when (obj) {
    is String -> println("Es una cadena")
    is Int -> println("Es un entero")
    is Boolean -> println("Es un booleano")
    else -> println("Tipo desconocido")
}
```

Aquí se verifica el tipo de `obj`. Si es una cadena, imprimirá "Es una cadena".

#### 4. **Expresiones complejas**:
No solo puedes comparar valores directos, también puedes usar expresiones o condiciones más complejas en cada rama.

```kotlin
val number = 10

when {
    number % 2 == 0 -> println("Es par")
    number % 2 != 0 -> println("Es impar")
}
```

En este ejemplo, `when` no evalúa una variable específica, sino una condición. El primer bloque se ejecuta si `number` es par, y el segundo si es impar.

#### 5. **Uso como expresión**:
En Kotlin, `when` puede devolver un valor, similar a cómo lo hace una función, lo que lo hace muy útil cuando quieres asignar un valor dependiendo del resultado de la evaluación.

```kotlin
val x = 2

val result = when (x) {
    1 -> "Uno"
    2 -> "Dos"
    3 -> "Tres"
    else -> "Desconocido"
}

println(result)  // Imprime: Dos
```

Aquí, `when` devuelve un valor dependiendo del caso, y ese valor se asigna a la variable `result`.

#### 6. **Sin expresión de entrada**:
No siempre necesitas pasar un valor a `when`. Puedes usarlo simplemente para evaluar condiciones directamente.

```kotlin
val y = 15

when {
    y < 10 -> println("Es menor que 10")
    y in 10..20 -> println("Está entre 10 y 20")
    else -> println("Es mayor que 20")
}
```

En este caso, `when` no está evaluando una expresión en particular, sino que actúa como una serie de condiciones independientes.

### Diferencias entre `when` y `switch`:

| Característica                  | `when` en Kotlin                       | `switch` en otros lenguajes (como Java) |
|----------------------------------|----------------------------------------|----------------------------------------|
| Tipos de datos                   | Puede evaluar cualquier tipo de datos  | Solo puede evaluar tipos primitivos (int, char, etc.) y cadenas en versiones más recientes de Java |
| Rango de valores                 | Permite evaluar rangos (`in 1..10`)    | No permite rangos                      |
| Evaluación de tipos              | Permite usar el operador `is` para comprobar el tipo de una variable | No tiene esta capacidad                |
| Es opcional la expresión de entrada | No requiere una expresión de entrada para evaluar condiciones | `switch` siempre requiere una expresión de entrada |
| Retorno de valores               | Puede devolver un valor (ser usado como expresión) | Solo ejecuta instrucciones            |

### Resumen:

- **`when`** es una estructura de control en Kotlin que permite ejecutar diferentes bloques de código en función de una expresión o varias condiciones.
- Es más versátil que `switch` porque puede evaluar expresiones complejas, rangos, tipos de datos y devolver valores.
- Puede usarse tanto con una expresión como sin ella, permitiendo mayor flexibilidad en la estructura del código.
- `when` también se puede usar como una expresión que devuelve un valor, lo que permite asignar el resultado directamente a una variable.


