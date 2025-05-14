
# Mode

## Sin aplicar ordenamiento

```

X: vector
Inicio

maxFrecuencia <- 0
mapa : {frecuencia de la moda : Set con los valores de las modas}

	Para i <- 0 Hasta N-1
		frecuencia <- 0
		Para j <- 0 Hasta N-1
			Si X[j] == X[i] Entonces
				frecuecia = frecuencia + 1
			FinSi
	
		Si frecuencia > maxFrecuencia Entonces
			maxFrecuencia <- frecuencia
			Limpia mapa
			Inserta nueva frecuencia y valor de moda
		FinSi
	
		Si frecuencia == maxFrecuencia Entonces
			Agrega X[i] al set de los valores de las modas
		FinSi
	FinPara

	retorna mapa

Fin	
```


17 5 12 9 18 10 4 18 1 11  // 10
256 operaciones elementales
La moda de frecuencia 2 es: 18

41 operaciones elementales   
La moda de frecuencia 2 es: 2



13 12 4 10 9 20 11 15 10 11 8 20 4 14 4 6 13 17 6 10  // 20
915 operaciones elementales
Las modas de frecuencia 3 son:
4
10

83 operaciones elementales
Las modas de frecuencia 3 son:
4
10





8 4 13 18 20 8 20 6 7 18 6 2 6 19 11 6 2 2 18 17 17 20 20 3 8 5 9 14 7 6 13 19 11 17 11 10 16 11 15 15   // 40
3456 operaciones elementales
La moda de frecuencia 5 es: 6

147 operaciones elementales
La moda de frecuencia 5 es: 6





9 18 8 3 7 17 10 13 14 16 18 18 4 14 16 1 2 18 8 17 16 6 20 11 5 9 10 4 18 15 7 3 7 4 16 19 19 1 2 17 11 9 20 7 17 5 4 17 1 11 15 19 5 2 5 6 11 8 13 3 12 10 13 9 13 15 17 1 19 14 20 3 17 6 4 14 15 17 6 13 3 6 1 3 10 6 3 9 19 16 1 14 1 5 13 11 8 13 2 12  // 100
20862 operaciones elementales
La moda de frecuencia 8 es: 17

329 operaciones elementales
La moda de frecuencia 8 es: 17




6 3 13 5 18 16 17 16 13 13 17 18 6 15 8 12 20 4 20 12 1 20 11 16 2 17 18 17 17 8 10 11 18 16 3 4 15 14 12 8 10 11 4 11 1 11 11 17 16 18 2 18 18 7 18 8 12 4 6 6 8 4 12 6 20 11 9 7 9 11 19 3 7 8 13 11 6 20 20 11 4 5 18 14 3 6 15 7 7 13 10 15 15 9 3 14 5 7 10 16 8 17 7 7 17 18 4 13 19 5 7 11 5 17 19 10 17 20 17 
7 15 20 4 8 2 8 15 17 8 10 13 20 11 16 17 5 9 8 7 11 20 19 8 5 20 15 16 13 19 13 10 8 10 7 6 19 1 18 8 8 16 9 18 20 13 5 15 13 5 16 19 6 19 6 3 4 16 9 8 14 17 16 18 11 1 18 8 18 15 17 8 5 4 10 6 14 20 7 1 4   // 200
82951 operaciones elementales
La moda de frecuencia 18 es: 8

629 operaciones elementales
La moda de frecuencia 18 es: 8

| Elementos | Operaciones 1er Algoritmo | Operaciones 2do Algoritmo |
| --------- | ------------------------- | ------------------------- |
| 10        | 406                       | 111                       |
| 20        | 1442                      | 215                       |
| 40        | 5376                      | 433                       |
| 100       | 32152                     | 1110                      |
| 200       | 128006                    | 2309                      |
5 2 9 3 11 19 10 2 19 17     // 10
41 operaciones elementales   
La moda de frecuencia 2 es: 2


4 4 6 19 3 9 12 18 8 12 15 9 12 1 15 15 16 17 6 3  // 20
86 operaciones elementales
Las modas de frecuencia 3 son:
12
15
## Aplicando ordenamiento

```

Inicio
    Ordena arreglo X
    arrayModes <- mapa de enteros a conjuntos de enteros
    maxFrecuencia <- 0

	frecuenciaMapa <- mapa de enteros a enteros
	
    Para i <- 0 Hasta tamaño de X - 1
		frecuenciaMapa[X[i]] aumenta en 1
		maxFrecuencia <- maximo de (maxFrecuencia, frecuenciaMapa[X[i]])

	Para i <- Hasta tamaño de X - 1
		Si frecuenciaMapa[X[i]] == maxFrecuencia Entonces
			Inserta en llave maxFrecuencia el elemento X[i]
		FinSi
    FinPara
    Devuelve arrayModes
FinFunción


```