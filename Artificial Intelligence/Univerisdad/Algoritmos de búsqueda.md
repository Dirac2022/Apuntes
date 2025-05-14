
---

# 🎯 Algoritmos de Búsqueda en Inteligencia Artificial

---

## 1. 🔵 Búsqueda en Amplitud (BFS – Breadth-First Search)

### 📘 Teoría:

- Explora primero los nodos más cercanos a la raíz (nivel por nivel).
- Usa una **cola FIFO**.
- **Completa** y **óptima** si el costo de cada paso es igual.
- Puede requerir mucha memoria.

### ⚙️ Características:

- Estructura: **cola**
- Complejidad temporal: $\mathcal{O}(b^d)$
- Complejidad espacial: $\mathcal{O}(b^d)$

### 🧠 Pseudocódigo:

```python
BFS(inicio, objetivo):
    crear cola ← nueva cola FIFO
    insertar nodo inicio en cola
    mientras cola no esté vacía:
        nodo ← sacar de cola
        si nodo == objetivo:
            retornar solución
        para cada hijo en sucesores(nodo):
            si hijo no ha sido visitado:
                marcar como visitado
                insertar hijo en cola
```

---

## 2. 🔴 Búsqueda en Profundidad (DFS – Depth-First Search)

### 📘 Teoría:

- Explora primero el camino más profundo antes de retroceder.
- Usa una **pila (LIFO)**.
- No es completa en espacios infinitos y no es óptima.
- Consume poca memoria.

### ⚙️ Características:

- Estructura: **pila**
- Complejidad temporal: $\mathcal{O}(b^m)$
- Complejidad espacial: $\mathcal{O}(bm)$

### 🧠 Pseudocódigo:

```python
DFS(inicio, objetivo):
    crear pila ← nueva pila LIFO
    insertar nodo inicio en pila
    mientras pila no esté vacía:
        nodo ← sacar de pila
        si nodo == objetivo:
            retornar solución
        para cada hijo en sucesores(nodo) en orden inverso:
            si hijo no ha sido visitado:
                marcar como visitado
                insertar hijo en pila
```

---

## 3. 🟢 Búsqueda de Costo Uniforme (UCS – Uniform Cost Search)

### 📘 Teoría:

- Expande el nodo con **menor costo acumulado (g(n))**.
- Usa una **cola de prioridad ordenada por costo**.
- Es **completa y óptima**, incluso si los pasos tienen diferentes costos.
- Variante de Dijkstra para búsqueda en IA.

### ⚙️ Características:

- Estructura: **cola de prioridad (por costo g)**
- Complejidad: $\mathcal{O}(b^d)$, depende del número de nodos y del costo más pequeño

### 🧠 Pseudocódigo:

```python
UCS(inicio, objetivo):
    crear frontera ← cola de prioridad ordenada por costo g(n)
    insertar nodo inicio con costo 0
    mientras frontera no esté vacía:
        nodo ← sacar nodo con menor g(n)
        si nodo == objetivo:
            retornar solución
        para cada hijo en sucesores(nodo):
            costo ← g(nodo) + costo(nodo, hijo)
            si hijo no está en frontera o tiene mayor costo:
                actualizar o insertar hijo con nuevo costo
```

---

## 4. 🟡 Búsqueda Primero el Mejor (GBF – Greedy Best-First Search)

### 📘 Teoría:

- Expande el nodo que **parece más cercano al objetivo** según una **heurística h(n)**.
- **No es óptimo ni completo**.
- Muy eficiente si la heurística es buena.

### ⚙️ Características:

- Estructura: **cola de prioridad (por h(n))**
- Ideal para búsquedas rápidas con recursos limitados

### 🧠 Pseudocódigo:

```python
GBF(inicio, objetivo, h):
    crear frontera ← cola de prioridad ordenada por h(n)
    insertar nodo inicio
    mientras frontera no esté vacía:
        nodo ← sacar nodo con menor h(n)
        si nodo == objetivo:
            retornar solución
        para cada hijo en sucesores(nodo):
            si hijo no ha sido visitado:
                insertar hijo en frontera
```

