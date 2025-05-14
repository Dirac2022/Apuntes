
# Overview

![[gaussian splatting demo.gif]]

Es un método para crear una escena 3D compleja usando un video o serie de imágenes. Hace uso de los llamados **Radiance Fields** como **NeRF** con una particularidad. 3D GS es más rápido de entrenar y se pueden lograr un mayor nivel de detalle. 3D GS logra representaciones de escenas en tiempo real de forma increíblemente rápida.

Usando un método matemático llamado **Structure-from-Motion** **[SfM](app://obsidian.md/Notes%20Paper%20Surver%203D%20Gaussian%20Splatting#Structure-from-Motion%20(SfM))** las diferencias entre estas imágenes se calculan para formar la nube de puntos 3D.

![[Structure from Motion.gif]]


cada punto se convierte en un **gaussiano 3D** (un elipsoide) Los gaussianos 3D tiene parámetros que les permiten entrar en un proceso de optimización iterativo que les permite afinarlos hasta que coincidan con las fotos originales ajustando sus posiciones 3D, la opacidad del color y **como varían sus detalles desde diferentes direcciones**.

El entrenamiento también utiliza un **Adaptative Density Control** (Control de densidad adaptativo), lo que significa que cuando un gaussiano es demasiado transparente, se elimina o cuando un gaussiano es demasiado grande para una parte detallada de la escena, se divide en dos.

![[under-over reconstruction gaussians.webp]]

Para ver estos gaussianos usamos una técnica llamada **[rasterizacion](app://obsidian.md/Notes%20Paper%20Surver%203D%20Gaussian%20Splatting#Rasterization)** que los proyecta sobre una superficie 2D.

![[Pipeline 3D GS.png]]

# Introduction

El objetivo de la reconstrucción de escenas 3D basada en imágenes es convertir una colección de vistas o videos que capturan una escena en un modelo 3D que puede ser procesado y entendido por computadoras.

- Modelado y animación 3D
- Navegación robótica
- Preservación histórica
- Realidad aumentada/virtual
- Conducción autónoma

Los primeros intentos de la reconstrucción de escenas 3D comenzó incluso antes del auge del Depp Learning con campos de luz  y métodos básicos de reconstrucción de escenas. **NeRF** presentó un nuevo enfoque que aprovecha las redes neuronales profundas, esto permite el mapeo directo de coordenadas espaciales a color y densidad. Sin embargo su implementación tenía un costo

- Intensidad computacional
- **Capacidad de edición**

Es en este contexto que aparece el 3D Gaussian splatting (GS), no como una mejora incremental sino como un nuevo enfoque.

3D GS ofrece una flexibilidad que permite controlar los objetos y la dinámica de la escena, un factor crucial en escenarios complejos que involucran geometrías intrincadas y condiciones de iluminación variables.

# Background

## Problem formulation
#### 2.1.1 Radiance Field
Un campo de radiancia es una representación de la distribución de luz en un espacio 3D, que captura cómo la luz interactúa con las superficies y materiales en el entorno.
Matemáticamente, un campo de radiancia puede describirse como una función $L : \mathbb{R}^5 \to \mathbb{R}^+$, donde $L(x, y, z, \theta, \phi)$ asigna un punto en el espacio $(x, y, z)$ y una dirección especificada por coordenadas esféricas $(\theta, \phi)$ a un valor de [[Notes Paper Surver 3D Gaussian Splatting#Radiancia|radiancia]] no negativo.

#### 2.1.2 Implicit Radiance Field
Un campo de radiancia implícito representa la distribución de la luz en una escena sin definir explícitamente la geometría de la misma. Por ejemplo, en NeRF, se emplea MLP, para mapear un conjunto de coordenadas espaciales $(x, y, z)$ y direcciones de visualización $(\theta, \phi)$ a valores de color y densidad.

La radiancia en cualquier punto no se almacena de forma explícita, sino que se calcula en tiempo real consultando el MLP. Por lo tanto, la función puede escribirse como:

$$L_{\text{implícito}}(x, y, z, \theta, \phi) = \text{MLP}(x, y, z, \theta, \phi). \tag{1}$$

Este formato permite una representación diferenciable y compacta de escenas complejas, aunque a menudo con el costo de una alta carga computacional debido al trazado volumétrico de rayos (_volumetric ray marching_).

#### 2.1.3 Explicit Radiance Field 
En contraste, un campo de radiancia explícito representa directamente la distribución de la luz en una estructura espacial discreta, como una cuadrícula de **[[Notes Paper Surver 3D Gaussian Splatting#Voxel|vóxeles]]** o un conjunto de puntos . Cada elemento en esta estructura almacena la información de radiancia correspondiente a su ubicación respectiva en el espacio. Esto permite un acceso más directo y, a menudo, más rápido a los datos de radiancia, pero a costa de un mayor uso de memoria y, potencialmente, una menor resolución.

Una forma genérica para la representación de un campo de radiancia explícito puede escribirse como:

$$L_{\text{explícito}}(x, y, z, \theta, \phi) = \text{DataStructure}[(x, y, z)] \cdot f(\theta, \phi), \tag{2}$$

donde **DataStructure** podría tener el formato de volúmenes, nubes de puntos, etc. **$f(\theta, \phi)$** es una función que modifica la radiancia en función de la dirección de visualización.


#### 2.1.4 3D Gaussian Splatting: Best-of-Both Worlds
Usa **gaussianas 3D** aprendibles como una representación flexible y eficiente. Estas gaussianas se optimizan bajo la supervisión de imágenes de múltiples vistas para representar con precisión la escena.

==Este pipeline diferenciable basado en gaussianas 3D combina los beneficios de la optimización basada en redes neuronales y el almacenamiento de datos explícitos y estructurados==.
La representación basada en gaussianas 3D se formula como:

$$L_{\text{3DGS}}(x, y, z, \theta, \phi) = \sum_i G(x, y, z, \mu_i, \Sigma_i) \cdot c_i(\theta, \phi), \tag{3}$$

donde $G$ es la función gaussiana con media $\mu_i$ y covarianza $\Sigma_i$, y $c$ representa el color dependiente de la vista.



## Context and Terminology

### Scene Reconstruction and Rendering
   - Reconstrucción: Crear modelos 3D desde imágenes o datos
   - Renderización: Transformar datos 3D en imágenes 2D
   - Base histórica: Radiance fields, Structure-from-Motion


![[Structure from Motion - medium.webp]]

### Neural Rendering and Radiance Fields
   - Combina deep learning con técnicas gráficas tradicionales
   - Radiance Fields: Describen la luz en cada punto del espacio
   - NeRFs: Usan redes neuronales (MLPs) para modelar estos campos

### Volumetric Representations and Ray-Marching
   - Modela objetos como volúmenes completos, no solo superficies
   - Útil para efectos como niebla o materiales translúcidos
   - Ray-marching: Técnica para trazar luz a través de volúmenes
   - Desventaja: Alto costo computacional

![[ray marching.gif]]


### Point-based Rendering
   - Usa puntos en lugar de polígonos
   - Efectivo para datos geométricos complejos
   - 3D GS mejora esto usando Gaussianos anisotrópicos
   - Proporciona representación más continua y cohesiva

Esta evolución de técnicas llevó al desarrollo de 3D Gaussian Splatting, que busca combinar las ventajas de estos enfoques mientras minimiza sus limitaciones.

# 3D GAUSSIAN SPLATTING: PRINCIPLES

Consideremos una escena representada por (millones de) gaussianas 3D optimizadas. El objetivo es generar una imagen desde una posición de cámara específica.

A diferencia de NeRF (volumetric ray marching) GS 3D comienza proyectando estas gaussianas 3D en un plano de imagen basado en píxeles, un proceso denominado "splatting". Después, el GS 3D ordena estas gaussianas y calcula el valor para cada píxel. El renderizado de NeRFs y GS 3D puede verse como un proceso inverso uno del otro.

![[Pasted image 20250113181039.png]]


1. **Comenzamos con la definición de una gaussiana 3D, que es el elemento mínimo de la representación de escena en GS 3D**
2. **Describimos cómo estas gaussianas 3D pueden usarse para renderizado diferenciable**
3. **Introducimos la técnica de aceleración utilizada en GS 3D, que es la clave para el renderizado rápido**


### Rendering with Learned 3D Gaussians
Una escena está representada por millones de Gaussianos 3D optimizados. El objetivo es generar una imagen desde una pose específica de cámara. A diferencia de NeRF que usa ray marching volumétrico, los Gaussianos 3D (3DGS) proyectan directamente sobre el plano de imagen.
#### Propiedades de un Gaussiano 3D

Cada Gaussiano 3D se caracteriza por:

| Propiedad                       | Descripción                     | Representación      |
| ------------------------------- | ------------------------------- | ------------------- |
| Centro ($\mu$)                  | Posición en espacio 3D          | Vector 3D           |
| Opacidad ($\alpha$)             | Transparencia                   | Escalar             |
| Matriz de Covarianza ($\Sigma$) | Forma 3D                        | Matriz 3x3          |
| Color ($c$)                     | Apariencia dependiente de vista | Armónicos esféricos |

![[Pasted image 20250113171733.png]]

#### Frustum Culling  
Determina qué Gaussianos están fuera del frustum de la cámara para optimizar recursos.

![[frustum culling.gif]]


#### Splatting (Proyección)

La proyección de Gaussianos 3D a 2D se realiza mediante:

$$\Sigma' = J W \Sigma W^T J^T$$

Donde:
- $\Sigma$: Matriz de covarianza 2D proyectada
- $W$: Transformación de vista
- $J$: Jacobiano de la transformación proyectiva

#### Renderización por Píxeles

El color final de un píxel se calcula mediante composición alfa:

$$C = \sum_{n=1}^{|N|} c_n \alpha'_n \prod_{j=1}^{n-1} (1-\alpha'_j)$$

La opacidad final $\alpha'_n$ se calcula como:

$$\alpha'_n = \alpha_n \times \exp(-\frac{1}{2}(x'-\mu'_n)^T {\Sigma'_n}^{-1} (x'-\mu'_n))$$


![[gaussian 3D.gif]]



Donde:
- $x'$: Coordenadas en espacio proyectado
- $\mu'_n$: Centro proyectado
- $\alpha_n$: Opacidad aprendida
- $c_n$: Color aprendido

#### Tiles (Patches)
- En lugar de procesar píxel por píxel, el sistema divide la imagen en cuadrados de 16×16 píxeles llamados "tiles"
- Si un Gaussiano 3D proyectado cubre varios tiles, se crea una copia para cada tile afectado
- Esto reduce significativamente la carga computacional

#### Renderizado paralelo
- Cada Gaussiano recibe un identificador de tile y un valor de profundidad
- Esta información se codifica en una estructura de bytes (ID en bits superiores, profundidad en bits inferiores)
- El procesamiento es independiente para cada tile, permitiendo paralelización
- Se aprovecha la arquitectura CUDA, tratando los tiles como bloques y los píxeles como threads
- Los píxeles dentro de un mismo tile comparten memoria, mejorando la eficiencia


![[Pasted image 20250113165507.png]]


![[Pasted image 20250113165521.png]]

### Optimization of 3D Gaussian Splatting

#### Parameter Optimization

##### Loss Function
Una vez completada la síntesis de la imagen, se puede medir la diferencia entre la imagen renderizada y ground truth (las imágenes reales o de referencia que se usan para entrenar el modelo). Todos los parámetros aprendibles se optimizan mediante descenso de gradiente estocástico usando las funciones de pérdida $\mathcal{l}_1$ y D-SSIM:

$$\mathcal{L} = (1-\lambda)L_1 + \lambda \mathcal{L}_{D-SSIM}  \tag{7}$$

Donde:
- $\lambda \in [0,1]$ es un factor de ponderación
- La función de pérdida de **3D GS** difiere de la de **NeRF**
- NeRF calcula la pérdida a nivel de píxel en lugar de nivel de imagen debido al costoso ray-marching

##### Parameter Update
   - La mayoría de las propiedades de un Gaussiano 3D pueden optimizarse directamente mediante retropropagación
   - Optimizar directamente la matriz de covarianza $\Sigma$ puede resultar en una matriz no semi-definida positiva

**Solución Propuesta**
   - Se optimiza un cuaternión $q$ y un vector 3D $s$
   - $q$ representa rotación
   - $s$ representa escala
   - La matriz de covarianza $\Sigma$ se reconstruye como:
     $$\Sigma = RSS^TR^T$$
   Donde:
   - $R$: Matriz de rotación (derivada de $q$)
   - $S$: Matriz de escalado (derivada de $s$)

3. **Grafo Computacional**
   - Existe un grafo computacional complejo para obtener la opacidad α:
     - $q \text{ y } s \to \Sigma$
     - $\Sigma \to \Sigma'$
     - $\Sigma' \to α$
   - Para evitar el costo de la diferenciación automática, 3D GS deriva los gradientes para $q$ y $s$ para calcularlos directamente durante la optimización

#### Density Control
##### Initialization
3D GS comienza con un conjunto inicial de puntos dispersos obtenidos de:
- Structure from Motion (SfM), o
- Inicialización aleatoria

Es importante notar que una buena inicialización es esencial para:
- La convergencia
- La calidad de la reconstrucción

##### Point Densification
Durante esta fase, 3D GS aumenta adaptativamente la densidad de Gaussianos para capturar mejor los detalles de una escena.

**Proceso**
1. Se realiza en intervalos regulares (después de cierto número de iteraciones)
2. Se enfoca en Gaussianos con grandes gradientes posicionales en el espacio de vista
3. Implica:
   - **Clonación**: Crear copias de Gaussianos pequeños en áreas sub-reconstruidas
   - **División**: Reemplazar Gaussianos grandes con dos más pequeños en regiones sobre-reconstruidas

Detalles:
- **Clonación**: La copia se mueve hacia el gradiente posicional
- **División**: Los nuevos Gaussianos tienen una escala reducida por un factor específico

##### Point Pruning
Es la eliminación de Gaussianos superfluos o menos impactantes, funcionando como proceso de regularización.

**Criterios de Eliminación**
1. Gaussianos virtualmente transparentes ($\alpha$ bajo un umbral específico)
2. Gaussianos excesivamente grandes en:
   - Espacio mundial (world-space)
   - Espacio de vista (view-space)

**Control de Densidad**
- El valor alfa de los Gaussianos se establece cerca de cero después de cierto número de iteraciones
- Esto previene aumentos injustificados en la densidad cerca de las cámaras de entrada

# APPLICATION AREAS

## Simultaneous Localization and Mapping (SLAM)
SLAM es un problema computacional central en robótica y sistemas autónomos. Implica el desafío de que un robot/dispositivo entienda su posición en un entorno desconocido mientras mapea simultáneamente el diseño del entorno.

3D GS entra en el dominio SLAM como un enfoque innovador para la representación de escenas. Los sistemas SLAM tradicionales a menudo usan nubes de puntos/surfels o rejillas de vóxeles  para representar entornos. En contraste, 3D GS utiliza Gaussianos anisotrópicos para representar mejor los entornos.

![[Pasted image 20250114190426.png]]
## Autonomous Driving
En la conducción autónoma, 3D GS se puede utilizar para reconstruir una escena mezclando puntos de datos en una representación cohesiva y continua. Esto es particularmente útil para:
- Manejar densidades variables de puntos de datos
- Asegurar una reconstrucción suave y precisa del fondo estático
- Representar objetos dinámicos en una escena


![[Pasted image 20250114190547.png]]