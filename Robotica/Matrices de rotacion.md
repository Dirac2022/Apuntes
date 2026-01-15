
## Representación de la orientación

- Un punto queda totalmente definido en el espacio a través de los datos de su posición.
- Sin embargo, para el caso de un sólido rígido, es necesario además definir cuál es su orientación con respecto a un sistema de referencia.
- Una orientación en el espacio tridimensional viene definida por tres grados de libertad o tres componentes linealmente independientes.
- Para poder describir de forma sencilla la orientación de un objeto respecto a un sistema de referencia, es habitual asignar solidariamente al objeto un nuevo sistema, y después estudiar la relación espacial existente entre los dos sistemas.
- De forma general, esta relación vendrá dada por la posición y orientación del sistema asociado al objeto respecto al de referencia.
- Para el análisis de los distintos métodos de representar orientaciones se supondrá que ambos sistemas coinciden en el origen, y que, por tanto, no existe cambio alguno de posición entre ellos.


## Matrices de rotación

- Para describir las orientaciones utilizamos las matrices de rotación.
- Sea el sistema OXY el de referencia fijo y el sistema OUV el móvil, solidario al objeto.
- Un vector $\mathbf{p}$ del plano se puede representar como:

$$
\mathbf{P} = p_x i_x + p_y j_y \quad \text{(1)}
$$
$$
\mathbf{P} = p_u i_u + p_v j_v \quad \text{(2)}
$$

- De (1) y (2) se puede demostrar que:

$$
p_x = (p_u i_x i_u + p_v i_x j_v) \quad \text{(3)}
$$
$$
p_y = (p_u j_y i_u + p_v j_y j_v) \quad \text{(4)}
$$

- De (3) y (4):

$$
\begin{bmatrix} p_x \\ p_y \end{bmatrix} = \mathbf{R} \begin{bmatrix} p_u \\ p_v \end{bmatrix}
$$

- De donde se deduce:

$$
\mathbf{R} = \begin{bmatrix} i_x i_u & i_x j_v \\ j_y i_u & j_y j_v \end{bmatrix} \quad \text{(5)}
$$



## Matrices de rotación (2D)

- La matriz **R** es la llamada matriz de rotación, que define la orientación del sistema OUV con respecto al sistema OXY, y que sirve para transformar las coordenadas de un vector en un sistema a las del otro.
- En el caso de dos dimensiones, la orientación viene definida por un único parámetro independiente.
- Si se considera la posición relativa del sistema OUV girado un ángulo α sobre el OXY, tras realizar los correspondientes productos escalares, la matriz **R** será de la forma:

$$
R = \begin{bmatrix} \cos \alpha & -\sin \alpha \\ \sin \alpha & \cos \alpha \end{bmatrix} \quad \text{(6)}
$$


![[Pasted image 20251021143022.png]]


<h5>Ejercicio 3</h5>

1. Dado el vector (-3,2) en el plano, rota el vector un ángulo de 180 grados en sentido antihorario alrededor del origen del plano.  
   **Rpta:** (3,-2)

2. Dado el vector (2,-2) en el plano, rota el vector un ángulo de 60 grados en sentido antihorario alrededor del punto (-3,4).  
   **Rpta:** (4.6962, 5.3301)


## Matrices de rotación 3D

En un espacio tridimensional, el razonamiento a seguir es similar. Supónganse los
sistemas $OXYZ$ y $OUVW$, coincidentes en el origen, siendo el OXYZ el sistema de referencia
fijo, y el OUVW el solidario al objeto cuya orientación se desea definir.



$$
P_{xyw} = [p_x, p_y, p_z]^T = p_x \cdot i_x + p_y \cdot j_y + p_z \cdot k_z \quad \text{(7)}
$$
$$
P_{uvw} = [p_u, p_v, p_w]^T = p_u \cdot i_u + p_v \cdot j_v + p_w \cdot k_w \quad \text{(8)}
$$

- Se puede demostrar que:

$$
\begin{bmatrix} p_x \\ p_y \\ p_z \end{bmatrix} = R \begin{bmatrix} p_u \\ p_v \\ p_w \end{bmatrix} \quad \text{(9)}
$$

- Y deducir que:

$$
R = \begin{bmatrix}
i_x i_u & i_x j_v & i_x k_w \\
j_y i_u & j_y j_v & j_y k_w \\
k_z i_u & k_z j_v & k_z k_w
\end{bmatrix} \quad \text{(10)}
$$


![[Pasted image 20251021143120.png]]

### Matrices de rotación (Giros sobre ejes)

$R$ es la matriz de rotación que define la orientación del sistema $OUVW$ con respecto al sistema $OXYZ$. Es importante obtener la matriz de rotación correspondiente a sistemas girados sobre cada uno de los ejes del sistema de referencia.

- Giro alrededor de un ángulo $\alpha$ del eje OX:

