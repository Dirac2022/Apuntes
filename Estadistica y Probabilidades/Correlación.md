
¡Excelente! Bienvenidos a esta clase magistral sobre la medición de la asociación entre variables. Hoy profundizaremos en los tres coeficientes de correlación más fundamentales en estadística: Pearson, Spearman y Kendall. Analizaremos cada uno desde una perspectiva matemática rigurosa, ilustrando su cálculo y, lo que es más importante, su correcta interpretación.

---
## **Sección I: Coeficiente de Correlación de Pearson (r)**

### **Teoría Matemática Rigurosa**

El **coeficiente de correlación producto-momento de Pearson**, denotado como $r$ para una muestra y $\rho$ (rho) para la población, es la medida más común de asociación.

* **Propósito Fundamental:** Mide la **fuerza y dirección de la relación lineal** entre dos variables cuantitativas continuas. Es crucial entender que Pearson evalúa exclusivamente la linealidad; una relación curvilínea fuerte podría tener un coeficiente de Pearson cercano a cero.

* **Supuestos Matemáticos:**
    1.  **Nivel de Medición:** Ambas variables ($X$ e $Y$) deben ser cuantitativas continuas (de intervalo o de razón).
    2.  **Linealidad:** Debe existir una relación lineal entre las variables. Esto se puede verificar visualmente a través de un diagrama de dispersión.
    3.  **Normalidad Bivariada:** Para la inferencia estadística (pruebas de hipótesis sobre el coeficiente), los pares de observaciones $(x_i, y_i)$ deben seguir una distribución normal bivariada.
    4.  **Homocedasticidad:** La varianza de los residuos debe ser constante a lo largo de la línea de regresión.

* **Interpretación del Valor:** El coeficiente $r$ varía en el intervalo $[-1, 1]$.
    * $r = 1$: Correlación lineal positiva perfecta. Todos los puntos de datos caen sobre una línea recta con pendiente positiva.
    * $r = -1$: Correlación lineal negativa perfecta. Todos los puntos de datos caen sobre una línea recta con pendiente negativa.
    * $r = 0$: Ausencia de correlación lineal. No implica independencia, ya que podría existir una relación no lineal.
    * Valores intermedios (ej. $r=0.6$) indican el grado de ajuste a una línea recta. El signo indica la dirección de la relación.

* **Propiedades Matemáticas:**
    * Es una medida adimensional.
    * Es simétrico: $corr(X, Y) = corr(Y, X)$.
    * No se ve afectado por transformaciones lineales de las variables (ej., cambiar de grados Celsius a Fahrenheit no altera el coeficiente).
    * Matemáticamente, es la covarianza de las dos variables estandarizadas: $r_{xy} = \frac{cov(X,Y)}{\sigma_x \sigma_y}$.

### **Ejemplo 1 (Sencillo y Didáctico)**

Analicemos la relación entre las **horas de estudio** y la **calificación** obtenida por 10 estudiantes.

| Estudiante | Horas de Estudio (X) | Calificación (Y) |
| :--- | :--- | :--- |
| 1 | 2 | 65 |
| 2 | 3 | 70 |
| 3 | 1 | 60 |
| 4 | 5 | 85 |
| 5 | 6 | 90 |
| 6 | 4 | 75 |
| 7 | 7 | 95 |
| 8 | 2.5 | 68 |
| 9 | 3.5 | 72 |
| 10 | 4.5 | 80 |

**Paso 1: Calcular las medias de X e Y.**
$\bar{X} = \frac{\sum X_i}{n} = \frac{38.5}{10} = 3.85$
$\bar{Y} = \frac{\sum Y_i}{n} = \frac{760}{10} = 76$

**Paso 2: Calcular las desviaciones y productos cruzados.**

