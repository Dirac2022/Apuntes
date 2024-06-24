Creada por ISO

Revisar: https://medium.com/@imyashmithasritheran/the-osi-model-a-brief-overview-and-key-concepts-c304e6565998


Es un modelo estándar usado par describir el flujo de información de un dispositivo informático a otro que opera en un entorno de red.

<div style="text-align: center;">
    <img src="https://miro.medium.com/v2/resize:fit:640/format:webp/1*OXWqwut4DIPGeonjIgGyHw.png" alt="Texto alternativo de la imagen">
</div>

## Ejemplo de el proceso de transmitir un email usando el modelo OSI

1. Cuando una persona envía un correo, comienza en la *capa de aplicación* donde un protocolo es elegido y se pasa a la *capa de presentación*.
2. La *capa de presentación* comprime los datos y los envía a la *capa de sesión* para la inicialización de la comunicación.
3. Luego la *capa de transporte* **segmenta** los datos y los pasa a la *capa de red* para su **empaquetamiento**.
4. La *capa de enlace de datos* divide los datos aun más en **tramas** y los envía a la *capa física* donde se convierte en un flujo de unos y ceros.
5. Finalmente, los datos llegan a la capa física de el dispositivo receptor. El mismo proceso ocurre en reversa desde la capa inferior hasta que el receptor abra el correo.

# Conceptos previos

## PDU (Protocol Data Unit)

Es un término general utilizado en el contexto de la comunicación de red para referirse a la unidad de información que se transmite a través de un protocolo específico en una capa determinada del modelo OSI (Open Systems Interconnection) o del modelo TCP/IP. La estructura y tamaño de la PDU varían según la capa en la que se encuentre.


# Características del modelo
Este modelo tiene una explícita distinción entre tres conceptos básicos
1. Servicios: Cada capa desempeña ciertos **servicios**.
2. Interfaces: La **interfaz** de una capa le indica a los procesos superiores cómo pueden acceder a ella.
3. Protocolos: Cada capa decide qué **protocolos** usar.

Los protocolos en el modelo  OSI están ocultos de una mejor forma que en el modelo TCP/IP, además se pueden reemplazar con relativa facilidad a medida que la tecnología cambia.



# Capa de aplicación

Brinda acceso a los recursos de la red

<div style="text-align: center;">
    <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*BB7PRJBqeDWwvQogFyFx4A.png" alt="Texto alternativo de la imagen">
</div>

Esta es la capa donde el usuario interactúa con la data. La capa identifica los socios de comunicación que permitan la transmisión de datos para una aplicación. Un ejemplo directo de aplicación son los navegadores.

