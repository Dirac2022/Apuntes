


- **Parent (Padre):** En una estructura de conjuntos disjuntos, cada elemento (o nodo) en el conjunto tiene un padre. El padre de un elemento es otro elemento del conjunto al que pertenece. Los conjuntos disjuntos se organizan en una estructura de árbol, donde cada nodo apunta a su padre. El nodo que no tiene un padre se considera la raíz del árbol. La búsqueda del padre (también conocida como "find") se utiliza para determinar a qué conjunto pertenece un elemento.


- **Rank (Rango):** El rango de un nodo en un conjunto disjunto se utiliza para optimizar las operaciones de unión (o "union") en la estructura. Representa una estimación de la altura del árbol. Durante la operación de unión, se intenta fusionar el árbol más pequeño (menor rango) con el árbol más grande (mayor rango). Esto ayuda a mantener el árbol equilibrado y reduce la altura total del árbol, lo que a su vez mejora el rendimiento de las operaciones de búsqueda y unión.