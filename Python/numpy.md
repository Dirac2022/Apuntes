
```python
import numpy as np

```



# Parámetros comunes
### `like`
Este parámetro acepta un arreglo n dimensional existente, que servirá como referencia. 

## `np.arange()`
Genera un array de valores espaciados uniformemente dentro de un rango específico.

```python
np.arange(start, stop, step, dtype=None)
```

- `start` (opcional) :  Valor inicial (incluido). Por defecto es 0.
- `stop` (obligatorio) :  Valor final (no incluido).
- `step` (opcional) : Incremento entre valores. Por defecto es 1.
- `dtype` (opcional) : Tipo de dato del array (por ejemplo, `int`, `float`).
# Arrays

## `np.zeros()`

### Parametros
- **shape** : entero o tupla de enteros
- **dtye**:  Tipo de datos, por ejemplo `'numpy.float64'`
- **order** : `'C' o 'F'` donde `'C'` se almacenan datos multidimensionales por fila y `F` se almacenan por columna. Esta en `C` por defecto
- **like** : 

# `np.savetxt`
Es una función utilizada para guardar datos de un array en un archivo de texto. 

```python
np.savetxt(frame, X, fmt='%.18e', delimiter=' ', newline='\n', header='', footer='', comments='#', encoding=None)
```

| Parámetro   | Descripción                                                                      |
| ----------- | -------------------------------------------------------------------------------- |
| `fname`     | Nombre del archivo (puede incluir ruta) donde se guardarán los datos.            |
| `X`         | Array de NumPy que se quiere guardar.                                            |
| `fmt`       | Formato de las entradas (por defecto: `'%.18e'`, notación científica).           |
| `delimiter` | Separador usado entre los valores (por defecto: espacio).                        |
| `newline`   | Caracteres que separan las filas (por defecto: nueva línea `\n`).                |
| `header`    | Texto que se añadirá como cabecera en el archivo.                                |
| `footer`    | Texto que se añadirá al final del archivo.                                       |
| `comments`  | Prefijo para las líneas de comentarios (por defecto: `'#'`).                     |
| `encoding`  | Codificación del archivo (por defecto: `None`, usa la codificación del sistema). |

# `np.loadtxt`
Se usa para cargar datos desde un archivo de texto en un arreglo de NumPy.

```python
np.loadtxt(fname, dtype=<tipo>, delimiter=<separador>, skiprows=<saltos>, usecols=<columnas>, unpack=<booleano>, comments=<carácter>, encoding=<codificación>)
```

| Parámetro      | Descripción                                      | Valor por defecto |
|----------------|--------------------------------------------------|-------------------|
| `fname`        | Archivo de texto a leer                          | No tiene          |
| `dtype`        | Tipo de dato de los elementos                    | `float`           |
| `delimiter`    | Delimitador de los datos (ej. `,`, espacio)       | `None`            |
| `skiprows`     | Número de filas a saltar al principio            | 0                 |
| `usecols`      | Especifica las columnas a leer                   | `None`            |
| `unpack`       | Si debe devolver los valores como arrays separados | `False`          |

# Boolean Indexing en Numpy

El **boolean indexing** en NumPy permite filtrar elementos de un array usando condiciones lógicas. En lugar de acceder a los elementos por posición (`arr[0]`, `arr[1]`, etc.), se usa una máscara booleana, que es un array de valores `True`, `False`. 

```python
import numpy as np

# Crear un array
arr = np.array([10, 20, 30, 40, 50])

# Crear una máscara boolena: elementos > 25
mask = arr > 25
print(mask) # [False, False, True, True, True]

# Aplicar la máscara para filtrar los elementos
filtered_arr = arr[mask]
print(filtered_arr) # [30, 40, 50]
```



# `dtype`

| **Tipo**              | **Dtype en NumPy** | **Bits** | **Rango o Precisión**                        |
| --------------------- | ------------------ | -------- | -------------------------------------------- |
| **Enteros con signo** | `'int8'`           | 8        | -128 a 127                                   |
|                       | `'int16'`          | 16       | -32,768 a 32,767                             |
|                       | `'int32'`          | 32       | -2,147,483,648 a 2,147,483,647               |
|                       | `'int64'`          | 64       | -9.2e18 a 9.2e18                             |
| **Enteros sin signo** | `'uint8'`          | 8        | 0 a 255                                      |
|                       | `'uint16'`         | 16       | 0 a 65,535                                   |
|                       | `'uint32'`         | 32       | 0 a 4.2e9                                    |
|                       | `'uint64'`         | 64       | 0 a 1.8e19                                   |
| **Punto flotante**    | `'float16'`        | 16       | Baja precisión                               |
|                       | `'float32'`        | 32       | Precisión simple                             |
|                       | `'float64'`        | 64       | Precisión doble (por defecto)                |
|                       | `'float128'`       | 128      | Mayor precisión (si está disponible)         |
| **Números complejos** | `'complex64'`      | 64       | `float32` + `float32`                        |
|                       | `'complex128'`     | 128      | `float64` + `float64`                        |
|                       | `'complex256'`     | 256      | `float128` + `float128` (si está disponible) |