Algunos protocolos en la capa de aplicación:
- [[Protocolos#Protocolos en la capa de aplicación#Telnet|Telnet]]
- [[Protocolos#Protocolos en la capa de aplicación#rlogin|rlogin]]
- [[Protocolos#Protocolos en la capa de aplicación#FTP (File Transfer Protocol)|FTP]]
- [[Protocolos#Protocolos en la capa de aplicación#rlogin|TFTP]]
- [[Protocolos#Protocolos en la capa de aplicación#SMTP (Simple Mail Transfer Protocol)|SMPT]]
- [[Protocolos#Protocolos en la capa de aplicación#POP3 (Post Office Protocol version 3)|POP3]]
- [[Protocolos#Protocolos en la capa de aplicación#HTTP (Hypertext Transfer Protocol)|HTTP]]
- [[Protocolos#Protocolos en la capa de aplicación#HTTPS (Hypertext Transfer Protocol Secure)|HTTPS]]
- [[Protocolos#Protocolos en la capa de aplicación#SNMP (Simple Network Management Protocol)|SNMP]]
- [[Protocolos#Protocolos en la capa de aplicación#DNS (Domain Name System)|DNS]]

# Capa de presentación

Responsable de traducir, cifrar y comprimir data

<div style="text-align: center;">
    <img src="https://miro.medium.com/v2/resize:fit:640/format:webp/1*TGapkS1sr_-BkA9xyFW9Ww.png" alt="Texto alternativo de la imagen">
</div>

Formatea los datos mediante compresión, cifrado, etc., y luego los envía a otras capas.
En esta capa se comprime los datos y se reducen los bits necesarios para la transmisión en red

**Algunos formatos:**

- [[Formatos#Rich Text Format|Rich Text Format]]
- [[Formatos#Quick Time Movies|Quick Time Movies]]
- [[Formatos#MPEG Files|MPEG Files]]
- [[Formatos#JPEG Files|JPEG files]]

**Algunos protocolos:**
- [[Protocolos#SSL (Secure Sockets Layer)|SSL]]
- [[Protocolos#TLS (Transport Layer Security)|TLS]]

# Capa de sesión

Garantiza el establecimiento y la terminación de la sesión

<div style="text-align: center;">
    <img src="https://miro.medium.com/v2/resize:fit:640/format:webp/1*nu3cCRl5Q4HhSugOo1LcdQ.png" alt="Texto alternativo de la imagen">
</div>

La capa puede procesar fácilmente el establecimiento, uso y terminación de una conexión.
Agrega puntos de control (*checkpoints*) como puntos de sincronización en los datos para identificar el error fácilmente y evitar la perdida de datos

**En esta capa operan**:
- XWindow / sistema de ventanas y protocolo de red
- SQL / Lenguaje de consultas
- SAP / Sistema de software empresarial

**Algunos protocolos**:
- [[Protocolos#Protocolos en la capa de sesión#NFS (Network File System)|NFS]]
- [[Protocolos#Protocolos en la capa de sesión#RPC (Remote Procedure Call)|RPC]]
- [[Protocolos#Protocolos en la capa de sesión#NetBIOS (Network Basic Input/Output System)|NetBIOS]]


# Capa de transporte

Habilita el transporte de datos desde la maquina de origen hacia la de destino

<div style="text-align: center;">
    <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*xDzI3bJT4Chl_jby5UzGDw.png" alt="Texto alternativo de la imagen">
</div>

La capa de transporte gestiona la entrega de paquetes. Monitorea los datos, la segmentación y el control de errores.

*Funciones*
- Acepta los datos y los divide en unidades más pequeñas al enviarlos. Luego reensambla los datos al recibirlos.
- Sigue una dirección de punto de servicio para entregar el mensaje al proceso correcto.
- Esta capa proporciona un servicio orientado a la conexión al establecer una conexión, transferir datos y terminar el proceso. Es seguro, ya que el remitente recibe una confirmación de la entrega de los datos.

En esta capa la PDU se le conoce como *segmentos TCP* (para TCP) y *datagrama UDP* (para UDP).

**Los protocolos de esta capa son:**
- [[Protocolos#Protocolos en la capa de transporte#TCP (Transmission Control Protocol)|TCP]]
- [[Protocolos#Protocolos en la capa de transporte#UDP (User Datagram Protocol)|UDP]]


# Capa de red

Provee la interconectividad de redes (*internetworking*) and packet movement.

<div style="text-align: center;">
    <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*nUo6E2X7e0DmyfEkDFaDDA.png" alt="Texto alternativo de la imagen">
</div>

Actúa como controlador de red y es responsable de transferir datos entre nodos en una red. A cada nodo se le asigna una dirección única, y la capa de redes lee estas direcciones para garantizar que los datos se envíen a su correcto destino. Organiza los datos en *paquetes* y los envía a su destino para su posterior procedimiento.

**Funciones de la capa de redes**:
- Formula una conexión entre diferentes dispositivos en una capa.
- Decide la ruta ideal para la transferencia de información desde el origen hacia el destino. Este proceso es conocido como enrutamiento (*routing*).
- Esta capa sigue un esquema de direccionamiento para encontrar la dirección IP correcta universalmente.
- Divide la información en *paquetes* usando el *protocolo de internet*.

En esta capa la PDU se llama *paquete*. El paquete contiene la dirección IP de origen y destino, así como los datos de la *capa de transporte*. 

**Algunos protocolos en la capa de red:**

- [[Protocolos#Protocolos en la capa de red#IP (Internet Protocol)|IP]]
- [[Protocolos#Protocolos en la capa de red#ICMP (Internet Control Message Protocol)|ICMP]]
- [[Protocolos#Protocolos en la capa de red#IPSEC|IPSEC]]
- [[Protocolos#Protocolos en la capa de red#MPLS|MPLS]]
- [[Protocolos#Protocolos en la capa de red#ARP (Address Resolution Protocol)|ARP]]
- [[Protocolos#Protocolos en la capa de red#RARP|RARP]]
- [[Protocolos#Protocolos en la capa de red#DHCP (Dynamic Host Configuration Protocol)|DHCP]]
- 


# Capa de enlace de datos

La principal tarea de la capa de enlace de datos es transformar un medio de transmisión puro en un a línea que este libre de errores de transmisión. Enmascara los errores reales, de manera que la capa de red no los vea. Para logrear esta tarea, el emisor divide los datos de entrada en **tramas de datos** y transmite las tramas en **forma secuencial**, el receptor devuelve una **trama de configuración de recepción**.

<div style="text-align: center;">
    <img src="https://miro.medium.com/v2/resize:fit:640/format:webp/1*alWtJN_wYtpKIdlwvJbUgQ.png" alt="Texto alternativo de la imagen">
</div>


Opera con dos subcapas:

- **Control de Enlace Lógico (LLC)**: Esta subcapa identifica la dirección del protocolo desde el encabezado de la trama y transfiere los paquetes a la siguiente capa.

- **Control de Acceso al Medio (MAC)**: Esta subcapa establece una conexión con la capa física de la red.
En esta capa la PDU se llama *tramas*. Las *tramas* en la capa de enlace de datos están más enfocadas en la transmisión de datos **dentro de una red local**, mientras que los paquetes en la capa de red son utilizados para la comunicación entre redes y el enrutamiento de datos a nivel global en una red más amplia.

Estándares
- [[Estandares#Ethernet|Ethernet]]


Algunos protocolos
- [[Protocolos#Protocolos en la capa de enlace de datos#HDLC (High-Level Data Link Control)|HDLC]]
- 

- PDU FRAMES
- Ethernet
- HDLC
- PPP
- RAPA
- ATM
- Fiber cable
- Frame Relay


# Capa física

Responsable de proporcionar especificaciones mecánicas y eléctricas.


<div style="text-align: center;">
    <img src="https://miro.medium.com/v2/resize:fit:640/format:webp/1*FTpkuGa8KeggzQJfsgkEoQ.png" alt="Texto alternativo de la imagen">
</div>



Algunos estándares
- [[Estandares#EIA/TIA-449|EIA/TIA-449]]
- [[Estandares#EIA-530|EIA-530]]
- [[Estandares#V.35|V.35]]

Algunas interfaces
- [[Interfaces#HSSI|HSSI]]
- [[Interfaces#RS232|RS232]]
- [[Interfaces#ISDN|ISDN]]
- [[Interfaces#100BaseTX|100BaseTX]]
