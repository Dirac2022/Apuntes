
# Clase 04: Composición de la matriz homogénea en el sistema fijo y móvil - Robótica (Teoría)


## Contenido Clase 04

- Aplicaciones de las matrices homogéneas
- Orden de las transformaciones
- Operaciones respecto al sistema fijo
- Operaciones respecto al sistema móvil
- Significado geométrico de las matrices homogéneas
- Propiedades
- Convenciones en un robot de los vectores [n o a]

---

## Aplicaciones de las matrices homogéneas

Resumiendo, las diapositivas anteriores, las aplicaciones de las matrices homogéneas son:

a) Representar la posición y orientación de un sistema girado y trasladado O'UVW con respecto a un sistema fijo de referencia OXYZ.

b) Transformar un vector r expresado en coordenadas con respecto a un sistema O'UVW, a su expresión en coordenadas del sistema de referencia OXYZ.

c) Rotar (R) y trasladar (p) un vector r con respecto a un sistema de referencia fijo OXYZ para transformarlo en el $r'$.

$$H = 
\begin{bmatrix}
R_{3x3} & P_{3x1} \\
0 & 1
\end{bmatrix}
=
\begin{bmatrix}
Rotación & Traslación \\
0 & 1
\end{bmatrix}$$

$$\begin{bmatrix}
r_x \\
r_y \\
r_z \\
1
\end{bmatrix}
= H
\begin{bmatrix}
r_u \\
r_v \\
r_w \\
1
\end{bmatrix}$$

---

## Orden de las transformaciones

- La traslación y la rotación son transformaciones que se realizan en relación con un sistema de referencia.
	
- Por tanto, si se quiere expresar la posición y orientación de un sistema OUVW, originalmente coincidente con el de referencia y que ha sido rotado y trasladado según éste, habrá que tener en cuenta si primero se ha realizado la rotación y después la traslación o viceversa, pues se trata de transformaciones espaciales no conmutativas.
	
- En la figura, se parte de un sistema OUVW coincidente con OXYZ al que se va a aplicar una traslación según un vector $P_{x,y,z}$ y una rotación de 180° alrededor del eje OZ.
	
- Si primero se rota y después se traslada se obtiene un sistema final O'U'V'W'.
	
- En cambio, si primero se traslada y después se rota se obtiene otro sistema final O''U''V''W'', que representa una localización totalmente distinta a la del sistema final anterior.
	
- Se tendrá, por tanto, matrices homogéneas distintas según se realice una traslación seguida de rotación o una rotación seguida de traslación.

![[Pasted image 20251021121623.png]]



## Operaciones respecto el sistema fijo

Si el sistema $O'UVW$ se obtiene mediante rotaciones y traslaciones definidas con respecto al sistema fijo $OXYZ$, la matriz homogénea que representa cada transformación se deberá premultiplicar sobre las matrices de las transformaciones previas.

**Ejemplo:** Se quiere obtener la matriz de transformación que representa al sistema O'UVW obtenido a partir del sistema OXYZ mediante un giro de ángulo -90° alrededor del eje OX, de una traslación de vector $p_{xyz}$ (5, 5, 10) y un giro de 90° sobre el eje OZ.

**Solución:**
- La secuencia de transformaciones es: Rotx ($-90^\circ$) → T(p) → Rotz ($90^\circ$)
- Y el orden de multiplicación de matrices es: $H = \text{Rotz} \, (90^\circ) \, T(p) \, \text{Rotx} \, (-90^\circ)$

$$H = 
\begin{bmatrix}
0 & -1 & 0 & 0 \\
1 & 0 & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
1 & 0 & 0 & 5 \\
0 & 1 & 0 & 5 \\
0 & 0 & 1 & 10 \\
0 & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
1 & 0 & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & -1 & 0 & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}$$

---

## Operaciones respecto al sistema móvil

- Si el sistema O'UVW se obtiene mediante rotaciones y traslaciones definidas con respecto al sistema móvil, la matriz homogénea que representa cada transformación se deberá postmultiplicar sobre las matrices de las transformaciones previas.

**Ejemplo:** Obtener la matriz de transformación que representa las siguientes transformaciones sobre un sistema OXYZ fijo de referencia:
- Traslación de un vector $p_{xyz}$ (-3, 10, 10); giro de –90° sobre el eje O'U del sistema trasladado y giro de 90° sobre el eje O'V del sistema girado.