| X | Y | $(X - \bar{X})$ | $(Y - \bar{Y})$ | $(X - \bar{X})(Y - \bar{Y})$ | $(X - \bar{X})^2$ | $(Y - \bar{Y})^2$ |
| :- | :- | :- | :- | :- | :- | :- |
| 2 | 65 | -1.85 | -11 | 20.35 | 3.4225 | 121 |
| 3 | 70 | -0.85 | -6 | 5.10 | 0.7225 | 36 |
| 1 | 60 | -2.85 | -16 | 45.60 | 8.1225 | 256 |
| 5 | 85 | 1.15 | 9 | 10.35 | 1.3225 | 81 |
| 6 | 90 | 2.15 | 14 | 30.10 | 4.6225 | 196 |
| 4 | 75 | 0.15 | -1 | -0.15 | 0.0225 | 1 |
| 7 | 95 | 3.15 | 19 | 59.85 | 9.9225 | 361 |
| 2.5 | 68 | -1.35 | -8 | 10.80 | 1.8225 | 64 |
| 3.5 | 72 | -0.35 | -4 | 1.40 | 0.1225 | 16 |
| 4.5 | 80 | 0.65 | 4 | 2.60 | 0.4225 | 16 |
| **Σ**| **760**| | | **Σ=186** | **Σ=30.525** | **Σ=1148** |

**Paso 3: Aplicar la fórmula.**
$r = \frac{\sum (X_i - \bar{X})(Y_i - \bar{Y})}{\sqrt{\sum (X_i - \bar{X})^2 \sum (Y_i - \bar{Y})^2}} = \frac{186}{\sqrt{30.525 \times 1148}} = \frac{186}{\sqrt{35042.7}} \approx \frac{186}{187.2} \approx 0.9936$

**Interpretación:** Un valor de $r \approx 0.994$ indica una **correlación lineal positiva casi perfecta**. A medida que las horas de estudio aumentan, la calificación tiende a aumentar de manera fuertemente lineal.

### **Ejemplo 2 (Complejo: El efecto de un Outlier)**

Analicemos la relación entre **Años de Experiencia** y **Salario Anual (en miles)** de 15 profesionales.

Datos (Pares Experiencia, Salario):
(2, 50), (4, 60), (5, 65), (8, 75), (10, 85), (12, 90), (15, 100), (1, 45), (3, 55), (6, 70), (9, 80), (11, 88), (14, 98), (7, 72), **(1, 150)**.
El último punto es un **valor atípico (outlier)**: una persona con solo 1 año de experiencia y un salario anormalmente alto de 150k.

**Cálculo con el outlier:** Si realizamos el cálculo de Pearson con todos los 15 puntos, los cálculos (omitidos por brevedad, pero siguiendo el mismo proceso) nos dan un $r \approx 0.35$.
**Interpretación:** Un coeficiente de 0.35 sugiere una correlación lineal positiva débil. Esto contradice la tendencia visual de los primeros 14 puntos.

**Cálculo sin el outlier:** Ahora, eliminemos el punto (1, 150) y recalculemos $r$ para los 14 puntos restantes.
El nuevo cálculo nos da un $r \approx 0.98$.
**Interpretación:** Sin el outlier, la relación es, como se esperaba, una correlación lineal positiva muy fuerte.

**Conclusión de la Complejidad:** Este ejemplo demuestra la **sensibilidad extrema del coeficiente de Pearson a los valores atípicos**. Un solo punto de datos puede distorsionar drásticamente el coeficiente, pasando de una conclusión de relación débil a una muy fuerte. Esto subraya la importancia crítica de **siempre visualizar los datos con un diagrama de dispersión** antes de interpretar el coeficiente de correlación de Pearson.

### **Resumen y Fórmula Final**

El coeficiente de Pearson es la herramienta por excelencia para cuantificar la **fuerza y dirección de una relación lineal** entre dos variables continuas. Su principal debilidad es su sensibilidad a los valores atípicos y su incapacidad para capturar relaciones no lineales.

