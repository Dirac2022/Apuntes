Algorithms and Data Structures for Massive Datasets


Una estructura de datos es una forma de organizar, gestionar y almacenar datos para que puedan utilizarse de manera eficiente. Estas estructuras permiten realizar operaciones específicas sobre los datos, como búsqueda, eliminación y ordenamiento.

Las estructuras de datos pueden clasificarse de varias maneras

1. **Según su organización**
	- Estructuras de datos lineales: Arreglos, listas enlazadas, pilas, colas.
	- Estructuras de datos no lineales: Árboles, grafos.
2. **Según su tipo de acceso
	- Acceso directo: Arreglos
	- Acceso secuencial: Listas enlazadas
	- Acceso jerárquico: Árboles.
	- Acceso basado en relaciones: Grafos.
3. **Según su implementación
	- Estáticas: Tamaño fijo, como arreglos.
	- Dinámicas: pueden crecer o reducirse en tiempo de ejecución, como listas enlazadas.


# Diferencia entre algoritmos y estructura de datos

Un **algoritmo** es una secuencia de pasos bien definidos para resolver un problema. Es independiente de la estructura de datos utilizada.


| Característica | Algoritmo                             | Estructura de Datos                |
| -------------- | ------------------------------------- | ---------------------------------- |
| Propósito      | Resuelve un problema                  | Almacena y organiza datos          |
| Forma          | Serie de pasos lógicos                | Modelo de organización             |
| Independencia  | Independiente de la implementación    | Requiere implementación específica |
| Ejemplo        | Algoritmo de ordenamiento (QuickSort) | Árbol binario de búsqueda          |

Ejemplo de QuickSort
```python
def quicksort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[len(arr) // 2]
    izquierda = [x for x in arr if x < pivot]
    centro = [x for x in arr if x == pivot]
    derecha = [x for x in arr if x > pivot]
    return quicksort(izquierda) + centro + quicksort(derecha)

arr = [3, 6, 8, 10, 1, 2, 1]
print("Arreglo ordenado:", quicksort(arr))

```


## **Introducción a las Estructuras de Datos**

Las estructuras de datos son fundamentales en la programación, ya que permiten organizar y manipular datos de manera eficiente. En esta clase exploraremos los conceptos básicos de las estructuras de datos, su relación con los algoritmos y cómo plantear problemas de manera efectiva. También veremos ejemplos prácticos como el problema de la "mochila" y la abstracción de problemas.

---

## **1. Definición y descripción de una estructura de datos**

Una **estructura de datos** es una forma de organizar, gestionar y almacenar datos para que puedan utilizarse de manera eficiente. Estas estructuras permiten realizar operaciones específicas sobre los datos, como búsqueda, inserción, eliminación y ordenamiento.

### **Clasificación de las estructuras de datos**

Las estructuras de datos pueden clasificarse de varias maneras:

1. **Según su organización:**
    
    - **Estructuras de datos lineales:** Arreglos, listas enlazadas, pilas, colas.
        
    - **Estructuras de datos no lineales:** Árboles, grafos.
        
2. **Según su tipo de acceso:**
    
    - **Acceso directo:** Arreglos.
        
    - **Acceso secuencial:** Listas enlazadas.
        
    - **Acceso jerárquico:** Árboles.
        
    - **Acceso basado en relaciones:** Grafos.
        
3. **Según su implementación:**
    
    - **Estáticas:** Tamaño fijo, como arreglos.
        
    - **Dinámicas:** Pueden crecer o reducirse en tiempo de ejecución, como listas enlazadas.
        

### **Ejemplo básico en Python**

A continuación, mostramos una implementación simple de un arreglo en Python:

```python
# Definición de un arreglo en Python
arreglo = [10, 20, 30, 40, 50]

# Acceso a elementos
print("Primer elemento:", arreglo[0])  # 10
print("Último elemento:", arreglo[-1])  # 50

# Modificación de un elemento
arreglo[2] = 99
print("Arreglo modificado:", arreglo)
```

---

## **2. Diferencia entre algoritmos y estructuras de datos**

### **¿Qué es un algoritmo?**

Un **algoritmo** es una secuencia de pasos bien definidos para resolver un problema. Es independiente de la estructura de datos utilizada.

### **Diferencia clave**

