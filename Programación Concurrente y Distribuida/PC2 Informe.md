

# 1. Portada
* **Nombre del Proyecto:** Space Invaders Multijugador en Red
* **Asignatura:** CC4P1 Programación Concurrente y Distribuida
* **Alumno(s):** Mitchel Soto, Jared Orihuela, Yoel Mantari
* **Fecha:** 06-05-2025

# 2. Resumen (Abstract)
El proyecto "Space Invaders Multijugador en Red" se centra en la creación de un videojuego que revive el clásico arcade de Space Invaders, pero con la adición de un modo multijugador que permite a varios usuarios competir en tiempo real. El objetivo principal es desarrollar una versión funcional que no solo emule la experiencia original del juego, sino que también ofrezca una plataforma para que los jugadores interactúen y compitan entre sí. Para lograr esto, se utilizó Java Sockets para la comunicación en red y Swing para la interfaz gráfica, lo que permitió una implementación fluida y eficiente del juego. La metodología empleada incluye una arquitectura cliente-servidor, donde el servidor gestiona el estado del juego y la lógica, mientras que los clientes se encargan de la interfaz de usuario y la entrada del jugador. Los resultados obtenidos incluyen un juego completamente funcional en red, con características como movimiento de naves, disparos, lógica de enemigos, niveles y un sistema de puntuación, todo ello probado en un entorno de red real utilizando Ngrok para facilitar la conectividad externa.

# 3. Introducción
## 3.1. Contexto y Objetivos:
Space Invaders es un clásico videojuego de arcade que ha dejado una huella indeleble en la historia de los videojuegos desde su lanzamiento en 1978. Este juego, diseñado por Toshihiro Nishikado, se ha convertido en un ícono cultural, conocido por su jugabilidad adictiva y su innovador enfoque en la mecánica de disparo. La motivación para este proyecto surge de la Práctica 02 de CC4P1, donde se busca implementar una versión multijugador en red que permita a los jugadores competir entre sí. El objetivo principal es desarrollar una versión multijugador en red de Space Invaders, permitiendo a varios usuarios jugar simultáneamente, cada uno controlando una nave y compitiendo por la puntuación más alta. Este enfoque no solo busca recrear la experiencia original del juego, sino también enriquecerla al permitir la interacción entre jugadores, lo que añade un nivel de competitividad y diversión. La implementación de un sistema de puntuación y niveles también busca incentivar a los jugadores a mejorar sus habilidades y estrategias a medida que avanzan en el juego.

## 32. Alcance del Proyecto:
El alcance del proyecto abarca una serie de funcionalidades implementadas que son esenciales para la experiencia de juego. Estas incluyen el movimiento de las naves, el disparo de balas, la lógica de enemigos que se mueven y disparan, la gestión de múltiples jugadores, la progresión a través de niveles y un sistema de puntuación que recompensa a los jugadores por sus acciones. Las tecnologías clave utilizadas en este proyecto son Java SDK, Sockets para la comunicación en red, Swing para la creación de la interfaz gráfica y Ngrok para facilitar la conectividad externa. Se busca que el juego sea accesible y divertido, manteniendo la esencia del original mientras se adapta a las expectativas modernas de los jugadores.

# 4. Diseño y Arquitectura del Sistema
## 4.1. Arquitectura General (Cliente-Servidor):
La arquitectura del sistema se basa en un modelo cliente-servidor, donde el servidor actúa como el núcleo del juego, gestionando el estado del juego y la lógica, mientras que los clientes se encargan de la interfaz gráfica y la entrada del usuario. El servidor es responsable de mantener la coherencia del estado del juego, asegurando que todos los jugadores vean la misma información en tiempo real. Cada cliente se conecta al servidor y recibe actualizaciones sobre el estado del juego, lo que permite que todos los jugadores interactúen de manera sincronizada. Esta arquitectura no solo permite una experiencia de juego fluida, sino que también facilita la escalabilidad, ya que se pueden agregar más clientes sin necesidad de modificar la lógica del servidor. Además, el uso de hilos en el servidor permite manejar múltiples conexiones simultáneamente, lo que es crucial para un juego multijugador.