**Solución:**
- La secuencia de transformaciones es: $T(p) \rightarrow Rotu \, (-90°) \rightarrow Rotv \, (90°)$
- Y el orden de multiplicación de matrices es: $H = T(p) \, Rotx \, (-90°) \, Roty \, (90°)$

$$H = 
\begin{bmatrix}
1 & 0 & 0 & -3 \\
0 & 1 & 0 & 10 \\
0 & 0 & 1 & 10 \\
0 & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
1 & 0 & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & -1 & 0 & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
0 & 0 & 1 & 0 \\
0 & 1 & 0 & 0 \\
-1 & 0 & 0 & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
=
\begin{bmatrix}
0 & 0 & 1 & -3 \\
-1 & 0 & 0 & 10 \\
0 & -1 & 0 & 10 \\
0 & 0 & 0 & 1
\end{bmatrix}$$

---

## Ejercicio 1

- Partiendo del sistema fijo $OX_1Y_1Z_1$, llegue al sistema $OX_3Y_3Z_3$.
   a) Usando solo el sistema fijo $OX_1Y_1Z_1$.
   b) Usando solo los sistemas móviles que se vayan generando.

**Respuesta:**

$$\begin{bmatrix}
0 & 0 & -1 & 3 \\
1 & 0 & 0 & 3 \\
0 & -1 & 0 & 3 \\
0 & 0 & 0 & 1
\end{bmatrix}$$

---

## Ejercicio 2

- Partiendo del sistema fijo $OX_1Y_1Z_1$, llegue al sistema $OX_3Y_3Z_3$ a través del sistema $OX_2Y_2Z_2$.
- Es decir, utilizando los sistemas móviles que vaya generando (Existen varias formas de llegar a la misma respuesta).

**Respuesta:**

$$\begin{bmatrix}
0 & 0 & -1 & 3 \\
1 & 0 & 0 & 3 \\
0 & -1 & 0 & 3 \\
0 & 0 & 0 & 1
\end{bmatrix}$$

Note que la matriz homogénea es la misma obtenida en el ejercicio 1.

---

## Ejercicio 3

- Las coordenadas del punto p respecto al sistema $OX_2Y_2Z_2$ es$(0, 2, 1)$
   a) Utilizando matrices homogéneas calcular su coordenada respecto del sistema $OX_1Y_1Z_1$.
   b) Utilizando matrices homogéneas calcular su coordenada respecto al sistema $OX_3Y_3Z_3$.

**Respuesta:**
- **p** respecto a $OX_1Y_1Z_1$ es$(1, 0, 3)$
- **p** respecto a $OX_3Y_3Z_3$ es$(-3, 0, 2)$

---

## Ejercicio 4

- Partiendo del sistema fijo $OX_A Y_A Z_A$, llegue al sistema $OX_C Y_C Z_C$ directamente.

**Respuesta:**

$$\begin{bmatrix}
-0.5 & 0.87 & 0 & 3 \\
0.87 & 0.5 & 0 & 0 \\
0 & 0 & 1 & 2 \\
0 & 0 & 0 & 1
\end{bmatrix}$$

---

## Ejercicio 5

- Partiendo del sistema fijo $OX_A Y_A Z_A$, llegue al sistema $OX_C Y_C Z_C$ a través del sistema $OX_B Y_B Z_B$.
- Utilizando los sistemas móviles que vaya generando (Existen varias formas de llegar a la misma respuesta).

**Respuesta:**

$$\begin{bmatrix}
0 & -0.5 & 0.87 & 3 \\
0 & 0.87 & 0.5 & 0 \\
-1 & 0 & 0 & 2 \\
0 & 0 & 0 & 1
\end{bmatrix}$$

Note que la matriz homogénea es la misma obtenida en el ejercicio 4.

---

## Ejercicio 6

- Partiendo del sistema fijo $OX_A Y_A Z_A$, llegue al sistema $OX_C Y_C Z_C$ a través del sistema $OX_B Y_B Z_B$.
- Es decir, utilizando los sistemas móviles que vaya generando (Existen varias formas de llegar a la misma respuesta).

**Respuesta:**

$$\begin{bmatrix}
0.7997 & 0.6004 & 0 & -3 \\
0.6004 & -0.7997 & 0 & 4 \\
0 & 0 & -1 & 2 \\
0 & 0 & 0 & 1
\end{bmatrix}$$

---

## Ejercicio 7

