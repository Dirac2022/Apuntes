
# Linear Regression Model
```python
from sklearn.linear_model import LinearRegression

model = LinearRegression(fit_intercept=True, normalize=False, copy_X=True, n_jobs=None)
```

### Parameters
- `fit_intercept` : Si es `False`, los datos están centrados en el origen ($\beta_0=0$)
- `normalize` :  Normaliza los datos antes de entrenar. (Ahora se recomienda usar `StandardScaler`)
- `copy_X` : Crea una copia de los datos para evitar modificar los originales
- `n_jobs` : Número de procesadores a usar para el cálculo. Si es `-1`. 


### Attributes
- `coef_` : Array con coeficientes $\beta_i$ de la regresión. (Sin el termino independiente).
- `intercept_` : $\beta_0$
- `rank_` : Rango de la matriz de características $X$.
- `singular_` : Valores singulares de $X$ después de $SVD$. Útil para detectar **multicolinealidad**.


### Methods
- `fit(X, y)`: Entrena el modelo con los datos $X$ e $y$
- `predict(X)` : Hace predicciones para nuevas muestras $X$ basadas en el modelo entrenado.
- `score(X, y)` : Retorna el coeficiente de determinación $R^2$, indicando que tan bien el modelo explica los datos. 
- `get_params(deep=True)` : Devuelve los hiperparámetros del modelo.
- `set_params(**params)` : Permite modificar los hiperparámetros del modelo antes de entrenarlo.


# Logistic Regression Model

```python
from sklearn.linear_model import LogisticRegression
model = LogisticRegression(
	penalty='l2',
	C=1.0,
	fit_intercept=True
	solver='lbfgs',
	max_iter=100,
	multi_class='auto'
)
```


### Parameters
- `penalty` : Tipo de regularización (`l2`, `l1`, etc.)
- `C` : Controla la regularización (valores más pequeños significan mayor regularización)
- `fit_intercept` : Si es `True`, agrega un término independiente al modelo.
- `solver` : Algoritmo de optimización (`lbfgs` por defecto, útil para multiclase)
- `max_iter` : Número máximo de iteraciones antes de detener el entrenamiento
- `multi_class` : Define cómo manejar problemas multiclase (`auto`, `ovr`, `multinomial`)


### Atributos
- `coef_` : Matriz de coeficientes del modelo
- `intercept_`: Término independiente del modelo
- `classes_` : Clases aprendidas durante el entrenamiento


### Métodos
- `fit(X, y)` : Entrena el modelo con los datos
- `predict(X)` : Predice la clase de nuevas muestras
- `predict_proba(X)` : Devuelve la probabilidad de cada clase
- `score(X, y)` : Retorna la precisión del modelo


# Varios

## `StandardScaler`
Se utiliza para normalizar características centrándolas en la media y escalándolas a una varianza unitaria. 

Para cada característica $X_i$ se aplica la transformación [[Regression with multiple input variables#Z-score normalization|Z-score normalization]]. Después de la transformación
- Cada característica tiene una media de 0
- Cada característica tiene una varianza de 1.

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
```

### Métodos
- `fit(X)` : Calcula la media y la desviación estándar en los datos `X` (sin transformar los datos)
- `transform(X)` : Transforma `X` usando la media y la desviación estándar previamente calculadas
- `fit_transform(X)` : Calcula la media y la desviación estándar y transforma `X` es una sola operación.
- `inverse_transform(X_scaled)` : Deshace la normalización, devolviendo los datos a su escala original.

### Atributos
- `mean_, var_` : Media y varianza de cada característica
- `scale_` : Desviación estándar de cada característica.


## `SGDRegressor`

(*Stochastic Gradient Descent Regressor*) es un modelo de regresión lineal que se entrena mediante **descenso de gradiente estocástico (SGD)**.

```python
from sklearn.linear_model import SGDRegressor

model = SGDRegressor(loss="squared_error", penalty="l2", alpha="0.001", max_iter=1000, tol=1e-3)
```

### Parámetros
- `loss` : Función de perdida utilizada para minimizar el error.
- `penalty` : Tipo de regularización aplicada (`l2`, `l1`, `elasticnet`) para evitar sobreajuste.
- `alpha` : Coeficiente de regularización que controla la penalización en los coeficientes.
- `max_iter` : Número máximo de iteraciones para la convergencia del algoritmo.
- `tol`: Tolerancia para detectar la optimización si el cambio en la función de pérdida es menor que este valor.

### Atributos
- `coef_` : Coeficientes $\beta_i$ de la regresión
- `intercept_` : Término independiente $\beta_0$
- `n_iter_` : Número de iteraciones realizadas hasta la convergencia
- `t_`: Número total de actualizaciones de los coeficientes.

### Métodos
- `fit(X, y)` : Entrena el modelo usando SGD en los datos $X, y$
- `predict(X)` : Hace predicciones para nuevas muestras.
- `score(X, y)` : Retorna el coeficiente de determinación $R^2$
- `partial_fit(X, y)` : Permite entrenar el modelo de manera incremental, útil para datos en streaming.
- `get_params(deep=True)` : Devuelve los hiperparámetros del modelo.
- `set_params(**params)` : Modifica los hiperparámetros antes del entrenamiento


### Ejemplo

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.linear_model import SGDRegressor
from sklearn.preprocessing import StandardScaler
from sklearn.metrics import mean_squared_error, r2_score

# Generar datos sintéticos (X en el rango de 0 a 10, y con ruido)
np.random.seed(42)
X = 10 * np.random.rand(100, 1)
y = 3 * X.squeeze() + 5 + np.random.randn(100)  # y = 3X + 5 + ruido

# Dividir en datos de entrenamiento y prueba
X_train, X_test = X[:80], X[80:]
y_train, y_test = y[:80], y[80:]

# Estandarización de los datos (importante para SGD)
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

# Crear el modelo con parámetros específicos
sgd_reg = SGDRegressor(max_iter=1000, tol=1e-3, learning_rate="invscaling", eta0=0.01, penalty="l2")

# Entrenar el modelo
sgd_reg.fit(X_train_scaled, y_train)

# Hacer predicciones en el conjunto de prueba
y_pred = sgd_reg.predict(X_test_scaled)

# Evaluar el modelo
mse = mean_squared_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)

# Mostrar resultados
print(f"Coeficiente estimado (β1): {sgd_reg.coef_[0]}")
print(f"Término independiente (β0): {sgd_reg.intercept_[0]}")
print(f"Error cuadrático medio (MSE): {mse:.4f}")
print(f"Coeficiente de determinación (R²): {r2:.4f}")

# Graficar los resultados
plt.scatter(X_test, y_test, color="blue", label="Datos reales")
plt.plot(X_test, y_pred, color="red", linewidth=2, label="Predicción (SGD)")
plt.xlabel("X")
plt.ylabel("y")
plt.legend()
plt.title("Regresión Lineal con SGDRegressor")
plt.show()

```
