Emocionarse por aprender ROS y trabajar con robots que utilizan ROS, como ==Baxter y TurtleBot==, es el comienzo de una gran aventura. Las características y beneficios de ROS son significativos, pero la curva de aprendizaje es pronunciada. A través de prueba y error, hemos recorrido un camino por muchas de las aplicaciones de ROS, probando de todo. En este libro, esperamos presentarte lo mejor de nuestro conocimiento sobre ROS y ofrecerte instrucciones detalladas paso a paso para tu camino. Nuestro enfoque se centra en el uso de los robots ROS que destacamos, concretamente TurtleBot, Baxter, Crazyflie y Bebop, así como robots simulados como Turtlesim y Hector.

Este libro proporciona información introductoria, así como aplicaciones avanzadas que presentan estos robots de ROS. Los capítulos comienzan con lo básico, como configurar tu computadora y cargar ROS y los paquetes para los robots y herramientas de ROS. Se proporcionan instrucciones claras, junto con pasos para solucionar problemas cuando no se obtienen los resultados deseados. Los fundamentos de ROS se describen primero con la simulación de Turtlesim y luego con cada uno de los robots presentados. Comenzando con los comandos básicos de ROS, se exploran los paquetes de ROS, nodos, temas y mensajes para obtener un conocimiento general de estos sistemas robóticos de ROS. Se proporciona información técnica sobre estos robots de ejemplo para describir todas las capacidades del robot.

ROS abarca todo un espectro de conceptos de software, implementación y herramientas que intentan proporcionar una visión homogénea de los complejos sistemas e integración de software que se requieren en robótica. Ya están disponibles amplias bibliotecas de controladores e interfaces de sensores y actuadores, así como los algoritmos más recientes y eficientes. Lo que ROS no proporciona directamente se importa de otros proyectos de código abierto prevalentes, como OpenCV. ROS también cuenta con una gama de herramientas que ahorran tiempo para controlar, monitorear y depurar aplicaciones robóticas: rqt, rviz, Gazebo, dynamic reconfigure y MoveIt, por nombrar algunas. En las páginas que siguen, cada una de estas áreas se presentará de forma incremental al lector como parte de los ejemplos de robots. ==Con TurtleBot, se exploran los temas de navegación y mapeo. Usando Baxter, se describen el control de articulaciones y la planificación de rutas para que lo comprendas==. Se incluyen simples scripts en Python para proporcionar ejemplos de implementación de elementos de ROS para muchos de estos robots. Todos estos robots están disponibles en simulación para realizar los ejercicios de este libro. Además, se ofrecen instrucciones para que puedas construir y controlar tus propios modelos de robots en simulación.

El poder de ROS, la variedad de robots que usan ROS y la diversidad y el apoyo de la extensa comunidad de ROS hacen que esta aventura valga la pena. Hay disponibles extensos tutoriales en línea, instrucciones en wikis, foros y trucos y consejos para ROS. ¡Así que sumérgete en las páginas de este libro para comenzar tu aventura con la robótica de ROS!

Por ejemplo, para mover los brazos de un robot, se emite un comando de ROS o se escriben scripts en Python o C++ por los diseñadores del robot, lo que hace que el robot responda como se le ha ordenado. Los scripts, a su vez, pueden llamar a varios programas de control que provocan el movimiento real de los brazos del robot. También es posible diseñar y simular tu propio robot utilizando ROS. Estos temas y muchos otros se tratarán en este libro. 

En este libro, aprenderás un conjunto de conceptos, software y herramientas que se aplican a un ejército cada vez mayor y más diverso de robots. Por ejemplo, el software de navegación de un robot móvil se puede utilizar, con algunos cambios, para funcionar en otro robot móvil. La navegación de vuelo de un robot aéreo es similar a la de un robot terrestre, y así sucesivamente. A lo largo del amplio espectro de la robótica, las interfaces del sistema están estandarizadas o se actualizan para soportar una mayor complejidad. Hay bibliotecas fácilmente disponibles para funciones comunes en robótica. ROS no solo se aplica al procesamiento central de la robótica, sino también a los sensores y otros subsistemas. La abstracción de hardware en ROS, combinada con el control de dispositivos de bajo nivel, acelera la actualización hacia las últimas tecnologías.