## 4.2. Diseño de Componentes:
* **Servidor:** La lógica principal del servidor se implementa en la clase `Servidor.java`, que gestiona las conexiones mediante `ServerSocket` y `ClientHandler`. El servidor controla el bucle de juego, actualiza el estado del juego y envía las actualizaciones a todos los clientes conectados. Además, se encarga de la lógica de puntuación y de la gestión de los niveles del juego. La implementación del servidor permite manejar la lógica del juego de manera centralizada, lo que facilita la sincronización de los estados de los jugadores y la gestión de eventos en tiempo real.
* **Cliente:** La clase `Cliente.java` maneja la conexión al servidor y la interfaz gráfica del usuario. Utiliza `JFrame` y `GamePanel` para mostrar el estado del juego y permite a los jugadores enviar acciones como mover su nave o disparar. La comunicación con el servidor se realiza a través de sockets, lo que permite un intercambio de datos eficiente. La interfaz gráfica se diseñó para ser intuitiva y fácil de usar, permitiendo a los jugadores concentrarse en la jugabilidad.
* **Modelo del Juego:** Las clases principales como `GameObject`, `Player`, `Alien`, `Bullet`, y `GameState` representan los elementos del juego. `GameObject` es una clase abstracta que define las propiedades y métodos comunes a todos los objetos del juego, mientras que las clases derivadas como `Player` y `Alien` implementan comportamientos específicos. `GameState` mantiene el estado actual del juego, incluyendo la lista de jugadores, aliens y balas activas. Este modelo permite una fácil extensión y modificación de los elementos del juego, facilitando la implementación de nuevas características en el futuro.

## 4.3. Protocolo de Comunicación y Concurrencia:
Se utiliza `ObjectInputStream` y `ObjectOutputStream` para la serialización de `GameState` y `MessageAction`, lo que permite enviar y recibir objetos complejos a través de la red. El servidor maneja hilos mediante `ExecutorService` para gestionar múltiples clientes y el bucle de juego, asegurando que cada cliente pueda interactuar sin interferir con los demás. El cliente tiene un hilo de escucha que recibe actualizaciones del servidor y actualiza la interfaz gráfica en consecuencia. Se implementa sincronización para garantizar un acceso seguro a los datos compartidos, evitando condiciones de carrera y asegurando la integridad del estado del juego. Este enfoque permite que el juego funcione de manera eficiente y estable, incluso con múltiples jugadores conectados simultáneamente.

# 5. Implementación y Tecnologías
## 5.1. Entorno y Lenguaje:
Se utilizó Java SE Development Kit (versión JDK 8+) para el desarrollo del proyecto, aprovechando sus características de programación orientada a objetos y su robusto soporte para la programación en red. El entorno de desarrollo elegido fue Visual Studio Code y Sublime Text. 

## 5.2. Módulos Principales:
* `Servidor.java`: Contiene la lógica principal del servidor, gestionando las conexiones de los clientes y el bucle de juego. Esta clase es responsable de mantener el estado del juego y de enviar actualizaciones a todos los clientes conectados.
* `Cliente.java`: Maneja la conexión al servidor y la interfaz del cliente, permitiendo a los jugadores interactuar con el juego. Esta clase se encarga de recibir el estado del juego y de enviar las acciones del jugador al servidor.
* `ClientHandler.java`: Se encarga de gestionar la comunicación con cada cliente conectado, procesando las acciones enviadas y enviando el estado del juego. Esta clase permite que el servidor maneje múltiples clientes de manera eficiente.
* `GamePanel.java`: Se utiliza para renderizar el juego, mostrando los elementos gráficos en la pantalla. Esta clase es responsable de la representación visual del juego y de la actualización de la interfaz gráfica.
* `GameState.java`: Representa el estado del juego, incluyendo la lista de jugadores, aliens y balas activas. Esta clase es fundamental para mantener la coherencia del estado del juego entre el servidor y los clientes.
* `Player.java`, `Alien.java`, `Bullet.java`, `Boss.java`: Clases que representan los objetos del juego, cada una con sus propias propiedades y métodos. Estas clases permiten la creación y gestión de los elementos del juego de manera modular.

## 5.3. Networking y Conectividad:
Se implementó la comunicación utilizando `java.net.Socket` y `java.net.ServerSocket`, lo que permite establecer conexiones entre el servidor y los clientes. La implementación de la comunicación se basa en objetos serializables, lo que facilita el intercambio de datos complejos. Ngrok se utilizó para facilitar las pruebas y permitir que los jugadores se conecten a través de internet, proporcionando una URL pública que los clientes pueden utilizar para unirse al juego. 

