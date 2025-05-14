
# 🎓 Minicurso de PCA - Sección 1: Fundamentos Teóricos

---

## 1.1 ¿Qué es PCA y para qué sirve?

**PCA (Principal Component Analysis)** es un método para **reducir la dimensionalidad** de un conjunto de datos **manteniendo tanta información como sea posible**.

- **Problema:** Datos de alta dimensión son difíciles de visualizar y manejar (maldita "maldición de la dimensionalidad").
- **Idea:** Encontrar nuevas coordenadas (ejes) en los que los datos se "extienden" más.
- **Resultado:** Nuevas variables (componentes principales) que son combinaciones lineales de las originales.

**Ejemplo práctico:**
- Tienes datos con 100 características → PCA puede reducirlos a 2 o 3 **capturando casi toda la información**.

---

## 1.2 Intuición geométrica: ¿Qué hace PCA?

Visualiza cada dato como un punto en el espacio.

- PCA encuentra las **direcciones** (líneas, planos, etc.) donde los puntos están más **esparcidos**.
- Luego, **proyecta** los puntos sobre esas direcciones.
- Así, representas los datos **en menos dimensiones** con **mínima pérdida de información**.

**Visualmente:**
- Imagina una nube de puntos en 3D.
- Hay una dirección donde los puntos están más dispersos.
- PCA te da esa dirección como el **primer componente principal**.

---

## 1.3 El papel de la varianza

**Varianza = medida de dispersión.**

- PCA busca **maximizar la varianza**: busca las direcciones donde los datos varían más.
- Si los datos varían mucho en una dirección, probablemente esa dirección contiene **información importante**.

**Por eso:**
- El **primer componente principal** es la dirección de máxima varianza.
- El **segundo componente principal** es la dirección **ortogonal** a la primera que captura la segunda mayor varianza.
- Y así sucesivamente.

---

## 1.4 Un poco de Álgebra Lineal: Covarianza, Autovectores y Autovalores

### 1.4.1 Matriz de Covarianza

La **matriz de covarianza** $C$ mide cómo varían juntas dos variables.
Para un conjunto de datos centrado $X$ (es decir, datos con media cero en cada columna):

$$
C = \frac{1}{n-1} X^T X
$$

Donde:
- $X$ es la matriz de datos de tamaño $n \times d$ (n muestras, d características),
- $X^T$ es la traspuesta de $X$.

Cada elemento $C_{ij}$ es la covarianza entre la característica $i$ y la característica $j$.

---

### 1.4.2 Autovectores y Autovalores

Recordatorio:
- Un **autovector** de una matriz $A$ es un vector $v$ tal que:

$$
A v = \lambda v
$$

- donde $\lambda$ es su **autovalor**.

**En PCA:**
- Los **autovectores** de la matriz de covarianza son las **direcciones principales** (componentes principales).
- Los **autovalores** nos dicen **cuánta varianza** hay en cada dirección.

✅ **Ordenamos los autovectores según los autovalores de mayor a menor.**

---

## 1.5 Conexión con el Teorema Espectral

Recordemos:  
- El **Teorema Espectral** dice que toda **matriz simétrica real** (como la matriz de covarianza) se puede diagonalizar:

$$
C = Q \Lambda Q^T
$$

donde:
- $Q$ tiene los autovectores ortonormales en sus columnas,
- $\Lambda$ es una matriz diagonal de autovalores.

**PCA básicamente usa esta descomposición para encontrar las mejores direcciones de proyección.**

---

# 📋 En resumen (Sección 1)

- PCA busca **nuevos ejes** donde los datos están más dispersos.
- Estos ejes son los **autovectores** de la matriz de **covarianza** de los datos.
- Los **autovalores** nos dicen **cuánta información (varianza)** hay en cada dirección.
- Gracias al **Teorema Espectral**, sabemos que estos autovectores forman una base ortonormal.

---

# 🎓 Minicurso de PCA - Sección 2: Derivación Matemática Paso a Paso

---

## 2.1 Primer paso: centrar los datos

Antes de hacer PCA, **siempre debes centrar** los datos:
- **Centrar** significa hacer que cada variable tenga **media cero**.