|Característica|Algoritmo|Estructura de Datos|
|---|---|---|
|Propósito|Resuelve un problema|Almacena y organiza datos|
|Forma|Serie de pasos lógicos|Modelo de organización|
|Independencia|Independiente de la implementación|Requiere implementación específica|
|Ejemplo|Algoritmo de ordenamiento (QuickSort)|Árbol binario de búsqueda|

Ejemplo de algoritmo de ordenamiento (QuickSort) en Python:

```python
def quicksort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[len(arr) // 2]
    izquierda = [x for x in arr if x < pivot]
    centro = [x for x in arr if x == pivot]
    derecha = [x for x in arr if x > pivot]
    return quicksort(izquierda) + centro + quicksort(derecha)

arr = [3, 6, 8, 10, 1, 2, 1]
print("Arreglo ordenado:", quicksort(arr))
```

---

## **3. Planteamiento de problemas y "Setting Goals"**

Antes de implementar una solución, es crucial formular correctamente el problema. Para ello, se siguen los siguientes pasos:

1. **Entender el problema:** Identificar entrada, salida y restricciones.
    
2. **Definir objetivos:** ¿Buscamos optimizar memoria, tiempo o simplicidad?
    
3. **Elegir una estructura de datos adecuada:** Dependerá de la operación más frecuente.
    
4. **Diseñar el algoritmo:** Implementación lógica para resolver el problema.
    
5. **Evaluar y optimizar:** Medir eficiencia y mejorar si es necesario.
    

Ejemplo de **planteamiento de problemas**:

- **Problema:** Queremos buscar un elemento en una lista.
    
- **Objetivo:** Encontrar el número lo más rápido posible.
    
- **Posibles soluciones:**
    
    - Usar una **búsqueda secuencial** (si la lista es pequeña).
        
    - Usar una **búsqueda binaria** (si la lista está ordenada).
        

Ejemplo de búsqueda binaria en Python:

```python
def busqueda_binaria(arr, objetivo):
    izquierda, derecha = 0, len(arr) - 1
    while izquierda <= derecha:
        medio = (izquierda + derecha) // 2
        if arr[medio] == objetivo:
            return medio
        elif arr[medio] < objetivo:
            izquierda = medio + 1
        else:
            derecha = medio - 1
    return -1

lista = [1, 3, 5, 7, 9, 11]
elemento = 5
indice = busqueda_binaria(lista, elemento)
print(f"Elemento {elemento} encontrado en índice {indice}" if indice != -1 else "Elemento no encontrado")
```

---

## **4. Ejemplo práctico: La mochila y abstracción del problema**

### **Problema de la mochila (Knapsack Problem)**

El problema de la **mochila** es un problema clásico de optimización donde se busca seleccionar los objetos que maximicen el valor total sin exceder la capacidad de la mochila.

#### **Ejemplo:**

- **Entrada:** Una mochila con capacidad de 10 kg y objetos con pesos y valores diferentes.
    
- **Salida:** Máximo valor posible que se puede llevar sin exceder la capacidad.
    

Existen dos versiones:

1. **Mochila 0/1:** No se puede llevar fracciones de los objetos.
    
2. **Mochila fraccionaria:** Se pueden llevar fracciones de los objetos.
    

#### **Código en Python (Mochila Fraccionaria - Algoritmo Greedy)**

```python
class Objeto:
    def __init__(self, peso, valor):
        self.peso = peso
        self.valor = valor
        self.ratio = valor / peso  # Valor por unidad de peso

def mochila_fraccionaria(capacidad, objetos):
    objetos.sort(key=lambda x: x.ratio, reverse=True)  # Ordenamos por valor/peso
    valor_total = 0.0

    for obj in objetos:
        if capacidad >= obj.peso:
            capacidad -= obj.peso
            valor_total += obj.valor
        else:
            valor_total += obj.ratio * capacidad
            break
    
    return valor_total

# Definimos objetos con peso y valor
objetos = [Objeto(10, 60), Objeto(20, 100), Objeto(30, 120)]
capacidad_mochila = 50

print("Máximo valor que se puede llevar:", mochila_fraccionaria(capacidad_mochila, objetos))
```

---

## **Conclusión**

- Las **estructuras de datos** nos permiten organizar la información de manera eficiente.
    
- Los **algoritmos** son pasos lógicos para resolver problemas y dependen de la estructura de datos elegida.
    
- **Plantear correctamente un problema** nos ayuda a seleccionar la mejor estructura de datos y algoritmo.
    
