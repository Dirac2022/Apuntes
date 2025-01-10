

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
\[
\text{Cov}(X, Y) = \frac{1}{n} \sum_{i=1}^n \left( X_i - \mu_X \right) \left( Y_i - \mu_Y \right),
\]  
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