### 3.4. Interfaz Gráfica y Animación:
La interfaz gráfica se construyó utilizando Java Swing, que permite crear ventanas y componentes interactivos de manera sencilla. El juego se renderiza en `GamePanel` mediante el método `paintComponent`, que se llama cada vez que se necesita actualizar la pantalla. La animación se logra mediante actualizaciones frecuentes del estado del juego, lo que permite que los movimientos y disparos se vean fluidos y responsivos. Se implementaron técnicas de doble buffer para evitar parpadeos en la pantalla y mejorar la experiencia visual del jugador.

## 6. Pruebas y Guía de Ejecución
## 6.1. Pruebas Realizadas:
Se realizaron pruebas funcionales exhaustivas que incluyen la conexión de múltiples clientes, el movimiento de las naves, el disparo de balas, la puntuación y la sincronización del estado del juego. Se llevaron a cabo pruebas en un escenario con hasta 3 jugadores en diferentes máquinas a través de Ngrok, lo que permitió verificar la estabilidad y la funcionalidad del juego en un entorno de red real. Las pruebas también incluyeron la verificación de la lógica de puntuación y la correcta actualización del estado del juego en todos los clientes. Se documentaron los resultados de las pruebas para identificar áreas de mejora y asegurar que el juego cumpla con los requisitos establecidos.

## 6.2. Guía de Compilación:
El comando `javac` se utilizó para compilar el proyecto. Se proporcionaron instrucciones detalladas sobre cómo compilar el proyecto desde la línea de comandos, asegurando que cualquier persona pueda replicar el proceso sin problemas.

## 6.3. Guía de Ejecución:
* **Servidor:** Para iniciar el servidor, se debe ejecutar el comando correspondiente en la terminal, especificando el puerto en el que se desea escuchar. El servidor debe estar en ejecución antes de que los clientes intenten conectarse. Se proporcionaron ejemplos de comandos y configuraciones recomendadas para facilitar el proceso.
* **Cliente (local):** Se debe ejecutar el cliente con los parámetros adecuados para conectarse al servidor en la misma máquina, utilizando la dirección `127.0.0.1` y el puerto configurado. Se incluyeron instrucciones sobre cómo iniciar el cliente y qué esperar al conectarse.
* **Cliente (remoto con Ngrok):** El servidor utiliza Ngrok para obtener una URL pública. Los clientes remotos deben utilizar esta URL junto con el puerto proporcionado por Ngrok para conectarse al servidor, lo que permite que jugadores de diferentes ubicaciones se unan al juego sin complicaciones. Se proporcionaron pasos detallados sobre cómo configurar Ngrok y cómo los jugadores pueden unirse al juego utilizando la URL generada.


# 7. Conclusiones y Trabajo Futuro
### 7.1. Conclusiones:
El proyecto cumplió con los objetivos establecidos, logrando un juego funcional que permite la interacción multijugador. Se adquirieron conocimientos valiosos sobre programación en red, diseño de juegos y la implementación de interfaces gráficas. La experiencia de trabajar en este proyecto ha sido enriquecedora, permitiendo aplicar conceptos teóricos en un contexto práctico. Además, se logró crear un ambiente de juego competitivo y divertido, lo que demuestra la viabilidad de la implementación de juegos multijugador en red utilizando tecnologías accesibles.

### 7.2. Dificultades y Soluciones:
Se enfrentaron desafíos relacionados con la sincronización de datos y la conectividad de red. Estos problemas se abordaron mediante el uso de `synchronized` para garantizar un acceso seguro a los datos compartidos y la implementación de Ngrok para facilitar las pruebas de conectividad. La experiencia adquirida en la resolución de estos problemas será invaluable para futuros proyectos. También se identificaron áreas de mejora en la gestión de errores y la experiencia del usuario, lo que permitirá un desarrollo más robusto en el futuro.

### 7.3. Posibles Mejoras (Trabajo Futuro):
Se podrían implementar más niveles, enemigos con inteligencia artificial más compleja, power-ups, un sistema de chat integrado y persistencia de puntuaciones. Además, se podría considerar la posibilidad de añadir efectos de sonido y música de fondo para mejorar la experiencia del jugador. La implementación de un sistema de logros también podría aumentar la motivación de los jugadores y fomentar la competencia. Otras mejoras podrían incluir la optimización del rendimiento del juego y la expansión de la jugabilidad a través de nuevos modos de juego, como cooperativo o competitivo.

## 8. Anexos (Opcional)
* [Enlace al repositorio de código](#) (si aplica).
* Capturas de pantalla del juego en acción, mostrando diferentes momentos del juego y la interacción entre los jugadores. Se pueden incluir gráficos que representen la evolución del desarrollo del proyecto y su progreso a lo largo del tiempo.