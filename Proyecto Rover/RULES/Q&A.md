
## 1. porque caminio verde y el otro rojo

La imagen hace referencia al ERC 2024, el documento no explica el porqué de los colores rojo y verde

![[Pasted image 20250302223750.png]]
*Figura 7: Ejemplo de Subtarea de Travesía basada en ERC 2024. Comience desde el punto S4, alcance los puntos A-B-C-D y regrese a la línea de salida.*

## 2. el dron realmente apoya al rover? si es asi como?

Si, el dron sobrevuela la superficie para apoyar las actividades de reconocimiento de la superficie marciana, detectando posibles obstáculos. El dron tiene también que encontrar una sonda sellada que contiene material marciano, la cual será enviada de regreso a la Tierra. El dron también deberá aterrizar en caso de una tormenta de arena y luego continuar con la misión hasta llegar al **MLMOD** (Martian Lander Module)

Según las reglas, página 18 (Navigation Task (Sub-Tasks included: Traverse, Droning):
[[Competition Rules#Tarea de Navegación (Subtareas incluidas Travesía, Droning)]]

**Tarea de Navegación (Subtareas incluidas: Travesía, Droning)**
Cuando todas las tareas de Ciencia planificadas hayan finalizado, el rover debe encontrar el camino de regreso al **MLMOD (Módulo de Aterrizaje Marciano)** para entregar las muestras recolectadas que se enviarán de regreso a la Tierra. ==Según la ubicación actual del rover establecida con los datos del sistema de posicionamiento satelital en la MMO (Órbita Media de Marte), la pista de regreso al módulo de aterrizaje se cargó en la computadora del rover==. La travesía debe realizarse en modo autónomo debido al ancho de banda limitado y los retrasos encontrados al controlar el rover manualmente desde la Tierra.

Durante las actividades de travesía (en algunas de las ubicaciones en el camino y debido al terreno difícil) también se requiere utilizar el dron que forma parte del rover que aterrizó en Marte. ==La tarea principal del dron es sobrevolar la superficie de Marte para apoyar las actividades de reconocimiento, es decir, detectar posibles obstáculos que impidan el movimiento del rover, así como evaluar el valor del terreno en términos de futuras actividades de muestreo==. El dron que se mueve de forma autónoma tendrá que encontrar una sonda sellada que contenga material marciano que será enviado de regreso a la Tierra para su posterior investigación. Debido a la probabilidad de una tormenta de arena, también debería ser posible aterrizar temporalmente en un lugar seguro y luego continuar la misión. ==El destino del dron será MLMOD.==

## 3. para que te dan los autorcu si no puedo ver, y como llego al lugar destinado? solo por entrar a la región e interés?nesecito tener el mapa bien mapeado al final de recorriedo? investigar que realmente te dan unos días antes de la competencias, osea como te dan el mapa.


- Los **ArUco** son visibles para las cámaras del rover (si se puede xd) y pueden ser detectados por sensores de proximidad.

- Cito el texto exacto, la sección **7.1.1.4 Información adicional**, inciso g) Los detalles de la tarea, como la apariencia exacta de los puntos de referencia, la ubicación, el formato del mapa, los tipos de puntos de referencia y balizas personalizados permitidos, etc., se discutirán con los equipos y se presentarán durante la fase de diseño preliminar en las reglas. Se anima a los equipos a iniciar y participar activamente en estas discusiones. 

- El mapa final con coordenadas de cuadricula y POIs (Punto de interés) se proporcionará el día de calentamiento, si no se acuerda lo contrario. 
	> El día de calentamiento es el día anterior al desafío. Este día debe utilizarse para la calibración y otras actividades de preparación. El organizador dará a cada equipo un intervalo de tiempo limitado dentro del cual los equipos pueden realizar cualquier tipo de medición acordada con el organizador y basada en las especificaciones del informe final
## 4. explicar todas la imagenes

Las imágenes hacen referencia al ERC 2024 no hay más detalle o explicación que la propia descripción de las imágenes.

## 5. de que sirve saber el código ArUco si es que lo uso? ósea de que me sirve saber que numero o id es; o da otra información aparte de esa?

Los marcadores ArUco pueden ser fácilmente detectados por cámaras del rover y sensores de proximidad, supuestamente esto es una ayuda para la navegación y localización del rover. Al detectar el marcador, el sistema puede calcular su posición relativa a la cámara.  
## 6. la tarea de ciencias y navegación participan juntas? o como se llega al lugar donde se hacen muestras?

Si, y no xd. Son independientes, cada tarea es independiente, es decir, se evalúan por separado. Sin embargo, en las tareas de ciencias obviamente se necesita la navegación del rover, por ejemplo:


En la [[Competition Rules#7.3.1.1 Subtarea de Exploración Científica|Subtarea de Exploración Científica]] en la parte 3 **Exploración Científica**, se debe hacer un recorrido para detectar objetos potencialmente interesantes. De ahí viene como referencia la imagen del bisonte, pero sin contexto

![[Pasted image 20250302221757.png]]
*Figura 2: Ejemplo de Exploración Científica basada en ERC 2024. Comience desde el punto S1, explore el Mars Yard con el descubrimiento de huevos de Pascua y características geológicas, y finalmente regrese a S1.*


En la [[Competition Rules#7.3.1.3 Subtarea de Muestreo Profundo|Subtarea de Muestreo Profundo]] y [[Competition Rules#7.3.1.2 Subtarea de Muestreo Superficial|Subtarea de Muestreo Superficial]]
En el escenario de la tarea, los pasos 1 y 7
- 1. Llegar a la ubicación de muestreo
- 7. Conducir a la línea de salida/meta 

En la [[Competition Rules#7.3.1.4 Subtarea de Astro-Bio|Subtarea de Astro-Bio]]
- **Parte 1: Ciencia - Elección del Sitio de Medición**: Cuando el equipo esté listo para comenzar la prueba, los jueces entregarán el mapa de Marte con cinco ubicaciones marcadas. Estas ubicaciones corresponderán a los cinco sitios de medición de los cuales el equipo tendrá que elegir uno. Todos los sitios de medición estarán en el área designada del Mars Yard.


Además en la sección de Tareas de ciencia [[Competition Rules#7.3.1.1 Subtarea de Exploración Científica|Subtarea de Exploración Científica]] se detalla que se proporcionará los siguientes datos para los informes, resalto este punto:
- 3. **Imágenes de drones del Mars Yard junto con el modelo de elevación digital del área que se entregarán a más tardar tres semanas antes de las finales de ERC.**


## 7. en algum momento el rover se comunica con el dron o con otro organismo?

No se menciona en el documento que el rover se comunique directamente con el dron o con otro organismo. Sin embargo, en el capítulo **7.1.1.2 Subtarea de Droning**, se explica que el dron tiene la tarea de apoyar al rover en la detección de obstáculos y la evaluación del terreno. Aunque no se especifica una comunicación directa entre el rover y el dron, ambos trabajan en conjunto para completar las tareas de la competencia.

No encontré información al respecto.