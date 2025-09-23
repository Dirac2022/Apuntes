- La matriz R es la es la llamada matriz de rotación, que define la orientación del sistema $OUV$ con respecto al sistema $OXY$, y que sirve para transformar las coordenadas de un vector en un sistema a las del otro.
- En el caso de dos dimensiones, la orientación viene definida por un único parámetro independiente.
- Si se considera la posición relativa del sistema $OUV$ girado un ángulo $\alpha$ sobre el $OXY$, tras realizar los correspondientes productos escalares, la matriz $R$ será de la forma:


$$
R = 
\begin{bmatrix}
cos\,\alpha & -sen\,\alpha \\
sen\,\alpha & cos\,\alpha
\end{bmatrix}
$$


En un espacio tridimensional, el razonamiento a seguir es similar. Supónganse los
sistemas $OXYZ$ y $OUVW$, coincidentes en el origen, siendo el OXYZ el sistema de referencia
fijo, y el OUVW el solidario al objeto cuya orientación se desea definir.

![[Pasted image 20250909175330.png]]


# Matrices de transformación homogénea

En general, una matriz de transformación homogénea es una matriz $4 \times 4$ que representa una transformación en el espacio tridimensional, que consta de una combinación de traslación, rotación y escala. En robótica, la matriz de transformación homogénea se utiliza para representar la posición y orientación de un eslabón (elemento mecánico) de un robot en relación con su base o con el eslabón anterior.

## Coordenadas homogéneas
- Un elemento de un espacio n-dimensional, se encuentra representado en coordenadas homogéneas por $n + 1$ dimensiones, de tal forma que un vector $p(x, y, z)$ vendrá representado por $p(wx, wy, wz, w)$, donde w tiene un valor arbitrario y representa un factor de escala.
- El factor de escala w se utiliza para realizar transformaciones de escala y proyección.
- De forma general, un vector $p = ai + bj + ck$, donde i, j y k son los vectores unitarios de los ejes OX, OY y OZ del sistema de referencia OXYZ, se representa en coordenadas homogéneas mediante el vector columna:

\[
p = 
\begin{bmatrix}
x \\
y \\
z \\
w
\end{bmatrix}
\sim
\begin{bmatrix}
aw \\
bw \\
cw \\
w
\end{bmatrix}
\sim
\begin{bmatrix}
a \\
b \\
c \\
1
\end{bmatrix}
\]

- Por ejemplo, el vector $2i + 3j + 4k$ se puede representar en coordenadas homogéneas como [2, 3, 4, 1]T, o como [4, 6, 8, 2]T o también como [-6, -9, -12, -3]T, etc.

## Matrices homogéneas
- A partir de la definición de las coordenadas homogéneas surge el concepto de matriz de transformación homogénea.
- Se define como matriz de transformación homogénea $H$ a una matriz de dimensión $4 \times 4$ que representa la transformación de un vector de coordenadas homogéneas de un sistema de coordenadas a otro.

\[
H = 
\begin{bmatrix}
R_{3 \times 3} & P_{3 \times 1} \\
f_{1 \times 3} & w_{1 \times 1}
\end{bmatrix}
=
\begin{bmatrix}
\text{Rotación} & \text{Traslación} \\
\text{Perspectiva} & \text{Escalado}
\end{bmatrix}
\]

- Una matriz homogénea se haya compuesta por cuatro submatrices de distinto tamaño: una submatriz $R_{3 \times 3}$ que corresponde a una matriz de rotación; una submatriz $P_{3 \times 1}$ que corresponde al vector de traslación; una submatriz $f_{1 \times 3}$ que representa una transformación de perspectiva, y una submatriz $w_{1 \times 1}$ que representa un escalado global.

### Submatrices de la matriz homogénea
- Submatriz de rotación: se utiliza para representar una transformación de rotación en los ejes $x, y, z$ del espacio tridimensional.
- Submatriz de traslación: se utiliza para representar el desplazamiento de un objeto en el espacio tridimensional.
- Submatriz de perspectiva: también conocida como matriz de proyección, se utiliza para transformar las coordenadas 3D de un objeto en coordenadas 2D.
- Submatriz de escalado global: se utiliza para representar la escala en los ejes $x, y, z$ del espacio tridimensional.
- En robótica generalmente sólo interesará conocer el valor de la submatriz de rotación $R_{3x3}$ y la submatriz de traslación $p_{3x1}$, considerándose las componentes de la submatriz de perspectiva $f_{1x3}$ nulas y de la submatriz de escalado global $w_{1x1}$ la unidad.
- Al tratarse de una matriz (4 x 4), los vectores sobre los que se aplique deberán contar con 4 dimensiones, que serán las coordenadas homogéneas del vector tridimensional de que se trate.

