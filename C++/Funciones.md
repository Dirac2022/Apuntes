
# Funciones lambda

Son una forma de definir funciones anónimas en línea.

## Sintaxis

```
[captures](parameteres) -> return_type { body}
```
- **captures**: Especifica qué variables externas a la lambda serán capturadas y cómo. Las capturas pueden ser por valor (`[=]`) o por referencia (`[&]`).
- **parameters**: Lista de parámetros como en cualquier función regular.
- **return_type**: (Opcional) Especifica el tipo de retorno de la lambda.
- **body**: El cuerpo de la función lambda.

## Ejemplo

```cpp
#include <iostream>

int main() {

	// Ejemplo básico
    auto sum = [](int a, int b) -> int {
        return a + b;
    };

    std::cout << "La suma de 3 y 4 es: " << sum(3, 4) << std::endl;

	// Captura por valor
	int x = 10;
	auto lambda = [x]() { 
		std::cout << "x capturado por valor: " << x << std::endl;
	};
	x = 20; lambda(); // Imprime 10
	
	// Captura por referencia
	int x = 10;
	auto lambda = [&x]() { 
		std::cout << "x capturado por referencia: " << x << std::endl; 
	}; 
	x = 20; lambda(); // Imprime 20
    return 0;
}

```


## Observaciones
- No se puede aplicar recursividad en las funciones lambda

# Function

Es una plantilla de la biblioteca stándar (std) que representa un objeto que puede actuar como una función o un puntero a una función. Proporciona una manera de almacenar, copiar y manipular funciones, incluidas las [[C++/Funciones#Funciones lambda|funciones lambda]], funciones miembro de clases y punteros a funciones.


**VENTAJAS**
- **Flexibilidad**: Puede contener cualquier tipo de función que coincida con su firma de tipo.
- **Polimorfismo**: Puede almacenar diferentes tipos de funciones y llamarlas de manera uniforme.
- **Interoperabilidad**: Puede ser asignado a funciones, lambdas y punteros a funciones.

**DESVENTAJAS**
- Puede tener un ligero sobrecosto de rendimiento en comparación con punteros a funciones.
- Requiere una cantidad adicional de memoria para almacenar el objeto `std::function`.

## Sintaxis
```
std::function<tipo_retorno(tipo_arg1, tipo_arg2, ..., tipo_argN)> nombre_funcion;
```

- `tipo_retorno`: Es el tipo de dato que devuelve la función.
- `tipo_arg1, tipo_arg2, ..., tipo_argN`: Son los tipos de los argumentos que recibe la función.
- `nombre_funcion`: Es el nombre del objeto `std::function`.

## Ejemplo
```cpp
#include <iostream>
#include <functional>

int main() {
    // Declaración de un objeto std::function para almacenar una función lambda
    std::function<int(int, int)> f = [](int a, int b) -> int {
        return a + b;
    };

    // Llamada a la función lambda almacenada
    std::cout << "La suma de 3 y 4 es: " << f(3, 4) << std::endl;

    return 0;
}

```