$$
Rotx(\alpha) = \begin{bmatrix}
1 & 0 & 0 \\
0 & \cos \alpha & -\sin \alpha \\
0 & \sin \alpha & \cos \alpha
\end{bmatrix} \quad \text{(11)}
$$

- Giro alrededor de un ángulo $\phi$$ del eje OY:

$$
Roty(\phi) = \begin{bmatrix}
\cos \phi & 0 & \sin \phi \\
0 & 1 & 0 \\
-\sin \phi & 0 & \cos \phi
\end{bmatrix} \quad \text{(12)}
$$

- Giro alrededor de un ángulo $\theta$$ del eje OZ:

$$
Rotz(\theta) = \begin{bmatrix}
\cos \theta & -\sin \theta & 0 \\
\sin \theta & \cos \theta & 0 \\
0 & 0 & 1
\end{bmatrix} \quad \text{(13)}
$$




## Composición de rotaciones

Las matrices de rotación pueden componerse para expresar la aplicación continua de varias rotaciones. Así, si al sistema OUVW se le aplica una rotación de ángulo α sobre OX, seguida de una rotación de ángulo φ sobre OY y de una rotación de ángulo θ sobre OZ, la rotación global puede expresarse como:

$$
T = Rotz (\theta) \ Roty (\phi) \ Rotx (\alpha)
$$

$$
= \begin{bmatrix}
C\theta & -S\theta & 0 \\
S\theta & C\theta & 0 \\
0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
C\phi & 0 & S\phi \\
0 & 1 & 0 \\
-S\phi & 0 & C\phi
\end{bmatrix}
\begin{bmatrix}
1 & 0 & 0 \\
0 & C\alpha & -S\alpha \\
0 & S\alpha & C\alpha
\end{bmatrix}
$$

$$
= \begin{bmatrix}
C\theta C\phi & -S\theta C\alpha + C\theta S\phi S\alpha & S\theta S\alpha + C\theta S\phi C\alpha \\
S\theta C\phi & C\theta C\alpha + S\theta S\phi S\alpha & -C\theta S\alpha + S\theta S\phi C\alpha \\
-S\phi & C\phi S\alpha & C\phi C\alpha
\end{bmatrix} \quad \text{(14)}
$$

- Donde $C\theta$ expresa $\cos \theta$ y $S\theta$ expresa $\sin \theta$.


<h5>Ejercicio 4</h5>

Rotar el vector $[2, 3, 4]$ alrededor de los ejes $x$, $y$ y $z$ en ese orden, con ángulos de 37, 53 y -90 grados sexagesimales respectivamente.

**Rpta:**
```
(-0.01135356, -5.1967973, 1.41179634)
```


## Sistema fijo y Sistema móvil

En un **sistema fijo**, las rotaciones se aplican respecto a ejes que no cambian de orientación. Las matrices de rotación se multiplican en orden inverso al de las rotaciones.

En un **sistema móvil**, las rotaciones se hacen sobre los ejes del propio objeto, que van cambiando con cada rotación. Aquí, las matrices de rotación se multiplican en el mismo orden en que se aplican las rotaciones.

La principal diferencia es que en el sistema móvil los ejes cambian de orientación durante las rotaciones, mientras que en el sistema fijo permanecen constantes.

## Ángulos de Euler

- Para la representación de orientación en un espacio tridimensional mediante una matriz de rotación es necesario definir nueve elementos.
- Otro método de definición de orientación son los llamados ángulos de Euler que hace uso de únicamente de tres componentes para su descripción.
- Todo sistema OUVW solidario al cuerpo cuya orientación se quiere describir, puede definirse con respecto al sistema OXYZ mediante tres ángulos: $\phi$$ (phi), $\theta$$ (theta), $\psi$$ (psi), denominados ángulos de Euler que representan los valores de los giros a realizar sobre tres ejes ortogonales entre sí.

![[Pasted image 20251021143500.png]]



### Ángulos de Euler WUW

- Si se parte de los sistemas OXYZ y OUVW, inicialmente coincidentes, se puede colocar al sistema OUVW en cualquier orientación siguiendo los siguientes pasos:
  1. Girar el sistema OUVW un ángulo $\phi$$ con respecto al eje OZ, convirtiéndose así en el OU'V'W'.
  2. Girar el sistema OU'V'W' un ángulo $\theta$$ con respecto al eje OU', convirtiéndose así en el OU''V''W''.
  3. Girar el sistema OU''V''W'' un ángulo $\psi$$ con respecto al eje OW'' convirtiéndose finalmente en el OU''V''W''.

- Es importante que estas operaciones se realicen en la secuencia especificada, pues las operaciones de giros consecutivos sobre ejes no son conmutativas.


![[Pasted image 20251021143618.png]]



<h5>Ejercicio 5</h5>
Rotar el vector \[2,3,4] usando ángulos de Euler en la convención WUW.

Los ángulos que utilizaremos serán:
- Primero, una rotación de 45° alrededor del eje Z.
- Luego, una rotación de 30° alrededor del eje U’.
- Finalmente, otra rotación de –60° alrededor del eje W”.

