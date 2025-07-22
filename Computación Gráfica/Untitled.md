Aquí tienes las respuestas detalladas a tus preguntas:

---

## 2. Sistema Visual Humano vs. Visión Computacional 👁️‍💻

El **sistema visual humano** es un sistema biológico increíblemente complejo y eficiente para procesar información visual. Sus componentes principales y sus análogos en la **visión computacional** se pueden describir de la siguiente manera:

**Sistema Visual Humano:**

1. **Ojo (Cámara Biológica):**
    - **Córnea y Cristalino (Lentes):** Enfocan la luz que entra al ojo. La córnea proporciona la mayor parte del poder refractivo, mientras que el cristalino ajusta el enfoque fino para diferentes distancias (acomodación).
        - _Ejemplo:_ Cuando miras un objeto lejano y luego uno cercano, el cristalino cambia de forma para mantener la imagen nítida.
    - **Iris y Pupila (Diafragma/Apertura):** El iris es un músculo coloreado que regula el tamaño de la pupila, controlando la cantidad de luz que ingresa al ojo. Se adapta a diferentes niveles de iluminación.
        - _Ejemplo:_ En un día soleado, la pupila se contrae; en la oscuridad, se dilata.
    - **Retina (Sensor de Imagen):** Es una capa sensible a la luz en la parte posterior del ojo que contiene células fotorreceptoras:
        - **Conos:** Responsables de la visión del color y la agudeza visual en condiciones de buena iluminación. Hay tres tipos, sensibles a diferentes longitudes de onda (rojo, verde, azul).
        - **Bastones:** Mucho más sensibles a la luz que los conos, permiten la visión en condiciones de baja luminosidad (visión escotópica), pero no distinguen colores.
        - _Ejemplo:_ En una habitación oscura, inicialmente no ves nada, pero después de un tiempo, los bastones se activan y comienzas a distinguir formas.
    - **Nervio Óptico (Cable de Transmisión):** Un haz de fibras nerviosas que transmite la información visual procesada por la retina desde el ojo hasta el cerebro. El punto donde el nervio óptico sale del ojo crea un "punto ciego" porque no hay fotorreceptores allí.
    - **Cerebro (Unidad de Procesamiento Principal - CPU/GPU Biológica):** Específicamente, el lóbulo occipital y otras áreas asociadas son responsables del procesamiento complejo de la información visual. Esto incluye el reconocimiento de formas, colores, movimiento, profundidad y la interpretación de escenas.
        - _Ejemplo:_ Reconoces la cara de un amigo instantáneamente, incluso si solo ves una parte de ella o está en un ángulo diferente.

**Visión Computacional:**

1. **Cámara (Sensor de Entrada):**
    - **Lente (Óptica):** Similar a la córnea y el cristalino, enfoca la luz del entorno sobre el sensor de imagen. Las cámaras pueden tener lentes fijas o intercambiables con diferentes distancias focales y capacidades de zoom.
    - **Diafragma (Apertura):** Controla la cantidad de luz que llega al sensor, análogo al iris y la pupila. Una apertura más grande (número f más pequeño) deja pasar más luz.
    - **Sensor de Imagen (CCD/CMOS):** Un chip electrónico que convierte la luz en señales eléctricas. Está compuesto por una matriz de píxeles, cada uno de los cuales mide la intensidad de la luz.
        - _Ejemplo:_ Las cámaras digitales usan sensores CMOS o CCD para capturar imágenes. Los filtros de color (como el patrón Bayer) sobre los píxeles permiten capturar información de color, similar a los conos.
    - **Cable/Interfaz de Datos (Bus de Datos):** Transmite los datos de la imagen desde la cámara a la unidad de procesamiento (por ejemplo, USB, MIPI CSI).
    - **Unidad de Procesamiento (CPU, GPU, FPGA, ASIC):** Ejecuta algoritmos para procesar y analizar los datos de la imagen. Esto puede incluir tareas como:
        - **Preprocesamiento:** Eliminación de ruido, ajuste de contraste.
        - **Segmentación:** Dividir la imagen en regiones u objetos significativos.
        - **Extracción de Características:** Identificar puntos clave, bordes, texturas.
        - **Reconocimiento de Objetos:** Identificar y clasificar objetos en la imagen (por ejemplo, usando redes neuronales convolucionales - CNNs).
        - **Seguimiento de Objetos:** Seguir el movimiento de objetos a lo largo del tiempo.
        - _Ejemplo:_ Un sistema de reconocimiento facial en un smartphone utiliza algoritmos para detectar una cara, extraer sus características y compararlas con una base de datos.

