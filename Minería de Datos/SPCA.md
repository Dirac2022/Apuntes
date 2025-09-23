
# 🎓 Minicurso de **Sparse PCA (SPCA)**

## 1.1 ¿Por qué Sparse PCA?

Ya sabes que **PCA** encuentra combinaciones lineales de variables originales que maximizan la varianza.
El problema es que:

* En PCA clásico, **cada componente principal usa *todas*** las variables originales (con pesos distintos).
* Esto hace que los componentes sean **difíciles de interpretar**:

  * Ejemplo: el primer componente puede ser una mezcla de las 100 variables → imposible explicar claramente qué significa.
* En áreas como **biología, neurociencia, minería de datos**, la **interpretabilidad** es clave.

👉 **Sparse PCA** surge para resolver esto:

* Busca **componentes principales dispersos (sparse)**, es decir, que usen **pocas variables significativas**.
* Así, cada componente es más **fácil de interpretar** y puede revelar **estructuras ocultas** en los datos.

---

## 1.2 Intuición de Sparse PCA

* En PCA normal:

  * Un componente es un vector $w \in \mathbb{R}^d$ con entradas **densas** (casi todas diferentes de 0).
* En **SPCA**:

  * Queremos que $w$ tenga **muchos ceros** → solo unas pocas variables “entran en juego”.

Visualmente:

* PCA: cada eje nuevo es una combinación de todas las variables.
* SPCA: cada eje nuevo es una combinación **sólo de algunas variables relevantes**.

---

## 1.3 Formalización matemática

Recordemos que PCA resolvía:

$$
\max_{w} \; w^T C w \quad \text{sujeto a } \; \|w\|_2 = 1
$$

donde $C$ es la matriz de covarianza.

👉 En SPCA añadimos una restricción de **sparsity (dispersión)**.
Existen varias formas, pero la más común es añadir una penalización tipo **L1** (como en LASSO):

$$
\max_{w} \; w^T C w - \alpha \|w\|_1
\quad \text{sujeto a } \; \|w\|_2 = 1
$$

* $\|w\|_1 = \sum |w_i|$ → fomenta que muchos pesos sean **exactamente cero**.
* $\alpha > 0$ → controla cuánta dispersión imponemos:

  * $\alpha = 0$: recuperamos PCA clásico,
  * $\alpha$ grande: obtenemos vectores muy escasos, pero quizá con menor varianza capturada.

---

## 1.4 Diferencias clave entre PCA y SPCA

| Aspecto                      | PCA clásico                                | Sparse PCA                                          |
| ---------------------------- | ------------------------------------------ | --------------------------------------------------- |
| **Varianza explicada**       | Máxima posible                             | Algo menor (se sacrifica un poco)                   |
| **Combinación de variables** | Usa todas las variables                    | Usa pocas (sparse)                                  |
| **Interpretación**           | Difícil: cada componente es mezcla de todo | Fácil: cada componente involucra pocas variables    |
| **Aplicación práctica**      | Reducción de dimensionalidad “técnica”     | Interpretación y selección de variables importantes |

---

## 1.5 Métodos para resolver SPCA

Resolver SPCA es más complejo que PCA (ya no basta con autovectores).
Existen varios enfoques:

1. **Penalización L1 (LASSO-like):**

   * Se resuelve con técnicas de optimización convexa.
   * Implementado en scikit-learn (`SparsePCA`).

2. **Penalización combinatoria:**

   * Restringir explícitamente el número de variables no nulas en $w$.
   * Más difícil de optimizar (problema NP-hard).

3. **Métodos de rotación (varimax, etc.):**

   * Tras PCA, se aplican transformaciones para hacer más “sparse” los componentes.

---

## 1.6 Interpretación en minería de datos

Sparse PCA no solo reduce dimensionalidad, también actúa como una forma de **selección de características**:

* Identifica **qué variables importan más** en cada componente.
* Útil cuando:

  * Tenemos muchas variables correlacionadas,
  * Queremos explicar fenómenos en términos claros (ej. en biología: genes relevantes).

Ejemplo intuitivo:

* Dataset con 1000 genes → PCA mezcla todos.
* SPCA → cada componente podría estar relacionado con un subconjunto pequeño de genes → más interpretable.

---

## 1.7 Ejemplo sencillo (conceptual)

Supón que tienes 5 variables: $x_1, x_2, x_3, x_4, x_5$.

* **PCA clásico** podría dar un primer componente:

$$
v_1 = (0.45, 0.43, 0.40, 0.42, 0.47)
$$

👉 Difícil de interpretar, todas pesan parecido.

* **SPCA** podría dar:

$$
v_1 = (0.70, 0.65, 0, 0, 0)
$$

👉 Mucho más claro: el componente principal depende sobre todo de $x_1, x_2$.
(Quizá revelando que esas dos variables describen la variación principal).

---

## 1.8 Relación con PCA clásico

* SPCA **no reemplaza** PCA, sino que lo **extiende**.
* Cuando no hay restricción de dispersión ($\alpha = 0$), SPCA = PCA.
* Piensa en PCA como **"máxima compresión"** y en SPCA como **"compresión interpretable"**.

---

# 📋 En resumen

1. **Problema de PCA:** difícil de interpretar porque los componentes combinan todas las variables.
2. **Solución:** Sparse PCA añade restricciones de dispersión (L1) → componentes con pocos pesos no nulos.
3. **Ventaja:** más interpretabilidad, útil para selección de variables y análisis exploratorio.
4. **Costo:** se pierde algo de varianza explicada.
5. **Implementación:** se resuelve con optimización convexa → disponible en librerías como scikit-learn.

---

¿Quieres que te prepare también un **ejemplo práctico paso a paso** con un dataset pequeño (tipo el de 3D → 1D que ya hiciste en PCA) pero ahora comparando PCA vs SPCA, para que veas cómo cambia la interpretabilidad?