**Rpta:** (4.10053917, 0.98790901, 3.34807621)



### Ángulos de Euler WVW

- Si se parte de los sistemas OXYZ y OUVW, inicialmente coincidentes, se puede colocar al sistema OUVW en cualquier orientación siguiendo los siguientes pasos:
  1. Girar el sistema OUVW un ángulo $\phi$$ con respecto al eje OZ, convirtiéndose así en el OU'V'W'.
  2. Girar el sistema OU'V'W' un ángulo $\theta$$ con respecto al eje OV', convirtiéndose así en el sistema OU''V''W'.
  3. Girar el sistema OU''V''W'' un ángulo $\psi$$ con respecto al eje OW'', convirtiéndose finalmente en el OU''V''W''.
- Como antes, es preciso considerar que el orden de los giros no es conmutativo.

![[Pasted image 20251021143725.png]]


<h5>Ejercicio 6</h5>

- Rotar el vector [2,3,4] usando ángulos de Euler en la convención WVW.

Los ángulos que utilizaremos serán:
- Primero, una rotación de 45° alrededor del eje Z.
- Luego, una rotación de 30° alrededor del eje V’.
- Finalmente, otra rotación de –60° alrededor del eje W''.

**Rpta:** (3.78166096, 3.45349156, 1.66506351)



### Ángulos de Euler XYZ

- Estos giros sobre los ejes fijos se denominan guiñada, cabeceo y alabeo (Yaw, Pitch y Roll).
- Si se parte de los sistemas OXYZ y OUVW, al igual que en el caso anterior, se puede colocar al sistema OUVW en cualquier orientación siguiendo los siguientes pasos:
  - Girar el sistema OUVW un ángulo $\phi$ con respecto al eje OX. Es el denominado Yaw o guiñada.
  - Girar el sistema OUVW un ángulo $\theta$ con respecto al eje OY. Es el denominado Pitch o cabeceo.
  - Girar el sistema OUVW un ángulo $\psi$ con respecto al eje OZ. Es el denominado Roll o alabeo.
- También considerar que no se trata de una transformación conmutativa.


![[Pasted image 20251021143806.png]]


<h5>Ejercicio 7</h5>
Rotar el vector [2,3,4] usando ángulos de Euler en la convención XYZ.

Los ángulos que utilizaremos serán:
- Primero, una rotación de 45° alrededor del eje X.
- Luego, una rotación de 30° alrededor del eje Y.
- Finalmente, otra rotación de –60° alrededor del eje Z.

**Rpta:** (1.49108984, -3.99685692, 3.28660705)



## Par de rotación

- La representación de la orientación de un sistema OUVW con respecto al sistema de referencia OXYZ también puede realizarse mediante la definición de un vector unitario $\mathbf{k} (k_x, k_y, k_z)$$ y un ángulo de giro $\theta$$, tal que el sistema OUVW corresponde al sistema OXYZ girado un ángulo $\theta$$ sobre el eje $\mathbf{k}$$. El eje $\mathbf{k}$$ ha de pasar por el origen $O$$ de ambos sistemas. Al par $(k, \theta)$$ se le denomina par de rotación.
- Esta orientación se puede representar como Rot$(k, \theta)$$.
- La aplicación de un par de rotación que rote un vector $p$$ un ángulo $\theta$$ alrededor del vector unitario $k$$ se realiza a través de la siguiente expresión:

$$
\text{Rot}(k, \theta) \, p = p \cos \theta + (k \times p) \sin \theta + k(k \cdot p)(1 - \cos \theta)
$$



## Par de rotación (Matriz de rotación)

- Donde la matriz de rotación es:

$$
R(k, \theta) = 
\begin{bmatrix}
\cos\theta + k_x^2(1 - \cos\theta) & k_xk_y(1 - \cos\theta) - k_z\sin\theta & k_xk_z(1 - \cos\theta) + k_y\sin\theta \\
k_yk_x(1 - \cos\theta) + k_z\sin\theta & \cos\theta + k_y^2(1 - \cos\theta) & k_yk_z(1 - \cos\theta) - k_z\sin\theta \\
k_zk_x(1 - \cos\theta) - k_y\sin\theta & k_zk_y(1 - \cos\theta) + k_x\sin\theta & \cos\theta + k_z^2(1 - \cos\theta)
\end{bmatrix}
$$

- Y el punto rotado es:

$$
p' = R(k, \theta) \cdot p
$$

$$
p' = p\cos(\theta) + (k \times p)\sin(\theta) + k(k \cdot p)(1 - \cos(\theta))
$$


<h5>Ejercicio 8</h5>

1. Rotar el vector (2, 1) un ángulo de 45 grados en sentido antihorario alrededor del origen utilizando el vector (1, 1) como el eje de rotación.

**Rpta:** (1.85355339, 1.14644661, -0.5)



