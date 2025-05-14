
# Companion object
En Kotlin, un **companion object** es un bloque especial dentro de una clase que permite definir métodos y propiedades que pertenecen a la clase en sí, no a las instancias de la clase. Es como una forma de definir miembros estáticos, similar a lo que se haría en Java con `static`.

El **companion object** se utiliza cuando necesitas comportamientos o valores que no dependen de una instancia específica de la clase. Al ser declarado dentro de la clase, el `companion object` tiene acceso a los miembros privados de esa clase.

### Ejemplo básico:

```kotlin
class MiClase {
    companion object {
        fun metodoEstatico() {
            println("Este es un método del companion object.")
        }
    }
}

fun main() {
    MiClase.metodoEstatico()  // Llamada sin crear una instancia
}
```

### Características clave:
| Característica                | Descripción                                                                 |
|-------------------------------|-----------------------------------------------------------------------------|
| Relación con la clase          | El `companion object` está asociado a la clase, pero no a una instancia de ella. |
| Acceso a miembros privados     | Puede acceder a miembros privados de la clase.                              |
| Nombre del companion object    | Puede ser nombrado, aunque el nombre por defecto es `Companion`.            |
| Uso estático                   | Permite definir métodos y propiedades estáticas (a nivel de clase).         |

Es útil para crear **factories**, **singletons** o para organizar código que no tiene sentido que pertenezca a una instancia específica.