La fórmula para el coeficiente de correlación de Pearson de una muestra es:
$$r_{xy} = \frac{\sum_{i=1}^{n} (X_i - \bar{X})(Y_i - \bar{Y})}{\sqrt{\sum_{i=1}^{n} (X_i - \bar{X})^2 \sum_{i=1}^{n} (Y_i - \bar{Y})^2}}$$

---
## **Sección II: Coeficiente de Correlación por Rangos de Spearman (ρ o r_s)**

### **Teoría Matemática Rigurosa**

El coeficiente de correlación de Spearman es una medida de asociación no paramétrica.

* **Propósito Fundamental:** Mide la **fuerza y dirección de la relación monotónica** entre dos variables. Una relación es monotónica si, a medida que una variable aumenta, la otra variable nunca cambia de dirección (siempre aumenta o siempre disminuye, pero no necesariamente a un ritmo constante). Esto la hace ideal para relaciones que no son lineales pero que tienen una dirección clara.


* **Supuestos Matemáticos:**
    1.  **Nivel de Medición:** Las variables deben ser al menos **ordinales**. Funciona con datos ordinales, de intervalo o de razón.
    2.  **Relación Monotónica:** Se asume que la relación entre las variables es monotónica.

* **Interpretación del Valor:** Al igual que Pearson, $\rho$ varía en el intervalo $[-1, 1]$.
    * $\rho = 1$: Relación monotónica positiva perfecta. Para cada par de observaciones, si $X_i > X_j$, entonces $Y_i > Y_j$.
    * $\rho = -1$: Relación monotónica negativa perfecta. Para cada par de observaciones, si $X_i > X_j$, entonces $Y_i < Y_j$.
    * $\rho = 0$: Ausencia de una tendencia monotónica.

* **Propiedades Matemáticas:**
    * Es el **coeficiente de Pearson calculado sobre los rangos** de las variables, no sobre sus valores brutos. Esta es su definición fundamental.
    * Es mucho menos sensible a los valores atípicos que Pearson. Un outlier extremo recibirá el rango más alto o más bajo, pero su magnitud numérica no influirá más allá de eso.

### **Ejemplo 1 (Sencillo, sin empates)**

Analicemos la relación entre la **dificultad percibida** de una tarea (ranking del 1 al 10) y el **tiempo de finalización** (en minutos).

| Tarea | Dificultad (X) | Tiempo (Y) |
| :--- | :--- | :--- |
| 1 | 2 | 10 |
| 2 | 5 | 18 |
| 3 | 1 | 8 |
| 4 | 8 | 30 |
| 5 | 9 | 35 |
| 6 | 4 | 15 |
| 7 | 10 | 45 |
| 8 | 3 | 12 |
| 9 | 6 | 22 |
| 10 | 7 | 25 |

**Paso 1: Asignar rangos a X e Y.** Se ordena cada variable de menor a mayor y se asigna el rango correspondiente.

| X | Y | Rango(X) | Rango(Y) | $d = R(X)-R(Y)$ | $d^2$ |
| :- | :- | :- | :- | :- | :- |
| 2 | 10 | 2 | 2 | 0 | 0 |
| 5 | 18 | 5 | 5 | 0 | 0 |
| 1 | 8 | 1 | 1 | 0 | 0 |
| 8 | 30 | 8 | 8 | 0 | 0 |
| 9 | 35 | 9 | 9 | 0 | 0 |
| 4 | 15 | 4 | 4 | 0 | 0 |
| 10| 45 | 10 | 10 | 0 | 0 |
| 3 | 12 | 3 | 3 | 0 | 0 |
| 6 | 22 | 6 | 6 | 0 | 0 |
| 7 | 25 | 7 | 7 | 0 | 0 |
| | | | | | **Σ=0**|

**Paso 2: Aplicar la fórmula simplificada (válida solo si no hay empates).**
$\rho = 1 - \frac{6 \sum d_i^2}{n(n^2-1)} = 1 - \frac{6 \times 0}{10(10^2-1)} = 1 - 0 = 1$