**Comparación y Diferencias Clave:**

|   |   |   |
|---|---|---|
|**Característica**|**Sistema Visual Humano**|**Visión Computacional**|
|**Sensor**|Retina (conos y bastones)|Sensor de imagen (CCD, CMOS)|
|**Adaptación Luz**|Iris/Pupila, adaptación química de fotorreceptores|Ajuste de apertura, tiempo de exposición, ISO|
|**Procesamiento**|Masivamente paralelo, integrado con la cognición|Algorítmico, secuencial o paralelo (GPU)|
|**Aprendizaje**|Experiencial, continuo, desde el nacimiento|Basado en datos (datasets), requiere entrenamiento explícito|
|**Interpretación**|Contextual, semántica, influenciada por la experiencia|Literal, basada en patrones aprendidos, puede carecer de contexto|
|**Robustez**|Alta robustez a variaciones, oclusiones, iluminación|Sensible a variaciones no vistas en el entrenamiento, ruido|
|**Consumo Energía**|Muy bajo|Puede ser alto, especialmente para procesamiento complejo|
|**Resolución**|Variable, alta en la fóvea, disminuye en la periferia|Uniforme, definida por el sensor|
|**Campo de Visión**|Amplio, con visión periférica|Generalmente más limitado, depende de la lente|

Aunque la visión computacional se inspira en el sistema visual humano, existen diferencias fundamentales. El cerebro humano realiza un procesamiento mucho más sofisticado y contextual que los sistemas actuales de visión por computadora. Sin embargo, la visión computacional puede superar al ser humano en tareas específicas como la detección de patrones muy sutiles o el trabajo en condiciones extremas (por ejemplo, imágenes infrarrojas o ultravioletas).

---

## 3. Filtros Pasa-Baja y Pasa-Alta en Cascada en el Dominio de la Frecuencia 📉📈

En el dominio de la frecuencia, aplicar un filtro a una imagen significa multiplicar la transformada de Fourier de la imagen por la función de transferencia del filtro.

Consideremos HPB​(u,v) como la función de transferencia de un **filtro pasa-baja** y HPA​(u,v) como la de un **filtro pasa-alta**. Un filtro pasa-baja ideal atenúa o elimina las altas frecuencias (detalles finos, ruido) y deja pasar las bajas frecuencias (componentes suaves, brillo general). Un filtro pasa-alta ideal hace lo contrario: atenúa o elimina las bajas frecuencias y deja pasar las altas.

**1. Pasa-Baja y luego Pasa-Alta:**

Si una imagen I(x,y) con transformada de Fourier F(u,v) primero pasa por un filtro pasa-baja y luego por un filtro pasa-alta, el resultado en el dominio de la frecuencia es:

G1​(u,v)=[F(u,v)⋅HPB​(u,vdisn)]⋅HPA​(u,v)=F(u,v)⋅HPB​(u,v)⋅HPA​(u,v)

Esto significa que primero se atenúan las altas frecuencias y luego, del resultado, se atenúan las bajas frecuencias. Idealmente, si el filtro pasa-baja elimina todas las frecuencias por encima de una frecuencia de corte $\omega_c_1$ y el filtro pasa-alta elimina todas las frecuencias por debajo de una frecuencia de corte $\omega_c_2$:

- Si $\omega_c_1 < \omega_c_2$ (el corte del pasa-baja es menor que el del pasa-alta), la mayoría o todas las frecuencias serían atenuadas, resultando en una imagen muy oscura o negra. Se crea una banda de rechazo entre $\omega_c_1$ y $\omega_c_2$.
- Si $\omega_c_1 > \omega_c_2$ (el corte del pasa-baja es mayor que el del pasa-alta), el resultado es un **filtro pasa-banda**, que permite el paso de frecuencias entre $\omega_c_2$ y $\omega_c_1$.

**2. Pasa-Alta y luego Pasa-Baja:**

Si la imagen pasa primero por un filtro pasa-alta y luego por un filtro pasa-baja, el resultado en el dominio de la frecuencia es:

G2​(u,v)=[F(u,v)⋅HPA​(u,v)]⋅HPB​(u,v)=F(u,v)⋅HPA​(u,v)⋅HPB​(u,v)

Dado que la multiplicación es conmutativa, **el orden de aplicación de los filtros lineales en cascada, en el dominio de la frecuencia, no altera el resultado final**. Es decir, G1​(u,v)=G2​(u,v). Aplicar un pasa-baja y luego un pasa-alta es matemáticamente equivalente a aplicar un pasa-alta y luego un pasa-baja, siempre que los filtros sean lineales e invariantes en el tiempo (LTI), lo cual es el caso de los filtros de frecuencia estándar.

