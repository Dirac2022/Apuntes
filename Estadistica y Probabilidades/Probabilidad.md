

# Esperanza matemática

$$
E(x) = \sum_{x \ \in \ \mathbb{R}_x} xp(x)
$$



## Teorema

$$
E[H(x)] = \sum_{x \ \in \ \mathbb{R}_x} H(x)p(x)
$$
## Teorema
Si $x$ es una variable aleatoria y $a$, $b$ constantes, entonces
- $E(a) = a$
- $E[aH(x) + bG(x)] = aE[H(x)] + bE[G(x)]$


# Varianza

$$
Var(x) = \sigma^2 = E[(x-\mu)^2] = \sum_{x \ \in \ \mathbb{R}_x} (x-u)^2p(x)
$$


# Independencia

$$
P({X=x} \ \cap {Y=y}) = P({X=x}) \cdot P({Y=y})
$$


## Observacion
Para vectores aleatorios, si $X$ y $Y$ son independientes, entonces

$$
E[XY] = E(X)E(Y)
$$


### Clase: Covarianza, Correlación Bidimensional y Coeficiente de Pearson

#### **1. Covarianza**
La **covarianza** mide la relación lineal entre dos variables aleatorias $X$ e $Y$. Nos dice cómo cambian juntas las dos variables:  
- **Positiva**: Si $X$ aumenta y $Y$ también aumenta.  
- **Negativa**: Si $X$ aumenta y $Y$ disminuye.  
- **Cero**: Si no hay una relación lineal clara entre $X$ e $Y$.  

**Fórmula de la covarianza:**
$$
\text{Cov}(X, Y) = \frac{1}{n} \sum_{i=1}^n \left( X_i - \mu_X \right) \left( Y_i - \mu_Y \right),
$$  
donde:  
- $X_i, Y_i$: Valores individuales de las variables $X$ e $Y$.  
- $\mu_X, \mu_Y$: Medias de las variables $X$ e $Y$.  
- $n$: Número total de observaciones.

#### **Propiedades de la covarianza:**
1. Si $\text{Cov}(X, Y) > 0$, $X$ e $Y$ tienden a moverse en la misma dirección.  
2. Si $\text{Cov}(X, Y) < 0$, $X$ e $Y$ tienden a moverse en direcciones opuestas.  
3. Si $\text{Cov}(X, Y) = 0$, no hay una relación lineal entre $X$ e $Y$.  

**Limitación de la covarianza:**  
La magnitud de la covarianza depende de las unidades de medida de $X$ e $Y$, lo que dificulta la comparación entre diferentes relaciones.

---

#### **2. Correlación Bidimensional**
La **correlación** es una medida adimensional que cuantifica la intensidad y dirección de la relación lineal entre dos variables. Normaliza la covarianza dividiéndola entre los productos de las desviaciones estándar de $X$ e $Y$.  

**Fórmula de la correlación (Coeficiente de Pearson):**
\[
\rho(X, Y) = \frac{\text{Cov}(X, Y)}{\sigma_X \sigma_Y},
\]  
donde:  
- $\text{Cov}(X, Y)$: Covarianza entre $X$ e $Y$.  
- $\sigma_X, \sigma_Y$: Desviaciones estándar de $X$ e $Y$.  

El coeficiente de correlación $\rho$ toma valores en el intervalo \([-1, 1]\):  
- **\(+1\)**: Correlación lineal positiva perfecta.  
- **\(-1\)**: Correlación lineal negativa perfecta.  
- **\(0\)**: No hay correlación lineal.  

#### **Ventajas sobre la covarianza:**
1. Es una medida normalizada, lo que facilita comparaciones.  
2. Es más interpretativa: indica tanto la fuerza como la dirección de la relación.

---

#### **3. Coeficiente de Pearson**
El **coeficiente de Pearson** es una medida específica de correlación bidimensional que asume que la relación entre las variables es lineal. Es una de las formas más comunes de calcular la correlación.  

**Pasos para calcular $r$ (Coeficiente de Pearson):**
1. **Obtener las medias:** Calcula $\mu_X$ y $\mu_Y$.  
2. **Calcular desviaciones:** Restar las medias de cada valor:  
  $$
   x_i' = X_i - \mu_X, \quad y_i' = Y_i - \mu_Y.
  $$
