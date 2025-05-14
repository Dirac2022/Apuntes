

FastSLAM es un algoritmo basado en **filtros de partículas** que se utiliza para resolver el problema de **Simultaneous Localization and Mapping (SLAM)**, es decir, el problema en el que un robot debe construir un mapa de su entorno mientras simultáneamente estima su propia posición dentro de ese mapa.


# Conceptos clave
- **Estado del sistema $x_t$**:
	Representa la variable que queremos estimar en el tiempo $t$ (por ejemplo, la posición de un robot).
- **Observaciones $z_t$**:
	Son las mediciones del entorno que obtiene el sistema, usualmente con sensores como cámaras o LIDAR.
- **Acciones de control $u_t$**:
	Son las acciones realizadas por el robot (ejemplo: avanzar, girar).
- **Conjunto de partículas $\{x_i^{[i]}\}_{i=1}^N$
	- Se representa el estado con **múltiples hipótesis** llamadas partículas
	- Cada partícula tiene un **peso** asociado $w_t^{[i]}$, que indica qué tan probable es esa hipótesis.


# Filtro de partículas
Es un método basado en **Monte Carlo** para la distribución de estados en sistemas dinámicos no lineales con ruido. Su objetivo es aproximar la **distribución de probabilidad** del estado del sistema usando un conjunto de muestras o partículas.

## Representación del Estado del Sistema
El problema de estimación de estados en un sistema dinámico se modela mediante un **Modelo de Estado Oculto**, donde el estado $x_t$, evoluciona con base en:

1. **Modelo de transición del estado**
$$ x_t = f(x_{t-1}, u_t) + v_t $$

donde:
- $x_t$ es el estado del sistema en el tiempo $t$
- $u_t$ es la acción de control
- $f(\cdot)$ es la función de transición del estado.
- $v_t \sim p(v)$  es ruido del sistema, normalmente modelado como gaussiano.

2. **Modelo de observación**
$$ z_t = h(x_t) + w_t $$
donde:
- $z_t$ es la observación realizada en $t$.
- $h(\cdot)$ es la función de observación
- $w_t \sim p(w)$ es ruido en la observación, típicamente gaussiano

El objetivo del filtro de partículas es estimar la distribución de probabilidad del estado del sistema, es decir, la **densidad de probabilidad a posteriori**:
$$ p(x_t | z_{1:t}) $$
dado un conjunto de observaciones $z_{1:t} = \{z_1, z_2, \dots, z_t\}$.

## Representación con Partículas
El **Filtro de Partículas** aproxima la distribución de probabilidad $p(x_t|z_{1:t})$ mediante un conjunto de $N$ muestras o partículas:
$$ \{ x_t^{[i]}, w_t^{[i]} \}_{i=1}^N $$
donde:
- $x_t^{[i]}$ es la posición de la partícula $i$ en el tiempo $t$.
- $w_t^{[i]}$ es el peso asociado a la partícula $i$.

La distribución de probabilidad se estima mediante una suma ponderada de funciones delta de Dirac:
$$ p(x_t|z_{1:t}) \approx \sum_{i=1}^N w_t^{[i]} \delta(x_t - x_t^{[i]})$$
donde $\delta(\cdot)$ es la función delta de Dirac.


# Algoritmo
El proceso se repite en cada instante de tiempo $t$

## Inicialización
- Se generan $N$ partículas aleatorias, cada una representando una posible posición del sistema
- Se asigna un peso igual a cada partícula
$$ w_0^{[i]} = \dfrac{1}{N} $$
## Predicción (Movimiento del sistema)
- Se actualiza cada partícula según el modelo de movimiento
$$ x_t^{[i]} = f(x_{t-1}^{[i]}, u_t) +  \text{ruido} $$
- Aquí, $f(\cdot)$ es la ecuación de movimiento del robot, y se añade un poco de ruido para simular incertidumbre.

## Corrección (Incorporar la observación)
- Cada partícula se compara compara con la nueva observación $z_t$ y se recalcula su peso:
$$ w_t^{[i]} = p(z_t | x_t^{[i]}) $$
- Es decir, se usa la probabilidad de obtener la medición actual $z_t$ dado el estado de la partícula $x_t^{[i]}$

## Muestreo (Resampling)
- Se elimina las partículas con pesos bajos y se duplican las partículas con pesos altos
- Esto evita que partículas irrelevantes sigan ocupando recursos

## Estimación final
- Se obtiene la estimación del estado como el **promedio ponderado** de todas las partículas:
$$ \hat{x}_t = \sum_{i=1}^N w_t^{[i]} x_t^{[i]} $$



# Anexos


## Systematic Resampling
Es un método eficiente para seleccionar partículas en **filtros de partículas** y **FastSLAM**. Su objetivo es **reducir la degeneración de partículas**, donde pocas partículas dominan el conjunto y otras desaparecen.