# Basado en Learn Python A Beginner's Guide to Python, NumPy, Pandas and Scipy

- NumPy is a Python library
- NumPy is used for working with arrays
- NumPy is short for "Numerical Python"

## Basics

### Introduction
NumPy is a Python library used for working with arrays. It also has functions for working in the domain of linear algebra, Fourier transform and matrices.

**Why use NumPy**
- NumPy aims to provide an array object that is up to 50x faster than traditional Python list.
- The array object in NumPy is called `ndarray`, it provides a lot of supporting functions that make working with `ndarray` very easy.

**Why is NumPy Faster Than Lists?**
- NumPy arrays are stored at one continuous place in memory unlike lists, so processes can access and manipulate them very efficiently. 
- This behavior is called locality of reference in computer science. 
- This is the main reason why NumPy is faster than lists. Also it is optimized to work with the latest CPU architectures.

**Which Language is NumPy written in?**
NumPy is a Python library and is written partially in Python, but most of the parts that require fast computation are written in C or C++.


### Getting Started


**Installation of NumPy**
Install it using this command
```bash
pip install numpy
```

**Checking NumPy Version**

```python
import numpy as np
print(np.__version__)

```

### Creating Arrays
NumPy is used to work with arrays. The array object in NumPy is called `ndarray`

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5])
print(arr)
print(type(arr))
```


#### Dimensions in Arrays
A dimension in arrays is one level of array depth (nested arrays)

**0-D Arrays**
0-D arrays are scalars
```python
arr = np.array(42)
print(arr)
```

**1-D Arrays**
An array that has 0-D arrays as its elements is called uni-dimensional or 1-D array
```python
arr = np.array([1, 2, 3, 4, 5])
print(arr)
```

**2-D Arrays**
An array that has 1-D arrays as its elements is called a 2-D array. These are often used to represent matrix or 2nd order tensors.
```python
arr = np.array([[1, 2, 3],
			    [4, 5, 6]])

print(arr)
```


**3-D Arrays**
An array that has 2-D arrays (matrices) as its elements is called 3-D array. These are often used to represent a 3rd order tensor.
```python
arr = np.array([[[1, 2, 3], [4, 5, 6]],
				 [[1, 2, 3], [4, 5, 6]]])

print(arr)
```


**Check Numbers of Dimensions?**
NumPy Arrays provides the ``ndim`` attribute that returns an integer that tells us how many dimensions the array has.

```python
import numpy as np

a = np.array(42)
b = np.array([1, 2, 3, 4, 5])
c = np.array([[1, 2, 3], [4, 5, 6]])
d = np.array([[[1, 2, 3], [4, 5, 6]], [[1, 2, 3], [4, 5, 6]]])