3. **Multiplicar y promediar:**  
  $$
   \text{Cov}(X, Y) = \frac{1}{n} \sum_{i=1}^n x_i' y_i'.
  $$
4. **Dividir por las desviaciones estándar:**  
  $$
   r = \frac{\text{Cov}(X, Y)}{\sigma_X \sigma_Y}.
  $$

#### **Interpretación del coeficiente de Pearson ($r$):**
1. **Cercano a +1**: Relación lineal positiva fuerte.  
2. **Cercano a -1**: Relación lineal negativa fuerte.  
3. **Cercano a 0**: Relación lineal débil o inexistente.

---

### Ejemplo Práctico

Supongamos que tenemos dos variables:  
- $X$: Horas de estudio.  
- $Y$: Calificación en un examen.

| $X$ | $Y$ |
|--------|--------|
| 2      | 50     |
| 3      | 60     |
| 5      | 80     |
| 7      | 100    |

1. **Calcular las medias:**  
  $$
   \mu_X = \frac{2+3+5+7}{4} = 4.25, \quad \mu_Y = \frac{50+60+80+100}{4} = 72.5.
  $$
2. **Calcular las desviaciones estándar $\sigma_X$ y $\sigma_Y$.**  
3. **Usar las fórmulas de covarianza y correlación:**  
   - Covarianza: $\text{Cov}(X, Y)$.  
   - Coeficiente de Pearson: $r$.

---

### Conclusión
- La **covarianza** indica cómo se relacionan dos variables en términos de dirección, pero no es normalizada.  
- La **correlación bidimensional** (como el coeficiente de Pearson) nos da una medida estandarizada que es más fácil de interpretar y comparar.
# Resolución: Covarianza, Correlación y Coeficiente de Pearson

## Datos iniciales
| X (Horas) | Y (Calificaciones) |
|-----------|-------------------|
| 2 | 50 |
| 3 | 60 |
| 5 | 80 |
| 7 | 100 |

## Paso 1: Calcular las medias

$$\mu_X = \frac{2 + 3 + 5 + 7}{4} = \frac{17}{4} = 4.25$$

$$\mu_Y = \frac{50 + 60 + 80 + 100}{4} = \frac{290}{4} = 72.5$$

## Paso 2: Calcular desviaciones respecto a la media
Calculamos $X_{dev} = X_i - \mu_X$ y $Y_{dev} = Y_i - \mu_Y$

| X | μX | X_dev | Y | μY | Y_dev |
|---|-------|--------|---|-------|--------|
| 2 | 4.25 | -2.25 | 50 | 72.5 | -22.5 |
| 3 | 4.25 | -1.25 | 60 | 72.5 | -12.5 |
| 5 | 4.25 | 0.75 | 80 | 72.5 | 7.5 |
| 7 | 4.25 | 2.75 | 100 | 72.5 | 27.5 |

## Paso 3: Calcular la covarianza
| X_dev | Y_dev | Producto |
|-------|--------|----------|
| -2.25 | -22.5 | 50.625 |
| -1.25 | -12.5 | 15.625 |
| 0.75 | 7.5 | 5.625 |
| 2.75 | 27.5 | 75.625 |

$$\sum X_{dev} \cdot Y_{dev} = 50.625 + 15.625 + 5.625 + 75.625 = 147.5$$

$$Cov(X, Y) = \frac{147.5}{4} = 36.875$$

## Paso 4: Calcular desviaciones estándar
Para $\sigma_X$:

$$\sigma_X^2 = \frac{1}{4} [(-2.25)^2 + (-1.25)^2 + (0.75)^2 + (2.75)^2]$$
$$\sigma_X^2 = \frac{1}{4}[5.0625 + 1.5625 + 0.5625 + 7.5625] = \frac{14.75}{4} = 3.6875$$
$$\sigma_X = \sqrt{3.6875} \approx 1.92$$

Para $\sigma_Y$:

$$\sigma_Y^2 = \frac{1}{4}[(-22.5)^2 + (-12.5)^2 + (7.5)^2 + (27.5)^2]$$
$$\sigma_Y^2 = \frac{1}{4}[506.25 + 156.25 + 56.25 + 756.25] = \frac{1475}{4} = 368.75$$
$$\sigma_Y = \sqrt{368.75} \approx 19.2$$

## Paso 5: Calcular el coeficiente de Pearson

