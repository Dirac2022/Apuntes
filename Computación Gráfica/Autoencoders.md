
---

Aplicaciones

- Detección de anomalías (ECG) - Anomaly detection
- Eliminación de ruido (daños) Data denoising (ex. images, audio)
- Reconstrucción de Imágenes - Image inpainting
- Encontrar información - Information retrieval

---

Propiedades

- **Sensible a las entradas lo suficiente como para construir una reconstrucción con precisión.**
- **Lo suficientemente insensible a las entradas como para que el modelo no simplemente memorice o sobreajuste a los datos de entrenamiento**

---

Función de perdida

Un término restringe al modelo a ser sensible a las entradas (es decir, pérdida de reconstrucción) y un segundo termino restringe la memorización/sobreajuste (regularizador).

$$
L(x, \hat{x}) + \text{regularizer}
$$
---


Tipos

- Incompleto (Undercomplete)
- Disperos (Sparse)
- Sin ruido (Denoising)

---

**Auntoenconders Incompleto**

- Idealmente, esta aquitectura aprenderá y describirá los atributos latentes de la imagen.

![[Pasted image 20250711050157.png]]


Se puede ver como una generalización de PCA.
**Mientras que PCA intenta descubrir un hiperplano de dimensiones inferiores que describa los datos originales, los autoencoders son capaces de aprender variedades no lineales**

![[Pasted image 20250711050340.png]]

---


**Autoencoders - Disperso**

![[Pasted image 20250711050453.png]]


Funcion de perdida

- Regularizacion L1
$$
L(x, \hat{x}) + \lambda \sum_i |a_i^{(h)}|
$$

- Distancia KL

$$
L(x, \hat{x}) + \sum_j KL (\rho | \hat{\rho}_j)
$$
---

Autoencoders - Denoising

![[Pasted image 20250711051310.png]]
Más bien, el modelo aprende un campo vectorial para mapear los datos de entrada hacia una variedad de dimensiones inferiores.

Si esta variedad describe con precisión los datos naturales, efectivamente habremos "cancelado" el ruido agregado.

