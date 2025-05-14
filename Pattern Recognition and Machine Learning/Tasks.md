
# 1. Introduction

- [ ] Introduction 1 

## 1.1 Example: Polynomial Curve Fitting
- [ ] Example: Polynomial Curve Fitting 4

## 1.2 Probability Theory
- [ ] Probability Theory 12
- [ ] 1.2.1 Probability densities 17
- [ ] 1.2.2 Expectations and covariances 19
- [ ] 1.2.3 Bayesian probabilities 21
- [ ] 1.2.4 The Gaussian distribution 24
- [ ] 1.2.5 Curve fitting re-visited 28
- [ ] 1.2.6 Bayesian curve fitting 30

##  1.3 Model Selection
- [ ] Model Selection 32

## 1.4 The Curse of Dimensionality
- [ ] The Curse of Dimensionality 33

## 1.5 Decision Theory
- [ ] Decision Theory 38
- [ ] 1.5.1 Minimizing the misclassification rate 39
- [ ] 1.5.2 Minimizing the expected loss 41
- [ ] 1.5.3 The reject option 42
- [ ] 1.5.4 Inference and decision 42
- [ ] 1.5.5 Loss functions for regression 46

## 1.6 Information Theory
- [ ] Information Theory 48
- [ ] 1.6.1 Relative entropy and mutual information 55


# 2. Probability Distributions

| Nivel de Prioridad | Subcapítulo                                            | Justificación                                                                                                                         |
| ------------------ | ------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------- |
| **Indispensables** | **2.1 Binary Variables**                               | Introduce las variables binarias, esenciales para clasificaciones binarias, fundamentales en Machine Learning.                        |
|                    | **2.2 Multinomial Variables**                          | Base para clasificaciones multiclase, un concepto ampliamente usado en tareas de clasificación.                                       |
|                    | **2.3 The Gaussian Distribution**                      | Proporciona la base para entender datos continuos y su distribución, muy común en Machine Learning.                                   |
|                    | **2.3.1 Conditional Gaussian distributions**           | Importante para modelar relaciones condicionales entre variables gaussianas.                                                          |
|                    | **2.3.3 Bayes’ theorem for Gaussian variables**        | Introduce la inferencia probabilística para variables gaussianas, esencial en muchos métodos bayesianos.                              |
|                    | **2.4 The Exponential Family**                         | Concepto clave que engloba muchas distribuciones usadas en Machine Learning.                                                          |
|                    | **2.4.1 Maximum likelihood and sufficient statistics** | Fundamentales para entender cómo se estiman los parámetros en modelos probabilísticos.                                                |
| **Intermedios**    | **2.1.1 The beta distribution**                        | Utilizada como distribución a priori en problemas bayesianos. Importante, pero puede ser secundario en un curso introductorio.        |
|                    | **2.2.1 The Dirichlet distribution**                   | Extensión de la beta a variables multinomiales, relevante para enfoques bayesianos, pero menos crítico al inicio.                     |
|                    | **2.3.2 Marginal Gaussian distributions**              | Útil para inferencia cuando se trabaja con modelos gaussianos multivariados.                                                          |
|                    | **2.3.4 Maximum likelihood for the Gaussian**          | Método esencial para estimar parámetros, pero puede cubrirse al estudiar el máximo verosímil en general.                              |
|                    | **2.5.2 Nearest-neighbour methods**                    | Método intuitivo y básico para clasificación y regresión, importante como base en técnicas de aprendizaje supervisado.                |
|                    | **2.5 Nonparametric Methods**                          | Introduce técnicas alternativas como kernel density estimation, útiles pero no esenciales en una introducción.                        |
|                    | **2.5.1 Kernel density estimators**                    | Método no paramétrico relevante para análisis de datos y estimación de densidades, pero no crítico para un curso inicial.             |
| **Avanzados**      | **2.3.5 Sequential estimation**                        | Aborda problemas específicos de actualización secuencial de estimaciones, más avanzado.                                               |
|                    | **2.3.6 Bayesian inference for the Gaussian**          | Extiende el uso bayesiano a distribuciones gaussianas, esencial para cursos avanzados de inferencia bayesiana.                        |
|                    | **2.3.7 Student’s t-distribution**                     | Distribución robusta frente a valores atípicos, relevante para aplicaciones específicas, pero no central en Machine Learning inicial. |
|                    | **2.3.8 Periodic variables**                           | Caso especializado de variables cíclicas, útil en ciertos dominios (e.g., meteorología), pero no esencial.                            |
|                    | **2.3.9 Mixtures of Gaussians**                        | Introduce conceptos avanzados de modelos generativos y clustering, mejor para cursos avanzados.                                       |
|                    | **2.4.2 Conjugate priors**                             | Avanzado en inferencia bayesiana, útil en contextos específicos.                                                                      |
|                    | **2.4.3 Noninformative priors**                        | Importante para métodos bayesianos, pero más avanzado.                                                                                |


