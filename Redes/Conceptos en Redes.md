
# Ancho de Banda
El ancho de banda se refiere a la cantidad de datos que pueden ser transmitidos en una conexión de red en un período de tiempo dado. En términos más simples, el ancho de banda determina la velocidad máxima a la que se pueden enviar y recibir datos a través de una conexión de red. Cuanto mayor sea el ancho de banda, más datos podrán ser transmitidos en un período de tiempo determinado, lo que generalmente se traduce en una conexión más rápida y eficiente.

El ancho de banda depende de:
- Propiedades de medios físicos.
- Tecnologías de señalización y detección de señales de red.

| Unidad de Ancho de Banda | Abreviatura | Equivalencia  |
| ------------------------ | ----------- | ------------- |
| Bits por segundo         | bps/s       | $1$ bps       |
| Kilobits por segundo     | kbps/s      | $10^3$ bps    |
| Megabits por segundo     | Mbps        | $10^6$ bps    |
| Gigabits por segundo     | Gbps        | $10^9$ bps    |
| Terabits por segundo     | Tbps        | $10^{12}$ bps |


# Latencia
La latencia se refiere al tiempo que transcurre desde que se envía una solicitud hasta que se recibe una respuesta. En el contexto de la informática y las redes, la latencia se mide en milisegundos (ms) y representa el retraso que experimenta la comunicación entre dos dispositivos o sistemas.
## Latencia de red
Es el tiempo que tarda un paquete de datos en viajar desde un punto de origen hasta un punto de destino a través de una red. Este tipo de latencia puede estar influenciada por factores como la distancia física, la congestión de la red, la calidad de la conexión y la velocidad de transmisión.
## Latencia de almacenamiento
Se refiere al tiempo que tarda un sistema en acceder y recuperar datos almacenados en un dispositivo de almacenamiento, como un disco duro o una unidad de estado sólido (SSD). La latencia de almacenamiento está determinada por factores como la velocidad de rotación del disco, la tecnología de almacenamiento utilizada y la complejidad de las operaciones de lectura y escritura
## Latencia de procesamiento
Es el tiempo que tarda un sistema en procesar una solicitud o ejecutar una tarea después de recibirla. Esta latencia puede estar influenciada por la capacidad de procesamiento del sistema, la eficiencia del software utilizado y la complejidad de la tarea a realizar.


# Rendimiento de transferencia (Performance)

El rendimiento de transferencia, también conocido como rendimiento de red o simplemente performance en el contexto de redes de computadoras, se refiere a la medida de la eficiencia y velocidad con la que los datos pueden ser transmitidos a través de una red de computadoras. Es una métrica fundamental para evaluar el funcionamiento y la capacidad de una red en términos de su capacidad para transportar datos de manera rápida y confiable.

## Factores que Afectan el Rendimiento de Transferencia

El rendimiento de transferencia está influenciado por varios factores, entre los cuales se incluyen:

