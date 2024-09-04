Tomemos el caso de dos cadenas, queremos hallar la subcadena más grande que sea común a las cadenas originales.

Por ejemplo, tenemos las cadenas $S_1 = \{a, b, c, d, e, f, g, h, i, j\}$ y $S_2 = \{e, c, d, g, i\}$. La subcadena común más larga seria  $\{c, d, g, i \}$.

## Recursivamente

Estando en una etapa cualquiera del algoritmo, donde $i$ es la posición del caracter evaluado en la cadena $S_1$ y $j$ es la posición del caracter evaluado en la cadena $S_2$ el algoritmo se resumen en:

1. Si al menos uno de los caracteres es nulo (se llego al final de alguna cadena), retornar cero.
2. En caso contrario, validar si ambos caracteres son iguales, si es así, devolver la función aumentando una posición a ambas cadenas y sumar 1 a la función.
3. Sino se cumplen ninguno de los casos anteriores devolver el máximo de las funciones aumentando una posición en las cadenas.

```
LCS(i, j) {
	If (S1[i] is null OR S2[j] is null):
		return 0
	Else If (S1[i] == S2[j]):
		return 1 + LCS(i+1, j+1)
	Else
		return max(LCS(i+1, j), (i, j+1))
}
```


## Usando memoización y programación dinámica
Haremos uso de una matriz de $(n+1) \times (m+1)$ donde $n$ y $m$ son las longitudes de las cadenas.
Sea $LCS$ dicha matriz:

>[!important]
> Se debe llenar con ceros la primera fila y la primera columna, e iniciar la iteración en (1, 1)

```
If (S1[i-1] == S2[j-1]):
	LCS[i, j] = 1 + LCS[i-1, j-1]
Else
	LCS[i, j] = max(LCS[i-1, j], LCS[i, j-1])
```

La longitud de la subcadena (subsequencia máxima) se encontraría en la ultima entrada, es decir, en $LCS \ [n \ , \ \ m]$.

### Ejemplo

| CADENA |              |     | **l** | **o**        | **n**        | **g**          | **e**        | **s**          | **t**          |
| ------ | ------------ | --- | ----- | ------------ | ------------ | -------------- | ------------ | -------------- | -------------- |
|        | **POSICION** | *0* | *1*   | *2*          | *3*          | *4*            | *5*          | *6*            | *7*            |
|        | *0*          | 0   | 0     | 0            | 0            | 0              | 0            | 0              | 0              |
| **s**  | *1*          | 0   | 0     | 0            | 0            | 0              | 0            | 1              | 1              |
| **t**  | *2*          | 0   | 0     | 0            | 0            | 0              | 0            | 1              | 2              |
| **o**  | *3*          | 0   | 0     | $\nwarrow$ 1 | 1            | 1              | 1            | 1              | 2              |
| **n**  | *4*          | 0   | 0     | 1            | $\nwarrow$ 2 | $\leftarrow$ 2 | 2            | 2              | 2              |
| **e**  | *5*          | 0   | 0     | 1            | 2            | 2              | $\nwarrow$ 3 | $\leftarrow$ 3 | $\leftarrow$ 3 |