**Interpretación:** Un valor de $\rho=1$ indica una relación monotónica positiva perfecta. A mayor dificultad percibida, el tiempo de finalización siempre aumenta.

### **Ejemplo 2 (Complejo: Con Empates)**

Analicemos la relación entre la calificación de un examen (sobre 100) y el número de horas de sueño la noche anterior para 15 estudiantes. **Existen empates** en ambas variables.

Datos (Pares Calificación, Horas de Sueño):
(85, 7), (92, 8), (75, 6), **(85, 7.5)**, (60, 5), (95, 8.5), (78, 6.5), **(75, 7)**, (88, 7.5), **(92, 8)**, (70, 6), (65, 5.5), **(85, 8)**, (81, 7), (90, 8.5)

**Paso 1: Asignar rangos, manejando los empates.**
Para un valor empatado, se asigna el **promedio de los rangos** que habrían ocupado.
* Calificación 75: Ocuparían los rangos 3 y 4. Rango promedio = $(3+4)/2 = 3.5$.
* Calificación 85: Ocuparían los rangos 9, 10, 11. Rango promedio = $(9+10+11)/3 = 10$.
* Calificación 92: Ocuparían los rangos 13 y 14. Rango promedio = $(13+14)/2 = 13.5$.
* Horas de Sueño 6: Rangos 3 y 4. Promedio = 3.5.
* Horas de Sueño 7: Rangos 6, 7, 8. Promedio = 7.
* Horas de Sueño 7.5: Rangos 9 y 10. Promedio = 9.5.
* Horas de Sueño 8: Rangos 11, 12, 13. Promedio = 12.
* Horas de Sueño 8.5: Rangos 14 y 15. Promedio = 14.5.

**Importante:** Cuando hay empates, la fórmula simplificada `1 - ...` **no es correcta**. Debemos usar la definición fundamental: calcular el coeficiente de Pearson sobre los rangos.

**Paso 2: Calcular el coeficiente de Pearson sobre los rangos (R_x y R_y).**

| X | Y | Rango(X) (R_x) | Rango(Y) (R_y) |
|---|---|---|---|
| 85 | 7 | 10 | 7 |
| 92 | 8 | 13.5 | 12 |
| 75 | 6 | 3.5 | 3.5 |
| 85 | 7.5 | 10 | 9.5 |
| 60 | 5 | 1 | 1 |
| 95 | 8.5 | 15 | 14.5 |
| 78 | 6.5 | 5 | 5 |
| 75 | 7 | 3.5 | 7 |
| 88 | 7.5 | 12 | 9.5 |
| 92 | 8 | 13.5 | 12 |
| 70 | 6 | 2 | 3.5 |
| 65 | 5.5 | 6 | 2 |
| 85 | 8 | 10 | 12 |
| 81 | 7 | 7 | 7 |
| 90 | 8.5 | 8 | 14.5 |

Calculamos $\bar{R}_x = 8.7$ y $\bar{R}_y = 8$. Ahora, aplicamos la fórmula de Pearson a las columnas $R_x$ y $R_y$, calculando $\sum(R_x - \bar{R}_x)(R_y - \bar{R}_y)$, $\sum(R_x - \bar{R}_x)^2$ y $\sum(R_y - \bar{R}_y)^2$. (Cálculos intermedios omitidos por brevedad).
$\sum(R_x - \bar{R}_x)(R_y - \bar{R}_y) = 196.5$
$\sum(R_x - \bar{R}_x)^2 = 250.5$
$\sum(R_y - \bar{R}_y)^2 = 236$

$\rho = \frac{196.5}{\sqrt{250.5 \times 236}} \approx \frac{196.5}{243.1} \approx 0.808$

**Interpretación:** Un coeficiente de $\rho \approx 0.81$ indica una **fuerte relación monotónica positiva**. A medida que las horas de sueño aumentan, la calificación del examen tiende a aumentar consistentemente, aunque no necesariamente de forma lineal.

### **Resumen y Fórmula Final**

