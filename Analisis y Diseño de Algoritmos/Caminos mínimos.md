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


![[Pasted image 20240618165406.png]]
