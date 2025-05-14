

# ¿Qué es un Algoritmo genético?
- Métodos adaptativos generalmente usados en problemas de búsqueda y optimización de parámetros, basados en la reproducción sexual y en el principio de supervivencia del más apto.
- Es un algoritmo matemático altamente paralelo que transforma un conjunto de objetos matemáticos individuales con respecto al tiempo usando operaciones modeladas de acuerdo al principio Darwiniano de reproducción y supervivencia del más apto.
- Los organismos vivientes son consumados resolvedores de problemas.
- Por tanto, **algoritmo genético** es un modelo computacional de búsqueda de la posible mejor solución, basándose en la adaptación del modelo evolutivo.

# Evolución
- Aquellos individuos que tienen más éxito en sobrevivir y en atraer compañeros tienen mayor probabilidad de generar un gran número de descendientes.
- Esto significa que los genes de los individuos mejor adaptados se propagarán en sucesivas generaciones hacia un número de individuos creciente.
- Las especies evolucionan logrando unas características cada vez mejor adaptadas al entorno en el que viven.
- Los **Algoritmos Genéticos** usan una analogía directa con el comportamiento natural.
- Trabajan con una población de individuos, cada uno de los cuales representan una solución factible a un problema dado.
- Cuanto mayor sea la adaptación de un individuo al problema, mayor será la probabilidad de que el mismo sea seleccionado para reproducirse.
- De esta manera se produce una nueva población de posibles soluciones, la cual reemplaza a la anterior.
- A lo largo de las generaciones las buenas características se propagan a través de la población.
- Si el Algoritmo Genético ha sido bien diseñado la población convergerá hacia una solución óptima del problema.


# Ventajas y desventajas

| Ventajas                                                                                                                                                                            | Desventajas                                                                                                                                                                        |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| No necesitan conocimientos específicos sobre el problema que intentan resolver.                                                                                                     | Usan operadores probabilísticos, en vez de los típicos operadores determinísticos de las otras técnicas.                                                                           |
| Operan de forma simultánea con varias soluciones, en vez de trabajar de forma secuencial como las técnicas tradicionales.                                                           | Pueden tardar mucho en converger, o no converger en absoluto, dependiendo en cierta medida de los parámetros que se utilicen: tamaño de la población, número de generaciones, etc. |
| Cuando se usan para problemas de optimización (maximizar una función objetivo) resultan menos afectados por los máximos locales (falsas soluciones) que las técnicas tradicionales. | Pueden converger prematuramente debido a una serie de problemas de diversa índole                                                                                                  |
| Resulta sumamente fácil ejecutarlos en las modernas arquitecturas masivamente paralelas                                                                                             |                                                                                                                                                                                    |


# Limitaciones
- En el caso de que existan técnicas especializadas para resolver un determinado problema, lo más probable es que superen al Algoritmo Genético, tanto en rapidez como en eficacia.
- El gran campo de aplicación de los Algoritmos Genéticos se relaciona con aquellos problemas para los cuales no existen técnicas especializadas.
- Incluso en el caso en que dichas técnicas existan, y funcione bien, pueden efectuarse mejoras con los Algoritmos Genéticos.
# Cuando usar
No todos los problemas pudieran ser apropiados para la técnica, y se recomienda en general tomar en cuenta las siguientes características del mismo antes de intentar usarla:
- Su espacio de búsqueda (i.e., sus posibles soluciones) debe estar delimitado dentro de un cierto rango.
- Debe poderse definir una función de aptitud que nos indiqué qué tan buena o mala es una cierta respuesta.
- Las soluciones deben codificarse de una forma que resulte relativamente fácil de implementar en la computadora.

### **Genotipo y Fenotipo en Algoritmos Genéticos**

En el contexto de los **algoritmos genéticos**, los conceptos de **genotipo** y **fenotipo** son fundamentales para entender cómo se representan y evolucionan las soluciones a un problema. A continuación, se detalla cada uno de estos conceptos:

---

# Genotipo

**Definición:**
El **genotipo** se refiere a la representación interna o codificada de una solución dentro del algoritmo genético. Es la "información genética" que se manipula durante el proceso evolutivo, como la reproducción, la mutación y el cruce.

**Características:**
- **Codificación:** El genotipo suele representarse mediante estructuras de datos específicas, como cadenas binarias, cadenas de caracteres, listas de números, árboles, etc. La elección de la codificación depende del problema que se esté abordando.
  
  - *Ejemplo:* Para un problema de optimización, un genotipo podría ser una cadena binaria que representa los parámetros de la solución.

