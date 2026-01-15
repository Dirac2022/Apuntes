
# Clase 05: Cuaternios - Robótica (Teoría)

**Profesor:** Carlos Diaz  
**Email:** cdiazd@uni.edu.pe

---

## Contenido Clase 05

- Definición de cuaternio
- Interpretación del cuaternio
- Ley de composición interna de cuaternios
- Cuaternio conjugado
- Operaciones con cuaternios
- Utilización de los cuaternios
- Composición de rotaciones
- Rotaciones con traslaciones
- Paso de cuaternio a matriz homogénea
- Paso de matriz homogénea a cuaternio

---

## Definición de cuaternio

- Un cuaternio es una representación matemática utilizada en robótica y gráficos por computadora para describir rotaciones en el espacio tridimensional.
- Un cuaternio $Q$ está constituido por cuatro componentes $(q_0, q_1, q_2, q_3)$ que representan las coordenadas del cuaternio en una base $\{e, i, j, k\}$.
- Se denomina parte escalar del cuaternio a la componente en $e: q_0$, y parte vectorial al resto de componentes. De modo que un cuaternio se puede representar como:

$$Q = [q_0, q_1, q_2, q_3] = [s, v]$$

donde s representa la parte escalar (real), y v la parte vectorial (imaginaria).

---

## Interpretación del cuaternio

- Sea el cuaternio $Q = q_0 + q_1i + q_2j + q_3k$
- Si queremos representar una rotación de $\theta$ radianes alrededor de un eje unitario $(k_x, k_y, k_z)$, los componentes del cuaternio se calcularían así:
- La parte real:  
  $$q_0 = \cos\left(\frac{\theta}{2}\right)$$
- La parte imaginaria:  
  $$q_1 = k_x \cdot \sin\left(\frac{\theta}{2}\right)$$
  $$q_2 = k_y \cdot \sin\left(\frac{\theta}{2}\right)$$
  $$q_3 = k_z \cdot \sin\left(\frac{\theta}{2}\right)$$

---

## Ley de composición interna de cuaternios

- Un cuaternio está formado por cuatro componentes ($q_0, q_1, q_2, q_3$) que representan las coordenadas del cuaternio en una base $e, i, j, k$. Donde el escalar e se puede considerar igual a 1 e i, j, k son vectores unitarios imaginarios.

$$Q = q_0 e + q_1 i + q_2 j + q_3 k = (s, v)$$

- Sobre los elementos de la base se define una ley de composición interna o (producto) según se muestra en la tabla. De este modo los cuaternios forman un grupo cíclico de orden cuatro.

| o    | e    | i    | j    | k    |
|------|------|------|------|------|
| e    | e    | i    | j    | k    |
| i    | i    | -e   | k    | -j   |
| j    | j    | -k   | -e   | i    |
| k    | k    | j    | -i   | -e   |

---

## Cuaternio conjugado

- A un cuaternio $Q$ se le puede asociar su conjugado $Q^*$, en el que se mantiene el signo de la parte escalar y se invierte el de la vectorial.

$$Q^* = [q_0, -q_1, -q_2, -q_3] = (s, -v)$$

- Propiedades:
  1. El conjugado del conjugado de un cuaternio es el cuaternio original:

$$(Q^*) = Q$$

  2. El conjugado del producto de dos cuaternios es igual al producto de los conjugados en orden inverso:

$$(Q_1 \circ Q_2)^* = Q_2^* \circ Q_1^*$$

  3. El conjugado de un cuaternio unitario (cuaternio con norma igual a 1) es igual a su inverso multiplicativo:

$$(Q^*) = Q^{-1}$$

  4. El producto de un cuaternio por su conjugado es igual a su norma al cuadrado: $Q \circ Q^* = ||Q||^2$

---

## Operaciones algebraicas con cuaternios

- Se definen tres operaciones algebraicas sobre los cuaternios: producto, suma y producto con un escalar.
- El producto de dos cuaternios $Q_1$ y $Q_2$, viene dado por:

$$Q_3 = Q_1 \circ Q_2 = (s_1, v_1) \circ (s_2, v_2) = (s_1 s_2 - v_1 v_2, v_1 \times v_2 + s_1 v_2 + s_2 v_1)$$

