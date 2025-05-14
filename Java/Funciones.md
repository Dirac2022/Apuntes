
# Funciones lambda

## Interfaz funcional
Es una interfaz que contiene exactamente un método abstracto. Esto significa que solo puede tener un único método sin implementar, aunque puede tener otros métodos que sean por defecto o estáticos. 
Su propósito es permitir que las expresiones lambda las implementen, ofreciendo una forma concisa de representar funciones o comportamientos sin necesidad de definir una clase completa.

### Características principales
1. Un sólo método abstracto, el cual será implementado por la expresión lambda.
2. Métodos por defecto o estáticos.
3. Anotación `@FunctionalInterface`

### Ejemplo

```java
@FunctionalInterface
interface Operacion {
    int ejecutar(int a, int b);
}
```

Podemos usar una expresión lambda para implementar esta interfaz
```java
Operacion suma = (a, b) -> a + b
```

### Métodos adicionales permitidos
- `default`: son métodos con implementación por defecto, útiles si queremos proveer una funcionalidad estándar que puede ser sobrescrita.
- `static`: son métodos estáticos que también tienen implementación, pero no afectan el método abstracto.

### Ejemplos de Interfaces funcionales
1. **Runnable**: tiene el método `run()`
2. **Comparator**: tiene el método `compare()`

```java
(parameters) -> expression
// o
(parameters) -> { statements }

```

## Sintaxis básica

```
(parameters) -> expression
// o
(parameters) -> { statements }

```

### Ejemplo

Supongamos que tenemos una interfaz con un solo método a implementar
```java
@FunctionalInterface
interface Operacion {
	int ejecutar(int a, int b)
}
```

Ejemplo de uso
```java
public class LambdaEjemplo {
	public static void main(String[] args) {
		// Implementación de una función lambda para sumar
		Operacion suma = (a, b) -> a + b;

		// Para multiplicar
		Operaciones multiplicar = (a, b) -> a * b;

		System.out.println("Suma: " + suma.ejecutar(5, 3));
		System.out.println("Multiplicación: " + multiplicar.ejecutar(5, 3));
	}
}
```

