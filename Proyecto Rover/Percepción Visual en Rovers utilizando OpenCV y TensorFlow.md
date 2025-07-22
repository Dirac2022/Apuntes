
La percepción visual es una capacidad crítica en rovers autónomos, permitiéndoles detectar obstáculos y reconocer objetos en su entorno. Este artículo investiga el uso de visión computacional y aprendizaje profundo mediante las bibliotecas de OpenCV y TensorFlow en Python. Exploramos cómo OpenCV se emplea para el procesamiento de imágenes, mientras que TensorFlow facilita la clasificación mediante redes neuronales, proporcionando a los rovers una capacidad visual robusta y adaptable para la navegación autónoma

# ¿Qué es OpenCV?
OpenCV (Open Source Computer Vision Library) es una biblioteca de software de visión artificial y aprendizaje automático de código abierto. OpenCV se creó para proporcionar una infraestructura común para aplicaciones de visión artificial y para acelerar el uso de la percepción de máquinas en los productos comerciales.

La biblioteca cuenta con más de 2500 algoritmos optimizados, que incluyen un conjunto completo de algoritmos clásicos y de última generación de visión por computadora y aprendizaje automático. 

Los usos desplegados de OpenCV abarcan toda la gama, desde la unión de imágenes de StreetView, la detección de intrusiones en videos de vigilancia en Israel, el monitoreo de equipos mineros en China, la ayuda a robots a navegar y recoger objetos en Willow Garage, la revisión de pistas en busca de escombros en Turquía, la inspección de etiquetas en productos en fábricas de todo el mundo hasta la detección rápida de rostros en Japón.


# ¿Qué es TensorFlow?
TensorFlow es una librería de open source para Machine Learning. Fue desarrollado por Google. TensorFlow te permite construir y entrenar redes neuronales para detectar patrones y razonamientos usados por los humanos.

TensorFlow es multiplataforma, lo que permite trabajar con GPUs y CPUs e incluso con las unidades de procesamiento de tensores TPUs.

# OpenCV para detección de bordes
La detección de bordes es una técnica que nos ayuda a identificar cambios significativos en la intensidad de una imagen, lo que corresponde a las fronteras de los objetos presentes. El algoritmo de Canny es un popular algoritmo de detección de bordes. Fue desarrollado por John F. Canny.

## Etapas del algoritmo de Canny

### 1. Reducción del ruido
La detección de bordes en sensible al ruido presente en la imagen, Por ello el primer paso es suavizar la imagen utilizando un filtro Gaussiano de 5x5, lo que ayuda a eliminar el ruido y facilita la detección de bordes reales.

### 2. Calculo del gradiente de intensidad
Después de suavizar la imagen, se aplican filtros Sobel en las direcciones horizontal y vertical para obtener las derivadas $G_x$ y $G_y$. Con estas derivadas, se calcula la magnitud y dirección del gradiente en cada pixel:

$$
\text{Magnitud del gradiente} \, (G) = \sqrt{G_x^2 + G_y^2}
$$

$$
\text{Dirección del gradiente} \, (\theta) = \tan^{-1} \left( \frac{G_y}{G_x} \right)
$$
### 3. Supresión de no máximos
Este paso tiene como objetivo afinar los bordes detectados. Se examina cada pixel para determinar si es un máximo local en la dirección del gradiente. Si un pixel no es un máximo local, se suprime (se establece a cero), lo que resulta en bordes más delgados y precisos.

<div style="text-align: center;">
	<figure>
    <img src="https://docs.opencv.org/4.x/nms.jpg">
    <figcaption>El punto A está en el borde (en dirección vertical). La dirección del gradiente es perpendicular al borde. Los puntos B y C están en las direcciones del gradiente. Entonces, el punto A se compara con los puntos B y C para ver si forma un máximo local. Si es así, se considera para la siguiente etapa; de lo contrario, se suprime (se establece en cero).</figcaption>
    </figure>
</div>


### 4. Umbralización con histéresis
Se aplican dos umbrales: uno alto y uno bajo. Los pixeles con una magnitud de gradiente superior al umbral alto se consideran bordes fuertes y, por lo tanto, se mantienen. Los pixeles con una magnitud de gradiente entre los dos umbrales se consideran bordes débiles y se mantienen solo si están conectados a un borde fuerte. Los pixeles con una magnitud de gradiente inferior al umbral bajo se descartan,

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Proyecto Rover\umbralizacion.png">
    <figcaption></figcaption>
    </figure>
</div>


# Implementación de detección de bordes


### Tabla de posibles configuraciones de umbrales y su efecto

```python
edges = cv2.Canny(img, threshold1, threshold2)
```

| Umbral mínimo `threshold1` | Umbral máximo `threshold2` | Efecto en la detección de bordes                                |
| -------------------------- | -------------------------- | --------------------------------------------------------------- |
| 50                         | 150                        | Detecta más bordes, incluyendo ruido.                           |
| 100                        | 200                        | Detección de bordes moderada, buena para imágenes claras.       |
| 150                        | 250                        | Detecta solo bordes más definidos, puede perder detalles finos. |