$$r = \frac{Cov(X, Y)}{\sigma_X \cdot \sigma_Y} = \frac{36.875}{1.92 \cdot 19.2} = \frac{36.875}{36.864} \approx 1.0$$

## Resultados Finales:
1. Covarianza: $Cov(X, Y) = 36.875$
2. Desviaciones estándar:
   - $\sigma_X \approx 1.92$
   - $\sigma_Y \approx 19.2$
3. Coeficiente de Pearson: $r \approx 1.0$

Esto indica una relación lineal positiva perfecta entre horas de estudio y calificaciones.


---
# Análisis de Correlación y Covarianza

La covarianza y el coeficiente de correlación de Pearson son medidas estadísticas que evalúan la relación entre variables. La correlación momento-producto de Pearson es exactamente el mismo concepto que el coeficiente de correlación de Pearson - son nombres diferentes para la misma medida.

## Formulación Matemática

### Covarianza
La covarianza mide la variación conjunta de dos variables respecto a sus medias:

$$\text{Cov}(X,Y) = \frac{\sum_{i=1}^{n} (x_i - \bar{x})(y_i - \bar{y})}{n-1}$$

### Coeficiente de Correlación de Pearson
El coeficiente de correlación de Pearson (también llamado correlación momento-producto) normaliza la covarianza usando las desviaciones estándar:

$$r = \frac{\text{Cov}(X,Y)}{\sigma_X \sigma_Y} = \frac{\sum_{i=1}^{n} (x_i - \bar{x})(y_i - \bar{y})}{\sqrt{\sum_{i=1}^{n} (x_i - \bar{x})^2}\sqrt{\sum_{i=1}^{n} (y_i - \bar{y})^2}}$$

## Comparación de Medidas

| Característica | Covarianza | Correlación de Pearson |
|----------------|------------|----------------------|
| Rango de valores | (-∞, +∞) | [-1, +1] |
| Unidades | Unidades de X × Unidades de Y | Adimensional |
| Interpretación | Dirección de la relación | Dirección y fuerza de la relación |
| Sensibilidad a escala | Cambia con la escala | Invariante a la escala |

## Implementación en Python

```python
import numpy as np

def calcular_covarianza_correlacion(x, y):
    # Covarianza
    covarianza = np.cov(x, y)[0,1]
    
    # Correlación de Pearson
    correlacion = np.corrcoef(x, y)[0,1]
    
    return covarianza, correlacion

# Ejemplo
x = [1, 2, 3, 4, 5]
y = [2, 4, 5, 4, 5]

cov, corr = calcular_covarianza_correlacion(x, y)
print(f"Covarianza: {cov:.4f}")
print(f"Correlación: {corr:.4f}")
```

## Interpretación de Resultados

| Valor de Correlación | Interpretación |
|---------------------|----------------|
| r = 1 | Correlación positiva perfecta |
| 0.7 ≤ r < 1 | Correlación positiva fuerte |
| 0.3 ≤ r < 0.7 | Correlación positiva moderada |
| 0 < r < 0.3 | Correlación positiva débil |
| r = 0 | No hay correlación lineal |
| -0.3 < r < 0 | Correlación negativa débil |
| -0.7 < r ≤ -0.3 | Correlación negativa moderada |
| -1 < r ≤ -0.7 | Correlación negativa fuerte |
| r = -1 | Correlación negativa perfecta |



---
# Fórmula Detallada del Coeficiente de Correlación de Pearson

La fórmula expandida del coeficiente de correlación de Pearson usando covarianza y desviaciones estándar es:

$$r = \frac{\text{Cov}(X,Y)}{\sigma_X \sigma_Y} = \frac{\frac{1}{n-1}\sum_{i=1}^{n} (x_i - \bar{x})(y_i - \bar{y})}{\sqrt{\frac{1}{n-1}\sum_{i=1}^{n} (x_i - \bar{x})^2} \sqrt{\frac{1}{n-1}\sum_{i=1}^{n} (y_i - \bar{y})^2}}$$

Expandiendo más detalladamente y sustituyendo las medias:

