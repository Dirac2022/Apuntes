| Tipo          | Mutable        | Características                          | Uso Común                             |
| ------------- | -------------- | ---------------------------------------- | ------------------------------------- |
| `List`        | No             | Lista ordenada inmutable                 | Cuando los datos no deben cambiar     |
| `MutableList` | Sí             | Lista ordenada modificable               | Para datos que cambian frecuentemente |
| `ArrayList`   | Sí             | Implementación específica de MutableList | Cuando necesitas mejor rendimiento    |
| `Array`       | Solo elementos | Tamaño fijo, mejor rendimiento           | Para tamaños conocidos y fijos        |
| `Set`         | No             | Colección sin duplicados                 | Para datos únicos                     |
| `MutableSet`  | Sí             | Set modificable                          | Para datos únicos que cambian         |
| `Map`         | No             | Pares clave-valor inmutables             | Para relaciones fijas                 |
| `MutableMap`  | Sí             | Pares clave-valor modificables           | Para relaciones que cambian           |
