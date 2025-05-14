
# Función de la capa de transporte
La capa de transporte es responsable de establecer una sesión de comunicación temporal entre dos aplicaciones y de transmitir datos entre ellas. **Una aplicación genera datos que se envían desde una aplicación en un host de origen a una aplicación en un host de destino, independientemente del tipo de host destino, medio, ruta, o tamaño de la red**.
<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj14PxMGlaz6UBkZeFOPrv5FGwWX32_ujfyI4shOo11A-xktMVia2MnQcAD1yt2aOWZvjl3jawwQwV0_R9HwvqZ-D-qhR6iTiZPFInLUmBvqFKlGhQCnh1BSqOAPj4In-69XsFxVj1ABzDL/s1600/Funci%25C3%25B3n+de+la+capa+de+transporte.jpg">
    <figcaption></figcaption>
    </figure>
</div>

## Seguimiento de conversaciones individuales
En esta capa, cada conjunto de datos que fluye entre una aplicación de origen y una de destino se conoce como **conversación**. Un host puede tener varias aplicaciones que se comunican a través de la red de forma simultanea. Cada una de estas aplicaciones se comunica con una o más aplicaciones en uno o más host remotos. **Es responsabilidad de la capa de transporte mantener y hacer un seguimiento de todas estas conversaciones**.
<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi607QWKyfueWWwf_7GBOdfLp0XpOUh4a9Z1siVIT4BGjsGcKkor1QL9G5V8Vhmfa0DcS6jw-Cj2kgcSaDznsoPD9AmbcYiHX5l5azkPWAIHqzuq9TglAA50E5q1r5E1Uwb3Yxu3RRi7QOv/s1600/Responsabilidades+de+la+capa+de+transporte-1.jpg">
    <figcaption></figcaption>
    </figure>
</div>

## Seguimiento de datos y rearmado de segmentos
Los protocolos de la capa de transporte tienen servicios que segmentan los datos de aplicación en bloques de un tamaño apropiado. Estos servicios incluyen el encapsulamiento necesario en cada porción de datos. Se agrega un encabezado a cada bloque de datos para el rearmado. Este encabezado se utiliza para hacer un seguimiento del flujo de datos.

<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjk6PEnZh9JuP5qUSJoEDIwdsh-P_Ks73d2px6Hezi-LlbJ7p5WhgpKwgmiEOt0JMMr8w6NXg7cDTelCgNn9ciHIVdsAIquqnDNOKvE7szYxyOl8c6eeT9uUnFtngGk04-MNXdcr7SWwWOX/s1600/Responsabilidades+de+la+capa+de+transporte-2.jpg" width=700>
    <figcaption></figcaption>
    </figure>
</div>

Los protocolos de la capa de transporte describen cómo se utiliza la información del encabezado de dicha capa para rearmar las porciones de datos en flujos y transmitirlos a la capa de aplicación.

## Identificación de las aplicaciones
La capa de transporte asigna un identificador a cada aplicación para pasar flujos de datos a las aplicaciones adecuadas. Este identificador es un **número de puerto**. A todos los procesos de software que  requieran acceso a la red se les asigna un **número de puerto exclusivo** para ese host.


<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgjSqQnQWmrcH8PSkaVmi6Gc7r3Rf8nOQSpmNxEnBIesEOQMj0rG1HfULm3m6OTxsEfeoONKKKJOC7FC9K4kwUAfQDTTVPRtsVLiM6PU9Uy7blQ-Etj300LTyRgRxEya75fE_C0D0_Djwa3/s1600/Responsabilidades+de+la+capa+de+transporte-3.jpg">
    <figcaption></figcaption>
    </figure>
</div>


