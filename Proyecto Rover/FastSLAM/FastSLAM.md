


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