- Ejemplos como la **mochila** muestran cómo los problemas del mundo real pueden resolverse usando estructuras y algoritmos adecuados.
    

### **¿Qué sigue?**

El próximo tema puede profundizar en estructuras de datos como **listas enlazadas, pilas y colas**. ¿Quieres seguir con eso?




## **Mejoras en Colas de Prioridad: d-ary Heaps**

En esta clase, exploraremos cómo las colas de prioridad pueden mejorarse mediante el uso de **d-ary heaps**, una generalización de los montículos binarios (binary heaps). Analizaremos la **necesidad de manejar prioridades eficientemente**, cómo evolucionamos de **listas ordenadas a colas de prioridad**, la **API y operaciones principales**, el **análisis de rendimiento** y algunos **casos de uso** prácticos como encontrar los _k_ elementos más grandes.

---

# **1. Problema de Manejo de Prioridades en la Práctica**

El manejo de prioridades es un problema fundamental en la computación. Muchas aplicaciones requieren procesar elementos según su prioridad en lugar de en orden de llegada. Algunos ejemplos incluyen:

- **Sistemas operativos:** Planificación de procesos según prioridad.
    
- **Redes y telecomunicaciones:** Manejo de paquetes de datos priorizados.
    
- **Inteligencia artificial:** Algoritmos de búsqueda (A*, Dijkstra).
    
- **Simulaciones:** Eventos que ocurren en orden de prioridad.
    

Para resolver este problema, necesitamos una estructura eficiente para administrar elementos con prioridades y realizar operaciones como:

- **Insertar un nuevo elemento con prioridad.**
    
- **Actualizar la prioridad de un elemento existente.**
    
- **Extraer el elemento de mayor prioridad rápidamente.**
    

Diferentes estructuras de datos pueden utilizarse para resolver este problema, cada una con ventajas y desventajas.

---

# **2. De Listas Ordenadas a Colas de Prioridad**

Una **cola de prioridad** es una estructura de datos que permite insertar elementos y extraer el de mayor prioridad eficientemente. Veamos algunas implementaciones comunes y su eficiencia:

### **2.1. Usando una Lista Ordenada**

Podemos mantener una lista ordenada donde la prioridad más alta siempre esté al inicio.

- **Inserción:** O(n)O(n) (porque hay que mantener el orden).
    
- **Extracción del máximo:** O(1)O(1) (el primer elemento siempre es el mayor).
    

Código en Python:

```python
class ListaOrdenada:
    def __init__(self):
        self.lista = []

    def insertar(self, elemento):
        self.lista.append(elemento)
        self.lista.sort(reverse=True)  # Orden descendente para que el mayor esté primero

    def extraer_maximo(self):
        return self.lista.pop(0) if self.lista else None

pq = ListaOrdenada()
pq.insertar(5)
pq.insertar(2)
pq.insertar(8)
pq.insertar(3)
print("Elemento de mayor prioridad:", pq.extraer_maximo())  # 8
```

**Problema:** La inserción es costosa, O(n)O(n), lo que hace que esta implementación no sea ideal para grandes volúmenes de datos.

---

### **2.2. Usando un Heap Binario (Binary Heap)**

Un **montículo binario (binary heap)** es una estructura de árbol casi completo en la que:

1. La raíz tiene la prioridad más alta.
    
2. Cada nodo padre tiene prioridad mayor o igual que sus hijos.
    

Esto permite que la **inserción** y la **extracción del máximo** se realicen en **O(log⁡n)O(\log n)**.

**Problema:** Cuando el número de elementos es muy grande, la profundidad del árbol sigue siendo alta.

---

### **2.3. Mejorando con d-ary Heaps**

En un **d-ary heap**, cada nodo tiene **d hijos en lugar de solo 2**, reduciendo la profundidad del árbol y haciendo que ciertas operaciones sean más eficientes.

#### **Ventajas del d-ary heap**

- **Menos niveles** que un binary heap, lo que reduce el número de comparaciones.
    
- **Mejor rendimiento en la extracción del máximo** cuando se usa en arquitecturas con acceso a memoria más costoso.
    

**Desventajas:**

- **Inserción y heapify pueden ser más costosos**, ya que hay más hijos a comparar.
    

---

# **3. API y Operaciones Principales de un d-ary Heap**

## **Definición Formal**

Un **d-ary heap** es una generalización de un heap binario, donde cada nodo tiene hasta **d hijos**.

