
El **R²** es una métrica que evalúa cómo de bien un modelo de regresión explica la variabilidad de los datos.  
- **Rango**: Va de **0 a 1** (aunque puede ser negativo en modelos muy malos).  
- **Interpretación**:  
  - **R² = 1**: El modelo explica el 100% de la variabilidad de los datos (ajuste perfecto, pero sospecha de *overfitting*).  
  - **R² = 0**: El modelo no explica nada (es igual a predecir siempre la media de $y$).  
  - **R² negativo**: El modelo es peor que usar la media de $y$.

---

### **Fórmula de R²**
$$
R^2 = 1 - \frac{SS_{\text{res}}}{SS_{\text{tot}}}
$$

Donde:  
- $SS_{\text{res}}$: **Suma de Cuadrados Residual** (error del modelo).  
- $SS_{\text{tot}}$: **Suma de Cuadrados Total** (variabilidad total de los datos).  

---

### **Cálculo de $SS_{\text{res}}$ (Suma de Cuadrados Residual)**
Mide el error entre las predicciones ($\hat{y}_i$) y los valores reales ($y_i$):

$$
SS_{\text{res}} = \sum_{i=1}^{n} (y_i - \hat{y}_i)^2
$$

**Pasos para calcular $SS_{\text{res}}$:**  
1. **Obtener las predicciones del modelo** ($\hat{y}_i$) para cada dato.  
2. **Calcular el residuo** para cada observación: $y_i - \hat{y}_i$.  
3. **Elevar al cuadrado cada residuo**: $(y_i - \hat{y}_i)^2$.  
4. **Sumar todos los cuadrados**: $SS_{\text{res}} = \sum (y_i - \hat{y}_i)^2$.

---

### **Cálculo de $SS_{\text{tot}}$ (Suma de Cuadrados Total)**
Mide la variabilidad total de los datos respecto a la media ($\bar{y}$):

$$
SS_{\text{tot}} = \sum_{i=1}^{n} (y_i - \bar{y})^2
$$

**Pasos para calcular $SS_{\text{tot}}$:**  
1. **Calcular la media de $y$** ($\bar{y}$).  
2. **Restar la media a cada valor real**: $y_i - \bar{y}$.  
3. **Elevar al cuadrado cada diferencia**: $(y_i - \bar{y})^2$.  
4. **Sumar todos los cuadrados**: $SS_{\text{tot}} = \sum (y_i - \bar{y})^2$.


---

### **Ejemplo de R² Negativo**
Si el modelo es muy malo, $SS_{\text{res}}$ puede ser mayor que $SS_{\text{tot}}$, lo que lleva a $R^2 < 0$.  

**Ejemplo:**  
- $SS_{\text{res}} = 10$  
- $SS_{\text{tot}} = 8$  
$$
R^2 = 1 - \frac{10}{8} = 1 - 1.25 = -0.25
$$

**Interpretación**:  
- El modelo es un **25% peor** que predecir siempre la media.

---

### **Limitaciones de R²**
1. **No indica causalidad**: Un R² alto no implica que $X$ cause $y$.  
2. **No evalúa sobreajuste**: Un R² cercano a 1 puede deberse a *overfitting*.  
3. **Depende de la escala**: No es comparable entre modelos con diferente $y$.  
4. **No funciona para modelos no lineales complejos**: Usar otras métricas (ej: R² ajustado, MSE).

---

### **Resumen Visual**
| Componente         | Fórmula                            | Interpretación                          |
|---------------------|------------------------------------|-----------------------------------------|
| $SS_{\text{res}}$ | $\sum (y_i - \hat{y}_i)^2$    | Error del modelo (cuanto más bajo, mejor) |
| $SS_{\text{tot}}$ | $\sum (y_i - \bar{y})^2$      | Variabilidad total de los datos          |
| $R^2$            | $1 - \frac{SS_{\text{res}}}{SS_{\text{tot}}}$ | % de variabilidad explicada por el modelo |

---