$$r = \frac{\frac{1}{n-1}\sum_{i=1}^{n} \left(x_i - \frac{1}{n}\sum_{j=1}^{n}x_j\right)\left(y_i - \frac{1}{n}\sum_{j=1}^{n}y_j\right)}{\sqrt{\frac{1}{n-1}\sum_{i=1}^{n} \left(x_i - \frac{1}{n}\sum_{j=1}^{n}x_j\right)^2} \sqrt{\frac{1}{n-1}\sum_{i=1}^{n} \left(y_i - \frac{1}{n}\sum_{j=1}^{n}y_j\right)^2}}$$

Donde:
- r es el coeficiente de correlación de Pearson
- n es el número de observaciones
- $x_i$, $y_i$ son los valores individuales de cada variable
- $\bar{x}, \bar{y}$ son las medias de cada variable
- El numerador es la covarianza muestral
- Los términos bajo la raíz cuadrada son las varianzas muestrales de $X$ e $Y$

Esta forma expandida muestra todos los componentes del cálculo en una sola expresión matemática.



# Pregunta 4

## 1. Datos Corregidos
- t (edad): [40, 72, 35, 47, 21, 61] años
- p (presión): [105, 145, 100, 130, 95, 132] mmHg

## 2. Fórmula a Utilizar

$$r = \frac{\sum_{i=1}^{n} (t_i - \bar{t})(p_i - \bar{p})}{\sqrt{\sum_{i=1}^{n} (t_i - \bar{t})^2 \sum_{i=1}^{n} (p_i - \bar{p})^2}}$$

## 3. Cálculos Intermedios

### 3.1 Medias
$$\begin{align}
\bar{t} &= \frac{40 + 72 + 35 + 47 + 21 + 61}{6} = 46\\
\bar{p} &= \frac{105 + 145 + 100 + 130 + 95 + 132}{6} = 117.833
\end{align}$$

### 3.2 Tabla de Desviaciones

| i   | ti  | pi  | ti - t̄ | pi - p̄ | (ti - t̄)(pi - p̄) | (ti - t̄)² | (pi - p̄)² |
| --- | --- | --- | ------- | ------- | ------------------ | ---------- | ---------- |
| 1   | 40  | 105 | -6      | -12.833 | 76.998             | 36         | 164.686    |
| 2   | 72  | 145 | 26      | 27.167  | 706.342            | 676        | 738.048    |
| 3   | 35  | 100 | -11     | -17.833 | 196.163            | 121        | 318.016    |
| 4   | 47  | 130 | 1       | 12.167  | 12.167             | 1          | 148.037    |
| 5   | 21  | 95  | -25     | -22.833 | 570.825            | 625        | 521.346    |
| 6   | 61  | 132 | 15      | 14.167  | 212.505            | 225        | 200.704    |

### 3.3 Sumas
- $\sum(t_i - \bar{t})(p_i - \bar{p}) = 1775$
- $\sum(t_i - \bar{t})^2 = 1684$
- $\sum(p_i - \bar{p})^2 = 2090.837$

## 4. Cálculo Final

$$r = \frac{1775}{\sqrt{1684 \times 2090.837}} = 0.9459$$

## 5. Verificación con Python

```python
import numpy as np

t = np.array([40, 72, 35, 47, 21, 61])
p = np.array([105, 145, 100, 130, 95, 132])

r = np.corrcoef(t, p)[0,1]
print(f"Coeficiente de correlación: {r:.4f}")
```

## Interpretación
- r = 0.9459 indica una correlación positiva muy fuerte
- El signo positivo indica que cuando la edad aumenta, la presión tiende a aumentar
- El valor 0.9459 está muy cercano a 1, lo que sugiere una relación lineal muy fuerte
- El coeficiente de determinación r² = 0.8947 indica que el 89.47% de la variabilidad en la presión puede explicarse por la edad

¿Te gustaría que profundicemos en algún cálculo específico o en la interpretación?


## 1. Organización de Datos

Primero organizamos los datos en dos variables:
- t (edad): [40, 72, 35, 47, 21, 61] años
- p (presión): [105, 145, 100, 130, 95, 102] mmHg

## 2. Fórmula a Utilizar

$$r = \frac{\sum_{i=1}^{n} (t_i - \bar{t})(p_i - \bar{p})}{\sqrt{\sum_{i=1}^{n} (t_i - \bar{t})^2 \sum_{i=1}^{n} (p_i - \bar{p})^2}}$$

## 3. Cálculos Intermedios