## Multiplexión de conversaciones
Revisar concepto [[Conceptos en Redes#Multiplexión|Multiplexión]]

El envío de algunos tipos de datos (como transmisión de video) a través de una red, como un flujo completo de comunicación, puede consumir todo el ancho de banda disponible. Esto impedirá que se produzcan otras comunicaciones al mismo tiempo. También podría dificultar la recuperación de errores y la retransmisión de datos dañados.

La segmentación de los datos en partes más pequeñas permite que se entrelacen (*multiplexen*) varias comunicaciones de distintos usuarios en la misma red.

Para identificar cada segmento de datos, la capa de transporte agrega un encabezado que contiene datos binarios organizados en varios campos. Los valores de estos campos permiten que los distintos protocolos de la capa de transporte lleven a cabo variadas funciones de administración de la comunicación de datos.

<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhQR43MXh8kO37xb7prTqysWhchaohfCuhowW4cRoBAoynCz4I0r45QVkoF1a5P7nA9y3fqqIqbUijvYPPBXbxkBnm2UNKr0DwltgJT5wXNVuWNoNYDAkf-u1oUdTD7JMJUGb8_-8Nhy6J4/s1600/Multiplexi%25C3%25B3n+de+conversaciones.jpg" width=700>
    <figcaption></figcaption>
    </figure>
</div>

## Confiabilidad de la capa de transporte
La confiabilidad en la capa de transporte se refiere a la capacidad de esta capa para asegurar que los datos enviados desde una aplicación en un dispositivo lleguen de manera correcta, completa y en el orden adecuado a la aplicación de destino en otro dispositivo.

La capa de transporte es responsable de administrar los requisitos de confiabilidad de las conversaciones.

IP solo se ocupa de la estructura, direccionamiento y routing de los paquetes, mas no la forma en que se llevará a cabo el transporte de las mismas. Los protocolos de transporte especifican la manera en que se transfieren los mensajes entre los host. [[Protocolos#TCP|TCP]]/[[Protocolos#IP (Internet Protocol)|IP]] proporciona dos protocolos de la capa de transporte: el protocolo de control de transmisión [[Protocolos#TCP (Transmission Control Protocol)|TCP]] y el protocolo de datagramas de usuario [[Protocolos#UDP (User Datagram Protocol)|UDP]]. [[Protocolos#IP (Internet Protocol)|IP]] utiliza estos protocolos para habilitar la comunicación y la transferencia de datos entre los host.
<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiA34LyvhzYFsGPCf439GUHW0JJaoFCddpa7Sgvn4IFMMUeGXlNyzKmZF80kYipCJ_TRqpTd0DS7lt-ZiRueeU8IlbbmBKGmzghZk9u0pYGZ5OL1Lt83Tjp4oPqbGQ305rlLCNG2yLvmOUI/s1600/Confiabilidad+de+la+capa+de+transporte.jpg">
    <figcaption></figcaption>
    </figure>
</div>


# Números de puerto
El número de puerto de origen está asociado con la aplicación que origina la comunicación en el host local. El número de puerto de destino está asociado con la aplicación de destino en el host remoto.

### Puerto de origen
Es generado de manera dinámica por el dispositivo emisor para identificar una conversación entre dos dispositivos.

### Puerto de destino
El cliente coloca un número de puerto  de destino en el segmento para informar al servidor de destino el servicio solicitado, Por ejemplo, cuando un cliente especifica el puerto 80 en el puerto de destino, el servidor que recibe el mensaje sabe que se solicitan servicios web.

<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgCznbo5IIKbw3f1YFS1SIhbrJ3adSOFjuPwl3bHoSl7-prwAiX2ONYEg8m2kOSECh5beunMuvn0VBSXkiowHSGjGQKPowaX9ECwZKY7_KjyJie-WOfuLa_7PckKDaqrMcSPgCIJpsIAB_0/s1600/N%25C3%25BAmeros+de+puerto.jpg">
    <figcaption></figcaption>
    </figure>
</div>


## Grupos de números de puerto

[[Organizaciones#IANA (Internet Assigned Numbers Authority)|IANA]] es el organismo responsable de asignar los distintos números de puerto.

- **Puertos conocidos (números del 0 al 1023) :** estos números se reservan para servicios y aplicaciones. Al definir estos puertos bien conocidos para las aplicaciones de los servidores, las aplicaciones cliente se pueden programar para solicitar una conexión a ese puerto en particular y a su servicio relacionado.
- **Puertos registrados (números del 1024 al 49151):** IANA asigna estos números de puerto a una entidad que los solicite para utilizar con procesos o aplicaciones específicos.
- **Puertos dinámicos o privados (números 49152 a 65535):** también conocidos como puertos efímeros, usualmente el SO del cliente los asigna de forma dinámica cuando se inicia una conexión a un servicio. 

| Rango de números de puerto | Grupo de puertos               |
| -------------------------- | ------------------------------ |
| Entre 0 y 1023             | Puertos bien conocidos         |
| Entre 1024 a 49151         | Puertos registrados            |
| Entre 49152 a 65535        | Puertos privados y/o dinámicos |

### Algunos puertos

**Protocolo TCP**

| Número de puerto | Protocolo | Aplicación                                                                                             | Acrónimo                                                         |
| ---------------- | --------- | ------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------- |
| 20               | TCP       | Protocolo de transferencia de archivos (datos)                                                         | [[Protocolos#FTP (File Transfer Protocol)\|FTP]]                 |
| 21               | TCP       | Protocolo de transferencia de archivos (control)                                                       | [[Protocolos#FTP (File Transfer Protocol)\|FTP]]                 |
| 22               | TCP       | Shell Seguro                                                                                           | [[Protocolos#SSH (Secure Shell)\|SSH]]                           |
| 23               | TCP       | Telnet                                                                                                 | [[Protocolos#Telnet\|Telnet]]                                    |
| 25               | TCP       | Protocolo simple de transferencia de correo                                                            | [[Protocolos#SMTP (Simple Mail Transfer Protocol)\|SMTP]]        |
| 80               | TCP       | Protocolo de transferencia de hipertexto                                                               | [[Protocolos#HTTP (Hypertext Transfer Protocol)\|HTTP]]          |
| 110              | TCP       | Protocolo de oficina de correos versión 3                                                              | [[Protocolos#POP3 (Post Office Protocol version 3)\|POP3]]       |
| 143              | TCP       | Protocolo de acceso a mensajes de Internet                                                             | [[Protocolos#IMAP (Internet Message Access Protocol)\|IMAP]]     |
| 443              | TCP       | Protocolo seguro de transferencia de hipertexto                                                        | [[Protocolos#HTTPS (Hypertext Transfer Protocol Secure)\|HTTPS]] |
| 465              | TCP       | Protocolo simple de transferencia de correo (sobre [[Protocolos#SSL (Secure Sockets Layer)\|SSL]])     | [[Protocolos#SMTP (Simple Mail Transfer Protocol)\|SMTP]]        |
| 587              | TCP       | Protocolo simple de transferencia de correo (sobre [[Protocolos#TLS (Transport Layer Security)\|TSL]]) | [[Protocolos#SMTP (Simple Mail Transfer Protocol)\|SMTP]]        |
| 993              | TCP       | Protocolo de acceso a mensajes de Internet (sobre [[Protocolos#TLS (Transport Layer Security)\|TSL]])  | [[Protocolos#IMAP (Internet Message Access Protocol)\|IMAP]]     |
| 995              | TCP       | Protocolo de oficina de correos versión 3 (sobre [[Protocolos#TLS (Transport Layer Security)\|TSL]])   | [[Protocolos#POP3 (Post Office Protocol version 3)\|POP3]]       |

**Protocolo UDP**

| Número de puerto | Protocolo | Aplicación                                             | Acrónimo                                                        |
| ---------------- | --------- | ------------------------------------------------------ | --------------------------------------------------------------- |
| 67               | UDP       | Protocolo de configuración dinámica de host (servidor) | [[Protocolos#DHCP (Dynamic Host Configuration Protocol)\|DHCP]] |
| 68               | UDP       | Protocolo de configuración dinámica de host (cliente)  | [[Protocolos#DHCP (Dynamic Host Configuration Protocol)\|DHCP]] |
| 69               | UDP       | Protocolo de transferencia de archivos trivial         | [[Protocolos#TFTP (Trivial File Transfer Protocol)\|TFTP]]      |
| 161              | UDP       | Simple Network Management Protocol                     | [[Protocolos#SNMP (Simple Network Management Protocol)\|SNMP]]  |

**Ambos**

| Número de puerto | Protocolo | Aplicación                                             | Acrónimo                                                        |
| ---------------- | --------- | ------------------------------------------------------ | --------------------------------------------------------------- |
| 53               | UDP, TCP  | Servicio de nombres de dominio                         | [[Protocolos#DNS (Domain Name System)\|DNS]]                    |

# Comando netstat
A veces es necesario conocer las conexiones TCP activas que están abiertas y en ejecución en el host de red. Netstat es una utilidad de red que puede usarse para verificar esas conexiones.
El comando **netstat** intentará resolver direcciones IP en nombres de dominio y números de puerto en aplicaciones conocidas. 

<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjPTFjqwx1vbJ6GBBlWybp9ZCaGbTxdWRFo7NoOaMojHPQbNxJ06jz6faoLiJ1Hde-sgJhHDE6NrelZAK2V7q1n1uejAMq01RtAcJ2MEA_uzuzT4kEMY4m32Iz6EAjdCifyF-i85KV3ak3X/s1600/El+comando+netstat.jpg">
    <figcaption></figcaption>
    </figure>
</div>

# Socket
Se conoce como socket a la combinación de la dirección IP de origen y el número de puerto de origen, o de la dirección IP de destino y el número de puerto de destino. El socket se utiliza para identificar el servidor y el servicio que solicita el cliente.

| IP          | Puerto |
| ----------- | ------ |
| 192.168.1.5 | 1099   |
| 192.168.1.7 | 80     |
Juntos, estos dos sockets se combinan para formar un par de sockets: 192.168.1.5:1099,  192.168.1.7:80

Los sockets permiten que los diversos procesos que se ejecutan en un cliente se distingan entre si. También permite la diferenciación de diferentes conexiones a un proceso de servidor.

<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh-0NkD1KczyohsWD7nwioOSGDxEBU_BZnUn-TDkIXdirjSBZssSPaIdzVySym33vJOr4Ftzcx0JWQGhU2KszonIEzUVSqSb1p9PZnGgIsThFrp5tTlZO_pUZf928J19bCXPVGs1KCIlia2/s1600/Pares+de+sockets.jpg" >
    <figcaption></figcaption>
    </figure>
</div>



# Protocolo  TCP
Además de admitir funciones básicas de segmentación y rearmado de datos, el protocolo TCP brinda los siguientes servicios.

**Establecimiento de una sesión**
TCP es un protocolo orientado a conexión, por el cual establece una conexión antes del envío de datos y el límite de la cantidad de datos a enviar.

**Entrega confiable**
Se asegura que cada segmento que envía el origen llegue al destino. Por varias razones, es posible que un segmento se dañe o se pierda por completo a medida que se transmite en la red.

**Entrega en el mismo orden**
Los datos pueden llegar en el orden equivocado, debido a que las redes pueden proporcionar varias rutas que pueden tener diferentes velocidades de transmisión. Al numerar y secuenciar los segmentos, TCP puede asegurar que estos se rearmen en el orden correcto.

**Control del flujo**
Los hosts de red tienen recursos limitados. Cuando TCP advierte que estos recursos están sobrecargados, puede solicitar que la aplicación emisora reduzca la velocidad del flujo de datos. Esto lo lleva a cabo TCP, que regula la cantidad de datos que transmite el origen. El control de flujo puede evitar la necesitad de retransmitir los datos cuando los recursos del host receptor están desbordados.
## Encabezado TCP
TCP es un protocolo con información de estado, significa que realiza seguimiento del estado de la sesión de comunicación.
- **Puerto de origen (16 bits) y puerto de destino (16 bits)**: se utilizan para identificar la aplicación.
- **Número de secuencia (32 bits):** se utiliza para rearmar los datos.
- **Número de reconocimiento (32 bits):** indica los datos que se recibieron.
- **Longitud del encabezado (4 bits):** conocido como “desplazamiento de datos”. Indica la longitud del encabezado del segmento TCP.
- **Reservado (6 bits):** este campo está reservado para el futuro.
- **Bits de control (6 bits):** incluye códigos de bit, o marcadores, que indican el propósito y la función del segmento TCP.
- **Tamaño de la ventana (16 bits):** indica la cantidad de bytes que se puedan aceptar por vez.
- **Checksum (16 bits):** se utiliza para la verificación de errores en el encabezado y los datos del segmento.
- **Urgente (16 bits):** indica si la información es urgente.

<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEivJIdUlcWuQoeOqYTepPhHuflAKcwQQnFHHTLmM5K8uet-HXndkNHGe7tYZh_SATFtbyeaonPTkgkURlywnU5T95J1ux-qpoaKv36kHO45HWYv1mK24rHnEbcnTxN5yqi4JJqo5XuUppyf/s1600/Encabezado+TCP.jpg" width=700>
    <figcaption></figcaption>
    </figure>
</div>


## Proceso de comunicación TCP
Cada proceso de aplicación que se ejecuta en el servidor está configurado para utilizar un número de puerto, ya sea predeterminado o de forma manual, por el administrador del sistema. **Un servidor individual no puede tener dos servicios asignados al mismo número de puerto dentro de los mismos servicios de la capa de transporte.**

Por ejemplo, un host que ejecuta una aplicación de servidor web y una de transferencia de archivos no puede configurar ambas para utilizar el mismo puerto (por ejemplo, el puerto TCP 80). Una aplicación de servidor activa asignada a un puerto específico se considera abierta, lo que significa que la capa de transporte acepta y procesa los segmentos dirigidos a ese puerto. Toda solicitud entrante de un cliente direccionada al socket correcto es aceptada y los datos se envían a la aplicación del servidor. Pueden existir varios puertos abiertos simultáneamente en un servidor, uno para cada aplicación de servidor activa.

<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjLxJ0GLc0QM1i4326EV4BbyhRkagfcz2jCydq0qPcLMMcmKM9JUNGYImeO2CVRwtFC6t451bysSGqf6IjULUWE1intzlovmwGLcR1OY5s7K8D8wQiT-bA35ehLwC2NK1achTUkElDahu9u/s1600/Procesos+del+servidor+TCP-1.jpg" width=700>
    <figcaption></figcaption>
    </figure>
</div>

<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg2GSwVxj8GdEDJVKM067jkEMqRc1yjvK8L9_AdeTvUBbXxaHFwwgIutUvShcY26fg6H-D1suxz909Hej49KKmTx6vfVqGcvsfJiwJbgWcODTbmWGiR9TAsuoCJ6f4C-UJyWxx3_OB-kQ9k/s1600/Procesos+del+servidor+TCP-2.jpg" width=700>
    <figcaption></figcaption>
    </figure>
</div>


<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi-SGqQA8-8lHgBELeP9-4_NIZL8UBtCYa3JBFnmm-7Mzeh1AaHdnw8tPTOIv_1t-eMuilxaxmaKLzMvPRXDejD70o2wj3rYL70k0Zx0j_aMijufuvzR5ENuFGsLs669ffym6Mh-N2oxAQQ/s1600/Procesos+del+servidor+TCP-3.jpg" width=700>
    <figcaption></figcaption>
    </figure>
</div>


<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgjgOSQsaqt6NvhuAnlflp9GSLIrwfDqNF1XXuOef2_9BC1nM10JQ0FKshE7ee_cgpjdjF8wOYTFZkFS5zt11Cr_bazBT6OmrOBIohnqcZKQ7816yOrt5WbVmrhodONOyBM1gXBe39Q75iY/s1600/Procesos+del+servidor+TCP-4.jpg" width=700>
    <figcaption></figcaption>
    </figure>
</div>

<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEht1i5uEl7fajmGeLAwqEsRhMZSZ23ZRqJzPsAohNpTs_Zkgc3PsizyRBKXOjSfBZawO72lFG3NIM5qk4G_nnbrbSEfYO4gANp9ruZSGpFL00-m75A637NZ5hORah2MIBgQmtYw-h78GvwZ/s1600/Procesos+del+servidor+TCP-5.jpg" width=700>
    <figcaption></figcaption>
    </figure>
</div>

- **URG** - importante campo de puntero urgente
- **ACK** - importante campo de confirmación
- **PSH** - función de empujar
- **RST** - restablecer la conexión
- **SYN** - sincronizar los números de secuencia
- **FIN** - no hay más datos del emisor

### Establecimiento de la comunicación TCP
Una conexión TCP se establece en tres pasos:

- **Paso 1:** el cliente de origen solicita una sesión de comunicación de cliente a servidor con el servidor.
- **Paso 2:** el servidor reconoce la sesión de comunicación de cliente a servidor y solicita una sesión de comunicación de servidor a cliente.
- **Paso 3:** el cliente de origen reconoce la sesión de comunicación de servidor a cliente


<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEilYCNrNa63WvwUwJoO6DEIse4Rwu3DLRU3TbD7KklsMppGSyyUF02TfrSjM39PzMDJbX2uaGjp9ZSufW1LYfGZ1lgy_gRZaZPBBpczivWT2xiwoj3rVsAT0ii0cH7KkO_r8lEuk3VQJ907/s1600/Establecimiento+de+conexiones+TCP-1.jpg" width=700>
    <figcaption></figcaption>
    </figure>
</div>

<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgrBt7M1Xtk1-8g_YBPX0orr9J2q-2tzySdjGXQTFhIdcIRUx5BWehla5k_LYunhEqVgnTpWN33LKykAzQLnGUziNm-EkwFQSjk54q8trBoQCJmiuvQRtDb3oqkyLH8QD5RtmVYrIa4Iahg/s1600/Establecimiento+de+conexiones+TCP-2.jpg" width=700>
    <figcaption></figcaption>
    </figure>
</div>

<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj2mJrDUatn74T_KIX6MRnFG2hyphenhyphenFCyxQv0k-jmOeqHvYWGk8VjX-RCHmkeHF2GxJZExrZyEzwbnEr59mtyim_S2P3S-HVTrWeKx6N3sEaXgmctKd8ANN9OSMHzMWogMtIXkV1LYBsBmOZU_/s1600/Establecimiento+de+conexiones+TCP-3.jpg" width=700>
    <figcaption></figcaption>
    </figure>
</div>


### Finalización de la sesión TCP

- **Paso 1:** cuando el cliente no tiene más datos para enviar en la transmisión, envía un segmento con el marcador FIN establecido. pero el proceso de finalización puede ser iniciado por dos hosts cualesquiera que tengan una sesión abierta:
- **Paso 2:** el servidor envía un ACK para reconocer el marcador FIN y terminar la sesión de cliente a servidor.
- **Paso 3:** el servidor envía un FIN al cliente para terminar la sesión de servidor a cliente.
- **Paso 4:** el cliente responde con un ACK para reconocer el recibo del FIN desde el servidor.

Una vez reconocidos todos los segmentos, la sesión se cierra

<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj7vkIQPB7-eaMjBTmDB4U_EMx6qssBtqwEYD2Z9EbxtjMK8oREIcru1IAno_znFFAMZckTETJLrM4qwV7ffC2ZJysLLXDDrs8hMt_bYwPYlCkS1zohhEmPrtCbQ3yiMV5ZPbeeukkq1aax/s1600/Finalizaci%25C3%25B3n+de+la+sesi%25C3%25B3n+TCP.jpg" width=700>
    <figcaption></figcaption>
    </figure>
</div>

## Reordenamiento de segmentos TCP
Cuando se envían los segmentos se les establece un valor inicial llamado ISN (*Número de secuencia inicial*), este ISN representa el valor inicial para los bytes que se transmitirán en la sesión. Estos números en el encabezado se utilizan para reordenar los paquetes en el host receptor.

El proceso TCP receptor coloca los datos del segmento en un búfer de recepción. Los segmentos se colocan en el orden de secuencia correcto y se pasan a la capa de aplicación cuando se vuelven a ensamblar. Todos los segmentos que lleguen con números de secuencia desordenados se retienen para su posterior procesamiento. A continuación, cuando llegan los segmentos con bytes faltantes, tales segmentos se procesan en orden.

<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgSWvy_0HdiXZFuPVWn1Vz6Pnik9qxvQQCfkCkrQPZj3SxYigde2CohdYWJasR2sb79nw-BAfwzXqz8NM3jPRylbxpo3B7AkuaXK3NnwtKBXitjd_cNGPSXRGBSPdmZKi4vADd8QLrLZ0kr/s1600/Confiabilidad+de+TCP+-+entrega+ordenada.jpg" width=700>
    <figcaption></figcaption>
    </figure>
</div>


## Control de flujo TCP

![[Pasted image 20240527165931.png]]
![[Pasted image 20240527165940.png]]

# Protocolo UDP
UDP es un protocolo de transporte liviano que ofrece la misma segmentación rearmado de datos que TCP, pero sin la confiabilidad y el control del flujo de TCP.

- El **protocolo UDP** trabaja sin conexión, es decir, no sabe si el host receptor estará disponible para la escucha de los paquetes.

- Los **paquetes corruptos** o no entregados no se vuelven a enviar, ya que se desconoce cuales no fueron entregados porque no existe el acuse de recibo.

- La **reconstrucción de los datos** se realiza de forma desordenada, y mucho menos tiene control de flujo como TCP, es decir, que no controla la cantidad de paquetes de datos enviados.

- Los paquetes enviados por este protocolo se denominan **datagramas**.


## Cabecera UDP

El proceso de **checksum** se establece en la maquina emisora, este se consigue mediante el CRC (**Cyclic Redundancy Check**), que es una operación realizada con la cabecera y los datos del segmento. El host receptor realiza el mismo proceso y se compara para ver la integridad del paquete.

<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgEyIqB12V8O6nEJeRFUt78ScTry7dHUuZLErXvwT0l9_WqMv3eHeTz70Fu3Wu5aWjw8EqRSofgMvd526JrrPL7kJAzNo9Um9tJki-_s_AEJgSBg2BlsOmRZ1q8MCrmF6EkyqO7UTbjeJ-F/s1600/Encabezado+UDP.jpg" width=700>
    <figcaption></figcaption>
    </figure>
</div>


## Reensamblaje de datagramas UDP
UDP no realiza un seguimiento de los números de secuencia de la manera en que lo hace TCP. UDP simplemente reensambla los datos en el orden que se recibieron y los envía a la aplicación. Si la secuencia de datos es importante para la aplicación, esta debe identificar la secuencia adecuada y determinar cómo se deben procesar los datos.

<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhVHUtTvMKLYCjZzucp1PFQFW-irHsuMGsq70E4ucrLrOphrXD9EV9RtNrifX_sh0nezesgk2bzl9Ba0Z44eyhefdrNoHzd9fCRYvMZs3xxImkGcwFRF41usRhCfMMcRy3acbOZ5Hd0Qres/s1600/Reensamblaje+de+datagramas+de+UDP.jpg">
    <figcaption></figcaption>
    </figure>
</div>

# Utilidad de TCP y UDP

## Aplicaciones que utilizan TCP
TCP es un excelente ejemplo de cómo las diferentes capas de la suite de protocolos TCP/IP tienen funciones específicas. TCP se encarga de todas las tareas asociadas con la división del flujo de datos en segmentos, lo que proporciona confiabilidad, control del flujo de datos y reordenamiento de segmentos. TCP libera la aplicación de tener que administrar estas tareas. Las aplicaciones, como las que se muestran en la figura, simplemente puede enviar el flujo de datos a la capa de transporte y utilizar los servicios de TCP.

<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgEfUsVSY1RZqJF7_JSwAsP31KGLHwyqU-NxCGK2kEv90ZWzeYagoo79O2aoIruKjZh1_gBhjm3kkv9yHoaYKxrNPxZid2c8YIxrDE-bzpDUlPlrsNCdvj4gY9dkR7-YqCSqSD1J3ae46vA/s1600/Aplicaciones+que+utilizan+TCP.jpg">
    <figcaption></figcaption>
    </figure>
</div>

## Aplicaciones de utilizan UDP

- **Aplicaciones multimedia y vídeo en vivo:** pueden tolerar cierta pérdida de datos, pero requieren retrasos cortos o que no haya retrasos. Los ejemplos incluyen VoIP y la transmisión de vídeo en vivo.
- **Aplicaciones con solicitudes y respuestas simples:** aplicaciones con transacciones simples en las que un host envía una solicitud y existe la posibilidad de que reciba una respuesta o no. Por ejemplo, DNS y DHCP.
- **Aplicaciones que manejan la confiabilidad por su cuenta:** comunicaciones unidireccionales que no requieran control de flujo, detección de errores, reconocimientos ni recuperación de errores o que puedan ser manejados por la aplicación. Por ejemplo, SNMP y TFTP.

<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgDXYJPntPMi6wb3zO2DZmbEiLastOTbiBntY_J44d-HYesFt8NZKt4YiuoWmbSz3m4wgqqVMD-Ewpbt477l7WOkvbuhJ2eIViUTQpieLfIMfHsP84Vi8Tkr4LxngyBbPswNSF2AAMM2Eg5/s1600/Aplicaciones+que+utilizan+UDP.jpg">
    <figcaption></figcaption>
    </figure>
</div>

# Encapsulamiento

Las porciones de datos en las capas del modelo OSI se denominan *unidad de datos del protocolo (PDU)*. Durante el encapsulamiento, cada capa encapsula las PDU que recibe de la capa inferior de acuerdo con el protocolo que se utiliza. En cada etapa del proceso, una PDU tiene un nombre distinto para reflejar sus funciones nuevas.
<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhEe_cRkXHcn1ISm9gHPTj26-fuozvaHYbqwbwyFPgW-G1I4nmHEl0qRDmtBHCDnusX630rNdUq9_4Mt5rPEr6tdOz4LF9RS_GpkyNkUOx0qNHhCCQFGB2QS-6moe3PDKsj-4zRsqJrucke/s1600/Encapsulamiento-1.jpg">
    <figcaption></figcaption>
    </figure>
</div>

- **Datos**. Término general que se utiliza en la capa de aplicación para la PDU.
- **Segmento**. PDU de la capa de transporte.
- **Paquete**. PDU de la capa de red.
- **Trama**. PDU de la capa de enlace de datos.
- **Bits**. PDU de la capa física que se utiliza cuando se transmiten datos físicamente por el medio.

## Encapsulamiento en la capa de transporte

### Encapsulamiento
Cuando se envían mensajes en una red, el proceso de encapsulamiento opera desde las capas superiores hacia las capas inferiores. En cada capa, la información de la capa superior se considera como datos en el protocolo encapsulado. Por ejemplo, el segmento TCP se considera como datos en el paquete IP.

<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjl7JOgNYct5bTqt13gs2MzBVWPATOymlP5ql3GEUB_dNepT5Hua49LHmDK_UABUCUoPfChCibzgOnEK9HABFtfbmTA_g-CDCPjAdoPFQm7Oqg2vHrAIqzmxtKsDLzvt4RNho_IC1PKNws-/s1600/Conjunto+del+protocolos+TCP-IP+y+proceso+de+comunicaci%25C3%25B3n-2.jpg" width=700>
    <figcaption></figcaption>
    </figure>
</div>

### Desencapsulamiento
Este procese se invierte en el host receptor y se conoce como desencapsulamiento. Es el proceso que utilizan los dispositivos receptores para eliminar uno o más de los encabezados del protocolo. Los datos se desencapsulan mientras suben por la pila hacia la aplicación del usuario final.
<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiYW4fqa-HJAqaQ3coAJOS9elBDh0I2pe2Qp6M_llkGjZdgcmYU30y67JpWKr7aseLymy-hm2VAFOzKTeG-FolpZmM6U5rMnx6R2IO2G__bLYgkBpRP-2yqmm8ywlcXB-rY0U9Znihl2N1t/s1600/Operaci%25C3%25B3n+de+protocolo+para+enviar+y+recibir+un+mensaje.jpg" width=700>
    <figcaption></figcaption>
    </figure>
</div>