- Expresando por componentes:

$$q_{30} = q_{10} q_{20} - q_{11} q_{21} - q_{12} q_{22} - q_{13} q_{23}$$
$$q_{31} = q_{10} q_{21} + q_{11} q_{20} + q_{12} q_{23} - q_{13} q_{22}$$
$$q_{32} = q_{10} q_{22} - q_{11} q_{23} + q_{12} q_{20} + q_{13} q_{21}$$
$$q_{33} = q_{10} q_{23} + q_{11} q_{22} - q_{12} q_{21} + q_{13} q_{20}$$

- La suma de dos cuaternios $Q_1$ y $Q_2$ se define como:

$$Q_3 = Q_1 + Q_2 = (s_1, v_1) + (s_2, v_2) = (s_1 + s_2, v_1 + v_2)$$

- El producto por un escalar es:

$$Q_3 = aQ_2 = a(s_2, v_2) = (as_2, av_2)$$

- El producto de cuaternios es asociativo pero no es commutativo.

$$(Q_1 \circ Q_2) \circ Q_3 = Q_1 \circ (Q_2 \circ Q_3)$$

- La norma de un cuaternio es un número real:

$$||Q|| = \sqrt{q_0^2 + q_1^2 + q_2^2 + q_3^2}$$

- Se deduce que:

$$Q \circ Q^* = (q_0^2 + q_1^2 + q_2^2 + q_3^2) = ||Q||^2$$

- Y se cumple que:

$$||Q_1 \circ Q_2|| = ||Q_1|| \cdot ||Q_2||$$

- El inverso de un cuaternio distinto de cero es:  
  $$Q^{-1} = \frac{Q^*}{\|Q\|^2}$$

- Y se cumple que:  
  $$Q \circ Q^{-1} = Q^{-1} \circ Q = (1,0,0,0) = e$$

- Se puede definir el cuaternio identidad como:  
  $$I = e + 0i + 0j + 0k$$

- Se puede verificar:  
  $$\|Q^{-1}\| = \frac{I}{\|Q\|}$$

---

## Utilización de los cuaternios

- El cuaternio que representa un giro $\theta$ sobre un el vector $k$ unitario se puede expresar como:

$$Q = \text{Rot}(k, \theta) = \left( \cos \frac{\theta}{2}, k \sin \frac{\theta}{2} \right)$$

- La rotación expresada por el cuaternio $Q$ a un vector $r$, vendrá definida por el producto:

$$r' = Q \circ (0, r) \circ Q^*$$

- Para realizar esta operación, primero multiplicas $Q$ por $(0, r)$ y luego el resultado de esa multiplicación lo multiplicas por $Q^*$.

---

## Ejercicio 1

- Obtener el cuaternio que representa una rotación de $90^\circ$ sobre el vector $u = (3, -2, 1)$.  
  También realiza el programa en python

**Solución:**  
El eje de giro unitario será  
$$k = \frac{u}{\|u\|} = \frac{1}{\sqrt{14}} (3, -2, 1)$$

Con lo que aplicando la Ecuación:  

$$Q = \text{Rot}(k, \theta) = \left( \cos \frac{\theta}{2}, k \sin \frac{\theta}{2} \right)$$

$$Q = \text{Rot}(k, 90^\circ) = \left( \frac{\sqrt{2}}{2}, \frac{3}{\sqrt{14}}, \frac{-2}{\sqrt{14}}, \frac{\sqrt{2}}{\sqrt{14}}, \frac{1}{\sqrt{14}}, \frac{\sqrt{2}}{\sqrt{14}} \right) = (0.70711, 0.56695, -0.37796, 0.18898)$$

---

**Vector u:** [ 3 - 2 1]  
**Vector unitario k:** [ 0.80178373 - 0.53452248 0.26726124]  
**Cuaternio de rotación Q:**  
[ 0.70710678 0.56694671 - 0.37796447 0.18898224]

---

## Ejercicio 2

- Obtener el vector $r'$ resultante al aplicar la misma rotación del Ejercicio 1 sobre el vector $r = (5, 2, -6)$. También modifique el programa para calcular el resultado.

