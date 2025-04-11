
# Heurística

En el contexto de los algoritmos de búsqueda, una **heurística** es una función que estima el costo para alcanzar un objetivo desde un estado determinado. Las heurísticas son útiles porque ayudan a guiar el proceso de búsqueda, permitiendo que un algoritmo encuentre soluciones de manera más eficiente.

### Heurística Admisible

Una **heurística es admisible** si nunca sobrestima el costo real para alcanzar el objetivo desde un estado dado. Esto significa que, para cada nodo $n$:

$$ h(n) \leq h^*(n) $$

donde:
- $h(n)$: valor de la heurística en el nodo $n$.
- $h^*(n)$: costo real (óptimo) para alcanzar el objetivo desde el nodo $n$.

**Características de la Heurística Admisible:**

- **Mejor Garantía**: Si el algoritmo (como A*) utiliza una heurística admisible, garantizará que encontrará la solución óptima.
- **Ejemplo**: En un problema de navegación, si estás tratando de estimar la distancia a un destino y usas la distancia en línea recta (como la distancia euclidiana), esta es un ejemplo de una heurística admisible porque nunca puede ser mayor que la distancia real que tendrías que viajar.

### Heurística Consistente

Una **heurística es consistente** (o monótona) si satisface la siguiente condición para cualquier par de nodos $n$ y $m$:

$$ h(n) \leq c(n, m) + h(m) $$

donde:

- $c(n, m)$: costo para ir de $n$ a $m$.
- $h(n)$: valor de la heurística en $n$.
- $h(m)$: valor de la heurística en $m$.

**Características de la Heurística Consistente:**

- **Mejora de Eficiencia**: Asegura que el costo estimado desde $n$ hasta el objetivo no supera el costo real incurrido al ir de $n$ a otro nodo $m$ más el costo estimado desde $m$.
- **Evita Re-exploración**: Si un nodo ya ha sido expandido y se encuentra en la frontera del árbol de búsqueda, no tendrá que ser expandido de nuevo, lo que mejora la eficiencia del algoritmo.

### Comparación entre Heurística Admisible y Consistente

|**Característica**|**Heurística Admisible**|**Heurística Consistente**|
|---|---|---|
|**Definición**|No sobreestima el costo real al objetivo.|Cumple con una relación de costos entre nodos.|
|**Garantía**|Asegura que se encuentra una solución óptima.|Aumenta la eficiencia y evita expansión innecesaria de nodos.|
|**Relación**|Todas las heurísticas consistentes son admisibles.|No todas las heurísticas admisibles son consistentes.|
|**Ejemplo**|Distancia euclidiana en un mapa.|Heurísticas que son válidas en problemas de recorrido.|


- **Heurística Admisible**: Nunca sobrestima el costo al objetivo, asegurando soluciones óptimas.
- **Heurística Consistente**: Cumple la relación de costos, mejorando la eficiencia y evitando expansiones innecesarias de nodos.
