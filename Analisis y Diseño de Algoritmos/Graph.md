


# DFS (Depth First Search)


```
Variables globales
n : number of nodes in the graph
g = adjacency list representing graph
vistited = [false, ..., false] # size n

function dfs(at):
	if visited[at] is true:
		return
		
	visited[at] = true

	neighbours = graph[at] // Los vertices vecinos del vertice actual "at"
	for next in neighbours:
		dfs(next)
```

En nuestro caso no es necesario `n` ni `g` más si el arreglo `visited`. Podemos usar dos funciones, una principal desde donde se llamada el método y donde podemos inicializar nuestro arreglo `visited` y otro método recursivo que es el que hará el trabajo.