
# Dispositivos

## Switch core
Los switches core son un tipo de conmutador de alta capacidad que generalmente se coloca dentro de la red troncal o núcleo físico de una red. Sirven como puerta de acceso a una red de área amplia ([[Redes/Introducción#Redes de área amplia (WAN)|WAN]]) o Internet proporcionan el punto de acceso final para la red y permiten que varios módulos de agregación trabajen juntos.
<div style="text-align: center;">
	<figure>
		<img src="https://www.qualisit.com.ar/fotos_news/1499456214foto_01.jpg" alt="Texto alternativo de la imagen"> 
		<figcaption>Switch core</figcaption> 
	</figure> 
</div>

## Switch (conmutador)
Es un dispositivo de red que opera en la capa de enlace de datos (capa 2 del modelo OSI). Es utilizado para conectar equipos en red formando lo que se conoce como una red de área local [[Redes/Introducción#Redes de área local (LAN)|LAN]] y cuyas especificaciones técnicas siguen el estándar conocido como Ethernet (o técnicamente IEEE 802.3).
<div style="text-align: center;">
	<figure>
		<img src="https://www.instaladoresdetelecomhoy.com/imagenes/2023/02/switches-DELL.jpg"> 
		<figcaption>Switch</figcaption> 
	</figure> 
</div>

### Comparación con Switch core

|Característica|Switch|Switch Core|
|---|---|---|
|Capa de operación|Principalmente Capa 2|Capas 2 y 3|
|Ubicación en la red|Local, segmentos pequeños|Centro, red completa|
|Función|Conexión de dispositivos locales|Manejo del tráfico principal, interconexión de redes|
|Volumen de tráfico|Moderado|Alto|
|Complejidad|Baja a moderada|Alta|

En resumen, mientras que los switches comunes facilitan la comunicación dentro de segmentos locales de una red, los switches core son esenciales para gestionar y dirigir el tráfico en toda la red, soportando una mayor carga de datos y proporcionando funciones avanzadas de conectividad y redundancia.

## Gateway (puerta de enlace)
Es un dispositivo o software que actúa como intermediario entre dos redes diferentes, permitiendo la comunicación entre ellas. Su función principal es traducir los protocolos de comunicación utilizados en una red para que sean comprensibles por los dispositivos en otra red.
<div style="text-align: center;">
	<figure>
		<img src="https://ameclat.com/wp-content/uploads/2020/03/DAG10004FXO_3.png" width = 400 height = 400> 
		<figcaption>Gateway</figcaption> 
	</figure> 
</div>

## Access Point (Punto de acceso)
Es un dispositivo de red utilizado para conectar dispositivos inalámbricos, como computadoras portátiles, teléfonos inteligentes, tabletas y otros dispositivos habilitados  para Wi-Fi, a una red cableada existente o a Internet. El AP actúa como un intermediario entre los dispositivos inalámbricos y la red cableada, permitiendo la comunicación entre ellos.
<div style="text-align: center;">
	<figure>
		<img src="https://www.kroton.com.pe/wp-content/uploads/2016/11/EAP110-1-600x600.jpg" width=300 height=300> 
		<figcaption>Acceso Point TP-LINK</figcaption> 
	</figure> 
</div>

**Características**:
- Transmisión de señal inalámbirca
- Seguridad (WPA2)
- Gestión de usuarios
- Conectividad a la red cableada

## Router (Enrutador)
Es un dispositivo de red que se utiliza para interconectar diferentes redes informáticas y dirigir el tráfico de datos entre ellas. Su función principal es tomar paquetes de datos provenientes de una red y enviarlos a su destino correcto en otra red. Los paquetes de datos tienen varias capas o secciones una de ellas transporta la información de identificación, como emisor, tipo de datos, tamaño y, aún más importante, la dirección [[Protocolos#IP (Internet Protocol)|IP]] de destino El router prioriza los datos y elige la mejor ruta para cada transmisión.
<div style="text-align: center;">
	<figure>
		<img src="https://oechsle.vteximg.com.br/arquivos/ids/14226279-1000-1000/image-281962fac812406a9d7cdb52485c7909.jpg?v=638153364498770000" width=350 height=400> 
		<figcaption>Router TP-LINK</figcaption> 
	</figure> 
</div>

**Subred**: En un principio, su único significado era el de una colección de enrutadores y líneas de comunicación que transmitían paquetes desde el host de origen hasta el host de destino. 

Al proceso por el cual la red decide qué ruta tomar se le conoce como **algoritmo de enrutamiento** La manera en que cada enrutador toma la decisión de hacia dónde debe enviar el siguiente paquete se le denomina **algoritmo de reenvío**.

## Concentrador (Hub)

Un concentrador, también conocido como hub en inglés, es un dispositivo de red que actúa como un punto central para la conexión de múltiples dispositivos en una red local. Su función principal es recibir datos de un dispositivo y retransmitirlos a todos los demás dispositivos conectados a través de puertos individuales. Aunque fue ampliamente utilizado en el pasado, ha sido en gran medida reemplazado por dispositivos más avanzados como los switches en redes modernas.
<div style="text-align: center;">
	<figure>
		<img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjT0NhzUe6Mt6OkRsTzjGOFOm5YSqc-xDs2AdIrRByLs6ZAQxm45sTq7m-YRStyU1SAQJbhJd31_n-6-4gvanmuSDlfOckR98CMYYDNSCun-KzcshyphenhyphenYrZLLfLh7N0fx4HkUSqaUpWScA280/s1600/Selecci%25C3%25B3n_090.png"> 
		<figcaption>Hub</figcaption> 
	</figure> 
</div>

# Tecnologías

## VPN (Virtual Private Networks)
Es una tecnología que permite crear una conexión segura y cifrada entre un dispositivo y una red privada a través de Internet. Esto se logra mediante el uso de protocolos de cifrado y tunelización que protegen la información transmitida a través de la conexión VPN. Características: cifrado de datos, ocultamiento de la dirección IP, acceso a redes privadas, sorteo de restricciones geográficas.

## RFID (Identificación por Radio-Frecuencia
Son chips pasivos (es decir, no tienen batería) del tamaño de estampillas y ya es posible fijarlos a libros, pasaportes, mascotas, tarjetas de crédito y demás artículos en el hogar y fuera de él. Esto permite a los lectores RFID localizar los artículos y comunicarse con ellos a una distancia de hasta varios metros, dependiendo del tipo de RFID.

## XWindow (X Window System)

X Window System, comúnmente conocido como X Window, X11 o simplemente X, es un sistema de ventanas que proporciona una infraestructura estándar y un entorno gráfico para sistemas operativos tipo Unix y Unix-like. Fue desarrollado en el Massachusetts Institute of Technology (MIT) a principios de la década de 1980 y se ha convertido en el estándar de facto para la interfaz gráfica de usuario (GUI) en sistemas Unix y derivados.

Algunas características importantes de X Window System incluyen:

1. **Arquitectura Cliente-Servidor**: X Window sigue un modelo cliente-servidor, donde un servidor X se ejecuta en la máquina que maneja la pantalla, el teclado y el ratón, mientras que las aplicaciones (clientes X) se ejecutan en otras máquinas y se comunican con el servidor para dibujar ventanas y elementos gráficos en la pantalla.

2. **Protocolo de Comunicación**: X utiliza un protocolo de comunicación de red llamado X11 para facilitar la comunicación entre el servidor X y los clientes X. Este protocolo permite que las aplicaciones gráficas se ejecuten de manera remota en una red y se muestren en una pantalla local.

3. **Gestión de Ventanas**: X Window proporciona un conjunto de herramientas y bibliotecas para la creación y gestión de ventanas, iconos, menús, botones y otros elementos de la interfaz gráfica de usuario. Los administradores de ventanas, como X Window Managers, se utilizan para gestionar el diseño y el comportamiento de las ventanas en el entorno gráfico.

4. **Extensibilidad y Flexibilidad**: X es altamente modular y extensible, lo que permite a los desarrolladores crear y personalizar entornos gráficos según sus necesidades. Se pueden agregar extensiones al protocolo X11 para habilitar características adicionales, como aceleración de hardware, transparencia, efectos visuales, etc.

Aunque X Window System ha sido el estándar predominante en entornos Unix y Linux durante décadas, en los últimos años han surgido alternativas como Wayland, que buscan mejorar aspectos como la eficiencia, la seguridad y la integración con tecnologías modernas de gráficos y dispositivos. Sin embargo, X Window sigue siendo ampliamente utilizado y es compatible con una amplia variedad de aplicaciones y entornos de escritorio en sistemas Unix y derivados.


## ATM (Asynchronous Transfer Mode)
Es una tecnología de comunicación de datos que se utiliza en redes de telecomunicaciones para transmitir voz, datos y video de manera eficiente y confiable. Fue desarrollada en la década de 1980 y estandarizada por el ITU-T bajo la recomendación ATM (ITU-T I.361).

Algunos aspectos importantes sobre ATM son:

1. **Celdas:** ATM divide la información en unidades de datos llamadas celdas. Cada celda tiene un tamaño fijo de 53 bytes, con 48 bytes para la carga útil de datos y 5 bytes para la cabecera. Esta estructura fija de celdas facilita la transmisión eficiente y predecible de datos.

2. **Conexiones Virtuales:** ATM utiliza conexiones virtuales para establecer rutas lógicas entre nodos de la red. Estas conexiones pueden ser de dos tipos: conexiones virtuales permanentes (PVC) y conexiones virtuales conmutadas (SVC). Las PVC son conexiones preestablecidas y permanentes, mientras que las SVC se establecen dinámicamente según la demanda de tráfico.

3. **Velocidades de Transferencia:** ATM puede operar a velocidades que van desde 1.5 Mbps hasta varios Gbps (gigabits por segundo), lo que lo hace adecuado para aplicaciones que requieren altas tasas de transferencia de datos, como videoconferencia, transmisión de video de alta definición (HD), acceso a Internet de alta velocidad, entre otros.

4. **Calidad de Servicio (QoS):** ATM ofrece mecanismos avanzados de calidad de servicio para garantizar la entrega confiable y oportuna de datos. Esto incluye la asignación de prioridades a diferentes tipos de tráfico, la gestión de la congestión y la garantía de ancho de banda mínimo para aplicaciones críticas.

5. **Aplicaciones:** ATM ha sido utilizado en una variedad de aplicaciones, incluyendo redes de área amplia (WAN), redes de acceso a Internet, redes de telefonía y videoconferencia, y en entornos empresariales donde se requiere una comunicación confiable y de alta velocidad.

Aunque ATM fue una tecnología ampliamente adoptada en el pasado, su uso ha disminuido en favor de tecnologías como Ethernet y redes IP, que ofrecen mayor flexibilidad y escalabilidad. Sin embargo, ATM sigue siendo relevante en ciertos entornos donde se requiere calidad de servicio garantizada y altas velocidades de transmisión de datos.


