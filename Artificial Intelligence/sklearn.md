

# confusion_matrix
La función `confusion_matrix` de `sklearn.metrics` genera una **matriz de confusión** que permite evaluar el rendimiento de un modelo de clasificación al comparar las etiquetas reales con las etiquetas predichas. 

### Estructura básica de `confusion_matrix`

Para un **problema de clasificación binaria**, la matriz de confusión tiene la siguiente estructura:

|                  | Predicción: Clase Negativa (0) | Predicción: Clase Positiva (1) |
|------------------|-------------------------------|-------------------------------|
| **Clase Negativa (0)** | Verdaderos Negativos (TN)       | Falsos Positivos (FP)         |
| **Clase Positiva (1)** | Falsos Negativos (FN)           | Verdaderos Positivos (VP)     |

### Descripción de cada término:
- **TN (True Negative)**: Número de ejemplos donde el modelo predijo correctamente la clase negativa (0).
- **FP (False Positive)**: Número de ejemplos donde el modelo predijo incorrectamente la clase positiva (1) cuando la clase real era negativa (0).
- **FN (False Negative)**: Número de ejemplos donde el modelo predijo incorrectamente la clase negativa (0) cuando la clase real era positiva (1).
- **VP (True Positive)**: Número de ejemplos donde el modelo predijo correctamente la clase positiva (1).

### Ejemplo de uso de `confusion_matrix`

Supongamos que tienes las etiquetas reales (`y_true`) y las predicciones del modelo (`y_pred`):

```python
from sklearn.metrics import confusion_matrix

# Etiquetas reales y predicciones del modelo
y_true = [0, 1, 0, 1, 0, 1, 0, 0, 1, 1]  # Ejemplos de etiquetas reales
y_pred = [0, 1, 0, 0, 0, 1, 1, 0, 1, 1]  # Predicciones hechas por el modelo

# Generar la matriz de confusión
matriz = confusion_matrix(y_true, y_pred)

# Mostrar la matriz de confusión
print(matriz)
```

### Ejemplo de salida:
```
[[4 1]
 [1 4]]
```

Esta matriz indica lo siguiente:
- **TN = 4**: El modelo predijo correctamente 4 ejemplos de la clase negativa (0).
- **FP = 1**: El modelo predijo incorrectamente 1 ejemplo como positivo (1), cuando en realidad era negativo (0).
- **FN = 1**: El modelo predijo incorrectamente 1 ejemplo como negativo (0), cuando en realidad era positivo (1).
- **VP = 4**: El modelo predijo correctamente 4 ejemplos de la clase positiva (1).

### Generalización a problemas multiclase
Para **problemas de clasificación multiclase**, la matriz de confusión tiene una estructura más grande, donde cada fila y columna corresponde a una clase diferente. Los valores diagonales representan las predicciones correctas (donde la predicción coincide con la clase real), y los valores fuera de la diagonal representan errores de predicción.

En resumen, la matriz de confusión te da una visión clara de cuántas veces el modelo acierta o se equivoca en cada clase, lo que te ayuda a identificar patrones de error o desequilibrios en las predicciones.