### 3.1 Medias
$$\begin{align}
\bar{t} &= \frac{40 + 72 + 35 + 47 + 21 + 61}{6} = 46\\
\bar{p} &= \frac{105 + 145 + 100 + 130 + 95 + 102}{6} = 112.833
\end{align}$$

### 3.2 Desviaciones
| Observación | ti - t̄ | pi - p̄ | (ti - t̄)(pi - p̄) | (ti - t̄)² | (pi - p̄)² |
| ----------- | ------- | ------- | ------------------ | ---------- | ---------- |
| 1           | -6      | -7.833  | 47.000             | 36         | 61.360     |
| 2           | 26      | 32.167  | 836.333            | 676        | 1034.694   |
| 3           | -11     | -12.833 | 141.167            | 121        | 164.694    |
| 4           | 1       | 17.167  | 17.167             | 1          | 294.694    |
| 5           | -25     | -17.833 | 445.833            | 625        | 318.027    |
| 6           | 15      | -10.833 | -162.500           | 225        | 117.360    |

### 3.3 Sumas
- $\sum(t_i - \bar{t})(p_i - \bar{p}) = 1325$
- $\sum(t_i - \bar{t})^2 = 1684$
- $\sum(p_i - \bar{p})^2 = 1990.829$

## 4. Cálculo Final

$$r = \frac{1325}{\sqrt{1684 \times 1990.829}} = 0.7236$$

## 5. Verificación

Por si quieres verificar los cálculos, usemos Python:

```python
import numpy as np

t = np.array([40, 72, 35, 47, 21, 61])
p = np.array([105, 145, 100, 130, 95, 102])

r = np.corrcoef(t, p)[0,1]
print(f"Coeficiente de correlación: {r:.4f}")
```

## Interpretación del Resultado
- r = 0.7236 indica una correlación positiva fuerte
- El signo positivo indica que cuando la edad aumenta, la presión tiende a aumentar
- El valor 0.7236 está cercano a 1, lo que sugiere una relación lineal relativamente fuerte

¿Te gustaría que profundicemos en la interpretación o en algún paso específico del cálculo?



### (i) Coeficiente de correlación
El coeficiente de correlación es r = 0.9459

### (ii) Interpretación
Este valor indica una correlación positiva muy fuerte entre la edad y la presión sanguínea sistólica. Esto significa que:
- Existe una relación lineal muy fuerte donde la presión sanguínea aumenta con la edad
- Aproximadamente el 89.47% (r² = 0.9459² = 0.8947) de la variabilidad en la presión puede explicarse por la edad

## (b) Ecuación de Regresión

La ecuación de regresión lineal es:
$$p = 1.0540t + 69.3476$$

Donde:
- a = 69.3476 (intercepto)
- b = 1.0540 (pendiente)

## (c) Predicción para paciente de 50 años

Sustituyendo t = 50 en la ecuación:
`$$p = 1.0540(50) + 69.3476 = 122.05$$`

La presión sanguínea sistólica estimada para un paciente de 50 años sería aproximadamente 122 mmHg.

## (d) Explicación sobre paciente de 16 años

No se debería utilizar la ecuación de regresión para predecir la presión de un paciente de 16 años por las siguientes razones:

| Razón | Explicación |
|-------|-------------|
| Extrapolación | 16 años está fuera del rango de edades de la muestra (21-72 años) |
| Validez del modelo | El modelo se construyó con datos de adultos, no de adolescentes |
| Factores fisiológicos | La relación edad-presión puede ser diferente en adolescentes |
| Confiabilidad | Las predicciones fuera del rango de datos son menos confiables |

Observaciones sobre los cambios:
1. El coeficiente de correlación aumentó significativamente (de 0.7236 a 0.9459)
2. La pendiente de la recta aumentó (de 0.7868 a 1.0540)
3. El intercepto disminuyó (de 76.6397 a 69.3476)
4. La predicción para 50 años aumentó (de 116 a 122 mmHg)

Estos cambios muestran una relación más fuerte entre edad y presión sanguínea con el valor corregido.

¿Te gustaría que profundicemos en algún aspecto específico del análisis?


# Resolución Corregida de Problema de Correlación y Regresión Lineal

Vamos a recalcular todo con el valor correcto p = 132 mmHg para el último paciente.

## (a) Cálculo del Coeficiente de Correlación de Pearson



### (i) Coeficiente de correlación
El coeficiente de correlación es r = 0.9459