---

# Matrices de transformación homogénea

En general, una matriz de transformación homogénea es una matriz $4 \times 4$ que representa una transformación en el espacio tridimensional, que consta de una combinación de traslación, rotación y escala. En robótica, la matriz de transformación homogénea se utiliza para representar la posición y orientación de un eslabón (elemento mecánico) de un robot en relación con su base o con el eslabón anterior.

## Coordenadas homogéneas
- Un elemento de un espacio n-dimensional, se encuentra representado en coordenadas homogéneas por $n + 1$ dimensiones, de tal forma que un vector $p(x, y, z)$ vendrá representado por $p(wx, wy, wz, w)$, donde w tiene un valor arbitrario y representa un factor de escala.
- El factor de escala w se utiliza para realizar transformaciones de escala y proyección.
- De forma general, un vector $p = ai + bj + ck$, donde i, j y k son los vectores unitarios de los ejes OX, OY y OZ del sistema de referencia OXYZ, se representa en coordenadas homogéneas mediante el vector columna:

$$
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
$$

- Por ejemplo, el vector $2i + 3j + 4k$ se puede representar en coordenadas homogéneas como [2, 3, 4, 1]T, o como [4, 6, 8, 2]T o también como [-6, -9, -12, -3]T, etc.

## Matrices homogéneas
- A partir de la definición de las coordenadas homogéneas surge el concepto de matriz de transformación homogénea.
- Se define como matriz de transformación homogénea $H$ a una matriz de dimensión $4 \times 4$ que representa la transformación de un vector de coordenadas homogéneas de un sistema de coordenadas a otro.

$$
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
$$

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

$$
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
$$

- Esta expresión puede ser utilizada para representar la orientación y posición de un sistema O'UVW resultado de rotar y trasladar el sistema original OXYZ según $R_{3 \times 3}$ y $P_{3 \times 1}$ respectivamente.

## Ejercicios

### Ejercicio 1
- Calcule la matriz homogénea que describe la transformación de un objeto que se ha rotado 45 grados alrededor del eje z y se ha trasladado 2 unidades en x y 3 unidades en y.

### Ejercicio 2
- Calcule la matriz homogénea que describes la transformación de un objeto que primero se ha rotado 45 grados alrededor del eje z, luego 60 grados alrededor del eje x y finalmente 53 grados alrededor del eje y y se ha trasladado 2 unidades en x, 3 unidades en y, y 4 unidades en z.

### Transformación de coordenadas
- Asimismo, esta matriz puede servir para conocer las coordenadas $(r_x, r_y, r_z)$ del vector $\mathbf{r}$ en el sistema OXYZ a partir de sus coordenadas $(r_u, r_v, r_w)$ en el sistema O'UVW:

$$
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
$$

### Ejercicio 3
- Tenemos un vector r con coordenadas (2, 4, 6) en el sistema O'UVW. Queremos encontrar sus coordenadas en el sistema OXYZ. Sabemos que los ejes de O'UVW están rotados 45 grados en torno al eje Z en comparación con los ejes de OXYZ y que O'UVW se encuentra a 1 unidad a lo largo del eje X y 2 unidades a lo largo del eje Y con respecto a OXYZ.

### Ejercicio 4
- Tenemos un vector r con coordenadas (2, 4, 6) en el sistema O'UVW. Queremos encontrar sus coordenadas en el sistema OXYZ. Sabiendo que O'UVW se ha rotado primero 45 grados alrededor del eje z, luego 60 grados alrededor del eje x y finalmente 53 grados alrededor del eje y y se ha trasladado 2 unidades en x, 3 unidades en y, y 4 unidades en z.

### Transformación de vectores
- También se puede utilizar para expresar la rotación y traslación de un vector respecto de un sistema de referencia fijo OXYZ, de tal manera que un vector $r_{xyz}$ rotado según $R_{3 \times 3}$ y trasladado según $p_{3 \times 1}$ se convierte en el vector $r'_{xyz}$ dado por:

$$
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
$$

### Ejercicio 5
- Trasladar el vector $(2,3,4)$$ en OXYZ al punto $(5,6,7)$$ y rotelo 53 grados alrededor del eje X.  
Calcule su nueva coordenada en OXYZ.

### Ejercicio 6
- Trasladar el vector (2,3,4) en OXYZ al punto (5,6,7) luego rotelo 53 grados alrededor del eje X, luego 37 grados alrededor de Y y finalmente 75 grados alrededor de Z. Calcule su nueva coordenada en OXYZ.



## Matriz básica de Traslación
- Supóngase que el sistema O'UVW únicamente se encuentra trasladado un vector $p = p_x i + p_y j + p_z k$ con respecto al sistema OXYZ. La matriz T entonces corresponderá a una matriz homogénea de traslación:

$$
T(p) =
\begin{bmatrix}
1 & 0 & 0 & p_x \\
0 & 1 & 0 & p_y \\
0 & 0 & 1 & p_z \\
0 & 0 & 0 & 1
\end{bmatrix}
$$