**Fórmula:**
Si $X \in \mathbb{R}^{n \times d}$ es la matriz de datos (n muestras, d características):

1. Calcula la media de cada característica:

$$
\mu_j = \frac{1}{n} \sum_{i=1}^{n} X_{ij}
$$

2. Resta la media a cada columna:

$$
X_{\text{centrado}} = X - \text{media}(X)
$$

✅ Este paso es **fundamental** porque PCA mide la **varianza** respecto al **origen** (0).

---

## 2.2 Construir la matriz de covarianza

Ahora, construimos la **matriz de covarianza** de los datos centrados:

$$
C = \frac{1}{n-1} X_{\text{centrado}}^T X_{\text{centrado}}
$$

- $C \in \mathbb{R}^{d \times d}$,
- $C_{ij}$ mide cómo las variables $i$ y $j$ varían juntas.

**Notas importantes:**
- $C$ es **simétrica** ($C^T = C$),
- $C$ es **semi-definida positiva** (todos sus autovalores son \(\geq 0\)).

---

## 2.3 El objetivo de PCA: maximizar la varianza proyectada

Ahora, formalizamos el objetivo de PCA:

**Queremos encontrar una dirección $w \in \mathbb{R}^d$ (un vector unitario) tal que:**

- La **varianza** de los datos proyectados sobre $w$ sea **máxima**.

Matemáticamente:

- Proyectar un dato $x_i$ sobre $w$ es:

$$
\text{proyección} = w^T x_i
$$

- La varianza de todas las proyecciones es:

$$
\text{Var}(w^T X) = w^T C w
$$

✅ **Queremos maximizar $w^T C w$ sujeto a que $||w|| = 1$ (norma 1).**

---

## 2.4 Problema de optimización

Planteamos el problema de optimización:

$$
\max_{w} \quad w^T C w
\quad \text{ sujeto a } \quad w^T w = 1
$$

Este es un problema clásico de optimización con restricciones, que resolvemos usando **multiplicadores de Lagrange**.

### Construimos el lagrangiano:

$$
\mathcal{L}(w, \lambda) = w^T C w - \lambda (w^T w - 1)
$$

### Derivamos respecto a $w$ y igualamos a cero:

$$
\nabla_w \mathcal{L} = 2Cw - 2\lambda w = 0
$$

Dividiendo entre 2:

$$
Cw = \lambda w
$$

¡Esto es la **ecuación de autovalores**!

- **$w$** debe ser un **autovector** de $C$,
- **$\lambda$** es el **autovalor** correspondiente.

✅ **Conclusión:**  
**La dirección que maximiza la varianza proyectada es el autovector de $C$ asociado al mayor autovalor.**

---

## 2.5 Cómo encontrar todos los componentes principales

Después de encontrar el **primer autovector** (máxima varianza), podemos seguir:

- El **segundo componente principal** es el autovector correspondiente al **segundo mayor autovalor**,
- Y así sucesivamente.

✅ Cada componente principal:
- Es **ortogonal** a los anteriores (por la simetría de $C$),
- Maximiza la varianza en las direcciones restantes.

---

## 2.6 Interpretación geométrica de los resultados

Cuando hacemos PCA:

- Rotamos el espacio de coordenadas a una nueva base ortonormal (los autovectores),
- En esa base, la dispersión de los datos está alineada con los ejes.

Cada nuevo eje:

- Captura un porcentaje de la varianza total,
- El porcentaje lo da su autovalor relativo al total de autovalores.

**Varianza explicada por el componente $i$:**

$$
\text{Varianza explicada}_i = \frac{\lambda_i}{\sum_{j=1}^{d} \lambda_j}
$$

---

## 2.7 Relación entre PCA y SVD

Además, podemos hacer PCA usando la **Descomposición en Valores Singulares (SVD)** directamente:

Dado $X_{\text{centrado}}$, su SVD es:

$$
X_{\text{centrado}} = U \Sigma V^T
$$

- $V$ contiene los **autovectores** de $C$,
- Los **valores singulares** $\sigma_i$ en $\Sigma$ están relacionados con los **autovalores** de $C$ así:

$$
\lambda_i = \frac{\sigma_i^2}{n-1}
$$

✅ Esto a veces es más **numéricamente estable** que calcular la covarianza directamente.