- Si d=2d = 2, obtenemos un **binary heap**.
    
- Si d=3d = 3, obtenemos un **ternary heap**.
    
- Si d=4d = 4, obtenemos un **quaternary heap**, y así sucesivamente.
    

Las **propiedades del d-ary heap** son:

1. **Estructura casi completa:** Todos los niveles están llenos excepto el último.
    
2. **Propiedad de heap:** La clave de cada nodo padre es mayor (max-heap) o menor (min-heap) que la de sus hijos.
    

---

## **3.1. Algoritmos Principales**

### **Algoritmo de Inserción**

1. Agregar el nuevo elemento al final del heap.
    
2. Subirlo en el árbol ("heapify-up") comparándolo con su padre hasta restaurar la propiedad del heap.
    

**Complejidad:**

- O(log⁡dn)O(\log_d n) (mejor que O(log⁡2n)O(\log_2 n) en heaps binarios).
    

#### **Algoritmo**

insertar(heap, elemento):\text{insertar(heap, elemento)}:

1. Agregar el elemento al final.
    
2. Comparar con su padre:
    
    - Si es mayor, intercambiar y repetir.
        
    - Si no, detener.
        

---

### **Algoritmo de Extracción del Máximo**

1. Se devuelve el nodo raíz (de mayor prioridad).
    
2. Se reemplaza con el último nodo.
    
3. Se baja ("heapify-down") hasta restaurar la propiedad del heap.
    

**Complejidad:**

- O(dlog⁡dn)O(d \log_d n) (peor que un heap binario si dd es grande).
    

#### **Algoritmo**

extraer_max(heap):\text{extraer\_max(heap)}:

1. Guardar la raíz (máximo).
    
2. Mover el último elemento a la raíz.
    
3. Comparar con los hijos y bajar hasta restaurar el orden.
    

---

# **4. Implementación de un d-ary Heap en Python**

```python
class DaryHeap:
    def __init__(self, d):
        self.d = d
        self.heap = []

    def padre(self, i):
        return (i - 1) // self.d

    def hijo(self, i, k):
        return self.d * i + k + 1

    def insertar(self, valor):
        self.heap.append(valor)
        self._heapify_up(len(self.heap) - 1)

    def _heapify_up(self, i):
        while i > 0 and self.heap[i] > self.heap[self.padre(i)]:
            self.heap[i], self.heap[self.padre(i)] = self.heap[self.padre(i)], self.heap[i]
            i = self.padre(i)

    def extraer_max(self):
        if not self.heap:
            return None
        if len(self.heap) == 1:
            return self.heap.pop()

        maximo = self.heap[0]
        self.heap[0] = self.heap.pop()
        self._heapify_down(0)
        return maximo

    def _heapify_down(self, i):
        mayor = i
        for k in range(self.d):
            hijo_idx = self.hijo(i, k)
            if hijo_idx < len(self.heap) and self.heap[hijo_idx] > self.heap[mayor]:
                mayor = hijo_idx
        if mayor != i:
            self.heap[i], self.heap[mayor] = self.heap[mayor], self.heap[i]
            self._heapify_down(mayor)

# Uso del d-ary heap
heap = DaryHeap(3)  # Ternary Heap
heap.insertar(10)
heap.insertar(20)
heap.insertar(15)
heap.insertar(30)

print("Elemento de mayor prioridad:", heap.extraer_max())  # 30
```

---

# **5. Análisis de Rendimiento y Casos de Uso**

|Operación|Binary Heap (d=2d=2)|d-ary Heap (d>2d>2)|
|---|---|---|
|Inserción|O(log⁡2n)O(\log_2 n)|O(log⁡dn)O(\log_d n)|
|Extracción máx|O(log⁡2n)O(\log_2 n)|O(dlog⁡dn)O(d \log_d n)|

Casos de uso:

- **Dijkstra/A*:** Ternary heaps pueden mejorar el rendimiento.
    
- **Juegos y simulaciones:** Eventos priorizados.
    
- **Procesamiento de streams:** Encontrar los _k_ elementos más grandes.
    

---

### **Conclusión**

- Los **d-ary heaps** son una mejora de los binary heaps.
    
- Reducen la profundidad, mejorando inserciones pero aumentando el costo de extracción.
    
- Son útiles en algoritmos de grafos y procesamiento de datos.
    

¿Quieres profundizar más en algún aspecto? 🚀