- Un vector cualquiera $r$, representado en el sistema O'UVW por $r_{uvw}$, tendrá como componentes del vector con respecto al sistema OXYZ:

$$
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
$$

- Y a su vez, un vector $r_{xyz}$ desplazado según T tendrá como componentes $r'_{xyz}$:

$$
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
$$

### Ejemplo 1
- En la figura, el sistema O'UVW está trasladado un vector $p(6, -3, 8)$ con respecto del sistema OXYZ.  
Calcular las coordenadas del vector $r_{xyz}$ en el sistema OXYZ, sabiendo que las coordenadas en el sistema O'UVW son $r_{uvw}(-2, 7, 3)$.  

**Solución:**

$$
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
$$

### Ejemplo 2
- Calcular el vector $r'_{xyz}$ resultante de trasladar al vector $r_{xyz}(4, 4, 11)$ según la transformación T(p) con p(6, -3, 8).

**Solución:**

$$
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
$$

## Matriz básica de Rotación
- Suponga ahora que el sistema O'UVW sólo se encuentra rotado con respecto al sistema OXYZ.
- La submatriz de rotación $R_{3x3}$ será la que defina la rotación, y corresponde al tipo matriz de rotación que vimos la clase pasada.
- Así se pueden definir tres matrices homogéneas básicas de rotación según se realice ésta alrededor de cada uno de los tres ejes coordenados OX, OY y OZ del sistema de referencia OXYZ:

$$
\text{Rot}_X (\alpha) = 
\begin{bmatrix}
1 & 0 & 0 & 0 \\
0 & \cos \alpha & -\sin \alpha & 0 \\
0 & \sin \alpha & \cos \alpha & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
$$

$$
\text{Rot}_Y (\phi) =
\begin{bmatrix}
\cos \phi & 0 & \sin \phi & 0 \\
0 & 1 & 0 & 0 \\
-\sin \phi & 0 & \cos \phi & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
$$

$$
\text{Rot}_Z (\psi) =
\begin{bmatrix}
\cos \psi & -\sin \psi & 0 & 0 \\
\sin \psi & \cos \psi & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
$$

### Transformación de coordenadas con rotación
- Un vector cualquiera $r$, representado en el sistema girado O'UVW por  
  $$  r_{uvw} = (r_{u}, r_{v}, r_{w}),$$
  tendrá como componentes en el sistema OXYZ,  
  $$  r_{xyz} = (r_{x}, r_{y}, r_{z})$$  
  dadas por:  

$$
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
$$

- Y a su vez, un vector  
  $$  r_{xyz}$$
  rotado según $R$ vendrá expresado por  
  $$  r'_{xyz}$$  
  según:  

$$
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
$$

- Donde:  
$$
R = Rot_z (\psi) \, Rot_y (\phi) \, Rot_x (\alpha)
$$

### Ejemplo 3
- El sistema OUVW se encuentra girado -90° alrededor del eje OZ con respecto al sistema OXYZ. Calcular las coordenadas del vector $r_{xyz}$ si sus coordenadas en el sistema OUVW son $r_{uvw} = (4, 8, 12)^T$.

**Solución:**

$$
Rot_z (\psi) = 
\begin{bmatrix}
\cos \psi & -\sin \psi & 0 & 0 \\
\sin \psi & \cos \psi & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
$$

Para $\psi = -90^\circ$$, $\cos(-90^\circ) = 0$$, $\sin(-90^\circ) = -1$$:

$$
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
$$

## Rotación seguida de Traslación
- Rotación de un ángulo $\phi$$ sobre el eje OX seguido de una traslación de vector $P_{x,y,z}$$:

$$
T(p) \text{Rot}_x(\phi) = 
\begin{bmatrix}
1 & 0 & 0 & p_x \\
0 & \cos \phi & -\sin \phi & p_y \\
0 & \sin \phi & \cos \phi & p_z \\
0 & 0 & 0 & 1
\end{bmatrix}
$$

- Rotación de un ángulo $\theta$$ sobre el eje OY seguido de una traslación de vector $P_{x,y,z}$$:

$$
T(p) \text{Rot}_y(\theta) = 
\begin{bmatrix}
\cos \theta & 0 & \sin \theta & p_x \\
0 & 1 & 0 & p_y \\
-\sin \theta & 0 & \cos \theta & p_z \\
0 & 0 & 0 & 1
\end{bmatrix}
$$

- Rotación de un ángulo $\psi$$ sobre el eje OZ seguido de una traslación de vector $P_{x,y,z}$$:

$$
T(p) \text{Rot}_z(\psi) = 
\begin{bmatrix}
\cos \psi & -\sin \psi & 0 & p_x \\
\sin \psi & \cos \psi & 0 & p_y \\
0 & 0 & 1 & p_z \\
0 & 0 & 0 & 1
\end{bmatrix}
$$