### (ii) Interpretación
Este valor indica una correlación positiva muy fuerte entre la edad y la presión sanguínea sistólica. Esto significa que:
- Existe una relación lineal muy fuerte donde la presión sanguínea aumenta con la edad
- Aproximadamente el 89.47% (r² = 0.9459² = 0.8947) de la variabilidad en la presión puede explicarse por la edad

## (b) Ecuación de Regresión

La ecuación de regresión lineal es:
`$$p = 1.0540t + 69.3476$$`

Donde:
- a = 69.3476 (intercepto)
- b = 1.0540 (pendiente)

## (c) Predicción para paciente de 50 años

Sustituyendo t = 50 en la ecuación:
`$$p = 1.0540(50) + 69.3476 = 122.05$$`

La presión sanguínea sistólica estimada para un paciente de 50 años sería aproximadamente 122 mmHg.

## (d) Explicación sobre paciente de 16 años

No se debería utilizar la ecuación de regresión para predecir la presión de un paciente de 16 años por las siguientes razones:

| Razón | Explicación |
|-------|-------------|
| Extrapolación | 16 años está fuera del rango de edades de la muestra (21-72 años) |
| Validez del modelo | El modelo se construyó con datos de adultos, no de adolescentes |
| Factores fisiológicos | La relación edad-presión puede ser diferente en adolescentes |
| Confiabilidad | Las predicciones fuera del rango de datos son menos confiables |

Observaciones sobre los cambios:
1. El coeficiente de correlación aumentó significativamente (de 0.7236 a 0.9459)
2. La pendiente de la recta aumentó (de 0.7868 a 1.0540)
3. El intercepto disminuyó (de 76.6397 a 69.3476)
4. La predicción para 50 años aumentó (de 116 a 122 mmHg)

Estos cambios muestran una relación más fuerte entre edad y presión sanguínea con el valor corregido.

¿Te gustaría que profundicemos en algún aspecto específico del análisis?


# Cálculo de los Coeficientes de la Recta de Regresión

Para encontrar los valores de a y b en la ecuación p = at + b, usamos las fórmulas de regresión lineal simple:

## Fórmulas

### Para la pendiente (a):
$$a = \frac{\sum_{i=1}^{n} (t_i - \bar{t})(p_i - \bar{p})}{\sum_{i=1}^{n} (t_i - \bar{t})^2}$$

### Para el intercepto (b):
$$b = \bar{p} - a\bar{t}$$

## Proceso Paso a Paso

### 1. Datos y Medias
Usando los valores que ya calculamos anteriormente:
- $\bar{t} = 46$ (media de edades)
- $\bar{p} = 117.833$ (media de presiones)

### 2. Cálculo de la pendiente (a)

Usando la tabla anterior:

| i | ti | pi | ti - t̄ | pi - p̄ | (ti - t̄)(pi - p̄) | (ti - t̄)² |
|---|-----|-----|---------|---------|-------------------|------------|
| 1 | 40 | 105 | -6 | -12.833 | 76.998 | 36 |
| 2 | 72 | 145 | 26 | 27.167 | 706.342 | 676 |
| 3 | 35 | 100 | -11 | -17.833 | 196.163 | 121 |
| 4 | 47 | 130 | 1 | 12.167 | 12.167 | 1 |
| 5 | 21 | 95 | -25 | -22.833 | 570.825 | 625 |
| 6 | 61 | 132 | 15 | 14.167 | 212.505 | 225 |

$$a = \frac{1775}{1684} = 1.0540$$

### 3. Cálculo del intercepto (b)

Sustituyendo en la fórmula:
$$\begin{align}
b &= \bar{p} - a\bar{t} \\
b &= 117.833 - 1.0540(46) \\
b &= 117.833 - 48.484 \\
b &= 69.3476
\end{align}$$

### 4. Ecuación final

Por lo tanto, la ecuación de regresión es:
$$p = 1.0540t + 69.3476$$

### Interpretación de los coeficientes:
- b = 1.0540: Por cada año que aumenta la edad, la presión sistólica aumenta en promedio 1.0540 mmHg
- a = 69.3476: Es el valor teórico de la presión cuando t = 0 (aunque no tiene interpretación práctica en este contexto)

¿Te gustaría que profundicemos en algún aspecto específico de estos cálculos?