**Casos de Igualdad y Distinción (Butterworth, Gaussiano, Ideal):**

- **Filtros Ideales:**
    
    - Un filtro pasa-baja ideal HPBI​​(u,v) es 1 para frecuencias ∣(u,v)∣≤D0​ (radio de corte) y 0 en caso contrario.
    - Un filtro pasa-alta ideal HPAI​​(u,v) es 0 para frecuencias ∣(u,v)∣≤D1​ y 1 en caso contrario. (O, a menudo, HPAI​​(u,v)=1−HPBI​​(u,v) si se usa la misma D0​).
    - Si HPAI​​(u,v)=1−HPBI​​(u,v) (con el mismo radio de corte D0​), entonces HPBI​​(u,v)⋅HPAI​​(u,v)=HPBI​​(u,v)⋅(1−HPBI​​(u,v)). Dado que HPBI​​ solo toma valores de 0 o 1, si HPBI​​=1, entonces 1⋅(1−1)=0. Si HPBI​​=0, entonces 0⋅(1−0)=0. El producto siempre será 0. Esto significa que la combinación de un filtro pasa-baja ideal y su complementario pasa-alta ideal (con el mismo corte) resulta en una imagen completamente negra (filtro rechaza-todo).
    - Si tienen diferentes frecuencias de corte (D0,LP​ y D0,HP​), el resultado es un **filtro pasa-banda** (si D0,LP​>D0,HP​) o un **filtro rechaza-banda más amplio** (o eliminación total si D0,LP​<D0,HP​). El orden no cambia el resultado.
    - _Ejemplo:_ Aplicar un pasa-baja ideal con corte en 50 Hz y luego un pasa-alta ideal con corte en 20 Hz es igual a aplicar primero el pasa-alta de 20 Hz y luego el pasa-baja de 50 Hz. El resultado es un filtro pasa-banda ideal que deja pasar frecuencias entre 20 Hz y 50 Hz.
- **Filtros Butterworth y Gaussianos:**
    
    - Estos filtros tienen transiciones más suaves entre la banda de paso y la banda de rechazo.
        - Pasa-baja Butterworth: HPBB​​(u,v)=1+[D(u,v)/D0​]2n1​
        - Pasa-alta Butterworth: HPAB​​(u,v)=1+[D0​/D(u,v)]2n1​ (o 1−HPBB​​ si se deriva de un PB).
        - Pasa-baja Gaussiano: HPBG​​(u,v)=e−D(u,v)2/(2D02​)
        - Pasa-alta Gaussiano: HPAG​​(u,v)=1−e−D(u,v)2/(2D02​)
    - Para estos filtros no ideales, el producto HPB​(u,v)⋅HPA​(u,v) también formará una especie de **filtro pasa-banda**. La forma exacta de la banda dependerá de las frecuencias de corte (D0​) y, en el caso de Butterworth, del orden (n) de cada filtro.
    - **El resultado es igual independientemente del orden de aplicación** porque la multiplicación de sus funciones de transferencia en el dominio de la frecuencia es conmutativa: HPB​(u,v)⋅HPA​(u,v)=HPA​(u,v)⋅HPB​(u,v).
    - _Ejemplo:_ Si aplicas un filtro pasa-baja Gaussiano y luego un filtro pasa-alta Gaussiano (incluso con diferentes D0​), el efecto combinado es el mismo que si los aplicaras en orden inverso. El resultado será una atenuación tanto de las muy bajas como de las muy altas frecuencias, permitiendo que una banda intermedia de frecuencias pase con mayor amplitud. La suavidad de los filtros Gaussiano y Butterworth evita los artefactos de "ringing" que pueden ocurrir con los filtros ideales.

En resumen, **en el dominio de la frecuencia, para filtros lineales, el orden de aplicación de un filtro pasa-baja y un filtro pasa-alta en cascada no cambia el resultado final del filtrado**. El efecto combinado es generalmente un filtro pasa-banda (si las frecuencias de corte están configuradas para permitir una banda intermedia) o un filtro que atenúa aún más las frecuencias (si las bandas de rechazo se superponen significativamente). Esto es válido para filtros ideales, Butterworth y Gaussianos. La diferencia entre estos tipos de filtros radica en la forma de sus funciones de transferencia (abrupta para el ideal, suave para Butterworth y Gaussiano), lo que afecta la selectividad y los posibles artefactos en la imagen filtrada en el dominio espacial.