## Traslación seguida de Rotación
- Traslación de vector $p_{x,y,z}$ seguida de rotación de un ángulo $\phi$$ sobre el eje OX.

$$
Rot_x(\phi)T(p) =
\begin{bmatrix}
1 & 0 & 0 & p_x \\
0 & \cos \phi & -\sin \phi & p_y \cos \phi - p_z \sin \phi \\
0 & \sin \phi & \cos \phi & p_y \sin \phi + p_z \cos \phi \\
0 & 0 & 0 & 1
\end{bmatrix}
$$

- Traslación de vector $p_{x,y,z}$ seguida de rotación de un ángulo $\theta$$ sobre el eje OY.

$$
Rot_y(\theta)T(p) =
\begin{bmatrix}
\cos \theta & 0 & \sin \theta & p_x \cos \theta + p_z \sin \theta \\
0 & 1 & 0 & p_y \\
-\sin \theta & 0 & \cos \theta & p_z \cos \theta - p_x \sin \theta \\
0 & 0 & 0 & 1
\end{bmatrix}
$$

- Traslación de vector $p_{x,y,z}$ seguida de rotación de un ángulo $\psi$$ sobre el eje OZ.

$$
Rot_z(\psi)T(p) =
\begin{bmatrix}
\cos \psi & -\sin \psi & 0 & p_x \cos \psi - p_y \sin \psi \\
\sin \psi & \cos \psi & 0 & p_x \sin \psi + p_y \cos \psi \\
0 & 0 & 1 & p_z \\
0 & 0 & 0 & 1
\end{bmatrix}
$$

### Ejemplo 4
- En la figura, un sistema OUVW ha sido girado 90° alrededor del eje OX y, posteriormente, trasladado un vector $p(8, -4, 12)$ con respecto al sistema OXYZ . Calcular las coordenadas $(r_x, r_y, r_z)$$ del vector $r$ con coordenadas $r_{uvw}(-3, 4, -11)$.

**Solución:**

$$
T(p) Rot_x(\phi) = 
\begin{bmatrix}
1 & 0 & 0 & p_x \\
0 & \cos \phi & -\sin \phi & p_y \\
0 & \sin \phi & \cos \phi & p_z \\
0 & 0 & 0 & 1
\end{bmatrix}
$$

Para $\phi = 90^\circ$$, $\cos 90^\circ = 0$$, $\sin 90^\circ = 1$$:

$$
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
$$

### Ejemplo 5
- En la figura, un sistema OUVW ha sido trasladado un vector $p(8, -4, 12)$ con respecto al sistema OXYZ y girado 90° alrededor del eje OX. Calcular las coordenadas $(r_x, r_y, r_z)$$ del vector $r$ de coordenadas $r_{uvw}(-3, 4, -11)$.

**Solución usando $Rot_x(\phi)T(p)$:**

$$
Rot_x(\phi)T(p) =
\begin{bmatrix}
1 & 0 & 0 & p_x \\
0 & \cos \phi & -\sin \phi & p_y \cos \phi - p_z \sin \phi \\
0 & \sin \phi & \cos \phi & p_y \sin \phi + p_z \cos \phi \\
0 & 0 & 0 & 1
\end{bmatrix}
$$

Para $\phi = 90^\circ$$:

$$
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
$$

Luego:

$$
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
$$

## Composición de matrices homogéneas
- Una matriz de transformación homogénea sirve, para representar el giro y la traslación realizados sobre un sistema de referencia.
- Esta utilidad de las matrices homogéneas cobra aún más importancia cuando se componen las matrices homogéneas para describir diversos giros y traslaciones consecutivos sobre un sistema de referencia determinado.
- De esta forma, una transformación compleja podrá descomponerse en la aplicación consecutiva de transformaciones simples (giros básicos y traslaciones).

### Composición de rotaciones
- Por ejemplo, una matriz que representa un giro de un ángulo ψ sobre el eje OZ, seguido de un giro de ángulo θ sobre el eje OY y de un giro de un ángulo φ sobre el eje OX, puede obtenerse por la composición de las matrices básicas de rotación:

$$
R = Rot_z(\psi) \, Rot_y(\theta) \, Rot_x(\phi)
$$

- Debido a que el producto de matrices no es conmutativo, tampoco lo es la composición de transformaciones.

----
---
---

Aquí está la solución al problema, basada exclusivamente en los documentos PDF proporcionados.

### Resumen de la Solución

Para lograr la misma posición y orientación final, se debería aplicar una única transformación homogénea que consiste en:

- **Valores de Traslación (respecto al sistema fijo XYZ):**
    
    - $P_x = 3.799$ unidades
        
    - $P_y = 3.592$ unidades
        
    - $P_z = 5.714$ unidades
        
