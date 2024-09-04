
```
M: distancia de la estacion inicial a la estacion final
total: rendimiento acumulado
minContador:
contador: 0
arreglo de estaciones [E1, E2, E3, ..., Ek]
memo estructura que sirve para almacenar las rutas parciales
ruta

function(Ei, memo, total, contador) {
	If Ei + total >= M :
		total = Ei + Total
		contador ++
		If contador <= minContador :
			minContador = contador
			ruta = memo

	Else :
		memoaux <- memo
		Agrega Ei a memoaux;
		total = Ei + total;
		contador ++;
		Para cada j = i + 1 hasta k :
			function(Ej, memoaux, total, contador)
}
```