==ROS es un sistema de software robótico de código abierto que puede ser utilizado sin costos de licencia por universidades, agencias gubernamentales y empresas comerciales==. Las ventajas del software de código abierto son que el código fuente del sistema está disponible y puede modificarse según las necesidades del usuario. Más importante aún para algunos usuarios, el software puede usarse en un producto comercial siempre que se citen las licencias correspondientes. El software puede mejorarse y los usuarios y empresas pueden agregar módulos.

ROS es utilizado por muchos miles de usuarios en todo el mundo y el conocimiento puede compartirse entre ellos. Los usuarios van desde aficionados hasta desarrolladores profesionales de robots comerciales. Además del gran grupo de investigadores de ROS, existe un grupo llamado ROS-Industrial dedicado a aplicar el software de ROS a robots para manufactura. ==Otras versiones de ROS que se encuentran en desarrollo actualmente incluyen:
- **ROS-M** para sistemas robóticos militares
- **H-ROS**, un ROS de hardware para componentes robóticos interoperables
- **ROS 2.0** para actualizar ROS con las últimas tecnologías y software==

### ¿Quién controla ROS?

Una distribución de ROS es un conjunto de paquetes de software de ROS que se pueden descargar a tu computadora. Estos paquetes son respaldados por la **Open Source Robotics Foundation (OSRF)**, una organización sin fines de lucro. Las distribuciones se actualizan periódicamente y se les asignan nombres diferentes por la organización de ROS. Más detalles sobre la organización de ROS están disponibles en: [http://www.ros.org/about-ros/](http://www.ros.org/about-ros/).

### ¿Qué robots están usando ROS?

Hay una larga lista de robots en el sitio web del wiki de ROS, [http://wiki.ros.org/Robots](http://wiki.ros.org/Robots), que utilizan ROS. Por ejemplo, en este libro utilizamos cuatro robots diferentes para proporcionarte una experiencia con una amplia gama de capacidades de ROS. Estos robots son los siguientes:

==- **TurtleBot**, un robot móvil==
==- **Baxter**, un robot amigable de dos brazos==
==- **Crazyflie** y **Bebop**, robots voladores==

**Nodos, tópicos y mensajes en ROS**

Aquí exploraremos algunos de los componentes principales de ROS. Uno de los principales propósitos de ROS es facilitar la comunicación entre los nodos de ROS. Estos nodos representan el código ejecutable. El código puede residir completamente en una computadora, o los nodos pueden distribuirse entre varias computadoras o entre computadoras y robots. La ventaja de esta estructura distribuida es que cada nodo puede controlar un aspecto específico de un sistema.

Por ejemplo, un nodo puede capturar imágenes de una cámara y enviar las imágenes a otro nodo para su procesamiento. Después de procesar la imagen, el segundo nodo puede enviar una señal de control a un tercer nodo para controlar un manipulador robótico en respuesta a la vista de la cámara.

El mecanismo principal que utilizan los nodos de ROS para comunicarse es enviando y recibiendo mensajes. Los mensajes se organizan en categorías específicas llamadas **tópicos**. Los nodos pueden publicar mensajes en un tópico particular o suscribirse a un tópico para recibir información.

### **Nodos en ROS**

Básicamente, los nodos son procesos que realizan algún cálculo o tarea. Los nodos son en realidad procesos de software, pero con la capacidad de registrarse en el **nodo Maestro** de ROS y comunicarse con otros nodos en el sistema. La idea de diseño de ROS es que cada nodo sea independiente y se comunique con otros nodos utilizando la capacidad de comunicación de ROS. El nodo Maestro se describe en la sección sobre el **Maestro de ROS** más adelante.

Una de las fortalezas de ROS es que una tarea en particular, como controlar un robot móvil con ruedas, puede dividirse en una serie de tareas más simples. Las tareas pueden incluir la percepción del entorno usando una cámara o un escáner láser, la creación de mapas, la planificación de una ruta, la monitorización del nivel de la batería del robot y el control de los motores que impulsan las ruedas del robot. Cada una de estas acciones podría consistir en un nodo de ROS o una serie de nodos para cumplir con tareas específicas.

Un nodo puede ejecutar de manera independiente código para realizar su tarea, pero también puede comunicarse con otros nodos enviando o recibiendo mensajes. Los mensajes pueden consistir en datos, comandos u otra información necesaria para la aplicación.

### **Tópicos en ROS**

Algunos nodos proporcionan información para otros nodos, como haría un nodo de cámara, por ejemplo. Dicho nodo se dice que "publica" información que puede ser recibida por otros nodos. La información en ROS se denomina **tópico**. Un tópico define los tipos de mensajes que se enviarán sobre ese tópico.

Los nodos que transmiten datos publican el nombre del tópico y el tipo de mensaje que se enviará. El nodo publica los datos reales. Un nodo puede suscribirse a un tópico, y los mensajes transmitidos sobre ese tópico son recibidos por el nodo que se ha suscrito.

Siguiendo con el ejemplo de la cámara, el nodo de la cámara puede publicar la imagen en el tópico `camera/image_raw`. Los datos de la imagen del tópico `camera/image_raw` pueden ser usados por un nodo que muestra la imagen en la pantalla de la computadora. El nodo que recibe la información se dice que se "suscribe" al tópico que se publica, en este caso, `camera/image_raw`.

En algunos casos, un nodo puede tanto publicar como suscribirse a uno o más tópicos.

### **Mensajes en ROS**

Los mensajes de ROS se definen por el tipo de mensaje y el formato de los datos. El paquete de ROS llamado `std_msgs`, por ejemplo, tiene mensajes del tipo `String`, que consisten en una cadena de caracteres. Otros paquetes de mensajes para ROS tienen mensajes usados para la navegación de robots o sensores robóticos. El paquete `turtlesim` tiene su propio conjunto de mensajes que se relacionan con la simulación.

Veremos en la sección **Turtlesim - la primera simulación de robots en ROS** que el simulador Turtlesim crea dos nodos cuando se ejecuta. Turtlesim tiene relativamente pocos tópicos y mensajes, por lo que es ideal para el estudio inicial de ROS.

El sitio de ROS [http://www.ros.org/core-components/](http://www.ros.org/core-components/) describe las características de comunicación y específicas de los robots en ROS. Aquí exploraremos algunos de los componentes principales de un sistema ROS, incluyendo nodos de ROS y el nodo Maestro de ROS. Es importante que entiendas los **nodos**, **tópicos** y **mensajes** de ROS, ya que están involucrados en casi todas las actividades de ROS.

### **El nodo Maestro de ROS**

Los nodos de ROS son típicamente programas independientes que pueden ejecutarse simultáneamente en varios sistemas. El nodo Maestro de ROS proporciona servicios de **nombres y registro** a los nodos en el sistema ROS. Rastrea a los publicadores y suscriptores de los tópicos. La comunicación se establece entre los nodos mediante el nodo Maestro de ROS.

El rol del nodo Maestro es permitir que los nodos individuales de ROS se localicen entre sí. El protocolo más utilizado para la conexión es el **Protocolo de Control de Transmisión/Protocolo de Internet (TCP/IP)** estándar, llamado **TCPROS** en ROS. Una vez que los nodos pueden localizarse entre sí, pueden comunicarse entre sí de forma **peer-to-peer** (de igual a igual).

Una de las responsabilidades del nodo Maestro es rastrear los nodos cuando se ejecutan nuevos nodos y entran en el sistema. Así, el nodo Maestro proporciona una asignación dinámica de conexiones. Los nodos, sin embargo, no pueden comunicarse hasta que el nodo Maestro notifique a los nodos de la existencia de los demás. Un ejemplo sencillo se puede ver en [http://wiki.ros.org/Master](http://wiki.ros.org/Master).