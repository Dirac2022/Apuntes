
# unordered_map
`std::unordered_map` es una estructura de datos proporcionada por la biblioteca estándar de C++ que implementa un contenedor asociativo basado en tablas hash. Es similar a `std::map`, pero proporciona un acceso más rápido a los elementos, aunque no garantiza un orden específico de los mismos.

Aquí hay algunas características clave de `std::unordered_map`:

1. **Búsqueda Eficiente:** Las operaciones de inserción, borrado y búsqueda en un `std::unordered_map` tienen una complejidad promedio de O(1) en tiempo. Sin embargo, en el peor de los casos, la complejidad puede ser O(n) si hay colisiones de hash graves.

2. **No Ordenado:** A diferencia de `std::map`, los elementos en un `std::unordered_map` no están ordenados. No hay garantía de que los elementos se almacenen en un orden específico, ya que dependen de la función de hash utilizada.

3. **Claves Únicas:** Al igual que `std::map`, las claves en un `std::unordered_map` deben ser únicas. Si se inserta una clave que ya está presente, se actualizará el valor asociado a esa clave.

4. **Uso de Hashing:** `std::unordered_map` utiliza funciones hash para mapear las claves a índices en una tabla hash. Esto permite un acceso rápido a los elementos, pero puede dar lugar a colisiones si dos claves diferentes tienen el mismo valor hash.

5. **Iteradores:** `std::unordered_map` proporciona iteradores que permiten recorrer los elementos del contenedor en cualquier orden, pero no hay garantía sobre el orden en el que se devolverán los elementos.

6. **Uso de Plantillas:** Al igual que otros contenedores de la biblioteca estándar de C++, `std::unordered_map` es una plantilla, lo que significa que puede almacenar elementos de cualquier tipo de datos. Por ejemplo, `std::unordered_map<int, std::string>` almacenaría asociaciones de enteros a cadenas de caracteres.


## Ejemplo
Aquí hay un ejemplo de cómo usar `std::unordered_map`:

```cpp
#include <iostream>
#include <unordered_map>
#include <string>

int main() {
    // Crear un unordered_map que mapea nombres (strings) a edades (integers)
    std::unordered_map<std::string, int> mapaEdades;

    // Insertar elementos en el mapa
    mapaEdades["Juan"] = 30;
    mapaEdades["María"] = 25;
    mapaEdades["Carlos"] = 40;

    // Acceder a un elemento por su clave
    std::cout << "La edad de Juan es: " << mapaEdades["Juan"] << std::endl;

    // Iterar sobre los elementos del mapa
    for (const auto& par : mapaEdades) {
        std::cout << par.first << " tiene " << par.second << " años." << std::endl;
    }

    return 0;
}
```

Este código crea un `std::unordered_map` llamado `mapaEdades` que mapea nombres a edades, inserta algunos elementos en el mapa, accede a un elemento por su clave y luego itera sobre todos los elementos del mapa.

`std::unordered_map` es una plantilla de la biblioteca estándar de C++ que proporciona una interfaz para trabajar con un contenedor asociativo basado en tablas hash. Aquí están los atributos y funciones asociadas más comunes de `std::unordered_map`:

## Tipos miembro


1. `key_type`: Tipo de datos de la clave. Es el primer parámetro de plantilla de `std::unordered_map`.

2. `mapped_type`: Tipo de datos del valor asociado a la clave. Es el segundo parámetro de plantilla de `std::unordered_map`.

3. `value_type`: Tipo de datos de los elementos almacenados, que es un par `std::pair<const Key, T>`. Es decir, `std::pair` de la clave y el valor asociado.


## Funciones miembro

1. `insert(const value_type& value)`: Inserta un par clave-valor en el `std::unordered_map`.

2. `emplace(Args&&... args)`: Inserta un nuevo elemento en el `std::unordered_map` mediante la construcción in situ.

3. `erase(const key_type& key)`: Elimina el elemento con la clave especificada del `std::unordered_map`.

4. `find(const key_type& key)`: Busca un elemento con la clave especificada en el `std::unordered_map` y devuelve un iterador a él.

5. `at(const key_type& key)`: Devuelve una referencia al valor asociado a la clave especificada en el `std::unordered_map`.

6. `size()`: Devuelve el número de elementos en el `std::unordered_map`.

7. `empty()`: Devuelve `true` si el `std::unordered_map` está vacío, `false` en caso contrario.

8. `clear()`: Elimina todos los elementos del `std::unordered_map`.

9. `begin()`, `end()`, `cbegin()`, `cend()`: Funciones para obtener iteradores al principio y al final del `std::unordered_map`.

10. `bucket_count()`: Devuelve el número de buckets (contenedores) en el `std::unordered_map`.

11. `load_factor()`: Devuelve el factor de carga actual del `std::unordered_map`.

12. `rehash(size_type count)`: Cambia el número de buckets del `std::unordered_map` al menos al especificado.



# set


