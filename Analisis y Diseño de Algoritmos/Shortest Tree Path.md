- La longitud de un camino es su número de arcos o aristas
- El costo de un camino es la suma de los costos de sus arcos
- Dados dos vértices $s$ y $t$, un camino de costo mínimo de $s$ a $t$ es un camino de $s$ a $t$ con la propiedad de que ningún otro camino de $s$ a $t$ tiene costo menor. Podemos llamar a tal camino **camino mínimo** (siempre que sea posible).
- La distancia de un vértice $s$ a un vértice $t$ es el costo de un camino mínimo de $s$ a $t$ y lo denotamos por $\text{dist}(s,t)$. Por ejemplo: $\text{dist}(0,3)=2$, $\text{dist}(3,1)=3$, $\text{dist}(3,4)=\infty$

## Desigualdad triangular
Para cualesquiera tres vértices $u, v, w$ un dígrafo con costos en los arcos tales que 
$$
dis(u, w),\quad dist(u, v), \quad dist(v, w) < \infty
$$
se cumple que
$$
dist(u, w) \leq dist(u, v) + dist(v, w)
$$
## Propiedad
Todo **subcamino** de un camino mínimo es mínimo.

## Árbol de caminos mínimos (SPT)
- Un grafo dirigido o *dígrafo* es un tipo de grafo en el cual las aristas tienen un sentido definido.
- Dado un dígrafo y un vértice $s$, un árbol de caminos mínimos (Shortest Path Tree) a partir de $s$ es un subárbol que contiene $s$ y todos los vértices alcanzables por $s$ tal que todo camino en el árbol a partir de $s$ es mínimo.

### Problema
- Dado dos vértices $s$ y $t$ de un dígrafo con costos positivos en los arcos, encuentre un camino mínimo de $s$ a $t$.
- **Problema equivalente**: dado un vértice $s$ de un dígrafo con costos positivos en los arcos encontrar un SPT a partir de la raíz $s$.


## Algoritmo Dijkstra
**Idea**: construir un SPT adicionando un arco a la vez. Para ello elegir un vértice inicial $s$ y agregar el vértice $w$ cuya distancia sea el menor hacia $s$.

**algoritmoDijkstra(Grafo G, vértice s)**
	$T \gets \{s\}$
	Mientras la franja de $T$ no este vacía
		Si $v-w$ es un arco de la franja de $T$ y $dist(s, w)$ es menor hacia $s$
			$T \gets T + w$
	finMientras
**finAlgoritmoDijkstra**


```
n : cantidad de vertices
conjunto visited
cola
v_0 : vertice inicial
v = v_0

Mientras visited.size < n :
	Para cada vertice w vecino de v (v-w)
		Si dist(v_0 - v) + costo(v - w) < dist(v_0 - w):
			cola.push(v-w)
			dist[v_0 - w] = dist[v_0 - v] + costo(v- w)

	// Elige siguiente vertice v que no haya sido visitado de la cola
	v = pq.pop // este vertice tiene que ser valido, puede que ya haya sido 
			   // visitado
	Agrega v a visited 
FinMientras		 

```


## Algoritmo Floyd-Warshall

```
n <- cantidad de vertices del grafo
maxDist <- Numero muy grande

matriz de caminos cam de nxnv // Entradas maxDist
matriz de distancias dist de nxn // Entradas maxDist


// // Inicializamos la matriz dist, de distancias originales entre vertices
Para cada arista en aristas de grafo {
	// v1 y v2 los los vertices de la arista
	dist[v1][v2] = peso de la arista
}

// Inicializamos la matriz cam, las entradas tomaran como valor el indice de
// la columna 
for(row = 0; row < n; row ++) {
	for(col = 0; col < n; col ++) {
		if (dist[row][col] < maxDist)
			cam[row][col] = col
	}
}

for(int k = 0; k < n; k ++){
	for(int i = 0; i < n; i ++){
		for(int j = 0; j < n; j ++){	
			d = dist[i][k] + dist[k][j]
			// Si pasar por el vertice k produce un menor costo, actualizamos
			// las matrices de caminos y distancias, ahora, para ir del vertice i al j,             // debemos primero pasar por k
 			if(d < dist[i][j]) {
	 			cam[i][j] = cam[i][k];
	 			dist[i][j] = d;
 			}
		}
	}
}

// Imprimamos los caminos

```



## Algoritmo Bellman Ford

- E number of edges
- V number of vertices
- S id of the starting node
- D an array of size V that tracks the best distance from S to each node. 

1. Set every entry in D to $+\infty$
2. Set D[S] = 0
3. Relax each edge V-1 times.  Relax means taking an edge and trying to update the value from where the edge starts to where it ends.

```

// edge.from : vertice origen
edge.to : vertice destino

for v in G(V):
	D[v] = + inf

D[S] = 0

for (i = 0; i < V-1; i ++):
	for edge in graph.edges:
		// Relax edge (update D with shorter path)
		if (D[edge.from] + edge.cost < D[edge.tol])
			D[edge.to] = D[edge.from] + edge.cost

// Repeat to find nodes caught in a negative cycle
for (i = 0; i < V-1; i ++):
	for edge in graph.edges:
		if (D[edge.from] + edge.cost < D[edge.to])
			D[edge.to] = - inf
```