- **Ángulos de Rotación (Yaw, Pitch, Roll sobre ejes fijos XYZ):**
    
    - **Yaw ($\phi$ sobre $X$):** $21.80^\circ$
        
    - **Pitch ($\theta$ sobre $Y$):** $17.83^\circ$
        
    - **Roll ($\psi$ sobre $Z$):** $74.75^\circ$
        

---

### Cálculo Detallado

#### 1. Estrategia de Composición de Matrices

El problema describe una secuencia de transformaciones mixtas. Para encontrar la matriz de transformación homogénea ($H_{final}$) total, debemos componer las matrices individuales:

1. **Transformaciones respecto al sistema fijo (XYZ):** Se premultiplican (se añaden por la izquierda).
    
2. **Transformaciones respecto al sistema móvil (noa):** Se posmultiplican (se añaden por la derecha).
    

La matriz homogénea inicial, donde ambos sistemas coinciden, es la matriz identidad ($I$).

#### 2. Definición de Matrices de Transformación

Usaremos las siguientes matrices básicas:

- $Trans(p_x, p_y, p_z) = \begin{pmatrix} 1 & 0 & 0 & p_x \\ 0 & 1 & 0 & p_y \\ 0 & 0 & 1 & p_z \\ 0 & 0 & 0 & 1 \end{pmatrix}$
    
- $RotX(\alpha) = \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & \cos\alpha & -\sin\alpha & 0 \\ 0 & \sin\alpha & \cos\alpha & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix}$
    
- $RotY(\phi) = \begin{pmatrix} \cos\phi & 0 & \sin\phi & 0 \\ 0 & 1 & 0 & 0 \\ -\sin\phi & 0 & \cos\phi & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix}$
    
- $RotZ(\psi) = \begin{pmatrix} \cos\psi & -\sin\psi & 0 & 0 \\ \sin\psi & \cos\psi & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix}$
    

El sistema móvil `noa` corresponde a los ejes `UVW`, que a su vez se alinean con `XYZ`.

- Eje `n` $\rightarrow$ Eje `U` (Móvil X)
    
- Eje `o` $\rightarrow$ Eje `V` (Móvil Y)
    
- Eje `a` $\rightarrow$ Eje `W` (Móvil Z)
    

#### 3. Secuencia de Multiplicación

Sea $H$ la matriz de transformación total, que inicia como $I$.

1. Traslación de 5 en n (móvil): $H = I \cdot Trans_x(5)$
    
    $H = Trans(5, 0, 0)$
    
2. Rotación de $60^\circ$ en o (móvil): $H = H \cdot Rot_y(60^\circ)$
    
    $H = Trans(5, 0, 0) \cdot RotY(60^\circ)$
    
3. Rotación de $60^\circ$ en Z (fijo): $H = Rot_z(60^\circ) \cdot H$
    
    $H = RotZ(60^\circ) \cdot Trans(5, 0, 0) \cdot RotY(60^\circ)$
    
4. Traslación de 3 en a (móvil): $H = H \cdot Trans_z(3)$
    
    $H = RotZ(60^\circ) \cdot Trans(5, 0, 0) \cdot RotY(60^\circ) \cdot Trans(0, 0, 3)$
    
5. Rotación de $45^\circ$ en X (fijo): $H = Rot_x(45^\circ) \cdot H$
    
    $H_{final} = RotX(45^\circ) \cdot RotZ(60^\circ) \cdot Trans(5, 0, 0) \cdot RotY(60^\circ) \cdot Trans(0, 0, 3)$
    

#### 4. Cálculo de la Matriz Homogénea Final

Valores trigonométricos:

- $\cos(60^\circ) = 0.5$
    
- $\sin(60^\circ) = 0.8660$
    
- $\cos(45^\circ) = 0.7071$
    
- $\sin(45^\circ) = 0.7071$
    

Calculamos por partes:

- $H_A = Trans(5, 0, 0) \cdot RotY(60^\circ)$
    
    $H_A = \begin{pmatrix} 1 & 0 & 0 & 5 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} 0.5 & 0 & 0.8660 & 0 \\ 0 & 1 & 0 & 0 \\ -0.8660 & 0 & 0.5 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix} = \begin{pmatrix} 0.5 & 0 & 0.8660 & 5 \\ 0 & 1 & 0 & 0 \\ -0.8660 & 0 & 0.5 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix}$
    
- $H_B = H_A \cdot Trans(0, 0, 3)$
    
    $H_B = \begin{pmatrix} 0.5 & 0 & 0.8660 & 5 \\ 0 & 1 & 0 & 0 \\ -0.8660 & 0 & 0.5 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 3 \\ 0 & 0 & 0 & 1 \end{pmatrix} = \begin{pmatrix} 0.5 & 0 & 0.8660 & 7.598 \\ 0 & 1 & 0 & 0 \\ -0.8660 & 0 & 0.5 & 1.5 \\ 0 & 0 & 0 & 1 \end{pmatrix}$
    