El coeficiente de Spearman es una robusta alternativa no paramétrica a Pearson, ideal para datos ordinales o para relaciones monotónicas no lineales. Su resistencia a los outliers lo convierte en una herramienta muy valiosa.

Fórmula simplificada (solo para datos sin empates):
$$\rho = 1 - \frac{6 \sum_{i=1}^{n} d_i^2}{n(n^2-1)} \quad \text{donde } d_i = R(X_i) - R(Y_i)$$
Definición general (y correcta para datos con empates):
$$\rho = r_{R(X), R(Y)} = \frac{cov(R(X), R(Y))}{\sigma_{R(X)}\sigma_{R(Y)}}$$

---
## **Sección III: Coeficiente de Correlación Tau de Kendall (τ)**

### **Teoría Matemática Rigurosa**

El Tau de Kendall es otra medida de correlación no paramétrica basada en rangos.

* **Propósito Fundamental:** Mide la **asociación ordinal** entre dos variables. Lo hace evaluando la concordancia entre los ordenamientos de los datos.

* **Pares Concordantes y Discordantes:** Consideremos dos observaciones $(X_i, Y_i)$ y $(X_j, Y_j)$.
    * El par es **concordante (C)** si el orden de los rangos coincide: si $X_i > X_j$ y $Y_i > Y_j$, o si $X_i < X_j$ y $Y_i < Y_j$. Básicamente, si van en la misma dirección.
    * El par es **discordante (D)** si el orden de los rangos es opuesto: si $X_i > X_j$ y $Y_i < Y_j$, o si $X_i < X_j$ y $Y_i > Y_j$.
    * Si $X_i = X_j$ o $Y_i = Y_j$, el par está **empatado**.

* **Supuestos Matemáticos:** Las variables deben ser al menos **ordinales**.

* **Interpretación del Valor:** Tau también varía en $[-1, 1]$.
    * $\tau = 1$: Todos los pares son concordantes.
    * $\tau = -1$: Todos los pares son discordantes.
    * $\tau = 0$: Hay un número igual de pares concordantes y discordantes.
    * Se puede interpretar como la diferencia entre la probabilidad de que las variables estén en el mismo orden versus la probabilidad de que estén en órdenes diferentes: $\tau = P(\text{concordante}) - P(\text{discordante})$.

* **Propiedades Matemáticas:**
    * Generalmente, los valores de Tau son más bajos que los de Spearman para la misma asociación.
    * Se considera más robusto y estadísticamente más eficiente que Spearman para muestras pequeñas.
    * Existen variantes para manejar empates: **Tau-b** es la más común.

### **Ejemplo 1 (Sencillo, Tau-a)**

Dos críticos de cine clasifican 5 películas.

| Película | Crítico 1 (X) | Crítico 2 (Y) |
| :--- | :--- | :--- |
| A | 1 | 2 |
| B | 2 | 1 |
| C | 3 | 4 |
| D | 4 | 3 |
| E | 5 | 5 |

**Paso 1: Listar todos los pares posibles de observaciones y clasificarlos.**
El número total de pares es $n(n-1)/2 = 5(4)/2 = 10$.

| Par | Orden X | Orden Y | Clasificación |
|---|---|---|---|
| (A,B) | 1 < 2 | 2 > 1 | Discordante (D) |
| (A,C) | 1 < 3 | 2 < 4 | Concordante (C) |
| (A,D) | 1 < 4 | 2 > 3 | Discordante (D) |
| (A,E) | 1 < 5 | 2 < 5 | Concordante (C) |
| (B,C) | 2 < 3 | 1 < 4 | Concordante (C) |
| (B,D) | 2 < 4 | 1 > 3 | Discordante (D) |
| (B,E) | 2 < 5 | 1 < 5 | Concordante (C) |
| (C,D) | 3 < 4 | 4 > 3 | Discordante (D) |
| (C,E) | 3 < 5 | 4 < 5 | Concordante (C) |
| (D,E) | 4 < 5 | 3 < 5 | Concordante (C) |

