Los objetivos principales de realizar una prueba son
- Detectar un error.
- Tener un buen caso de prueba, es decir, que tenga más probabilidad de mostrar un error no descubierto antes.
- Descubrir un error no descubierto antes (éxito de la prueba).

# Diseños de caso de prueba
Un producto puede probarse siguiendo dos criterios:
1. Conocimiento del funcionamiento del producto (**Caja blanca**)
2. El conocimiento de la función específica para la que fue diseñado el producto (**Caja negra**


## Prueba de caja blanca
Se desarrolla con el fin de asegurar que todas las piezas del sistema tienen una operación interna que se ajusta a las especificaciones y que todos sus componentes internos se han aprobado en forma adecuada.

Este método de casos de prueba usa los detalles procedimentales del programa. Se busca obtener casos de prueba que:
- Garanticen que se ejecuta por lo menos una vez todos los caminos independientes de cada módulo.
- Verificar las decisiones de cada módulo.
- Verificar las decisiones lógicas (V/F).
- Ejecutar las estructuras internas de datos para asegurar su validez.

>[!tip] Explicacion
>1. **Ejecutar todos los caminos independientes de cada módulo:**
>- Esto significa que se debe asegurar que **cada posible ruta de ejecución** dentro de un módulo o función se ejecute al menos una vez durante las pruebas.
>- Cada ruta de ejecución corresponde a una **combinación de decisiones** o condiciones que pueden ser tomadas durante la ejecución. El objetivo es cubrir todas esas rutas posibles.
>2. **Verificar las decisiones de cada módulo**
>- Este punto se refiere a verificar que **las decisiones lógicas** (como las condiciones `if`, `else`, `switch`, etc.) en cada módulo del sistema se ejecuten correctamente.
>- Se busca garantizar que el flujo de control de cada módulo siga las decisiones tomadas en función de las entradas que recibe.
>3. **Verificar las decisiones lógicas (V/F):**
>- Las **decisiones lógicas** son condiciones que pueden ser **verdaderas (V)** o **falsas (F)**, como las comprobaciones en un `if` o en un `while`.
>- En las pruebas de caja blanca, se validan estos valores de verdad para asegurarse de que el sistema maneja correctamente todas las posibles condiciones.
>5. **Ejecutar las estructuras internas de datos para asegurar su validez:**
>- Esto implica probar cómo se manejan las estructuras de datos internas del sistema (como listas, pilas, colas, árboles, tablas hash, etc.).
>- Se verifica que el sistema mantenga la **coherencia y la validez** de estos datos durante las operaciones (por ejemplo, al insertar, eliminar o modificar elementos).


**Métodos de pruebas**

| Métodos de pruebas         | Características                                                                                                                                                  |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Pruebas de funcionalidad   | Se enfoca en los requisitos funcionales del software. Se centra en la coherencia de entrada y salida. No se enfoca en la estructura interna.                     |
| Pruebas de compatibiliad   | Se enfoca en conocer si es operable con cualquier sistema. Verifica funcionamiento correcto en su entorno.                                                       |
| Prueba de robustez         | Son las encargadas de verificar la capacidad del programa para soportar entradas incorrectas.                                                                    |
| Pruebas de comunicaciones  | Verifica el tiempo en que tardan hacer las transacciones de datos.                                                                                               |
| Pruebas de Caja Blanca     | Debes verificar todo lo que es valido y lo que no será valido para el sistema                                                                                    |
| Pruebas de Caja de Pandora | Consiste en abstenerse de realizar pruebas de depurar bastante bien un proyecto; se deja al cliente que lo ensaye y acepte. El resultado es una bomba de tiempo. |

## Pruebas de la estructura de control
- La prueba de condición se centra en  encontrar errores en condiciones lógicas en un módulo, aunque también puede detectar errores adicionales en el programa.
- En una condición se pueden dar los siguientes errores:
	1. Error de operador lógico
	2. Error en una variable lógica
	3. Error en una condición simple o compuesta
	4. Error en un operador relacional
	5. Error en una expresión aritmética
## Prueba de caja negra
Se realiza con el fin de asegurar que el producto es operativo.

Este tipo de prueba se centra en los requisitos funcionales del software y permite obtener entradas que prueben todos los requisitos funcionales del programa. Con este tipo de pruebas se intenta encontrar:
1. Funciones incorrectas o ausentes.
2. Errores de interfaz.
3. Errores en estructuras de datos o en accesos a bases de datos externas.
4. Errores de rendimiento.
5. Errores de inicialización y terminación.