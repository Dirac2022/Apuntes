
# Insertion Sort

```
N: tamaño del arreglo
X: arreglo desordenado

Inicio
	Desde i<-1 hasta N-1 hacer
		aux <- X[i]
		k <- i-1
		sw <- Falso
		Mientras No(sw) y (k>=0) Hacer
			Si aux < X[k] Entonces
				X[k+1] <- aux
				k <- k-1
			Sino
				sw <- Verdadero
			FinSi
		FinMientras
		X[k+1] <- aux
	FinDesde
Fin
```


# Merge Sort

## Merge

```
N: tamaño del arreglo fucionado
X: arreglo fucionado
X1: arreglo de la izquierda
X2: arreglo de la derecha
len1: tamaño del arreglo de la izquierda
len2: tamaño del arreglo de la derecha

Inicio
	i<-0, j<-0
	Mientras (i+j < N)
		Si (j == len2) OR (i < len1 AND  X1[i] < X2[j]) Entonces
			X[i+j] = X1[i++]
		Sino
			X[i+j] = X2[j++]
		FinSi
	FinMientras
Fin
```


## Merge Sort


```
X: arreglo desordenado
Inicio mergeSort
	n <- length(X)
	Si n < 2
		retorna
	Fin
	
	middle = n/2
	X1 <- X[0:middle
	X2 <- X[middle:n]

	mergeSort(X1, n/2)
	mergeSort(X2, n/2)
	merge(X, X1, X2, n, n/2, n/2)
Fin
```