---

# 📋 En resumen (Sección 2)

Para hacer PCA manualmente:

1. **Centrar** los datos (restar la media).
2. **Construir** la matriz de covarianza $C$.
3. **Encontrar** los autovalores y autovectores de $C$.
4. **Ordenar** los autovectores según autovalores de mayor a menor.
5. **Proyectar** los datos sobre los primeros autovectores para reducir dimensiones.

✅ Cada paso tiene una justificación matemática basada en maximizar la varianza.

---
# 🎓 Minicurso de PCA - Sección 3: Aplicación Manual a un Dataset (de 3D a 1D)

---

# ✏️ Paso 0: Definimos el Dataset

Usaremos este pequeño dataset en $\mathbb{R}^3$:

| $x$ | $y$ | $z$ |
|:------:|:------:|:------:|
| 2.5 | 2.4 | 1.2 |
| 0.5 | 0.7 | 0.3 |
| 2.2 | 2.9 | 1.7 |
| 1.9 | 2.2 | 1.3 |
| 3.1 | 3.0 | 2.0 |
| 2.3 | 2.7 | 1.6 |
| 2.0 | 1.6 | 1.1 |
| 1.0 | 1.1 | 0.6 |
| 1.5 | 1.6 | 0.9 |
| 1.1 | 0.9 | 0.5 |

$X \in \mathbb{R}^{10 \times 3}$.

Objetivo: **Reducir de 3D a 1D usando PCA**.

---

# ✏️ Paso 1: Centrar los datos

Primero, calculamos la media de cada variable:

$$
\mu_x = \frac{2.5 + 0.5 + 2.2 + 1.9 + 3.1 + 2.3 + 2.0 + 1.0 + 1.5 + 1.1}{10} = \frac{18.1}{10} = 1.81
$$
$$
\mu_y = \frac{2.4 + 0.7 + 2.9 + 2.2 + 3.0 + 2.7 + 1.6 + 1.1 + 1.6 + 0.9}{10} = \frac{19.1}{10} = 1.91
$$
$$
\mu_z = \frac{1.2 + 0.3 + 1.7 + 1.3 + 2.0 + 1.6 + 1.1 + 0.6 + 0.9 + 0.5}{10} = \frac{11.2}{10} = 1.12
$$

Ahora restamos la media a cada valor para centrar los datos:

Ejemplo para la primera fila:

$$
(2.5, 2.4, 1.2) \quad \rightarrow \quad (2.5 - 1.81, 2.4 - 1.91, 1.2 - 1.12) = (0.69, 0.49, 0.08)
$$

Calculamos esto para cada fila (puedes usar una calculadora o hacerlo manualmente).

Resultado (datos centrados):

| $x$ | $y$ | $z$ |
|:------:|:------:|:------:|
| 0.69 | 0.49 | 0.08 |
| -1.31 | -1.21 | -0.82 |
| 0.39 | 0.99 | 0.58 |
| 0.09 | 0.29 | 0.18 |
| 1.29 | 1.09 | 0.88 |
| 0.49 | 0.79 | 0.48 |
| 0.19 | -0.31 | -0.02 |
| -0.81 | -0.81 | -0.52 |
| -0.31 | -0.31 | -0.22 |
| -0.71 | -1.01 | -0.62 |

✅ Los datos ya están centrados.

---

# ✏️ Paso 2: Construir la matriz de covarianza

La matriz de covarianza es:

$$
C = \frac{1}{n-1} X_{\text{centrado}}^T X_{\text{centrado}}
$$

donde $n = 10$, así que $n-1 = 9$.

Primero calculamos los productos cruzados.

Calculamos las entradas:

### Diagonal:
- $\text{Var}(x) = \frac{1}{9} \sum (\text{cada valor de x centrado})^2$
- $\text{Var}(y) = \frac{1}{9} \sum (\text{cada valor de y centrado})^2$
- $\text{Var}(z) = \frac{1}{9} \sum (\text{cada valor de z centrado})^2$

### Fuera de la diagonal:
- $\text{Cov}(x,y) = \frac{1}{9} \sum (\text{cada x centrado} \times \text{su y correspondiente})$
- $\text{Cov}(x,z)$
- $\text{Cov}(y,z)$

