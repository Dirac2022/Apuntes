[Linear Discriminant Analysis (LDA) | by Ingo Nowitzky | TDS Archive | Medium](https://medium.com/data-science/linear-discriminant-analysis-lda-598d8e90f8b9)

**Linear Discriminant Analysis** is a **feature** / dimensionality **reduction** technique and **clustering algorithm**. It belongs to the class of Supervised Learning. Feature reduction means that we select those features of the data that are most valuable to separate the data into the classes.

Datasets in the industry usually have many features, and it is often unclear which of the features are "important" and which are less. Often, the goal is to differentiate the datasets from each other, i.e., to classify them.

A commonly used method is the well-known Principal Component Analysis (PCA). While PCA belongs to the **un**supervised methods, the less widespread LDA is a supervised method and thus learns from **labeled data**. Therefore, it is particularly suited for explaining failure patterns from large datasets.


### Goal and Principle of LDA

The goal of LDA is to linearly combine the features of the data so that the labels of the datasets are best separated from each other, and the number of new features is reduce to a predefined count. In other words, a **projection to a lower-dimensional space**


<div style="background-color:white; text-align:center">
<fig>
<img src="https://miro.medium.com/v2/resize:fit:1100/format:webp/1*fnaHijTNEzDgVLrnOfsKZQ.png" width=400 >
</fig>
</div>


### How does LDA work?

The process of Linear Discriminant Analysis (LDA) can be broken down into five key steps.

**Step 1:** Compute the _d_-dimensional mean vectors for each of the _k_ classes separately from the dataset.

Remember that LDA is a supervised machine learning technique, meaning we can utilize the known labels. In the first step, we calculate the mean vectors _mean_c_ for all samples belonging to a specific class _c_. To do this, we filter the feature matrix by class label and compute the mean for each of the _d_ features. As a result, we obtain _k_ mean vectors (one for each of the _k_ classes), each with a length of _d_ (corresponding to the _d_ features).


<div style="background-color:white; text-align:center">
<fig>
<img src="https://miro.medium.com/v2/resize:fit:2000/format:webp/1*N-VbzV-PotaEJ7nwK6oSIQ.png" >
</fig>
</div>

$$
mean_c = \dfrac{1}{n_c} \cdot \sum_{x \in \mathcal{C}_c} \mathbb{X}_c = [\mu_1, \mu_2, \dots, \mu_d]
$$

Según el artículo es: $\dfrac{1}{n_c - 1}$




¡Perfecto! Con esta información podemos hacer un ejemplo completo y corregido. Veo que en la imagen la fórmula tiene un pequeño error (usa `n_c - 1`), pero en LDA estándar es simplemente `n_c`.

---

Supongamos que tenemos **6 muestras (n=6)** con **3 características (d=3)** y **2 clases (k=2)**:

**Feature Matrix X** y **Label Vector Y**:

| Muestra | Label (Y) | X₁ (Feature 1) | X₂ (Feature 2) | X₃ (Feature 3) |
|---------|-----------|----------------|----------------|----------------|
| 1       | 0         | 4.0            | 2.0            | 1.0            |
| 2       | 0         | 2.0            | 4.0            | 2.0            |
| 3       | 0         | 3.0            | 3.0            | 1.5            |
| 4       | 1         | 8.0            | 6.0            | 7.0            |
| 5       | 1         | 7.0            | 5.0            | 6.0            |
| 6       | 1         | 9.0            | 7.0            | 8.0            |


**Paso 1: Calcular vectores medios para cada clase**

**Para la Clase 0 (c=0)**:
- **Muestras**: 1, 2, 3 → `n₀ = 3`
- **Cálculo del vector medio**:
  $$
  \mathbf{mean_0} = \frac{1}{n_0} \cdot \sum_{x \in C_0} X = \left[\mu_1, \mu_2, \mu_3\right]
  $$

  - **Feature 1 (X₁)**: (4.0 + 2.0 + 3.0)/3 = **3.0**
  - **Feature 2 (X₂)**: (2.0 + 4.0 + 3.0)/3 = **3.0**
  - **Feature 3 (X₃)**: (1.0 + 2.0 + 1.5)/3 = **1.5**

  $$
  \mathbf{mean_0} = \begin{bmatrix} 3.0 \\ 3.0 \\ 1.5 \end{bmatrix}
  $$

**Para la Clase 1 (c=1)**:
- **Muestras**: 4, 5, 6 → `n₁ = 3`
- **Cálculo del vector medio**:
  - **Feature 1 (X₁)**: (8.0 + 7.0 + 9.0)/3 = **8.0**
  - **Feature 2 (X₂)**: (6.0 + 5.0 + 7.0)/3 = **6.0**
  - **Feature 3 (X₃)**: (7.0 + 6.0 + 8.0)/3 = **7.0**

  $$
  \mathbf{mean_1} = \begin{bmatrix} 8.0 \\ 6.0 \\ 7.0 \end{bmatrix}
  $$


**Resultados del Paso 1**
- **Número de vectores medios (k)**: 2
- **Dimensión de cada vector (d)**: 3
- **Vectores obtenidos**:
  - Clase 0: `[3.0, 3.0, 1.5]`
  - Clase 1: `[8.0, 6.0, 7.0]`


**Explicación Conceptual**
1. **Filtrado por clase**: Separamos el dataset según la etiqueta Y
2. **Cálculo por característica**: Para cada columna de features, calculamos el promedio solo con las muestras de esa clase
3. **Vector resultante**: Cada `mean_c` representa el "centroide" de la clase c en el espacio d-dimensional


---


**Step 2:** Compute the scatter matrices (between-class scatter matrix and within-class scatter matrix).

==The **within-class scatter** matrix measures the variation among samples within the same class==. To find a subspace with optimal separability, ==we aim to minimize the values in this matrix==. In contrast, ==the **between-class scatter** matrix measures the variation between different classes==. For optimal separability, ==we aim to maximize the values in this matrix==.  
Intuitively, within-class scatter looks at how compact each class is, whereas between-class scatter examines how far apart different classes are.

The **within-class scatter** matrix $S_W$ is calculated as the sum of the scatter matrices $S_c$ for each individual class

$$
S_W = \sum_{c=1}^{k} S_c
$$
where
$$
S_c = \sum_{x \in C_c} (x - mean_c) \cdot (x - mean_c)^T
$$

The **between-class scatter** matrix $S_B$ is derived from the differences between the class means $mean_c$ and the overall mean of the entire dataset

$$
S_B = \sum_k^{c=1} n_c \cdot (mean_c - mean) \cdot (mean_c - mean)^T
$$
where *mean* refers to the mean vector calculated over all samples, regardless of their class labels.



---

**Recordando nuestro dataset:**
- **Clase 0**: Muestras 1, 2, 3 → `mean₀ = [3.0, 3.0, 1.5]`
- **Clase 1**: Muestras 4, 5, 6 → `mean₁ = [8.0, 6.0, 7.0]`

**Paso 2.1: Calcular la media global (`mean`)**
Calculamos el promedio de **todas** las muestras (sin importar la clase):

**Feature 1**: (4.0+2.0+3.0+8.0+7.0+9.0)/6 = **5.5**  
**Feature 2**: (2.0+4.0+3.0+6.0+5.0+7.0)/6 = **4.5**  
**Feature 3**: (1.0+2.0+1.5+7.0+6.0+8.0)/6 = **4.25**

$$
\mathbf{mean} = \begin{bmatrix} 5.5 \\ 4.5 \\ 4.25 \end{bmatrix}
$$

**Paso 2.2: Calcular matriz de dispersión intra-clase (S_W)**

Para cada clase, calculamos **S_c**:

**Para Clase 0**:
Para cada muestra en Clase 0, calculamos: `(x - mean₀) · (x - mean₀)ᵀ`

**Muestra 1**: `[4.0, 2.0, 1.0] - [3.0, 3.0, 1.5] = [1.0, -1.0, -0.5]`  
Producto exterior:  
$$
\begin{bmatrix} 1.0 \\ -1.0 \\ -0.5 \end{bmatrix} \cdot \begin{bmatrix} 1.0 & -1.0 & -0.5 \end{bmatrix} = \begin{bmatrix} 1.0 & -1.0 & -0.5 \\ -1.0 & 1.0 & 0.5 \\ -0.5 & 0.5 & 0.25 \end{bmatrix}
$$

**Muestra 2**: `[2.0, 4.0, 2.0] - [3.0, 3.0, 1.5] = [-1.0, 1.0, 0.5]`  
Producto exterior:  
$$
\begin{bmatrix} -1.0 \\ 1.0 \\ 0.5 \end{bmatrix} \cdot \begin{bmatrix} -1.0 & 1.0 & 0.5 \end{bmatrix} = \begin{bmatrix} 1.0 & -1.0 & -0.5 \\ -1.0 & 1.0 & 0.5 \\ -0.5 & 0.5 & 0.25 \end{bmatrix}
$$

**Muestra 3**: `[3.0, 3.0, 1.5] - [3.0, 3.0, 1.5] = [0.0, 0.0, 0.0]` → Matriz cero

**S₀ = Suma de las 3 matrices anteriores** =  
$$
\begin{bmatrix} 2.0 & -2.0 & -1.0 \\ -2.0 & 2.0 & 1.0 \\ -1.0 & 1.0 & 0.5 \end{bmatrix}
$$

**Para Clase 1**:
`mean₁ = [8.0, 6.0, 7.0]`

**Muestra 4**: `[8.0, 6.0, 7.0] - [8.0, 6.0, 7.0] = [0.0, 0.0, 0.0]`  
**Muestra 5**: `[7.0, 5.0, 6.0] - [8.0, 6.0, 7.0] = [-1.0, -1.0, -1.0]`  
Producto exterior:  
$$
\begin{bmatrix} 1.0 & 1.0 & 1.0 \\ 1.0 & 1.0 & 1.0 \\ 1.0 & 1.0 & 1.0 \end{bmatrix}
$$

**Muestra 6**: `[9.0, 7.0, 8.0] - [8.0, 6.0, 7.0] = [1.0, 1.0, 1.0]`  
Producto exterior:  
$$
\begin{bmatrix} 1.0 & 1.0 & 1.0 \\ 1.0 & 1.0 & 1.0 \\ 1.0 & 1.0 & 1.0 \end{bmatrix}
$$

**S₁ =**  
$$
\begin{bmatrix} 2.0 & 2.0 & 2.0 \\ 2.0 & 2.0 & 2.0 \\ 2.0 & 2.0 & 2.0 \end{bmatrix}
$$

**S_W = S₀ + S₁** =  
$$
\begin{bmatrix} 4.0 & 0.0 & 1.0 \\ 0.0 & 4.0 & 3.0 \\ 1.0 & 3.0 & 2.5 \end{bmatrix}
$$

**Paso 2.3: Calcular matriz de dispersión inter-clase (S_B)**

Para cada clase: `n_c × (mean_c - mean) · (mean_c - mean)ᵀ`

**Para Clase 0**:  
`mean₀ - mean = [3.0, 3.0, 1.5] - [5.5, 4.5, 4.25] = [-2.5, -1.5, -2.75]`  
Producto exterior:  
$$
\begin{bmatrix} 6.25 & 3.75 & 6.875 \\ 3.75 & 2.25 & 4.125 \\ 6.875 & 4.125 & 7.5625 \end{bmatrix}
$$  
Multiplicado por `n₀ = 3`:  
$$
\begin{bmatrix} 18.75 & 11.25 & 20.625 \\ 11.25 & 6.75 & 12.375 \\ 20.625 & 12.375 & 22.6875 \end{bmatrix}
$$

**Para Clase 1**:  
`mean₁ - mean = [8.0, 6.0, 7.0] - [5.5, 4.5, 4.25] = [2.5, 1.5, 2.75]`  
Producto exterior (igual que Clase 0 por simetría):  
$$
\begin{bmatrix} 6.25 & 3.75 & 6.875 \\ 3.75 & 2.25 & 4.125 \\ 6.875 & 4.125 & 7.5625 \end{bmatrix}
$$  
Multiplicado por `n₁ = 3`:  
$$
\begin{bmatrix} 18.75 & 11.25 & 20.625 \\ 11.25 & 6.75 & 12.375 \\ 20.625 & 12.375 & 22.6875 \end{bmatrix}
$$

**S_B = Suma de ambas** =  
$$
\begin{bmatrix} 37.5 & 22.5 & 41.25 \\ 22.5 & 13.5 & 24.75 \\ 41.25 & 24.75 & 45.375 \end{bmatrix}
$$

---

**Interpretación**
- **S_W (intra-clase)**: Mide cuán dispersas están las muestras **dentro** de cada clase (queremos minimizar)
- **S_B (inter-clase)**: Mide cuán separadas están las **medias de clase** entre sí (queremos maximizar)

En el siguiente paso, LDA encontrará direcciones que **maximicen S_B** mientras **minimizan S_W**.