- **Manipulación Genética:** Las operaciones genéticas (cruce, mutación) se aplican directamente sobre el genotipo. Por ejemplo, en una representación binaria, el cruce podría implicar intercambiar segmentos de dos cadenas binarias, y la mutación podría consistir en invertir un bit.

- **Flexibilidad:** El genotipo proporciona una representación flexible que permite explorar un amplio espacio de soluciones posibles. Sin embargo, es crucial que la codificación elegida permita una exploración eficiente y efectiva del espacio de soluciones.

**Importancia:**
El genotipo es esencial porque determina cómo se generan y combinan las soluciones. Una buena representación genética facilita la búsqueda de soluciones óptimas y mejora la eficiencia del algoritmo.

---

# Fenotipo

**Definición:**
El **fenotipo** es la interpretación o traducción del genotipo en una solución concreta al problema que se está intentando resolver. Es la "manifestación visible" de la información codificada en el genotipo.

**Características:**
- **Decodificación:** El fenotipo se obtiene a partir del genotipo mediante un proceso de decodificación. Este proceso convierte la representación interna en una solución utilizable.

  - *Ejemplo:* Si el genotipo es una cadena binaria que representa parámetros de un modelo, el fenotipo sería el modelo con esos parámetros aplicados.

- **Evaluación:** El fenotipo es lo que se evalúa para determinar la "aptitud" o "fitness" de una solución. Es la representación que se utiliza para medir qué tan buena es una solución respecto al problema planteado.

- **Interacción con el Entorno:** En algunos contextos, el fenotipo puede interactuar directamente con el entorno o con otros elementos del sistema, permitiendo una evaluación más completa de la solución.

**Importancia:**
El fenotipo es crucial porque es la representación tangible que se evalúa para guiar la evolución del algoritmo genético. Una correcta traducción del genotipo al fenotipo asegura que las operaciones genéticas generen soluciones válidas y efectivas.

---

### **Relación entre Genotipo y Fenotipo**

La relación entre genotipo y fenotipo en los algoritmos genéticos es análoga a la relación entre el ADN y las características físicas en organismos biológicos. Mientras que el genotipo contiene la información genética esencial para construir una solución, el fenotipo es la solución en sí misma que se evalúa y optimiza.

**Proceso Simplificado:**
1. **Inicialización:** Se generan individuos con genotipos aleatorios.
2. **Decodificación:** Cada genotipo se traduce en un fenotipo.
3. **Evaluación:** Se evalúa la aptitud de cada fenotipo.
4. **Selección:** Se seleccionan los mejores fenotipos para reproducirse.
5. **Reproducción:** Se aplican operaciones genéticas sobre los genotipos de los seleccionados para crear una nueva generación.
6. **Iteración:** Se repiten los pasos hasta cumplir con un criterio de parada (por ejemplo, alcanzar una solución suficientemente buena o un número máximo de generaciones).

---

### **Ejemplo Práctico**

**Problema:** Optimización de una función matemática.

- **Genotipo:** Una cadena binaria que codifica los valores de las variables de la función.
  
  - *Ejemplo:* `11001010` podría representar un conjunto específico de parámetros para la función.

- **Fenotipo:** Los valores decodificados de la cadena binaria que se utilizan para evaluar la función.
  
  - *Ejemplo:* La cadena `11001010` se decodifica a los valores `[102, 10]`, que son utilizados para calcular el valor de la función matemática.

**Proceso:**
1. **Generación Aleatoria:** Se crean varias cadenas binarias (genotipos) aleatoriamente.
2. **Decodificación:** Cada cadena se traduce en valores numéricos (fenotipos).
3. **Evaluación:** Se calcula el valor de la función para cada conjunto de valores.
4. **Selección y Reproducción:** Se seleccionan los mejores fenotipos y se combinan sus genotipos para crear nuevas soluciones.
5. **Iteración:** Se repite el proceso hasta encontrar el mínimo o máximo deseado de la función.

---

### **Conclusión**

Comprender la distinción y relación entre genotipo y fenotipo es fundamental para diseñar y aplicar efectivamente algoritmos genéticos. La **codificación adecuada del genotipo** facilita la exploración eficiente del espacio de soluciones, mientras que la **decodificación precisa al fenotipo** garantiza que las soluciones evaluadas sean válidas y útiles para resolver el problema en cuestión.

# Probabilidad de cruce
Es un valor aleatorio decimal $(0.0, \ 1.0)$ en el cual se obtiene para comprobar la probabilidad de cruce


# Mutación
Es el intercambio de características del gen del cromosoma

# Probabilidad de mutación
Valor el cual permite realizar la mutación, **tiende a ser pequeño**.