print(a.ndim)
print(b.ndim)
print(c.ndim)
print(d.ndim)
```


**Higher Dimensional Arrays**
An array can have any number of dimensions. When the array is created, you can define the number of dimensions by using the ``ndmin`` argument.

```python
import numpy as np
arr = np.array([1,2,3,4], ndmin=5)
print(arr)
print('number of dimensions :', arr.ndmin)
```


### Array Indexing
Array indexing is the same as accessing an array element.


**Access Array Elements**
Example:
Get the second element from the following array
```python
import numpy as np
arr = np.array([1, 2, 3, 4])
print(arr[1])
```

**Access 2-D Arrays**
To access elements from 2-D arrays we can use comma separated integers representing the dimension and the index of the element.

Example:
Access the 5th element on 2nd dim:
```python
arr = np.array([[1,2,3,4,5], [6,7,8,9,10]])
print("5th element on 2dn dim:", arr[1,4])
```


**Access 3-D Arrays**
To access elements from 3-D arrays we can use comma separated integers representing the dimensions and the index of the element.

Example:
Access the third element of the second array of the first array:
```python
arr = np.array([[[1, 2, 3], [4, 5, 6]], [[7, 8, 9], [10, 11, 12]]])
```

**Negative Indexing**
Use negative indexing to access an array from the end

Example:
Print the last element from the 2nd dim:
```python
arr = np.array([[1,2,3,4,5], [6,7,8,9,10]])
print("Last element from 2nd dim")
```


### Array Slicing
Slicing in Python means taking elements from one given index to another given index.
- We pass slice instead of index like this: `[start:end]` where `start` is included and `end` is excluded.
- We can also define the step, like this: `[start:end:step]`
- If we don´t pass `start` its considered 0
- If we don´t pass `end` its considered length of array in that dimension
- If we don´t pass `step` its considered 1

Example:
Slice elements from beginning to index 4
```python
arr = np.array([1, 2, 3, 4, 5, 6, 7])
print(arr[:4])
```

**Negative Slicing**
Example
Slice from the index 3 from the end to index 1 from the end
```python
arr = np.array([1, 2, 3, 4, 5, 6, 7])
print(arr[-3:-1])
```


**Step**
Example
Return every odd element from the entire array:
```python
arr = np.array([1, 2, 3, 4, 5, 6, 7])
print(arr[::2])
```


**Slicing 2-D Arrays**
Example
From the second element, slice elements from index 1 to index 4 (not included)
```python
arr = np.array([[1, 2, 3, 4, 5], [6, 7, 8, 9, 10]])
print(arr[1, 1:4])
```


From both elements, return index 2:
```python
arr = np.array([[1, 2, 3, 4, 5], [6, 7, 8, 9, 10]])
print(arr[:,2])
```


From both elements, slice index 1 to index 4 (not included), this will return a 2-D array:
```python
arr = np.array([[1, 2, 3, 4, 5], [6, 7, 8, 9, 10]])
print(arr[:,1:4])
```


### Data Types
Below is a list of all data types in NumPy and the characters used to represent them.
- `i` - integer
- `b` - boolean
- `u` - unsigned integer
- `f` - float
- `c` - complex float
- `m` - timedelta
- `M` - datetime
- `O` - object
- `S` - string
- `U` - unicode string
- `V` - fixed chunk of memory for other type  (void)


**Checking the Data Type of an Array**
The NumPy array object has a property called ``dtype`` that returns the data type of the array

Get the data type of an array object:
```python
import numpy as np
arr = np.array([1,2,3,4])
print(arr.dtype)
# int64
# Un entero de 64 bits
```

Get the data type of an array containing strings:
```python
arr = np.array(['apple', 'banana', 'cherry']) 
print(arr.dtype)
# <U6
# Significa unicode string con una longitud maxima de 6 caracteres
```

**Creating Array With a Defined Data Type**
We use the ``array()`` function to create arrays, this function can take an optional argument: ``dtype`` that allows us to define the expected data type of the array elements:

Create an array with data type string:
```python
arr = np.array([1, 2, 3, 4], dtype='S') 
print(arr) 
print(arr.dtype)
# |S1 
# | indica que es un tipo no nativo de NumPy
# S1 indica que es una cadena de longitud 1 (1 byte o caracter)
```

Create an array with data type 4 bytes integer
```python
arr = np.array([1, 2, 3, 4], dtype='i4')
print(arr)
print(arr.dtype)
# int32
```


**What if a value can not be converted**
If a type is given in which elements can't be casted then NumPy will raise a ``ValueError``. 
``ValueError``: In Python ``ValueError`` is raised when the type of passed argument to a function is unexpected/incorrect.

A non integer string like 'a' can not be converted to integer (will raise an error)
```python
arr = np.array(['a', '2', '3'], dtype='i')
# ValueError: invalid literal for int() with base 10: 'a'
```


**Converting data type on existing arrays**
- The best way to change the data type of an existing array, is to make a copy of the array with the ``astype()`` method. 
- The ``astype()`` function creates a copy of the array, and allows you to specify the data type as a parameter. 
- The data type can be specified using a string, like 'f' for float, 'i' for integer etc. or you can use the data type directly like float for float and int for integer.

Change data type from float to integer by using 'i' as parameter value:
```python
arr = np.array([1.1, 2.1, 3.1])
newarr = arr.astype('i')
print(newarr)
print(newarr.dtype)
# [1 2 3]
# int32
```

Change data type from float to integer by using int as parameter value:
```python
arr = np.array([1.1, 2.1, 3.1]) 
newarr = arr.astype(int) 
print(newarr) 
print(newarr.dtype)
# [1 2 3]
# int64
```

Change data type from integer to boolean:
```python
arr = np.array([1, 0, 3]) 
newarr = arr.astype(bool) 
print(newarr) 
print(newarr.dtype)
# [ True False True] 
# bool
```

### Copy vs View


- Array Shape
- Array Reshape
- Array Iterating
- Array Join
- Array Split
- Array Search
- Array Sort
- Array Filter

## Random

- Random Intro
- Data Distribution
- Random Permutation
- Seaborn Module
- Normal Dist
- Binomial Dist
- Poisson Dist
- Uniform Dist
- Logistic Dist
- Multinomial Dist
- Exponential Dist
- Chi Square Dist
- Rayleigh Dist
- Pareto Dist
- Zipf Dist

## Ufunc

- ufunc Intro
- Create Function
- Simple Arithmetic
- Rounding Decimals
- Logs
- Summations
- Products
- Differences
- Finding LCM
- Finding GCD
- Trigonometric
- Hyperbolic
- Set Operations





