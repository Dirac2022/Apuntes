Un **MST** de un grafo con costos en las aristas es un árbol generador cuyo costo (la suma de costos de sus aristas) no supera el costo de cualquier otro árbol generador.

## Algoritmo Boruvka
El algoritmo empieza considerando a cada nodo del grafo como una componente distinta y continúa seleccionando todos los arcos de menor coste que incidan en cada una de ellas, para posteriormente reformular las componentes resultantes

A partir de ahí, repite el proceso buscando en cada etapa los **arcos de coste mínimo** que inciden en cada componente, evitando que se formen ciclos, hasta que solo queda una.

**algoritmoBoruvka(Grafo G)**
$T$ $\leftarrow$ un bosque formado por vértices de $G$ sin aristas (componente). 
Mientras $T$ no sea un árbol generador
- Para cada componente $T_i$ de $T$ elegir la arista con menor peso $e_i$ que no forme circuito.
- Agregar $e_i$ a $T$.
FinMientras
**fin_algoritmoBoruvka**

### Algoritmo Boruvka
```
mapa parent // vertice : vertice
mapa rank   // vertice : int

Inicializa parent y rank

Define funcion parent
Define funcion Union

int n <- numero de vertices
set mst

Mientras n > 1
	mapa minAristas // {vertice: arista}
		Para cada arista en aristas // aristas del grafo G 
		set1 <- padre de vertice 1 de arista
		set2 <- padre de vertice 2 de arista
		Si set1 != set2
			Si arista < minAristas[set1]
				minAristas[set1] <- arista
			Si arista < minAristas[set2]
				minAristas[set2] <- arista
				
	Para cada entrada en minAristas
		set1 <- padre de vertice 1 de arista
		set2 <- padre de vertice 2  de arista
		si set1 != set2
			Agrega arista a mst
			une set1 y set2
			n --
```


## Algoritmo de Kruskal
- Escogemos una arista de costo mínimo entre todas las aristas, si esta arista forma un circuito con las aristas ya elegidas la rechazamos , caso contrario la adicionamos al conjunto.

- Al ir adicionando aristas se van generando un conjunto de subárboles (bosque) que eventualmente se juntan en un solo árbol.

- Si consideramos que al inicio tenemos V subárboles (un árbol con un solo vértice) en cada iteración escogemos una arista que tiene una punta en un subárbol y la otra punta en otro subárbol  

Otra forma de ver el algoritmos de Kruskal
1. Sort edges by ascending edge weight.
2. Walk through the sorted edges and look at the two nodes the edge belongs to, if the nodes are already unified we don´t include this edge, otherwise we include it and unify the nodes.
3. The algorithm terminates when every edge has been processed or all the vertices have been unified.


**algoritmoKruskal(G)**
	T $\leftarrow$  $\varnothing$
	mientras exista una arista permitida
		si e es una arista permitida de costo mínimo
			T $\leftarrow$ T  + e
	FinMientras
	Devuelva T
**finalgoritmoKruskal**

### Algoritmo Kruskal
```
array aristaSort <- aristas del grafo
ordena aristaSort
set mst

mapa parent // vertice : vertice
mapa rank   // vertice : int

Para arista en aristaSort
	v1 <- vertice 1 de arista
	v2 <- vertice 2 de arista

	Si padre de v1 y padre de v2 no se encuentean en parent
		parent[v1] = v1
		parent[v2] = v1
		rank[parent[v1]] = 0
		Agrega arista a mst


	Si padre de v1 se encuentra en parent y padre de v2 no o viceversa
		parent[v1] = find(v2)
		Agrega arista a mst

	Si ambos vertices estan dentro de algun DS
		root1 = find(v1)
		root2= find(v2)
		Si root1 != root2
			Si rank[root1] < rank[root2]
				parent[root1] = root2
			Si rank[root1] > rank[root2]
				parent[root2] = root1
			Sino
				parent[root2] = root1
				rank[root1] ++
			Agrega arista a mst
```

## Algoritmo de Prim
- Supongamos que tenemos un árbol $T$ que es un subgrafo de G.
- La franja de  es el conjunto de aristas que tiene una punta en T y otra fuera de T.
- La idea es ir adicionando al árbol $T$ una arista de **costo mínimo** que está en la franja de $T$.

**algoritmoPrim(G)**
	$T$ $\leftarrow$ $\{v\}$
	Mientras la franja de $T$ no esta vacía
		Si e es una arista de costo mínimo en la franja de $T$
			$T$ $\leftarrow$ $T + e$
	finMientras
**finalgoritmoPrim(G)**



### Algoritmo Prim
```
Input : vertice inicial v
priorityqueue pq 
set mst
n <- numero de vertices del grafo
set visited

Agrega v a visited

Mientras visited.size() < n
	Para cada arista en v
		Si la arista ya se encuentra en pq no se toma en cuenta
		Sino agrega arista a pq

	arista <- pq.front
	v1 <- vertice 1 de arista
	v2 <- vertice 2 de arista

	Mientras v1 y v2 esten registradas en visited
		dequeue pq
		arista <- pq.front
		v1 <- vertice 1 de arista
		v2 <- vertice 2 de arista

	Agrega arista a mst
	dequeue pq
	Agrega vertice no visitado a visited
	v <- vertice no visitado
```