# Procesamiento de imágenes en OpenCV
En el procesamiento de imágenes, estas se transforman para que sean más fáciles de analizar. Esto mejora la calidad visual y la relevancia de la información.

## Técnicas comunes en Procesamiento de Imágenes
En OpenCV, usamos varías técnicas para procesar imágenes. Algunas son:

- **Eliminación de ruido**: mejora la calidad de la imagen.
- **Ajuste de colores**: modifica la luminosidad y contraste.
- **Convolución**: Aplica filtros para destacar características.

- La función `waitKey()` detiene el programa hasta que el usuario actúa.
- `destroyAllWindows()` cierra todas las ventanas

| Técnica              | Aplicación en OpenCV                      |
| -------------------- | ----------------------------------------- |
| Eliminación de ruido | Usada en la función ``GaussianBlur()``    |
| Ajuste de colores    | Aplicada con ``cv2.convertScaleAbs()``    |
| Convolución          | Implementada a través de `cv2.filter2D()` |


# Modelos de detección de objetos
Los tres principales modelos de detección de objetos que se usan en la actualidad son **Faster R-CNN**, **YOLO** y **SSD**. Cada uno con sus propias ventajas y desventajas en términos de complejidad, velocidad, precisión y eficiencia.

### Faser R-CNN (Region-bases CNN)
Es un modelo de detección de objetos de dos etapas que primero propone regiones de interés y luego clasifica. Si bien las Faster R-CNN brindan resultados precisos, su velocidad se ve comprometida debido al proceso de dos etapas.

### YOLO (You Only Look Once)
Es un modelo de una sola etapa que predice probabilidades de clase y cuadros delimitadores en una sola pasada. Los modelos YOLO son conocidos por su velocidad excepcional, capaces de realizar inferencias en tiempo real, pero pueden sacrificar algo de precisión en comparación con otros modelos

### SSD (Single Shot MultiBox Detector)
También es un modelo de una etapa que realiza la detección en múltiples escalas dentro de una sola red. Logra un equilibrio entre la velocidad de YOLO y la precisión de las Faster R-CNN.

### Comparación entre modelos

| Modelo       | Complejidad | Velocidad | Exactitud | Eficiencia      |
| ------------ | ----------- | --------- | --------- | --------------- |
| Faster R-CNN | Alto        | Lento     | Alto      | Menos eficiente |
| YOLO         | Medio       | Rapido    | Medio     | Eficiente       |
| SSD          | Bajo        | Rapido    | Alto      | Eficiente       |


# Implementación de Detección de objetos

Usaremos `ssd_mobilenet_v2_320x320_coco17_tpu-8` como modelo de detección de objetos preentrenado disponible en TensorFlow. Combina el algoritmo de detección de objetos SSD con la arquitectura de red neuronal MobileNetV2. 
## Estructura del Proyecto

ROVER-TAREA3
│
├─ venv/  # Entorno virtual de Python
│   ├─ Include/
│   ├─ Lib/
│   ├─ Scripts/
│   └─ pyvenv.cfg
│
├─ pretrained_models/
│   └─ ssd_mobilenet_v2_320x320_coco17_tpu-8/
│       ├─ checkpoint/
│       ├─ saved_model/
│       ├─ mscoco_label_map.pbtxt  # Archivo de mapeo de etiquetas de COCO
│       └─ pipeline.config  # Archivo de configuración del modelo
│
├─ Scripts/
│   └─ script.py  # Script principal de Python

## Código

### Librerías
Usaremos `imutuls.video` como librería que nos ayudará con el procesamiento de video.
Librerías usadas
```python
from imutils.video import VideoStream
from imutils.video import FPS
import imutils
import tensorflow as tf
import numpy as np
import cv2
import time
```

### Cargamos el modelo
El modelo preentrenado convolucional  `ssd_mobilenet_v2_320x320_coco17_tpu-8` para la detección de objetos, esta cuenta con 80 objetos comunes.
```python
model = tf.saved_model.load("./pretrained_models/ssd_mobilenet_v2_320x320_coco17_tpu-8/saved_model")
```

### Método para leer el archivo de mapeo de etiquetas
```python
def read_label_map(label_map_path):
    item_id = None
    item_name = None
    items = {}
    
    with open(label_map_path, 'r') as file:
        for line in file:
            line.replace(" ", "")
            if line == "item{":
                pass
            elif line == "}":
                pass
            elif "id" in line:
                item_id = int(line.split(":", 1)[1].strip())
            elif "display_name" in line:
                item_name = line.split(":", 1)[1].replace("'", "").strip()
                
            if item_id is not None and item_name is not None:
                items[item_id] = item_name
                item_id = None
                item_name = None
    
    return items
```

### Asignamos colores a cada clase
- Definimos un diccionario `class_names` con los nombres de las clases
- En `class_colors` asignamos colores aleatorios a cada clase para visualizar las cajas delimitadoras en la imagen
```python
class_names = read_label_map("./pretrained_models/ssd_mobilenet_v2_320x320_coco17_tpu-8/mscoco_label_map.pbtxt")
class_colors = np.random.uniform(0, 255, size=(len(class_names), 3))
```

