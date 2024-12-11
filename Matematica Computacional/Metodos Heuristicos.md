
# Optimizacion Combinatoria
Se caracteriza por buscar las soluciones en un conjunto discreto.
- Problema de la mochila
- El problema del agente viajero
- El problema del ruteo de vehiculos

# Heuristicas
Una heuristica es un algoritmo aproximado que permite para resolver un problema de optimizacion mediante una aproximacion intuitiva, en la que la estructura del problema se utiliza de forma inteligente para obtener una buena solucion.

Se usan:
- En problemas de dificil solucion.
- Cuando no se conoce ningun metodo de solucion.
- Aunque existe un algoritmo exacto, su costo computacional es muy alto.


## Heuristica Local Search
- Se inicia con una solucion, no necesariamente buena.
- Se busca soluciones mejores en sus vecinos.
- No se memorizan soluciones obtenidas.

# Metaheuristica
Los procedimientos Metaheuristicos son una clase de metodos aproximados que estan diseados para resolver problemas difciles de optimizacion combinatoria, en los que los heuristicos clasicos no son efectivos. Los Metaheursticos proporcionan un marco general para crear nuevos algoritmos hibridos combinando diferentes conceptos derivados de
la inteligencia artificial, la evolucion biolgica y los mecanismos estadisticos

### Heuristicas

**Greedy:**

- **Idea:** Siempre elige la opción que parece mejor en ese momento, sin considerar las consecuencias a largo plazo.
- **Ejemplo:** En el problema del viajante, un algoritmo greedy podría elegir siempre la ciudad más cercana a la ciudad actual, sin importar si esa elección lleva a un camino más largo en el futuro.
- **Ventajas:** Simple y fácil de implementar.
- **Desventajas:** Puede quedar atrapado en óptimos locales y no encontrar la solución global óptima.


**Local Search:**

- **Idea:** Comienza en una solución inicial y explora el espacio de soluciones cercano para encontrar una solución mejor. Se mueve a un vecino mejor hasta que no se puede mejorar más.
- **Ejemplo:** Imagina que estás en una montaña y quieres encontrar el pico más alto. Local search te haría subir por la pendiente más empinada hasta llegar a una cima local.
- **Ventajas:** Puede encontrar soluciones de buena calidad rápidamente.
- **Desventajas:** Sufre del problema de los óptimos locales.



### Metaheurísticas

- **Iterated Local Search:**
    - **Idea:** Combina múltiples búsquedas locales. Después de encontrar un óptimo local, perturba la solución y comienza una nueva búsqueda local.
    - **Ejemplo:** Volviendo al ejemplo de la montaña, después de llegar a una cima local, podrías generar una nueva posición aleatoria y comenzar a subir nuevamente.
    - **Ventajas:** Es capaz de escapar de óptimos locales y explorar un espacio de soluciones más amplio


**Hill Climbing:**

- **Idea:** Similar al local search, pero con una diferencia: solo se mueve a un vecino mejor si este es estrictamente mejor que la solución actual.
- **Ventajas:** Simple y eficiente.
- **Desventajas:** Puede quedar atrapado en óptimos locales.