- [ ] Probability Distributions 67

## 2.1 Binary Variables
- [ ] Binary Variables 68
- [ ] 2.1.1 The beta distribution 71

## 2.2 Multinomial Variables
- [ ] Multinomial Variables 74
- [ ] 2.2.1 The Dirichlet distribution 76

## 2.3 The Gaussian Distribution
- [ ] The Gaussian Distribution  78
- [ ] 2.3.1 Conditional Gaussian distribution 85
- [ ] 2.3.2 Marginal Gaussian distributions 88
- [ ] 2.3.3 Bayes' theorem for Gaussian variables 90
- [ ] 2.3.4 Maximum likelihood for the Gaussian 93
2.3.5 Sequential estimation 94
2.3.6 Bayesian inference for the Gaussian 97
- [ ] 2.3.7 Student's t-distribution 102
2.3.8 Periodic variables 105
2.3.9 Mixture of Gaussians 110

## 2.4 The Exponential Family
- [ ] The Exponential Family 113
- [ ] 2.4.1 Maximum likelihood and sufficient statistics 116
2.4.2 Conjugate priors 117
2.4.3 Noninformative priors 117

## 2.5 Nonparametric Methods
- [ ] Nonparametric Methods 120
- [ ] 2.5.1 Kernel density estimators
- [ ] 2.5.2 Nearest-neighbour methods 124



# 3. Linear Models for Regression

|Nivel de Prioridad|Subcapítulo|Justificación|
|---|---|---|
|**Indispensables**|**3.1 Linear Basis Function Models**|Introduce los modelos lineales para regresión, que son básicos en Machine Learning.|
||**3.1.1 Maximum likelihood and least squares**|Explica el método de mínimos cuadrados y su conexión con el máximo de verosimilitud, clave para la implementación práctica.|
||**3.1.4 Regularized least squares**|Introduce la regularización, esencial para evitar el sobreajuste en modelos.|
||**3.2 The Bias-Variance Decomposition**|Proporciona una base teórica para comprender el equilibrio entre el sesgo y la varianza, fundamental para entender la calidad de los modelos.|
|**Intermedios**|**3.1.2 Geometry of least squares**|Explora una interpretación geométrica útil, aunque más conceptual.|
||**3.1.3 Sequential learning**|Extiende los conceptos básicos al aprendizaje secuencial, útil pero no crucial para empezar.|
||**3.1.5 Multiple outputs**|Explica cómo extender los modelos lineales a múltiples salidas, relevante en aplicaciones prácticas pero no siempre indispensable al inicio.|
||**3.3 Bayesian Linear Regression**|Introduce un enfoque bayesiano a los modelos lineales, útil para una comprensión más completa de la inferencia probabilística.|
||**3.3.1 Parameter distribution**|Describe cómo modelar la distribución de parámetros en el contexto bayesiano, una extensión útil pero secundaria para principiantes.|
||**3.3.2 Predictive distribution**|Profundiza en cómo realizar predicciones en un marco bayesiano, relevante en contextos avanzados.|
||**3.3.3 Equivalent kernel**|Aborda interpretaciones avanzadas de los modelos bayesianos, útil pero no esencial en un curso inicial.|
||**3.6 Limitations of Fixed Basis Functions**|Explica las limitaciones de las funciones base fijas, preparando para modelos más avanzados como los basados en kernels o redes neuronales.|
|**Avanzados**|**3.4 Bayesian Model Comparison**|Introduce métodos avanzados de comparación de modelos en un marco bayesiano, relevante para tareas complejas de modelado probabilístico.|
||**3.5 The Evidence Approximation**|Profundiza en la estimación de la evidencia, útil en contextos avanzados de selección de modelos.|
||**3.5.1 Evaluation of the evidence function**|Concepto teórico que amplía el análisis de la evidencia en modelos bayesianos, más avanzado.|
||**3.5.2 Maximizing the evidence function**|Describe técnicas para maximizar la evidencia, relevante en aplicaciones bayesianas avanzadas.|
||**3.5.3 Effective number of parameters**|Concepto útil para la interpretación de modelos bayesianos, pero no crucial para el aprendizaje inicial.|

