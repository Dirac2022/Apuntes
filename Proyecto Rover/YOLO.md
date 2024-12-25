You Only Look Once (YOLO) es un algoritmo de detección de objetos en tiempo real de última generación introducido en 2015 por Joseph Redmon, Santosh Divvala, Ross Girshick y Ali Farhadi en su famoso artículo de investigación **You Only Look Once: Unified, Real-Time Object Detection**.

Los autores enmarcan el problema de detección de objetos como una regresión en lugar de una tarea de clasificación mediante la separación espacial de cuadros delimitadores y la asociación de probabilidades a cada imagen detectada utilizando una sola red neuronal convolucional (CNN).

[Explicación de la detección de objetos YOLO: una guía para principiantes | Campamento de datos](https://www.datacamp.com/blog/yolo-object-detection-explained)

En el siguiente gráfico, observamos que YOLO está muy por encima de los otros detectores de objetos con 91 FPS.
![[Yolo comparative fps.png]]

<div style="text-align: center;">
<figure>
<img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Proyecto Rover\imgs\YOLO architecture.png">
<figcaption>
</figcaption>
YOLO Architecture
</figure>
</div>


La arquitectura funciona de la siguiente manera:

- Cambia el tamaño de la imagen de entrada a 448x448 antes de pasar por la red convolucional.
- Primero se aplica una convolución de 1x1 para reducir el número de canales, seguida de una convolución de 3x3 para generar una salida cuboidal.
- La función de activación bajo el capó es ReLU, a excepción de la capa final, que utiliza una función de activación lineal.
- Algunas técnicas adicionales, como la normalización de lotes y la deserción, regularizan el modelo y evitan que se sobreajuste.