**Solución:**

Con lo que aplicando la Ecuación:

$$r' = Q \circ (0, r) \circ Q^*$$

se obtiene que $r'$:

$$r' = (0.70711, 0.56695, -0.37796, 0.18898) \circ (0, 5, 2, -6) \circ (0, 70711, -0, 56695, 0, 37796, -0, 18898) = (0, 3, 74, 5, 43, 4, 63)$$

---

**Vector u: \[ 3 - 2 1]**

**Vector unitario k: \[ 0.80178373 - 0.53452248 0.26726124]**

**Cuaternio de rotación Q:**

**\[ 0.70710678 0.56694671 - 0.37796447 0.18898224]**

**Vector r: \[ 5  2 - 6]**

**Vector rotado r':**

**\[ -0.    3.74404099  5.43272285  4.63332273 ]**

---

## Composición de rotaciones

La composición de rotaciones con cuaternios consiste en multiplicar cuaternios entre sí. De tal forma, que el resultado de rotar según el cuaternio $Q_1$, para posteriormente rotar según $Q_2$, es el mismo que el de rotar según $Q_3$, obtenido por la expresión:

$$Q_3 = Q_2 \circ Q_1$$

---

## Rotaciones con traslaciones

El resultado de aplicar una traslación de vector $\mathbf{p}$ seguida de una rotación $\mathbf{Q}$ al sistema OXYZ, es un nuevo sistema OUVW, tal que las coordenadas de un vector $\mathbf{r}$ en el sistema OXYZ, conocidas en OUVW, serán:

$$(0, \, \mathbf{r}_{xyz}) = Q \circ (0, \, \mathbf{r}_{uvw}) \circ Q^* + (0, \, \mathbf{p})$$

Donde $\mathbf{Q}$ y $\mathbf{p}$ están definidas con respecto a los sistemas de referencia móviles.

El resultado de primero rotar y luego trasladar al sistema vendrá dado por:

$$(0, \, \mathbf{r}_{xyz}) = Q \circ (0, \, \mathbf{r}_{uvw} + \mathbf{p}) \circ Q^*$$

Donde $\mathbf{p}$ y $\mathbf{Q}$ están definidos con respecto a los sistemas de referencia móviles.

Si se mantiene el sistema OXYZ fijo y se traslada el vector $r$ según $p$ y luego se le rota según $Q$ se obtendrá:

$$(0, \mathbf{r}') = Q \circ (0, \mathbf{r} + p) \circ Q^{*}$$

Y si se aplica primero el giro y después la traslación $p$ al vector $r$, éste se convertirá en el $r'$ a través de la expresión:

$$(0, \mathbf{r}') = Q \circ (0, \mathbf{r}) \circ Q^{*} + (0, p)$$

Se observa que el empleo de cuaternios para la composición de rotaciones es un método computacionalmente muy práctico, pues basta multiplicar cuaternios entre sí, lo que corresponde a una expresión de productos y sumas simple. Además, permiten representar las rotaciones mediante solo 4 elementos, frente a los 9 utilizados en las matrices de rotación. Ésta es su principal ventaja.

---

## Paso de cuaternio a matriz homogenea

La representación de la matriz de transformación $H$ en función de las componentes de un cuaternio $Q$ viene dada por la siguiente matriz:

$$H = 2
\begin{bmatrix}
q_0^2 + q_1^2 - \frac{1}{2} & q_1q_2 - q_3q_0 & q_1q_3 + q_2q_0 & 0 \\
q_1q_2 + q_3q_0 & q_0^2 + q_2^2 - \frac{1}{2} & q_2q_3 - q_1q_0 & 0 \\
q_1q_3 - q_2q_0 & q_2q_3 + q_1q_0 & q_0^2 + q_3^2 - \frac{1}{2} & 0 \\
0 & 0 & 0 & \frac{1}{2}
\end{bmatrix}$$

---

## Paso de matriz homogénea a cuaternio

- La representación un cuaternio $Q$ en función de las componentes de la matriz de transformación $H$ viene dada por:

$$q_0 = \frac{1}{2} \sqrt{(n_x + o_y + a_z + 1)}$$
$$q_1 = sgn \, (o_z - a_y) \, \frac{1}{2} \sqrt{(n_x - o_y - a_z + 1)}$$
$$q_2 = sgn \, (a_x - n_z) \, \frac{1}{2} \sqrt{(-n_x + o_y - a_z + 1)}$$
$$q_3 = sgn \, (n_y - o_x) \, \frac{1}{2} \sqrt{(-n_x - o_y + a_z + 1)}$$

---

### Función sgn(x)

sgn(x) =  
$$\begin{cases} 
1 & \text{si} \, x > 0 \\ 
0 & \text{si} \, x = 0 \\ 
-1 & \text{si} \, x < 0 
\end{cases}$$

---

## Ejercicio 3

- Obtener el cuaternio asociado a la rotación definida por la matriz de rotación:

[1] [0] [0]

0 [1/√2] [−1/√2]

0 [1/√2] [1/√2]

Solución:

**Cuaternio:**

**[0.92387953 0.38268343 0.** **0.** **]**

---

## Ejercicio 4

- Encontrar el cuaternio y la matriz homogénea equivalente, a realizar los dos giros siguientes de manera consecutiva:
  a) Giro entorno a $k_1 = (1, 0, 1)$, un ángulo $\pi/4$.
  b) Giro entorno a $k_2 = (1, 1, 0)$, un ángulo $\pi/6$.