---

## 5. 🟣 Búsqueda A Estrella (A*)

### 📘 Teoría:

- Combina lo mejor de UCS y GBF:  
    Usa $f(n) = g(n) + h(n)$
    
- Es **completa y óptima** si:
    - h(n) es **admisible** (no sobreestima)
    - h(n) es **consistente** (monótona)

### ⚙️ Características:

- Estructura: **cola de prioridad (por f(n))**
- Ampliamente usada en planificación y navegación

### 🧠 Pseudocódigo:

```python
A_Estrella(inicio, objetivo, h):
    crear frontera ← cola de prioridad ordenada por f(n) = g(n) + h(n)
    insertar nodo inicio con g=0 y f=h(inicio)
    mientras frontera no esté vacía:
        nodo ← sacar nodo con menor f(n)
        si nodo == objetivo:
            retornar solución
        para cada hijo en sucesores(nodo):
            g_nuevo ← g(nodo) + costo(nodo, hijo)
            f_nuevo ← g_nuevo + h(hijo)
            si hijo no está en frontera o g_nuevo es menor:
                insertar o actualizar hijo con nuevos valores
```

---

## 🧠 Comparación rápida

|Algoritmo|Completo|Óptimo|Estructura|Estrategia|
|---|---|---|---|---|
|**BFS**|✔️|✔️|Cola FIFO|Explora nivel por nivel|
|**DFS**|❌|❌|Pila LIFO|Explora camino profundo primero|
|**UCS**|✔️|✔️|Cola por g(n)|Expande el camino más barato|
|**GBF**|❌|❌|Cola por h(n)|Elige el más prometedor (heurística)|
|**A***|✔️|✔️|Cola por f(n)|Balancea costo y heurística|

---

¿Te gustaría que te arme visualizaciones Mermaid, diagramas de flujo o una tabla comparativa en `.md` para Obsidian? También puedo generar ejemplos paso a paso para cada algoritmo.


¡Buena observación! 🙌  
Las letras como bb, dd, mm, nn, etc., son **parámetros estándar** que se utilizan para analizar la **complejidad temporal y espacial** de los algoritmos de búsqueda. Aquí te explico **qué significa cada uno** en este contexto:

---

## 🧮 Parámetros usados en el análisis de complejidad

|Símbolo|Significado|Ejemplo práctico|
|---|---|---|
|bb|**Factor de ramificación (branching factor)**: promedio de hijos por nodo|Si cada estado genera 2 nuevos estados → b=2b = 2|
|dd|**Profundidad de la solución más cercana** (óptima si hay varias)|Si la solución está a 4 pasos del nodo raíz → d=4d = 4|
|mm|**Profundidad máxima del espacio de búsqueda** (puede ser infinito en algunos casos)|Si exploras hasta el nivel 100 → m=100m = 100|
|nn|**Número total de nodos del espacio de búsqueda** (puede crecer exponencialmente)|En espacios grandes o sin solución|

---

## 🎯 Aplicaciones en la complejidad

- **BFS** (Búsqueda en amplitud):
    
    - Tiempo: O(b^d)
    - Espacio: O(b^d)  
        (porque guarda todos los nodos del nivel actual y el siguiente)
        
- **DFS** (Búsqueda en profundidad):
    
    - Tiempo: O(b^m)
    - Espacio: O(bm)  
        (solo guarda la profundidad del camino actual)
- **UCS**, **A***:
    
    - Tiempo y espacio: En el peor caso, **exponencial en d**
        → O(b^d), aunque depende del número de caminos y del costo mínimo por paso.

---

## 🧠 ¿Por qué se usan estas letras?

Porque nos permiten **comparar algoritmos sin depender de un problema específico**, usando una notación general que funciona para árboles, grafos, rompecabezas, búsquedas en mapas, etc.

---

¿Te gustaría que prepare una tarjeta visual tipo ficha técnica con todos estos valores explicados? También puedo mostrar cómo estos números crecen con ejemplos numéricos.