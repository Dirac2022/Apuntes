1. Definir la estructura Nodo:
   - Atributos: x, y (coordenadas), g (costo acumulado), h (heurística), f (g + h), padre.
   - Métodos: Calcular f() y comparar nodos (para la cola de prioridad).

2. Función Heurística (Distancia de Manhattan):
   - Calcular |x1 - x2| + |y1 - y2|.

3. Función esVálido(x, y, grid):
   - Verificar si (x, y) está dentro del mapa y no es un obstáculo.

4. Función esDiagonalVálida(x1, y1, x2, y2, grid):
   - Verificar si las celdas adyacentes a un movimiento diagonal están libres de obstáculos.

5. Función reconstruirRuta(nodo):
   - Reconstruir la ruta desde el nodo final hasta el inicio usando los punteros al padre.

6. Función A*(grid, inicio, destino):
   - Definir movimientos posibles (8 direcciones: arriba, abajo, izquierda, derecha, diagonales).
   - Definir costos asociados a cada movimiento (1.0 para rectos, 1.414 para diagonales).
   - Inicializar lista abierta (cola de prioridad) y lista cerrada (diccionario/mapa).
   - Crear nodo inicial y agregarlo a la lista abierta.

   - Mientras la lista abierta no esté vacía:
     a. Obtener el nodo con menor f(n) de la lista abierta.
     b. Si el nodo actual es el destino, reconstruir y devolver la ruta.
     c. Marcar el nodo actual como visitado (agregar a la lista cerrada).
     d. Para cada vecino:
        i. Calcular las coordenadas del vecino.
        ii. Si el vecino es válido y no está en la lista cerrada:
            - Si el movimiento es diagonal, verificar si es válido.
            - Calcular nuevo g (costo acumulado) y h (heurística).
            - Crear un nuevo nodo vecino.
            - Agregar el vecino a la lista abierta.

   - Si no se encuentra una ruta, devolver un vector vacío.

7. Función Principal:
   - Definir el mapa con obstáculos (1 = obstáculo, 0 = libre).
   - Definir punto de inicio y destino.
   - Ejecutar A* y mostrar la ruta encontrada.


# read

# Algoritmo A\* (A Estrella)

El algoritmo A\* es un algoritmo de búsqueda de rutas que encuentra el camino más corto entre un punto de inicio y un punto de destino en un grafo o una cuadrícula. Es ampliamente utilizado en inteligencia artificial, robótica, videojuegos y sistemas de navegación.

El algoritmo A\* combina dos enfoques:

1. **Búsqueda informada:** Utiliza una heurística para estimar el costo restante hasta el objetivo.
2. **Búsqueda de costo uniforme:** Garantiza que el camino encontrado sea el más corto en términos de costo acumulado.

## Función de Evaluación
El algoritmo evalúa nodos utilizando la función:

**$$
f(n) = g(n) + h(n)
$$

Donde:
- $g(n)$: Costo acumulado desde el nodo inicial hasta el nodo actual $n$.
- $h(n)$: Heurística, una estimación del costo desde el nodo actual $n$ hasta el nodo destino.

## Algoritmo A\*

1. **Inicialización:**
   - Agrega el nodo inicial a la lista abierta con $g(n) = 0$ y $h(n)$ calculado mediante la heurística.

2. **Bucle Principal:**
   - Mientras la lista abierta no esté vacía:
     a. Selecciona el nodo con el menor valor $f(n)$ de la lista abierta.
     b. Si este nodo es el destino, reconstruye y devuelve la ruta.
     c. Mueve el nodo actual a la lista cerrada.
     d. Para cada vecino del nodo actual:
        - Calcula $g(n)$ para el vecino.
        - Si el vecino no está en la lista abierta o cerrada, o si se encontró un camino más corto, actualiza su $g(n)$ y $f(n)$.
        - Agrega el vecino a la lista abierta.

3. **Finalización:**
   - Si la lista abierta se vacía y no se ha encontrado el destino, no existe una ruta válida.

---

## **Heurísticas en A\***

La heurística $h(n)$ es crucial para la eficiencia del algoritmo. Debe ser:
1. **Admisible:** Nunca sobrestimar el costo real hasta el destino.
2. **Consistente (o monótona):** Para cualquier nodo $n$ y su sucesor $n'$, $h(n) \leq g(n') + h(n')$.

### **Heurísticas Comunes**
- **Distancia de Manhattan:** Para movimientos en 4 direcciones (arriba, abajo, izquierda, derecha).
- **Distancia de Chebyshev:** Para movimientos en 8 direcciones (incluyendo diagonales).
- **Distancia Euclidiana:** Para movimientos en cualquier dirección, pero no siempre es admisible en cuadrículas.
## **Ejemplo Gráfico**

Supongamos un mapa con obstáculos:

```
0 0 0 0 0
0 1 1 1 0
0 1 0 0 0
0 1 0 1 0
0 0 0 1 0
```

- **Inicio:** (0, 0)
- **Destino:** (4, 4)

El algoritmo A\* explorará los nodos, evitando los obstáculos (1), y encontrará la ruta más corta, como:
$$
(0, 0) \rightarrow (1, 0) \rightarrow (2, 0) \rightarrow (3, 0) \rightarrow (4, 0) \rightarrow (4, 1) \rightarrow (4, 2) \rightarrow (4, 3) \rightarrow (4, 4)
$$