Ambos giros están definidos respecto del sistema fijo OXYZ.

c) ¿Cuál será el resultado de someter a los giros consecutivos a y b al punto, $p = (1, 1, 1)^2$.

Sugerencia:

Para a y b, se calcula el cuaternio $Q_1$ y el cuaternio $Q_2$, respectivamente, luego se obtiene el cuaternio resultante de aplicar los dos giros, considerando que es por medio de un sistema fijo:

$$Q = Q_2 \circ Q_1$$

---

### Solución:

| Parte a | Q1 = [0.9235795325112867, 0.27059895007299845, 0.0, 0.27059895007399845] |
| Parte b | Q2 = [0.9659258262898683, 0.1839127018922193, 0.1839127018922193, 0.0] |
| Cuaternio obtenido | Q: [0.842876229561879, 0.4799822148475231, 0.11955880919716724, 0.2118547648384245] |
| Matriz homogenea equivalente: | [0.8816 -0.2424 0.4049 0.    ] [0.4719 0.4495 -0.7585 0.    ] [0.0018 0.8598 0.5106 0.    ] [0.   0.   0.   1.    ] |

Calculado con matriz homogenea $p' = [1.0441 0.1629 1.3722 1.    ]$  
Calculado con puro cuaternios $p' = [0.    1.0442 0.1629 1.3723]$

---

## Ejercicio 5

- Al sistema de coordenadas OXYZ, se le realizan las siguientes transformaciones:
  a) Giro en torno al eje X un ángulo de $\pi/2$.
  b) Una traslación definida por el vector $d_2 = (2, 1, 1)$.
  c) Giro entorno al vector $k_3 = (1, 1, 0)$ un ángulo $\pi/3$.
  d) Giro definido por el cuaternio $Q_4 = (0.9659, 0, 0.2588, 0.2588)$.
  e) Traslación definida por el vector $d_5 = (2, 1, 2)$.

- Encontrar las coordenadas en el sistema OUVW del punto p que en el sistema OXYZ tiene por coordenadas $(1, 1, 1)$. Todos los movimientos están definidos en el sistema móvil OUVW.

Sugerencia: Como se hará rotaciones y traslaciones consecutivas. Utilice matrices homogéneas.

Realice las siguientes transformaciones:

H1 = R(x,90°)  
H2 = T(d_2)  
H3 = R(k_3,60°)  
H4 = R(Q_4)  
H5 = T(d_5)

Utilice el cuaternio y luego calcule su matriz homogenea Obtenga la matriz homogenea de este cuaternio

| A | Ser las transformaciones respecto a un sistema móvil, la transformación total, se calcula así: |
| H | = H1 * H2 * H3 * H4 * H5 |

Respuesta:  
$$x = -1.6160 \quad y = -2.5036 \quad z = -3.2191$$

---

FIN