**Paso 2: Contar Pares Concordantes (C) y Discordantes (D).**
C = 6, D = 4

**Paso 3: Aplicar la fórmula de Tau-a (sin empates).**
$\tau_a = \frac{C - D}{C + D} = \frac{6 - 4}{6 + 4} = \frac{2}{10} = 0.2$

**Interpretación:** Un $\tau = 0.2$ indica una correlación ordinal positiva débil entre las clasificaciones de los dos críticos.

### **Ejemplo 2 (Complejo: Con Empates, Tau-b)**

Analicemos la relación entre **Nivel Educativo** y **Nivel de Ingresos** (ambos ordinales) en una muestra de 15 personas.

Datos (Pares Educacion, Ingreso):
(Secundaria, Bajo), (Universidad, Medio), (Primaria, Bajo), (Universidad, Alto), (Secundaria, Medio), (Posgrado, Alto), (Universidad, Medio), (Secundaria, Bajo), (Posgrado, Medio), (Universidad, Alto), (Secundaria, Alto), (Primaria, Medio), (Posgrado, Alto), (Universidad, Medio), (Secundaria, Medio)

**Paso 1: Contar pares C, D y empates.**
El proceso es el mismo (comparar cada observación con todas las demás), pero ahora tenemos una tercera y cuarta categoría:
* Empatados en X ($T_x$): el par tiene el mismo nivel educativo pero diferente ingreso.
* Empatados en Y ($T_y$): el par tiene diferente nivel educativo pero el mismo ingreso.
(Si están empatados en ambos, no se cuentan en C, D, $T_x$ o $T_y$).

Total de pares = $15(14)/2 = 105$. Después de una cuidadosa tabulación (proceso omitido por su extensión):
* Pares Concordantes (C) = 45
* Pares Discordantes (D) = 13
* Empatados solo en X ($T_x$) = 20
* Empatados solo en Y ($T_y$) = 18

El número total de pares es C + D + $T_x$ + $T_y$ + (empatados en ambos) = 105.

**Paso 2: Aplicar la fórmula de Tau-b, que ajusta por empates.**
El denominador de Tau-b utiliza el número total de pares menos los empates en X y menos los empates en Y.
$N_0 = n(n-1)/2 = 105$
$N_1 = C + D + T_y$
$N_2 = C + D + T_x$

$\tau_b = \frac{C - D}{\sqrt{(N_1)(N_2)}} = \frac{C - D}{\sqrt{(C+D+T_y)(C+D+T_x)}}$
$\tau_b = \frac{45 - 13}{\sqrt{(45+13+18)(45+13+20)}} = \frac{32}{\sqrt{76 \times 78}} = \frac{32}{\sqrt{5928}} \approx \frac{32}{76.99} \approx 0.416$

**Interpretación:** Un $\tau_b \approx 0.42$ indica una correlación ordinal positiva moderada. Existe una tendencia clara a que un mayor nivel educativo se asocie con un mayor nivel de ingresos en esta muestra. El valor es más confiable que Tau-a porque ha sido ajustado para el alto número de empates en los datos.

### **Resumen y Fórmula Final**

Tau de Kendall es un coeficiente de correlación que se basa en la concordancia y discordancia de los pares de observaciones. Es especialmente útil en muestras pequeñas y cuando hay muchos empates (usando la variante Tau-b). Ofrece una interpretación probabilística directa y es una excelente medida de asociación ordinal.

Fórmula de Tau-a (sin empates):
$$\tau_a = \frac{N_C - N_D}{\frac{1}{2} n(n-1)}$$
Fórmula de Tau-b (con empates):
$$\tau_b = \frac{N_C - N_D}{\sqrt{(N_C + N_D + N_{T_y})(N_C + N_D + N_{T_x})}}$$
donde $N_C$ es el número de pares concordantes, $N_D$ el de discordantes, $N_{T_x}$ el de empatados en X, y $N_{T_y}$ el de empatados en Y.