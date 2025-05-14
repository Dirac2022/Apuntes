![[Pasted image 20250414103815.png]]
![[Pasted image 20250414103820.png]]

Perfecto, gracias por aclararlo. Aquí tienes **una explicación directa**, **el algoritmo paso a paso** y el **pseudocódigo** para cada uno: **Breadth-First Search**, **Iterative Deepening Search** y **Best-First Search**. También incluyo la **complejidad** y **cuándo usar cada uno**.

---

### 1. **Breadth-First Search (BFS)**

**Descripción breve:**  
Búsqueda por niveles. Recorre primero los nodos más cercanos al nodo inicial. Usa una cola FIFO. Garantiza la solución más corta si los costos son iguales.

**Algoritmo paso a paso:**

1. Crear una cola e insertar el nodo inicial.
2. Marcar el nodo como visitado.
3. Mientras la cola no esté vacía:  
    a. Sacar el primer nodo de la cola.  
    b. Si es la meta, detener.  
    c. Agregar todos los vecinos no visitados a la cola y marcarlos como visitados.

**Pseudocódigo:**

```
BFS(nodo_inicial):
    crear cola vacía Q
    crear conjunto vacío Visitados
    Q.encolar(nodo_inicial)
    Visitados.agregar(nodo_inicial)

    mientras Q no esté vacía:
        nodo ← Q.desencolar()
        si nodo es objetivo:
            retornar nodo
        para cada vecino en vecinos(nodo):
            si vecino no en Visitados:
                Q.encolar(vecino)
                Visitados.agregar(vecino)
```

**Complejidad:**

- Tiempo: O(bd)O(b^d)
- Espacio: O(bd)O(b^d)

**Cuándo usar:*
- Cuando los costos son iguales.
- Cuando necesitas el camino más corto.
- Cuando la memoria no es un gran problema.
### 2. **Iterative Deepening Search (IDS)**

**Descripción breve:**  
Búsqueda en profundidad con límite creciente. Cada iteración hace DFS hasta cierta profundidad. Usa menos memoria que BFS pero encuentra soluciones óptimas si los costos son iguales.

**Algoritmo paso a paso:**

1. Para profundidad límite desde 0 hasta infinito:  
    a. Ejecutar búsqueda en profundidad limitada desde el nodo inicial.  
    b. Si se encuentra la meta, terminar.

**Pseudocódigo:**

```
IDS(nodo_inicial):
    para límite desde 0 hasta ∞:
        resultado ← DLS(nodo_inicial, límite)
        si resultado ≠ NULL:
            retornar resultado

DLS(nodo, límite):
    si límite == 0 y nodo es objetivo:
        retornar nodo
    si límite > 0:
        para cada hijo en vecinos(nodo):
            resultado ← DLS(hijo, límite - 1)
            si resultado ≠ NULL:
                retornar resultado
    retornar NULL
```

**Complejidad:**

- Tiempo: O(bd)O(b^d)
- Espacio: O(d)O(d)

**Cuándo usar:**

- Cuando no conoces la profundidad de la solución.
- Cuando la memoria es limitada.
- Cuando necesitas solución óptima pero no puedes usar BFS.

### 3. **Best-First Search**

**Descripción breve:**  
Búsqueda guiada por heurística. Usa una función h(n)h(n) que estima qué tan cerca está un nodo de la meta. Selecciona el nodo con menor h(n)h(n). No garantiza solución óptima.

**Algoritmo paso a paso:**

1. Crear una cola de prioridad.
2. Insertar el nodo inicial con prioridad h(n)h(n).
3. Mientras la cola no esté vacía:  
    a. Sacar el nodo con menor h(n)h(n).  
    b. Si es meta, terminar.  
    c. Insertar sus vecinos no visitados con su heurística.

**Pseudocódigo:**

```
BestFirstSearch(nodo_inicial):
    crear cola de prioridad Q
    crear conjunto vacío Visitados
    Q.insertar(nodo_inicial, prioridad = h(nodo_inicial))

    mientras Q no esté vacía:
        nodo ← Q.extraer_min()
        si nodo es objetivo:
            retornar nodo
        Visitados.agregar(nodo)
        para cada vecino en vecinos(nodo):
            si vecino no en Visitados:
                Q.insertar(vecino, prioridad = h(vecino))
```

**Complejidad:**

- Tiempo: O(bd)O(b^d) en el peor caso
- Espacio: O(bd)O(b^d)

**Cuándo usar:**

- Cuando tienes una buena heurística.
- Cuando quieres velocidad sobre optimalidad.
- No garantiza camino más corto a menos que se use A*
-----

```python
import sys
from collections import deque
from utils import *

class Problem:
    def __init__(self, initial, goal=None):
        self.initial = initial
        self.goal = goal

    def actions(self, state):
        raise NotImplementedError

    def result(self, state, action):
        raise NotImplementedError

    def goal_test(self, state):
        if isinstance(self.goal, list):
            return is_in(state, self.goal)
        else:
            return state == self.goal

    def path_cost(self, c, state1, action, state2):
        return c + 1

    def value(self, state):
        raise NotImplementedError

class Node:
    def __init__(self, state, parent=None, action=None, path_cost=0):
        self.state = state
        self.parent = parent
        self.action = action
        self.path_cost = path_cost
        self.depth = 0
        if parent:
            self.depth = parent.depth + 1

    def __repr__(self):
        return "<Node {}>".format(self.state)

    def __lt__(self, node):
        return self.state < node.state

    def expand(self, problem):
        return [self.child_node(problem, action)
                for action in problem.actions(self.state)]

    def child_node(self, problem, action):
        next_state = problem.result(self.state, action)
        next_node = Node(next_state, self, action, problem.path_cost(self.path_cost, self.state, action, next_state))
        return next_node

    def solution(self):
        return [node.action for node in self.path()[1:]]

    def path(self):
        node, path_back = self, []
        while node:
            path_back.append(node)
            node = node.parent
        return list(reversed(path_back))

    def __eq__(self, other):
        return isinstance(other, Node) and self.state == other.state

    def __hash__(self):
        return hash(self.state)

def breadth_first_tree_search(problem):
    frontier = deque([Node(problem.initial)])
    while frontier:
        node = frontier.popleft()
        if problem.goal_test(node.state):
            return node
        frontier.extend(node.expand(problem))
    return None

def depth_first_tree_search(problem):
    frontier = [Node(problem.initial)]
    while frontier:
        node = frontier.pop()
        if problem.goal_test(node.state):
            return node
        frontier.extend(node.expand(problem))
    return None

def depth_first_graph_search(problem):
    frontier = [(Node(problem.initial))]
    explored = set()
    while frontier:
        node = frontier.pop()
        if problem.goal_test(node.state):
            return node
        explored.add(node.state)
        frontier.extend(child for child in node.expand(problem)
                        if child.state not in explored and child not in frontier)
    return None

def breadth_first_graph_search(problem):
    node = Node(problem.initial)
    if problem.goal_test(node.state):
        return node
    frontier = deque([node])
    explored = set()
    while frontier:
        node = frontier.popleft()
        explored.add(node.state)
        for child in node.expand(problem):
            if child.state not in explored and child not in frontier:
                if problem.goal_test(child.state):
                    return child
                frontier.append(child)
    return None

```