- $H_C = RotZ(60^\circ) \cdot H_B$
    
    $H_C = \begin{pmatrix} 0.5 & -0.8660 & 0 & 0 \\ 0.8660 & 0.5 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} 0.5 & 0 & 0.8660 & 7.598 \\ 0 & 1 & 0 & 0 \\ -0.8660 & 0 & 0.5 & 1.5 \\ 0 & 0 & 0 & 1 \end{pmatrix} = \begin{pmatrix} 0.25 & -0.8660 & 0.4330 & 3.799 \\ 0.4330 & 0.5 & 0.7500 & 6.580 \\ -0.8660 & 0 & 0.5 & 1.5 \\ 0 & 0 & 0 & 1 \end{pmatrix}$
    
- $H_{final} = RotX(45^\circ) \cdot H_C$
    
    $H_{final} = \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 0.7071 & -0.7071 & 0 \\ 0 & 0.7071 & 0.7071 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} 0.25 & -0.8660 & 0.4330 & 3.799 \\ 0.4330 & 0.5 & 0.7500 & 6.580 \\ -0.8660 & 0 & 0.5 & 1.5 \\ 0 & 0 & 0 & 1 \end{pmatrix}$
    
    $H_{final} = \begin{pmatrix} 0.25 & -0.8660 & 0.4330 & 3.799 \\ 0.9186 & 0.3536 & 0.1767 & 3.592 \\ -0.3062 & 0.3536 & 0.8839 & 5.714 \\ 0 & 0 & 0 & 1 \end{pmatrix}$
    

#### 5. Extracción de Valores de Traslación

La matriz de transformación homogénea tiene la forma $H = \begin{bmatrix} R_{3\times3} & P_{3\times1} \\ 0 & 1 \end{bmatrix}$. El vector de traslación $P$ es la última columna.

De $H_{final}$:

- **$P_x = 3.799$**
    
- **$P_y = 3.592$**
    
- **$P_z = 5.714$**
    

#### 6. Extracción de Ángulos de Rotación (Roll, Pitch, Yaw)

Debemos descomponer la submatriz de rotación $R_{final}$:

$R_{final} = \begin{pmatrix} 0.25 & -0.8660 & 0.4330 \\ 0.9186 & 0.3536 & 0.1767 \\ -0.3062 & 0.3536 & 0.8839 \end{pmatrix}$

Usamos la convención `Yaw-Pitch-Roll (XYZ)` definida en los apuntes, que corresponde a giros sobre ejes fijos. La matriz de composición para giros fijos $Z-Y-X$ (Roll-Pitch-Yaw) se calcula como $R = RotZ(\psi) \cdot RotY(\theta) \cdot RotX(\phi)$.

La matriz resultante de esta composición $R = RotZ(\psi)RotY(\theta)RotX(\phi)$ es:

$R = \begin{pmatrix} C\psi C\theta & C\psi S\theta S\phi - S\psi C\phi & C\psi S\theta C\phi + S\psi S\phi \\ S\psi C\theta & S\psi S\theta S\phi + C\psi C\phi & S\psi S\theta C\phi - C\psi S\phi \\ -S\theta & C\theta S\phi & C\theta C\phi \end{pmatrix}$

Igualamos esta matriz genérica con nuestra $R_{final}$:

$R_{final} = \begin{pmatrix} R_{11} & R_{12} & R_{13} \\ R_{21} & R_{22} & R_{23} \\ R_{31} & R_{32} & R_{33} \end{pmatrix} = \begin{pmatrix} 0.25 & -0.8660 & 0.4330 \\ 0.9186 & 0.3536 & 0.1767 \\ -0.3062 & 0.3536 & 0.8839 \end{pmatrix}$

1. Calcular $\theta$ (Pitch sobre Y):
    
    $R_{31} = -S\theta = -0.3062$
    
    $S\theta = 0.3062$
    
    $\theta = \arcsin(0.3062) = 17.83^\circ$
    
    $C\theta = \cos(17.83^\circ) = 0.9520$
    
2. Calcular $\phi$ (Yaw sobre X):
    
    $R_{32} = C\theta S\phi = 0.3536 \implies S\phi = 0.3536 / 0.9520 = 0.3714$
    
    $R_{33} = C\theta C\phi = 0.8839 \implies C\phi = 0.8839 / 0.9520 = 0.9285$
    
    Usando atan2:
    
    $\phi = \operatorname{atan2}(S\phi, C\phi) = \operatorname{atan2}(0.3714, 0.9285) = 21.80^\circ$
    
3. Calcular $\psi$ (Roll sobre Z):
    
    $R_{11} = C\psi C\theta = 0.25 \implies C\psi = 0.25 / 0.9520 = 0.2626$
    
    $R_{21} = S\psi C\theta = 0.9186 \implies S\psi = 0.9186 / 0.9520 = 0.9649$
    
    Usando atan2:
    
    $\psi = \operatorname{atan2}(S\psi, C\psi) = \operatorname{atan2}(0.9649, 0.2626) = 74.75^\circ$


----