### Inicialización de la cámara
Se inicializa la cámara usando `VideoStream` de `imutils`, se da un tiempo de espera para que se estabilice y se empieza a contar los FPS
```python
if __name__ == '__main__':
	# Creamos un flujo de video (vs) usando VideoStream de imutils.video, que
    # recuperara las imagenes de la camara
    print("Start camera ...")
    vs = VideoStream(src=0, resolution=(1600, 1200)).start()
    time.sleep(2.0)
    fps = FPS().start()
```

A su vez, presentamos estas opciones:
- Mediante una cámara de Rasperry PI:
```python
vs = VideoStream(usePiCamera=True, resolution=(1600, 1200)).start()
```
- Mediante un archivo de video
```python
vc = cv2.VideoCapture('./data/Splash - 23011.mp4') # ruta del video
```

#### Loop principal
Dentro del bloque anterior:
- Es necesario convertir el formato de imágenes de BGR (OpenCV) a RGB (TensorFlow)
```python
while True:

	# Capturamos un frame de la camara
	img = vs.read()
	img = imutils.resize(img, width=800)
	img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

	h, w, _ = img.shape
	input_tensor = np.expand_dims(img, 0)

	resp = model(input_tensor)

	# Validar si hay detecciones con un puntaje superior al umbral
	detections_made = False
```


##### Bucle que itera  los resultados de la detección de objetos
Dentro del bucle principal

- `resp['detection_boxes']` contiene las coordenadas normalizadas de las cajas delimitadoras para cada objeto detectado
- `resp['detection_classes']` contiene los índices de las clases de los objetos detectados.
- `resp['detection_scores']` contiene los puntajes de confianza de las detecciones

```python
for boxes, classes, scores in zip(resp['detection_boxes'].numpy(), resp['detection_classes'], resp['deteccion_scores'].numpy()):

	for box, cls, score in zip(boxes, classes, scores):
		if score > 0.61: # Umbral de confianza
			detections_made = True
			# Coordenadas de la caja delimitadora
			ymin = int(box[0] * h)
			xmin = int(box[1] * w)
			ymax = int(box[2] * h)
			xmax = int(box[3] * w)


		cls = int(cls)
		if cls in class_names:
		label = "{}: {:.2f}%".format(class_names[cls], score * 100)
		cv2.putText(img, label, (xmin, ymin-10), 
					cv2.FONT_HERSHEY_SIMPLEX, 1, 
					class_colors[cls], 1)
		print("Class_name: ", class_names[cls])

		X = (xmax + xmin) / 2
		Y = (ymax + ymin) / 2
		poslbl = "X: ({}, {})".format(X, Y)
		cv2.circle(img, (int(x) - 15, int(Y)), 1, class_colors[cls], 2)
		cv2.putText(img, poslbl, 
					(int(X), int(Y)),
					cv2.FONT_HERSHEY_SIMPLEX, 0.5, class_colors[cls], 2)

		# Dibujamos la caja delimitadora
		cv2.rectangle(img, (xmin, ymin), (xmax, ymax), class_colors[cls], 4)
```

##### Comprobación de detecciones realizadas
```python
# Si no hay detecciones, continuar mostrando el cuadro sin procesar
if not detections_made:
	print("[INFO] No se detectaron objetos en este cuadro")

```

##### Mostramos el frame y capturamos la entrada de teclado
```python
cv2.imshow("Frame", img)
key = cv2.waitKey(1) & 0xFF
if key == ord("q"):
	break

fps.update()
```

### Parte final
- Detenemos el contador de FPS
- Mostramos estadísticas
- Liberamos los recursos
```python
fps.stop()
print("[INFO] elapsed time: {:.2f}".format(fps.elapsed())) # Tiempo transcurrido
print("[INFO] approx. FPS: {:.2f}".format(fps.fps())) # FPS promedio
cv2.destroyAllWindows()
vs.stop()
```



# Referencias

- [About - OpenCV](https://opencv.org/about/)
- [¿Qué es TensorFlow y para qué sirve?](https://www.incentro.com/es-ES/blog/que-es-tensorflow)
- [OpenCV: Canny Edge Detection](https://docs.opencv.org/4.x/da/d22/tutorial_py_canny.html)
- [YOLOv8 vs SSD: Cómo elegir el modelo de detección de objetos adecuado](https://keylabs-ai.translate.goog/blog/yolov8-vs-ssd-choosing-the-right-object-detection-model/?_x_tr_sl=en&_x_tr_tl=es&_x_tr_hl=es&_x_tr_pto=sge#:~:text=YOLOv8%20and%20SSD%20are%20popular,simpler%20architecture%20compared%20to%20YOLOv8.)
- [Visión por Computadora con OpenCV: Desde la Teoría a la Práctica](https://lovtechnology.com/vision-por-computadora-con-opencv-desde-la-teoria-a-la-practica/)
- https://www.aranacorp.com/es/reconocimiento-de-objetos-con-tensorflow-y-opencv/

