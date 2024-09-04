
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
