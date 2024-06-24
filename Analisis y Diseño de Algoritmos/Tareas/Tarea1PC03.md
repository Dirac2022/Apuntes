Teniendo billetes de 70, 30, 10 y 5 sol. Cambie 353 soles
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

Si se tienen 5 objetos cuyos pesos son 10, 20, 30, 40 y 50, y sus valores son 20, 30, 66, 40 y 60, respectivamente. Además se sabe que la capacidad de la mochila es de 100 kg. Resuelva usando los criterios anteriores y compárelos.



```
capacidadMochila = 100
w = {10,20,30,40,50}
v = {20,30,66,40,60}

peso <- 0
mientras peso < capacidadMochila
	mientras 0 < 100
		i <- 2 = seleccionarMasPrometedor() // v[2] = 66 es el elemento de mayor valor
												que se pueda escoger
		si (0 + 30 < 100) Si
			peso = 0 + 30 = 30
			
	mientras 30 < 100
		i <- 2 = seleccionarMasPrometedor()
		si (30 + 30 < 100) Si
			peso = 30 + 30 = 60

	mientras 60 < 100
		i <- 2 = seleccionarMasPrometedor()
		si (60 + 30 < 90) Si
			peso = 60 + 30 = 90

	mientras 90 < 100
		i <- seleccionarMasPrometedor() // No hay un valor que cumpla la condicion
										// peso + w[i] < capacidadMochila
FinMientras

El maximo beneficio hallado es 3 * 66 = 198 




Usando criterio de elemento de menor peso

w = {10,20,30,40,50}
v = {20,30,66,40,60}

peso <- 0
mientras peso < capacidadMochila
	mientras 0 < 100
		i <- 0 = seleccionarMasPrometedor() // w[0] = 30 es el elemento de menor peso
		si (0 + 10 < 100) Si
			peso = 0 + 10 = 10
			
	mientras 10 < 100
		i <- 0 = seleccionarMasPrometedor()
		si (10 + 10 < 100) Si
			peso = 10 + 10 = 20

	mientras 20 < 100
		i <- 0 = seleccionarMasPrometedor()
		si (20 + 10 < 100) Si
			peso = 20 + 10 = 30

	mientras 30 < 100
		i <- 0 = seleccionarMasPrometedor()
		si (30 + 10 < 100) Si
			peso = 30 + 10 = 40

	mientras 40 < 100
		i <- 0 = seleccionarMasPrometedor()
		si (40 + 10 < 100) Si
			peso = 40 + 10 = 50

	mientras 50 < 100
		i <- 0 = seleccionarMasPrometedor()
		si (50 + 10 < 100) Si
			peso = 50 + 10 = 60

	mientras 60 < 100
		i <- 0 = seleccionarMasPrometedor()
		si (60 + 10 < 100) Si
			peso = 60 + 10 = 70

	mientras 70 < 100
		i <- 0 = seleccionarMasPrometedor()
		si (70 + 10 < 100) Si
			peso = 70 + 10 = 80

	mientras 80 < 100
		i <- 0 = seleccionarMasPrometedor()
		si (80 + 10 < 100) Si
			peso = 80 + 10 = 90

	mientras 90 < 100
		i <- seleccionarMasPrometedor() // No hay un valor que cumpla la condicion
										// peso + w[i] < capacidadMochila
FinMientras

El maximo beneficio hallado es 9 * 20 = 180



Usando criterio de elemento que tenga mayor valor por unidad de peso

w = {10,20,30,40,50}
v = {20,30,66,40,60}

// w_v = {2, 3/2, 11/5, 1, 6/5} son las tasas valor/peso

peso <- 0
mientras peso < capacidadMochila
	mientras 0 < 100
			i <- 2 = seleccionarMasPrometedor() // w_v[2] = 11/5 es el elemento de
												// mayor valor por unidad de peso
		si (0 + 30 < 100) Si
			peso = 0 + 30 = 30
			
	mientras 30 < 100
		i <- 2 = seleccionarMasPrometedor()
		si (30 + 30 < 100) Si
			peso = 30 + 30 = 60

	mientras 60 < 100
		i <- 2 = seleccionarMasPrometedor()
		si (60 + 30 < 100) Si
			peso = 60 + 30 = 90

	mientras 90 < 100
		i <- seleccionarMasPrometedor() // No hay un valor que cumpla la condicion
										// peso + w[i] < capacidadMochila

FinMientras


El maximo beneficio hallado es 3 * 66 = 198
```