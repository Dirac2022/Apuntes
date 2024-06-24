
Para muchos problemas de optimización usar **programación dinámica** para determinar las mejores opciones es **excesivo**, y algoritmos más simples y eficientes serán suficientes.
Un algoritmo **greedy** siempre hace la mejor elección en el momento. Es decir, hace una elección óptima local con la esperanza de que esta elección conduzca a una optima solución global.

**Los algoritmos greedy no siempre producen una solución óptima**.

El método greedy es bastante poderoso y funciona bien para un rango amplio de problemas, por ejemplo
- *Árbol de expansión mínimo*
- *Algoritmo de Dijkstra*


```
NUM = 4
resto = 353

denominaciones[4] = {70,30,10,5}
numBilletes[4] = {0,0,0,0}

cambio(353, 4) monto = 353, numBilletes = 4
	suma <- 0
	iDen <- 0
	mientras (suma < monto)
		0 < 353
			iDen <- 0 = seleccionVoraz(353-0)
				seleccionVoraz(353)
				j <- 0
				Mientras (0 < 4 y denominaciones[0] = 70 > 353) No cumple
				retorna 0
			Si iDen >= 4 NO 
			numBilletes[0] <- numBilletes[0] + 1 = 1, numBilletes = {1,0,0,0}
			suma <- 0 + denominaciones[0], suma = 70
			
		70 < 353
			iDen <- 0 = seleccionVoraz(283)
				seleccionVoraz(283)
				j <- 0
				Mientras (0 < 4 y denominaciones[0] = 70 > 283) No cumple
				retorna 0
			Si iDen >= 4  NO
			numBilletes[0] <- numBilletes[0] + 1 = 2, numBilletes = {2,0,0,0}
			suma <- 70 + denominaciones[0], suma = 140

		140 < 353
			iDen <- 0 = seleccionVoraz(213)
				seleccionVoraz(213)
				j <- 0
				Mientras (0 < 4 y denominaciones[0] = 70 > 283) No cumple
				retorna 0
			Si iDen >= 4  NO
			numBilletes[0] <- numBilletes[0] + 1 = 3, numBilletes = {3,0,0,0}
			suma <- 140 + denominaciones[0], suma = 210

		210 < 353
			iDen <- 0 = seleccionVoraz(143)
				seleccionVoraz(143)
				j <- 0
				Mientras (0 < 4 y denominaciones[0] = 70 > 143) No cumple
				retorna 0
			Si iDen >= 4  NO
			numBilletes[0] <- numBilletes[0] + 1 = 4, numBilletes = {4,0,0,0}
			suma <- 210 + denominaciones[0], suma = 280

		280 < 353
			iDen <- 0 = seleccionVoraz(73)
				seleccionVoraz(73)
				j <- 0
				Mientras (0 < 4 y denominaciones[0] = 70 > 73) No cumple
				retorna 0
			Si iDen >= 4  NO
			numBilletes[0] <- numBilletes[0] + 1 = 5, numBilletes = {5,0,0,0}
			suma <- 280 + denominaciones[0], suma = 350

		350 < 353
			iDen <- seleccionVoraz(3)
				seleccionVoraz(3)
					j <- 0
					Mientras (0 < 4 y denominaciones[0] = 70 > 3)
						j <- 1
					Mientras (1 < 4 y denominaciones[1] = 30 > 3)
						j <- 2
					Mientras (2 < 4 y denominaciones[2] = 10 > 3)
						j <- 3
					Mientras (3 < 4 y denominaciones[3] = 5 > 3)
						j <- 4
					Mientras (4 < 4 y denominaciones[2] = 10 > 3) No cumple
					retorna 4
			iDen <- 4 
			Si iDen >= 4  Si
				retorne: "No se encontro solución. Cambio incompleto"

NO HAY UNA SOLUCIÓN PARA EL PROBLEMA USANDO ESTE ALGORITMO				
```
denominaciones[4]