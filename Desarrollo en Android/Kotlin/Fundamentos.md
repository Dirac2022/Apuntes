


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