- [ ] Linear Models for Regression 137
## 3.1 Linear Basis Functions Models
- [ ] Linear Basis Functions Models 138
- [ ] 3.1.1 Maximum likelihood and least squares 140
- [ ] 3.1.2 Geometry of least squares 143
- [ ] 3.1.3 Sequential learning 143
- [ ] 3.1.4 Regularized least squares 144
- [ ] 3.1.5 Multiple outputs 146
## 3.2 The Bias-Variance Decomposition
- [ ] The Bias-Variance Decomposition 147

## 3.3 Bayesian Linear Regression
- [ ] Bayesian Linear Regression 152
- [ ] 3.3.1 Parameter distribution 152
- [ ] 3.3.2 Predictive distribution 156
- [ ] 3.3.3 Equivalent kernel 159
## 3.4 Bayesian Model Comparison
Bayesian Model Comparison 161

## 3.5 The Evidence Approximation
The Evidence Approximation 165
3.5.1 Evaluation of the evidence function 166
3.5.2 Maximizing the evidence function 168
3.5.3 Effective number of parameters 170
## 3.6 Limitations of Fixed Basis Functions
- [ ] Limitations of Fixed Basis Functions 172


# 4. Linear Models for Classification
- [ ] Linear Models for Classification 179
## 4.1 Discriminant Functions
- [ ] Discriminant Functions 181
- [ ] 4.1.1 Two classes 181
- [ ] 4.1.2 Multiple classes 182
- [ ] 4.1.3 Least squares for classification 184
- [ ] 4.1.4 Fisher's linear discriminant 186
- [ ] 4.1.5 Relation to least squares 189
4.1.6 Fisher's discriminant for multiple classes 191
- [ ] 4.1.7 The perceptron algorithm 192

## 4.2 Probabilistic Generative Models
- [ ] Probabilistic Generative Models 196
- [ ] 4.2.1 Continuous inputs 198
- [ ] 4.2.2 Maximum likelihood solution 200
4.2.3 Discrete features 202
4.2.4 Exponential family 202

## 4.3 Probabilistic Discriminative Models
- [ ] Probabilistic Discriminative Models 203
- [ ] 4.3.1 Fixed basis functions 204
- [ ] 4.3.2 Logistic regression 205
- [ ] 4.3.3 Iterative reweighted least squares 207
- [ ] 4.3.4 Multiclass logistic regression 209
4.3.5 Probit regression 210
4.3.6 Canonical link functions 212
## 4.4 The Laplace Approximation
The Laplace Approximation 213
4.4.1 Model comparison and BIC 216

## 4.5 Bayesian Logistic Regression
Bayesian Logistic Regression 217
4.5.1 Laplace approximation 217
4.5.2 Predictive distribution 218