- Un robot está ubicado a 1 metro de una mesa. La mesa tiene 1 metro de alto y 1 metro cuadrado. Un sistema O1X1Y1Z1 está fijado al borde de la mesa. Un cubo que mide 20 cm de lado se coloca en el centro de la mesa, con el sistema O2X2Y2Z2 establecido en el centro del cubo. Una cámara se sitúa directamente sobre el centro del bloque, a 2 metros sobre la superficie de la mesa, con el sistema O3X3Y3Z3 adjunto.
- Encuentra las transformaciones homogéneas que relacionan cada uno de estos sistemas con el sistema base O0X0Y0Z0.
- Encuentra la transformación homogénea que relaciona el sistema O2X2Y2Z2 con el sistema de la cámara O3X3Y3Z3.

---

## Ejercicio 8

- Si el bloque sobre la mesa se rota$90^\circ$ alrededor de$Z_2$ y se mueve de manera que su centro tiene coordenadas$(0.5, 0.8, 0.1)^T$ relativas al sistema$O_1X_1Y_1Z_1$, calcula la transformación homogénea que relaciona el sistema del bloque con el sistema de la cámara; y el sistema del bloque con el sistema base.

---

## Significado geométrico de las matrices homogéneas

- La matriz de transformación se puede escribe de la forma:

$$H = 
\begin{bmatrix}
n_x & o_x & a_x & p_x \\
n_y & o_y & a_y & p_y \\
n_z & o_z & a_z & p_z \\
0 & 0 & 0 & 1
\end{bmatrix} =
\begin{bmatrix}
n & o & a & p \\
0 & 0 & 0 & 1
\end{bmatrix}$$

- Donde $n, o, a$ es una terna ortonormal que representa la orientación $y$ $p$ es un vector que representa la posición.

---

## Propiedades

1. Si se considera un vector $r_{uvw} = [0, 0, 0, 1]^T$, es decir, el origen del sistema O'UVW, la aplicación de la matriz H que representa la transformación de O'UVW con respecto a OXYZ, se obtiene $r_{xyz}$:

$$r_{xyz} =
\begin{bmatrix}
n & o & a & p \\
0 & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
0 \\
0 \\
0 \\
1
\end{bmatrix}
=
\begin{bmatrix}
p_x \\
p_y \\
p_z \\
1
\end{bmatrix}$$

que coincide con el vector columna $p$ de H. Por tanto, este vector columna representa la posición del origen de O'UVW con respecto del sistema OXYZ. De esta forma se puede obtener "visualmente" el vector $p$ si se dispone el grafico final de las transformaciones.

2. Si se considera el vector de coordenadas homogéneas$[1, 0, 0, 1]^T$ con respecto del sistema O'UVW, es decir, el vector director (unitario) del eje coordenado O'U del sistema O'UVW, y suponiendo el vector p de traslación nulo, se tendrá:

$$\begin{bmatrix}
r_x \\
r_y \\
r_z \\
1
\end{bmatrix}
=
\begin{bmatrix}
n_x & o_x & a_x & p_x \\
n_y & o_y & a_y & p_y \\
n_z & o_z & a_z & p_z \\
0 & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
1 \\
0 \\
0 \\
1
\end{bmatrix}
=
\begin{bmatrix}
n_x \\
n_y \\
n_z \\
1
\end{bmatrix}$$

Es decir, el vector columna n representa las coordenadas del eje OU del sistema OUVW con respecto del sistema OXYZ. De forma similar, sucede con los vectores o y a. De esta forma se puede obtener "visualmente" los vectores [n o a] si se dispone el grafico final de las transformaciones.

---

## Ejercicio 9

- Teniendo en cuenta las propiedades geométricas de las transformaciones homogéneas. Determine a partir de la figura la matriz H.

$$H = 
\begin{bmatrix}
n_x & o_x & a_x & p_x \\
n_y & o_y & a_y & p_y \\
n_z & o_z & a_z & p_z \\
0 & 0 & 0 & 1
\end{bmatrix} =
\begin{bmatrix}
n & o & a & p \\
0 & 0 & 0 & 1
\end{bmatrix}$$

**Respuesta:**

$$\begin{bmatrix}
0 & -0.5 & 0.87 & 3 \\
0 & 0.87 & 0.5 & 0 \\
-1 & 0 & 0 & 2 \\
0 & 0 & 0 & 1
\end{bmatrix}$$

Note que la matriz homogénea es la misma obtenida en los ejercicios 4 y 5.

---

## Propiedades

- Consecuentemente, los vectores $n$, $o$ y a definen una terna ortonormal a derechas, lo que significa que:
  $$  ||n|| = ||o|| = ||a|| = 1$$
  $$  n \times o = a$$