En un filtro de partículas, cada partícula $x_t^{[i]}$ tiene un peso $w_t^{[i]}$, que representa la probabilidad relativa de que esa partícula sea el estado correcto. Con el tiempo, algunas partículas tiene pesos muy pequeños y contribuyen poco al resultado final.

Una solución es remuestrar partículas seleccionando las más representativas según su peso.

Dado un conjunto de $N$ partículas $\{x_t^{[i]}\}^N_{i=1}$ con pesos normalizados $w_t^{[i]}$, el muestreo sistemático selecciona nuevas partículas de la siguiente manera:

### 1. Generar posiciones de muestreo
Se genera un conjunto de posiciones uniformemente espaciadas en el intervalo $[0, 1]$:
$$ u_i = \dfrac{i-1+u}{N} \ , \quad i = 1, 2, \dots, N $$
donde $u \sim U(0, 1)$ es un número aleatorio en $[0, 1]$ para introducir aleatoriedad en el proceso.

### 2. Construir la CDF de los pesos
Se calcula la **suma acumulativa** de los pesos

$$ C_j = \sum_{k=1}^j w_t^{[k]} $$
Esto representa la probabilidad acumulada de seleccionar la partida $x_t^{[j]}$


### 3. Seleccionar partículas
Para cada posición $u_i$, se encuentra el índice $j$ tal que:

$$ c_{j-1} < u_i \leq C_j $$
La partícula $x_t^{[j]}$ se selecciona para el nuevo conjunto.







### **¿Cuál es el mejor método de resampling para FastSLAM?**

El **resampling por ruleta (Roulette Wheel Selection)** funciona bien en general, pero no es necesariamente el mejor para **FastSLAM**, ya que este algoritmo maneja **una gran cantidad de partículas y datos de mapeo**.

## Métodos de resampling
Existen otros métodos de **resampling**, cada uno con ventajas y desventajas:

1️⃣ **Resampling por Ruleta (Multinomial Resampling)** 🔄
- Método clásico que selecciona partículas proporcionalmente a sus pesos.
- **Problema**: Puede provocar la degeneración de partículas porque las más pesadas se copian muchas veces.
- **Costo computacional**: $O(N)$
- **Uso recomendado**: Para sistemas con pocas partículas.

2️⃣ **Resampling Sistemático (Systematic Resampling)** 📏

- Se generan puntos uniformemente espaciados en el intervalo [0,1] y se seleccionan partículas en base a estos puntos.

- **Ventaja**: Reduce la varianza en la selección de partículas.
- **Costo computacional**: $O(N)$

- **Uso recomendado**: Para evitar sesgo y mejorar la diversidad de partículas.


3️⃣ **Resampling Estratificado (Stratified Resampling)** 🎯

- Divide el intervalo [0,1] en subintervalos de tamaño 1N\frac{1}{N}, generando una muestra aleatoria en cada subintervalo.
- **Ventaja**: Reduce la varianza del muestreo respecto a la ruleta.
- **Costo computacional**: $O(N)$
- **Uso recomendado**: Cuando queremos mejor precisión en la selección de partículas.


4️⃣ **Resampling de Ruido de Baja Discrepancia (Residual Resampling)** 🌟

- Se copian directamente las partículas que tienen pesos altos y luego se remuestrean las restantes de forma aleatoria.
- **Ventaja**: Más eficiente en términos de diversidad.
- **Costo computacional**: O(N)O(N)
- **Uso recomendado**: Para evitar pérdida de diversidad sin aumentar demasiado el costo computacional.

### **¿Cuál es el mejor para FastSLAM?**

📌 **Para FastSLAM, el mejor método suele ser el resampling sistemático o estratificado**, porque:

- **Reduce la degeneración de partículas** (problema típico de FastSLAM).
- **Es más eficiente** que la ruleta, ya que mantiene mejor la diversidad.
- **Evita la selección repetitiva de pocas partículas**, mejorando la exploración del mapa.

📢 **Conclusión**:

- Si queremos algo simple: **Usar resampling sistemático.**
- Si queremos más precisión: **Usar resampling estratificado.**
- Si queremos el más eficiente: **Usar residual resampling.**

---

# **📌 Ahora sí, ¡implementemos el código en Python!**

Voy a escribirlo usando **resampling sistemático** (ya que es mejor que la ruleta).

✅ **Código Implementado:** Hemos escrito una implementación básica del **filtro de partículas con remuestreo sistemático**.

🔹 **¿Qué sigue?** Podemos:  
1️⃣ **Visualizar gráficamente la evolución de las partículas.**  
2️⃣ **Probar otros métodos de resampling** (estratificado o residual).  
3️⃣ **Aplicarlo a un caso real**, como localización en un mapa.

📢 **¿Qué te gustaría hacer ahora?** 🚀