1. [[Conceptos en Redes#Ancho de Banda|Ancho de banda]]

2. [[Conceptos en Redes#Latencia|Latencia]]

3. **Jitter:** Variación en la latencia de la red, que puede resultar en una calidad inconsistente de la transmisión de datos, especialmente para aplicaciones sensibles a la latencia.

4. **Pérdida de Paquetes:** La ocurrencia de paquetes de datos perdidos durante la transmisión, lo que puede requerir retransmisiones y afectar negativamente al rendimiento general de la red.

5. **Congestión de la Red:** La saturación de la red debido a un alto volumen de tráfico, lo que puede provocar retardos y pérdida de paquetes.

## Medición del Rendimiento de Transferencia

El rendimiento de transferencia se puede medir utilizando diversas métricas, como:

- **Tasa de Transferencia:** La cantidad de datos transferidos por unidad de tiempo, generalmente medida en bits por segundo (bps) o en sus múltiplos (Kbps, Mbps, Gbps).

- **Tiempo de Respuesta:** El tiempo total que tarda una solicitud de datos en ser procesada y recibir una respuesta, incluyendo la latencia de la red y el tiempo de procesamiento en los sistemas finales.

- **Throughput:** La cantidad real de datos que se pueden transferir a través de la red en condiciones específicas, teniendo en cuenta la pérdida de paquetes, la latencia y otros factores.



# Crosstalk
El crosstalk, también conocido como diafonía, es un fenómeno no deseado en redes de computadoras y sistemas de comunicación que ocurre cuando una señal eléctrica o electromagnética se "contamina" o se "filtra" en un canal adyacente, causando interferencia entre las señales.

## Definición
El crosstalk se produce cuando hay una sobreposición no deseada de señales eléctricas o electromagnéticas entre canales de comunicación cercanos, como cables, líneas de transmisión o circuitos impresos. Esta interferencia puede provocar distorsión en las señales originales y afectar negativamente el rendimiento y la fiabilidad de la comunicación.

## Tipos de Crosstalk

Existen dos tipos principales de crosstalk:

1. **Crosstalk de Canal:** Ocurre cuando la señal de un canal se acopla de manera no deseada en otro canal adyacente debido a la proximidad física de los cables o dispositivos de comunicación. Este tipo de crosstalk es común en cables de red, como cables Ethernet, donde las señales de un par trenzado pueden interferir con las señales de otro par cercano.

2. **Crosstalk de Componente:** Ocurre dentro de un dispositivo electrónico, donde las señales en diferentes partes del circuito se acoplan de manera no deseada debido a la proximidad física de los componentes. Por ejemplo, en una placa de circuito impreso (PCB), las señales en pistas cercanas pueden acoplarse y provocar interferencia.

## Impacto del Crosstalk

El crosstalk puede tener varios efectos negativos en el rendimiento de la comunicación, incluyendo:

- **Distorsión de la Señal** 
- **Reducción de la Velocidad de Transmisión** 
- **Aumento de Errores de Transmisión** 

## Mitigación del Crosstalk

Para mitigar los efectos del crosstalk, se pueden tomar varias medidas, como:

- **Separación Física:**  para reducir el acoplamiento entre señales.

- **Blindaje Electromagnético** para reducir la propagación de señales no deseadas.

- **Uso de Pares Trenzados:** los pares trenzados están diseñados específicamente para minimizar el crosstalk.



# Host
Se refiere a cualquier dispositivo conectado a una red de computadoras que tiene una dirección única y puede enviar o recibir datos dentro de esa red. Los hosts de red pueden ser tanto dispositivos físicos como virtuales y desempeñan un papel fundamental en la comunicación y el intercambio de información en una red.

## Características Principales

- **Dirección IP:** Cada host de red tiene una dirección IP única que lo identifica dentro de la red. Esta dirección se utiliza para dirigir los datos hacia el host correcto en la red.

- **Dispositivos Físicos y Virtuales:** Los hosts de red pueden ser dispositivos físicos, como computadoras, servidores, impresoras, enrutadores, o dispositivos virtuales, como máquinas virtuales alojadas en servidores físicos.

- **Funciones de Comunicación:** Los hosts de red pueden actuar como fuentes o destinos de datos en la red. Pueden enviar datos a otros hosts, recibir datos de otros hosts, o ambos.

- **Protocolos de Red:** Los hosts de red utilizan diferentes protocolos de red para comunicarse y transmitir datos, como el protocolo [[Protocolos#TCP (Transmission Control Protocol)|TCP]] [[Protocolos#IP (Internet Protocol)|IP]] en Internet.

## Ejemplos de Hosts de Red

1. **Computadoras de Escritorio y Portátiles**
2. **Servidores**
3. **Dispositivos de Red:** Incluyen enrutadores, conmutadores, puntos de acceso inalámbrico y otros dispositivos de red que facilitan la conectividad y la comunicación entre los diferentes hosts en la red.
4. **Dispositivos IoT (Internet of Things):** Son dispositivos conectados a la red que pueden recopilar, enviar o recibir datos, como sensores inteligentes, cámaras de seguridad, termostatos inteligentes, entre otros.



# Data Center (Centro de datos)

Un data center es una instalación física que alberga equipos de computación y sistemas de almacenamiento de datos, así como componentes de redes y telecomunicaciones. Estos centros están diseñados para almacenar, procesar, gestionar y distribuir grandes volúmenes de datos de manera segura y eficiente.

## Componentes Principales de un Data Center:

1. **Servidores:** Equipos de cómputo que ejecutan aplicaciones y procesos.

2. **Almacenamiento:** Dispositivos y sistemas de almacenamiento de datos, como discos duros, matrices de discos (RAID), almacenamiento en red (NAS) o almacenamiento en sistemas de área de almacenamiento (SAN).

3. **Redes:** Equipos de red, como routers, switches y firewalls, que facilitan la comunicación entre los servidores y otros dispositivos en el centro de datos, así como la conectividad con redes externas.

4. **Sistemas de Energía:** Fuentes de alimentación redundantes, sistemas de respaldo de energía (como generadores diésel o baterías) y sistemas de distribución de energía para garantizar el suministro eléctrico continuo y la protección contra fallos de energía.

5. **Sistemas de Refrigeración:** Sistemas de aire acondicionado y refrigeración que controlan la temperatura y la humedad dentro del centro de datos para mantener los equipos en condiciones óptimas de funcionamiento.

6. **Seguridad Física y Lógica:** Medidas de seguridad física, como cámaras de vigilancia, controles de acceso y sistemas de detección de intrusos, así como medidas de seguridad lógica, como firewalls y sistemas de detección y prevención de intrusiones (IDS/IPS).

Los data centers pueden ser de diferentes tamaños y capacidades, desde pequeñas instalaciones locales hasta enormes centros de datos a escala empresarial o incluso a nivel de infraestructura de [[Cloud Computing Review|nube]]. Estos centros juegan un papel fundamental en la infraestructura de tecnología de la información (TI) de organizaciones de todo tipo, incluyendo empresas, instituciones educativas, proveedores de servicios en la [[Cloud Computing Review|nube]] y empresas de telecomunicaciones.


# Multiplexión
La multiplexión es una técnica utilizada en las redes de computadoras y sistemas de comunicación para combinar múltiples señales de información en una sola señal de transmisión. Esto permite que varios canales de datos compartan una misma línea de comunicación, optimizando el uso del ancho de banda disponible.


# Sistemas distribuidos
Un sistema distribuido es un conjunto de computadoras independientes que actúan de manera conjunta para parecer un único sistema coherente. Estos sistemas están diseñados para compartir recursos y tareas a través de una red de computadoras. La comunicación entre estas computadoras se realiza mediante mensajes.

### Características de los Sistemas Distribuidos

| Característica         | Descripción                                                                                                                                     |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| **Transparencia**      | El sistema oculta la complejidad de sus componentes y el modo en que interactúan, proporcionando una interfaz única al usuario.                  |
| **Escalabilidad**      | Capacidad de aumentar el rendimiento y la capacidad del sistema mediante la adición de más nodos sin afectar negativamente su funcionamiento.    |
| **Fiabilidad**         | Capacidad de continuar operando correctamente a pesar de fallos en algunos de sus componentes.                                                   |
| **Heterogeneidad**     | Los sistemas distribuidos pueden estar compuestos por diferentes tipos de hardware y software, interactuando sin problemas.                      |
| **Flexibilidad**       | Facilidad para modificar, actualizar o escalar el sistema sin interrumpir su operación.                                                          |
| **Concurrencia**       | Múltiples procesos se ejecutan de manera simultánea y cooperativa, compartiendo recursos y datos de manera segura y eficiente.                    |
| **Seguridad**          | Mecanismos para proteger datos y recursos compartidos de accesos no autorizados y garantizar la integridad de la información.                    |

### Arquitectura de los Sistemas Distribuidos

Los sistemas distribuidos pueden organizarse de diversas formas. A continuación se presentan algunas arquitecturas comunes:

| Arquitectura          | Descripción                                                                                                 |
|-----------------------|-------------------------------------------------------------------------------------------------------------|
| **Cliente-Servidor**  | Un servidor proporciona servicios a múltiples clientes que realizan peticiones y reciben respuestas.        |
| **P2P (Peer-to-Peer)**| Todos los nodos actúan como iguales, compartiendo recursos directamente sin un servidor central.            |
| **Multicapa**         | Divide las funciones en capas, como presentación, lógica de negocio y acceso a datos, distribuidas en diferentes nodos. |

### Ejemplo de Sistema Distribuido: World Wide Web (WWW)

La **WWW** es un ejemplo clásico de un sistema distribuido. En este sistema, múltiples servidores web almacenan información que los navegadores de los usuarios (clientes) pueden solicitar y mostrar. La arquitectura cliente-servidor es evidente aquí, donde los clientes envían solicitudes [[Protocolos#HTTP (Hypertext Transfer Protocol)|HTTP]]  a los servidores que responden con los recursos solicitados (páginas web, imágenes, videos, etc.).