### Forma final de la matriz homogénea
- Finalmente, la matriz homogénea $H$ resultará ser de la siguiente forma:

\[
H = 
\begin{bmatrix}
R_{3 \times 3} & P_{3 \times 1} \\
0 & 1
\end{bmatrix}
=
\begin{bmatrix}
Rotación & Traslación \\
0 & 1
\end{bmatrix}
\]

- Esta expresión puede ser utilizada para representar la orientación y posición de un sistema O'UVW resultado de rotar y trasladar el sistema original OXYZ según $R_{3 \times 3}$ y $P_{3 \times 1}$ respectivamente.

## Ejercicios

### Ejercicio 1
- Calcule la matriz homogénea que describe la transformación de un objeto que se ha rotado 45 grados alrededor del eje z y se ha trasladado 2 unidades en x y 3 unidades en y.

### Ejercicio 2
- Calcule la matriz homogénea que describes la transformación de un objeto que primero se ha rotado 45 grados alrededor del eje z, luego 60 grados alrededor del eje x y finalmente 53 grados alrededor del eje y y se ha trasladado 2 unidades en x, 3 unidades en y, y 4 unidades en z.

### Transformación de coordenadas
- Asimismo, esta matriz puede servir para conocer las coordenadas $(r_x, r_y, r_z)$ del vector $\mathbf{r}$ en el sistema OXYZ a partir de sus coordenadas $(r_u, r_v, r_w)$ en el sistema O'UVW:

\[
\begin{bmatrix}
r_x \\
r_y \\
r_z \\
1
\end{bmatrix}
= \mathbf{H}
\begin{bmatrix}
r_u \\
r_v \\
r_w \\
1
\end{bmatrix}
\]

### Ejercicio 3
- Tenemos un vector r con coordenadas (2, 4, 6) en el sistema O'UVW. Queremos encontrar sus coordenadas en el sistema OXYZ. Sabemos que los ejes de O'UVW están rotados 45 grados en torno al eje Z en comparación con los ejes de OXYZ y que O'UVW se encuentra a 1 unidad a lo largo del eje X y 2 unidades a lo largo del eje Y con respecto a OXYZ.

### Ejercicio 4
- Tenemos un vector r con coordenadas (2, 4, 6) en el sistema O'UVW. Queremos encontrar sus coordenadas en el sistema OXYZ. Sabiendo que O'UVW se ha rotado primero 45 grados alrededor del eje z, luego 60 grados alrededor del eje x y finalmente 53 grados alrededor del eje y y se ha trasladado 2 unidades en x, 3 unidades en y, y 4 unidades en z.

### Transformación de vectores
- También se puede utilizar para expresar la rotación y traslación de un vector respecto de un sistema de referencia fijo OXYZ, de tal manera que un vector $r_{xyz}$ rotado según $R_{3 \times 3}$ y trasladado según $p_{3 \times 1}$ se convierte en el vector $r'_{xyz}$ dado por:

\[
\begin{bmatrix}
r'_x \\
r'_y \\
r'_z \\
1
\end{bmatrix}
=
H
\begin{bmatrix}
r_x \\
r_y \\
r_z \\
1
\end{bmatrix}
\]

### Ejercicio 5
- Trasladar el vector \((2,3,4)\) en OXYZ al punto \((5,6,7)\) y rotelo 53 grados alrededor del eje X.  
Calcule su nueva coordenada en OXYZ.

### Ejercicio 6
- Trasladar el vector (2,3,4) en OXYZ al punto (5,6,7) luego rotelo 53 grados alrededor del eje X, luego 37 grados alrededor de Y y finalmente 75 grados alrededor de Z. Calcule su nueva coordenada en OXYZ.

## Matriz básica de Traslación
- Supóngase que el sistema O'UVW únicamente se encuentra trasladado un vector $p = p_x i + p_y j + p_z k$ con respecto al sistema OXYZ. La matriz T entonces corresponderá a una matriz homogénea de traslación:

\[
T(p) =
\begin{bmatrix}
1 & 0 & 0 & p_x \\
0 & 1 & 0 & p_y \\
0 & 0 & 1 & p_z \\
0 & 0 & 0 & 1
\end{bmatrix}
\]

