


# DFS (Depth First Search)

```
// variables globales
n <- numero de nodos del grafo
vistited = [false, ..., false] # tamaño n


// current es el vertice evaluado
function dfs(int current, visited):

	if visited[current] is true:
		return
		
	visited[current] = true

	neighbours = graph[current] // Los vertices vecinos o adyacentes del vertice
							   // current
	for next in neighbours:
		dfs(next, visited)

// Se llama al metodo dfs(inicial, visited)
// donde inicial es el vertice inicial para el recorrido por profundidad
```

Podemos usar dos funciones, una principal desde donde se llamada el método y donde podemos inicializar nuestro arreglo `visited` y otro método recursivo que es el que hará el trabajo.

# BFS (Breadth First Search)

```
function bfs(initial) {
	n <- numero de nodos del grafo
	vistited = [false, ..., false] # tamaño n
	queue q
	q.enqueue(initial)
	visited[initial] = true

	While (q is not empty)
		current = q.dequeue

		neighbours = graph[current] // Los vertices vecinos o adyacentes del vertice
								   // current
	
		For next in neighbours:
			If next is not visited:
				q.enqueue(next)
				visited[current] = true

}

```