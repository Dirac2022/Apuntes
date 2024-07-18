
1. Escoge un nodo $s$, el cual será el nodo inicial para el camino
2.  Calcula y guarda el valor óptimo del nodo inicial $s$ a cada nodo $x$.

Para calcular la solución óptima para caminos de longitud 3, necesitamos recordar (almacenar) dos cosas de cada uno de los n = 2 casos:

1. El **conjunto de nodos visitados** en el subcamino
    
2. El **índice del último nodo visitado** en el camino
    

Juntos, estas dos cosas forman nuestro estado de programación dinámica. Hay N nodos posibles que podríamos haber visitado por última vez y $2^N$ subconjuntos posibles de nodos visitados. Por lo tanto, el espacio necesario para almacenar la respuesta a cada subproblema está limitado por $O(N 2^N)$.

```
N <- numero de vertices
START_NODE <- nodo inicial
FINISHED_STATE <-  2^N - 1 : estado final donde todos los nodos han sido visitados
distance : matriz de distancias entre vertices


minTourCost : Almacenara el costo del tour, al inicio un numero muy grande
tour: lista que guarda el tour optimo

/*
matriz debe ser cuadrada
Cantidad de nodos entre 2 y 32 inclusive
*/


function solve{

	state <- 1 << START_NODE
	
	memo : matriz de N x 2^N que memoriza los costos de los subproblemas
	prev : matriz de N x 2^N que memoriza los caminos previos
	
	minTourCost = tsp(START_NODE, state, memo, prev)

	// Obtener el camino
	index <- START_NODE
	Mientras (True):
		agrega index a tour
		nextIndex = prev[index][state]
			If nextIndex == null
				break;
		nextState <- state con el vertice nextIndex marcado como visitado
		state <- nextState
		index <- nexIndex

	tour.add(START_NODE)
}



function tsp(i, state, memo, prev) {
	If state == FINISHED_STATE:
		return distance[i][START_NODE]
	If memo[i][state] != null:
		return memo[i][state]

	minCost <- numero muy grande
	index <- -1

	Para cada next desde 0 a N-1:
		Si next ya ha sido visitado en state continua

		// nextState = state | (1 << next);
		nextState <- state con el vertice next marcado como visitado
		newCost <- distance[i][next] + tsp(next, nextState, memo, prev)

		If newCost < minCost:
			minCost <- newCost
			index <- next

	prev[i][state] <- index
	memo[i][state] = minCost
	return minCost
}

// 


```