- Un vector cualquiera $r$, representado en el sistema O'UVW por $r_{uvw}$, tendrá como componentes del vector con respecto al sistema OXYZ:

\[
\begin{bmatrix}
r_x \\
r_y \\
r_z \\
1
\end{bmatrix}
=
\begin{bmatrix}
1 & 0 & 0 & p_x \\
0 & 1 & 0 & p_y \\
0 & 0 & 1 & p_z \\
0 & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
r_u \\
r_v \\
r_w \\
1
\end{bmatrix}
=
\begin{bmatrix}
r_u + p_x \\
r_v + p_y \\
r_w + p_z \\
1
\end{bmatrix}
\]

- Y a su vez, un vector $r_{xyz}$ desplazado según T tendrá como componentes $r'_{xyz}$:

\[
\begin{bmatrix}
r'_x \\
r'_y \\
r'_z \\
1
\end{bmatrix}
=
\begin{bmatrix}
1 & 0 & 0 & p_x \\
0 & 1 & 0 & p_y \\
0 & 0 & 1 & p_z \\
0 & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
r_x \\
r_y \\
r_z \\
1
\end{bmatrix}
=
\begin{bmatrix}
r_x + p_x \\
r_y + p_y \\
r_z + p_z \\
1
\end{bmatrix}
\]

### Ejemplo 1
- En la figura, el sistema O'UVW está trasladado un vector $p(6, -3, 8)$ con respecto del sistema OXYZ.  
Calcular las coordenadas del vector $r_{xyz}$ en el sistema OXYZ, sabiendo que las coordenadas en el sistema O'UVW son $r_{uvw}(-2, 7, 3)$.  

**Solución:**

\[
\begin{bmatrix}
r_x \\
r_y \\
r_z \\
1
\end{bmatrix}
=
\begin{bmatrix}
1 & 0 & 0 & 6 \\
0 & 1 & 0 & -3 \\
0 & 0 & 1 & 8 \\
0 & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
-2 \\
7 \\
3 \\
1
\end{bmatrix}
=
\begin{bmatrix}
4 \\
4 \\
11 \\
1
\end{bmatrix}
\]

### Ejemplo 2
- Calcular el vector $r'_{xyz}$ resultante de trasladar al vector $r_{xyz}(4, 4, 11)$ según la transformación T(p) con p(6, -3, 8).

**Solución:**

\[
\begin{bmatrix}
r_x' \\
r_y' \\
r_z' \\
1
\end{bmatrix}
=
\begin{bmatrix}
1 & 0 & 0 & 6 \\
0 & 1 & 0 & -3 \\
0 & 0 & 1 & 8 \\
0 & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
4 \\
4 \\
11 \\
1
\end{bmatrix}
=
\begin{bmatrix}
10 \\
1 \\
19 \\
1
\end{bmatrix}
\]

## Matriz básica de Rotación
- Suponga ahora que el sistema O'UVW sólo se encuentra rotado con respecto al sistema OXYZ.
- La submatriz de rotación $R_{3x3}$ será la que defina la rotación, y corresponde al tipo matriz de rotación que vimos la clase pasada.
- Así se pueden definir tres matrices homogéneas básicas de rotación según se realice ésta alrededor de cada uno de los tres ejes coordenados OX, OY y OZ del sistema de referencia OXYZ:

\[
\text{Rot}_X (\alpha) = 
\begin{bmatrix}
1 & 0 & 0 & 0 \\
0 & \cos \alpha & -\sin \alpha & 0 \\
0 & \sin \alpha & \cos \alpha & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
\]

\[
\text{Rot}_Y (\phi) =
\begin{bmatrix}
\cos \phi & 0 & \sin \phi & 0 \\
0 & 1 & 0 & 0 \\
-\sin \phi & 0 & \cos \phi & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
\]

\[
\text{Rot}_Z (\psi) =
\begin{bmatrix}
\cos \psi & -\sin \psi & 0 & 0 \\
\sin \psi & \cos \psi & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
\]

### Transformación de coordenadas con rotación
- Un vector cualquiera $r$, representado en el sistema girado O'UVW por  
  \[  r_{uvw} = (r_{u}, r_{v}, r_{w}),\]
  tendrá como componentes en el sistema OXYZ,  
  \[  r_{xyz} = (r_{x}, r_{y}, r_{z})\]  
  dadas por:  

