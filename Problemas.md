![[Pasted image 20241101184343.png]]

$$
\begin{aligned}
{1, +, 3, *, 5} \\
1+3*5
\end{aligned}
$$

{1,+,3,*,5}

$$
{0, 1, 2, 3, 4, 5, 6, 7, 8}
$$

$$
{1, 2, 3, 4, 5}
$$
$$
{1,2,3} {4, 5}
$$
M(0,5) = Max{M(0,3) op M(4,5)}

$$
M(i, j) = max(M(i, k){+/*}M(k+1,j))
$$
$$
M(3, 7) = max{(M(3,4)+*M(5,7), M(3,5)+*M(6,7), M(3,6)+*M(7,7)}
$$
$$
\{5, *, 1, +, 3, *, 4\}
$$

n = 4
$$
\begin{pmatrix}
5_{(0,0)} & 0 & 0 & 0_{(0,3)} \\
0 & 1 & 0 & 0 \\
0 & 0 & 3 & 0 \\
0 & 0 & 0 & 4 \\
\end{pmatrix}
$$
M(0, 0) = array(0);

```python
# array = \{5, *, 1, +, 3, *, 4\}
n = len(array) // 2 + 1 # 4
# Inicializamos nuestra matrix nxn con valores 0
# Las entradas de la  diagonal toman los valores de su posicion
# i = 2, 3, 4
for tam_subArreglo in range(2, n):
	# primero tomaremos arreglos de tamaño 2, luego de 3, luego de 4
	# tam_subArraglo = 2 [i, j]
	for i in range(n - tam_subArreglo + 1): # (0, 1) (1, 2) (2, 3) (3, 4)
		j = i + tam_subArreglo - 1
		M[i][j] = '-infito'

		for k range(i, j): # # array = \{5, *, 1, +, 3, *, 4\}
			op = array[2 * k + 1]

			if op == '*':
				resultado = M[i][k] * M[k+1][j]

			elif op == '+':
				resultado = M[i][k] + M[k+1][j]

			M[i][j] = max(M[i][j], val)	
return M[0][n-1]
```



![[Pasted image 20241101193355.png]]

[5, 4, 3, 1, 8, 9, 7] , 10


carros = {5, 4, 3, 1, 8, 9, 7}
subin =  {0, 1, 2, 3, 4, 5, 6}

funcion(10, carros) {

	funcionrec(i, linea1, linea2, linea3) {
		si i == len(carros)
			return algo // caso base
		maximo{
		funcionrec(i+1, linea1 + carroi, linea2, linea3)
		funcionrec(i+1, linea1, linea2 + carroi, linea3)
		funcionrec(i+1, linea1, linea2 + carroi, linea3 + carroi)
		}	
	}
}

maximautos(i, linea1, linea2, linea3) = maximo{
	1+maximoautos(i+1, linea1 + autoi, linea2, linea3), si linea1+autoi +1 <= len(transbordador)
	1+maximoautos(i+1, linea1 + autoi, linea2, linea3) 
	1+maximoautos(i+1, linea1 + autoi, linea2, linea3)
}

```python
# T: Longitud del transbordador = 10
# carros = {5, 10, 3, 1, 8, 9, 7}

# 
funcion(T, carros) {
	inizializa memoizacion  # guardar los valores
	funcionRec(i, linea1, linea2, linea3) {
		# Caso base
		Si el caso (i, linea1, linea2, linea3) esta en 
		memoizacion -> return memoizacion(i, linea1, linea2, linea3)

		if i == len(carros) {
			return 0
		}

		solTemp : Arreglo 
		if linea1 + carros[i] + 1 <= T:
			Agrega a solTemp 1 + funcionRec(i+1, linea1 + carros[i], linea2, linea3)
		if linea2 + carros[i] + 1 <= T:
			Agrega a solTemp  1 + funcionRec(i+1, lineal, linea2 + carros[i], linea3)
		if linea3 + carros[i] + 1 <= T:
			Agrega a solTemp  1 + funcionRec(i+1, linea1, linea2, linea3 + carros[i])

		defaul: Agrega a solTemp funcionRec(i+1, linea1, linea2, linea3)
		
		result = max(solTemp)
		memoizacion(i, c1, c2, c3) = result
		return result
	}
	funcionRec(0, 0, 0, 0)
}
```




![[Pasted image 20241101200042.png]]
-------



-------



------



----


Si el siguiente carro ingresa a linea1
(l1,l2, l3, ..., ln), : li
len(li) + 1 < len(cantidadcarros) en linea1

len(li) + 1 < len(cantidadcarros) en linea2

len(li) + 1 < len(cantidadcarros) en linea3

max{los tres de arribo}

funcion(li, linea1, linea2, linea3) = max{li+1}



------

-----

-----

---

