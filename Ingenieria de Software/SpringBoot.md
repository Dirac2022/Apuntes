

# `fromEntity()`
El método convierte una entidad individual (`Hotel`) y la convierte a un objeto (`HotelResponse`) para ser devuelto y presentado en el cliente.


# `fromEntities()`
Convierte una colección de entidades en una lista de objetos `HotelResponse`. Se usa cuando se desea formar un conjunto de entidades en una lista de objetos `HotelResponse`

**¿Cómo funciona?**:
- `HotelResponse.fromEntities(List<Hotel> hotels)` toma una lista de entidades `Hotel` y la convierte en una lista de objetos `HotelResponse`.
- Esto se hace utilizando el método `fromEntity()` en cada uno de los elementos de la lista.



# `stream()`
Convierte una colección en un flujo (stream), que permite procesar los elementos de la colección de manera funcional. Esto habilita el uso de métodos como `map()`, `filter()`, `reduce()`, entre otros, que operan sobre cada elemento de la colección de forma declarativa y eficiente.


>[!info] **¿Qué es un stream?**
>Un **stream** es una secuencia de elementos que se pueden procesar de manera secuencial o paralela. Los streams en Java permiten trabajar de manera más flexible y eficiente con colecciones, sin la necesidad de usar bucles explícitos.

# `map()`
Este método transforma cada elemento del stream en un nuevo valor.
En el ejemplo de `findHotelesByCiudad`, cada hotel de la lista se convierte en un objeto `HotelResponse` usando el método `HotelResponse.fromEntity`.

- **¿Cómo funciona?**: Para cada elemento del stream, el método `map()` aplica una **función de transformación**. En este caso, la función es `HotelResponse::fromEntity`, que convierte cada objeto `Hotel` en un objeto `HotelResponse`.

```java
public List<HotelResponse> findHotelesByCiudad(Ciudad ciudad) {
        return hotelRepository.findByCiudad(ciudad).stream()
                .map(HotelResponse::fromEntity)
                .collect(Collectors.toList());
    }
```



# `collect()`
Este método es usado para recopilar los resultados de un stream y devolverlos en una nueva colección (por ejemplo, una lista, conjunto, etc.). En el ejemplo de `findHotelesByCiudad`, después de aplicar `map()` a cada `Hotel`, `collect()` recoge todos los `HotelResponse` generados y los coloca en una nueva lista.

**¿Cómo funciona?**: `collect()` acepta un **recolector** (como `Collectors.toList()`) que determina cómo recoger los elementos del stream y almacenarlos en una nueva colección.

- **`Collectors.toList()`**: Es un **recolector** que acumula los elementos del stream en una lista.
## ¿Cómo interactúan `map()`, `collect()` y `stream()` en `findHotelesByCiudad`?**

```java
return hotelRepository.findByCiudad(ciudad).stream()         .map(HotelResponse::fromEntity)         .collect(Collectors.toList());`
```

- **`findByCiudad(ciudad)`**: Obtiene una lista de hoteles asociados a la ciudad de la base de datos.
- **`.stream()`**: Convierte la lista de hoteles en un flujo para ser procesado funcionalmente.
- **`.map(HotelResponse::fromEntity)`**: Transforma cada hotel en un `HotelResponse`.
- **`.collect(Collectors.toList())`**: Recoge todos los `HotelResponse` generados en una nueva lista.