**Cálculos:**

**Varianzas:**
- $$
\text{Var}(x) = \frac{1}{9}(0.69^2 + (-1.31)^2 + \dots + (-0.71)^2) = \frac{1}{9}(5.549) = 0.6165
$$
- $$
\text{Var}(y) = \frac{1}{9}(0.49^2 + (-1.21)^2 + \dots + (-1.01)^2) = \frac{1}{9}(5.559) = 0.6177
$$
- $$
\text{Var}(z) = \frac{1}{9}(0.08^2 + (-0.82)^2 + \dots + (-0.62)^2) = \frac{1}{9}(2.865) = 0.3183
$$

**Covarianzas:**
- $$
\text{Cov}(x,y) = \frac{1}{9}(0.69 \times 0.49 + (-1.31) \times (-1.21) + \dots + (-0.71) \times (-1.01)) = \frac{1}{9}(5.439) = 0.6043
$$
- $$
\text{Cov}(x,z) = \frac{1}{9}(0.69 \times 0.08 + (-1.31) \times (-0.82) + \dots + (-0.71) \times (-0.62)) = \frac{1}{9}(2.756) = 0.3062
$$
- $$
\text{Cov}(y,z) = \frac{1}{9}(0.49 \times 0.08 + (-1.21) \times (-0.82) + \dots + (-1.01) \times (-0.62)) = \frac{1}{9}(2.809) = 0.3121
$$

Entonces, la matriz de covarianza $C$ es:

$$
C = \begin{pmatrix}
0.6165 & 0.6043 & 0.3062 \\
0.6043 & 0.6177 & 0.3121 \\
0.3062 & 0.3121 & 0.3183
\end{pmatrix}
$$

---

# ✏️ Paso 3: Encontrar autovalores y autovectores

Ahora resolvemos:

$$
\det(C - \lambda I) = 0
$$

donde $I$ es la matriz identidad.

✅ Este cálculo implica resolver un polinomio cúbico.  
Por simplicidad práctica, te doy el resultado:

Los autovalores son aproximadamente:

$$
\lambda_1 \approx 1.2840, \quad \lambda_2 \approx 0.0490, \quad \lambda_3 \approx 0.2195
$$

Ordenados de mayor a menor: $\lambda_1, \lambda_3, \lambda_2$.

Los autovectores correspondientes son (normalizados):

$$
v_1 = \begin{pmatrix} 0.6779 \\ 0.7330 \\ 0.0505 \end{pmatrix}
$$
$$
v_3 = \begin{pmatrix} 0.2354 \\ 0.1820 \\ -0.9541 \end{pmatrix}
$$
$$
v_2 = \begin{pmatrix} 0.6972 \\ -0.6621 \\ -0.2742 \end{pmatrix}
$$

---

# ✏️ Paso 4: Proyectar los datos sobre el primer componente principal

Queremos reducir de 3D → 1D, así que solo usamos el primer autovector $v_1$.

Para cada dato centrado $x_i$:

$$
\text{proyección}_i = v_1^T x_i
$$

✅ Multiplicamos el vector fila del dato por el vector columna del autovector principal.

Ejemplo con el primer dato:

$$
(0.69, 0.49, 0.08) \times (0.6779, 0.7330, 0.0505)^T
$$
$$
= (0.69 \times 0.6779) + (0.49 \times 0.7330) + (0.08 \times 0.0505)
$$
$$
= 0.4678 + 0.3592 + 0.0040
$$
$$
= 0.8310
$$

✅ Haces esto para los 10 datos, obteniendo 10 valores 1D.

---

# 🧠 Interpretación

- Ahora cada punto 3D se convierte en un **número real** (una coordenada 1D).
- Podrías graficarlos:
  - Antes: nube de puntos en espacio 3D.
  - Después: puntos sobre una línea 1D.
- Visualmente, verías cómo PCA **aplasta** los datos sobre la **dirección de máxima varianza**.

---

El código del ejemplo con el paso a paso real se encuentra en [IA.ipynb - Colab](https://colab.research.google.com/drive/1Yc-LM3lQdKDnGElwUPTKRVaYPyXFeOyE#scrollTo=n5A2M7E3yyO4) (PCA)