\[
\begin{bmatrix}
    r_x \\
    r_y \\
    r_z \\
    1
\end{bmatrix}
= R
\begin{bmatrix}
    r_u \\
    r_v \\
    r_w \\
    1
\end{bmatrix}
\]

- Y a su vez, un vector  
  \[  r_{xyz}\]
  rotado según $R$ vendrá expresado por  
  \[  r'_{xyz}\]  
  según:  

\[
\begin{bmatrix}
    r'_x \\
    r'_y \\
    r'_z \\
    1
\end{bmatrix}
= R
\begin{bmatrix}
    r_x \\
    r_y \\
    r_z \\
    1
\end{bmatrix}
\]

- Donde:  
\[
R = Rot_z (\psi) \, Rot_y (\phi) \, Rot_x (\alpha)
\]

### Ejemplo 3
- El sistema OUVW se encuentra girado -90° alrededor del eje OZ con respecto al sistema OXYZ. Calcular las coordenadas del vector $r_{xyz}$ si sus coordenadas en el sistema OUVW son $r_{uvw} = (4, 8, 12)^T$.

**Solución:**

\[
Rot_z (\psi) = 
\begin{bmatrix}
\cos \psi & -\sin \psi & 0 & 0 \\
\sin \psi & \cos \psi & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
\]

Para \(\psi = -90^\circ\), \(\cos(-90^\circ) = 0\), \(\sin(-90^\circ) = -1\):

\[
\begin{bmatrix}
r_x \\
r_y \\
r_z \\
1
\end{bmatrix}
=
\begin{bmatrix}
0 & 1 & 0 & 0 \\
-1 & 0 & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
4 \\
8 \\
12 \\
1
\end{bmatrix}
=
\begin{bmatrix}
8 \\
-4 \\
12 \\
1
\end{bmatrix}
\]

## Rotación seguida de Traslación
- Rotación de un ángulo \(\phi\) sobre el eje OX seguido de una traslación de vector \(P_{x,y,z}\):

\[
T(p) \text{Rot}_x(\phi) = 
\begin{bmatrix}
1 & 0 & 0 & p_x \\
0 & \cos \phi & -\sin \phi & p_y \\
0 & \sin \phi & \cos \phi & p_z \\
0 & 0 & 0 & 1
\end{bmatrix}
\]

- Rotación de un ángulo \(\theta\) sobre el eje OY seguido de una traslación de vector \(P_{x,y,z}\):

\[
T(p) \text{Rot}_y(\theta) = 
\begin{bmatrix}
\cos \theta & 0 & \sin \theta & p_x \\
0 & 1 & 0 & p_y \\
-\sin \theta & 0 & \cos \theta & p_z \\
0 & 0 & 0 & 1
\end{bmatrix}
\]

- Rotación de un ángulo \(\psi\) sobre el eje OZ seguido de una traslación de vector \(P_{x,y,z}\):

\[
T(p) \text{Rot}_z(\psi) = 
\begin{bmatrix}
\cos \psi & -\sin \psi & 0 & p_x \\
\sin \psi & \cos \psi & 0 & p_y \\
0 & 0 & 1 & p_z \\
0 & 0 & 0 & 1
\end{bmatrix}
\]

## Traslación seguida de Rotación
- Traslación de vector $p_{x,y,z}$ seguida de rotación de un ángulo \(\phi\) sobre el eje OX.

\[
Rot_x(\phi)T(p) =
\begin{bmatrix}
1 & 0 & 0 & p_x \\
0 & \cos \phi & -\sin \phi & p_y \cos \phi - p_z \sin \phi \\
0 & \sin \phi & \cos \phi & p_y \sin \phi + p_z \cos \phi \\
0 & 0 & 0 & 1
\end{bmatrix}
\]

- Traslación de vector $p_{x,y,z}$ seguida de rotación de un ángulo \(\theta\) sobre el eje OY.

\[
Rot_y(\theta)T(p) =
\begin{bmatrix}
\cos \theta & 0 & \sin \theta & p_x \cos \theta + p_z \sin \theta \\
0 & 1 & 0 & p_y \\
-\sin \theta & 0 & \cos \theta & p_z \cos \theta - p_x \sin \theta \\
0 & 0 & 0 & 1
\end{bmatrix}
\]

- Traslación de vector $p_{x,y,z}$ seguida de rotación de un ángulo \(\psi\) sobre el eje OZ.

\[
Rot_z(\psi)T(p) =
\begin{bmatrix}
\cos \psi & -\sin \psi & 0 & p_x \cos \psi - p_y \sin \psi \\
\sin \psi & \cos \psi & 0 & p_x \sin \psi + p_y \cos \psi \\
0 & 0 & 1 & p_z \\
0 & 0 & 0 & 1
\end{bmatrix}
\]

### Ejemplo 4
- En la figura, un sistema OUVW ha sido girado 90° alrededor del eje OX y, posteriormente, trasladado un vector $p(8, -4, 12)$ con respecto al sistema OXYZ . Calcular las coordenadas \((r_x, r_y, r_z)\) del vector $r$ con coordenadas $r_{uvw}(-3, 4, -11)$.

**Solución:**

\[
T(p) Rot_x(\phi) = 
\begin{bmatrix}
1 & 0 & 0 & p_x \\
0 & \cos \phi & -\sin \phi & p_y \\
0 & \sin \phi & \cos \phi & p_z \\
0 & 0 & 0 & 1
\end{bmatrix}
\]

Para \(\phi = 90^\circ\), \(\cos 90^\circ = 0\), \(\sin 90^\circ = 1\):

\[
\begin{bmatrix}
r_x \\
r_y \\
r_z \\
1
\end{bmatrix} =
\begin{bmatrix}
1 & 0 & 0 & 8 \\
0 & 0 & -1 & -4 \\
0 & 1 & 0 & 12 \\
0 & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
-3 \\
4 \\
-11 \\
1
\end{bmatrix}
=
\begin{bmatrix}
5 \\
7 \\
16 \\
1
\end{bmatrix}
\]

### Ejemplo 5
- En la figura, un sistema OUVW ha sido trasladado un vector $p(8, -4, 12)$ con respecto al sistema OXYZ y girado 90° alrededor del eje OX. Calcular las coordenadas \((r_x, r_y, r_z)\) del vector $r$ de coordenadas $r_{uvw}(-3, 4, -11)$.

**Solución usando $Rot_x(\phi)T(p)$:**

\[
Rot_x(\phi)T(p) =
\begin{bmatrix}
1 & 0 & 0 & p_x \\
0 & \cos \phi & -\sin \phi & p_y \cos \phi - p_z \sin \phi \\
0 & \sin \phi & \cos \phi & p_y \sin \phi + p_z \cos \phi \\
0 & 0 & 0 & 1
\end{bmatrix}
\]

Para \(\phi = 90^\circ\):

\[
\begin{bmatrix}
1 & 0 & 0 & 8 \\
0 & 0 & -1 & -4 \cdot 0 - 12 \cdot 1 \\
0 & 1 & 0 & -4 \cdot 1 + 12 \cdot 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
=
\begin{bmatrix}
1 & 0 & 0 & 8 \\
0 & 0 & -1 & -12 \\
0 & 1 & 0 & -4 \\
0 & 0 & 0 & 1
\end{bmatrix}
\]

Luego:

\[
\begin{bmatrix}
r_x \\
r_y \\
r_z \\
1
\end{bmatrix}
=
\begin{bmatrix}
1 & 0 & 0 & 8 \\
0 & 0 & -1 & -12 \\
0 & 1 & 0 & -4 \\
0 & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
-3 \\
4 \\
-11 \\
1
\end{bmatrix}
=
\begin{bmatrix}
5 \\
1 \\
0 \\
1
\end{bmatrix}
\]

## Composición de matrices homogéneas
- Una matriz de transformación homogénea sirve, para representar el giro y la traslación realizados sobre un sistema de referencia.
- Esta utilidad de las matrices homogéneas cobra aún más importancia cuando se componen las matrices homogéneas para describir diversos giros y traslaciones consecutivos sobre un sistema de referencia determinado.
- De esta forma, una transformación compleja podrá descomponerse en la aplicación consecutiva de transformaciones simples (giros básicos y traslaciones).

### Composición de rotaciones
- Por ejemplo, una matriz que representa un giro de un ángulo ψ sobre el eje OZ, seguido de un giro de ángulo θ sobre el eje OY y de un giro de un ángulo φ sobre el eje OX, puede obtenerse por la composición de las matrices básicas de rotación:

\[
R = Rot_z(\psi) \, Rot_y(\theta) \, Rot_x(\phi)
\]

- Debido a que el producto de matrices no es conmutativo, tampoco lo es la composición de transformaciones.

```