- Como la matriz de rotación es ortonormal se cumple que:
  $$  [not]^{-1} = [not]^{T}$$

- La matriz inversa de la matriz homogénea de transformación $H$ corresponde a la siguiente expresión:

$$H =
\begin{bmatrix}
n_x & o_x & a_x & p_x \\
n_y & o_y & a_y & p_y \\
n_z & o_z & a_z & p_z \\
0 & 0 & 0 & 1
\end{bmatrix}$$

$$H^{-1} =
\begin{bmatrix}
n_x & n_y & n_z & -n^T p \\
o_x & o_y & o_z & -o^T p \\
a_x & a_y & a_z & -a^T p \\
0 & 0 & 0 & 1
\end{bmatrix}$$

---

## Convenciones en un robot de los vectores [n o a]

- Aplicado a un robot, la matriz de transformación homogénea permite describir la localización (posición y orientación) de su extremo con respecto a su base.

- Así, asociando a la base del robot un sistema de referencia fijo (OXYZ) y al extremo un sistema de referencia que se mueva con él, cuyo origen se encuentre en el punto **p**, los vectores directores **[n o a]** son escogidos de modos que:

- **a**: sea un vector en la dirección de aproximación del extremo del robot a su destino. (approach)
- **o**: sea un vector perpendicular a **a** en el plano definido por la pinza del robot. (orientation)
- **n**: sea un vector que forme una terna ortogonal con los dos anteriores. (normal)
- Formando así un sistema dextrógiro.

---

## Ejercicio 10

- Considere la siguiente secuencia de rotaciones:
  1. Rotar por$\phi$ alrededor del eje x de eje fijo.
  2. Rotar por$\theta$ alrededor del eje z móvil actual.
  3. Rotar por$\psi$ alrededor del eje x móvil actual.
  4. Rotar por$\alpha$ alrededor del eje z de eje fijo.

- Escriba un programa en Python que calcule e imprima simbólicamente la matriz homogénea resultante.

- Reemplace por los siguientes valores e imprima la matriz homogénea resultante:

| Angulo | Grados |
|--------|--------|
|$\phi$    | -30    |
|$\theta$    | 45    |
|$\psi$    | -60    |
|$\alpha$    | 75    |

---

## Ejercicio 11

- El sistema de coordenadas $O_1X_1Y_1Z_1$ se obtiene a partir del sistema de coordenadas  
   $O_0X_0Y_0Z_0$ mediante una rotación de $\pi/2$ alrededor del eje $X$ seguida de una rotación de  
   $\pi/2$ alrededor del eje $Y$ fijo, encuentre la matriz de homogénea $H$ que represente la transformación compuesta.  
   Esboce los sistemas de coordenadas inicial y final.

**Respuesta:**

$$\begin{bmatrix}
0 & 1 & 0 & 0 \\
0 & 0 & -1 & 0 \\
-1 & 0 & 0 & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}$$

---

## Ejercicio 12

- Suponga que se tienen tres sistemas de coordenadas: $O_1X_1Y_1Z_1$, $O_2X_2Y_2Z_2$ y $O_3X_3Y_3Z_3$, y suponga que:

$$R_2^1 = 
\begin{bmatrix}
1 & 0 & 0 \\
0 & \frac{1}{2} & -\frac{\sqrt{3}}{2} \\
0 & \frac{\sqrt{3}}{2} & \frac{1}{2}
\end{bmatrix}, \quad R_3^1 = 
\begin{bmatrix}
0 & 0 & -1 \\
0 & 1 & 0 \\
1 & 0 & 0
\end{bmatrix}$$

$R_2^1$ es la matriz de rotación que especifica la orientación del sistema $O_2X_2Y_2Z_2$ con respecto al sistema $O_1X_1Y_1Z_1$.

$R_3^1$ es la matriz de rotación que especifica la orientación del sistema $O_3X_3Y_3Z_3$ con respecto al sistema $O_1X_1Y_1Z_1$.

Encuentre la matriz homogénea H que represente a rotación $R_3^2$. Es decir, la matriz de rotación del sistema $O_3X_3Y_3Z_3$ con respecto al sistema $O_2X_2Y_2Z_2$.

**Respuesta:**

$$\begin{bmatrix}
0 & 0 & -1 & 0 \\
\sqrt{3}/2 & 1/2 & 0 & 0 \\
1/2 & -\sqrt{3}/2 & 0 & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}$$

---

FIN