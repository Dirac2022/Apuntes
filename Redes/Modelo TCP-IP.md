
https://medium.com/@diego.coder/introducci%C3%B3n-al-modelo-tcp-ip-53d6ad590bd2


# Introducción
El modelo TCP/IP estandariza la comunicación de los dispositivos en una red determinando principalmente reglas, comportamiento y seguridad.

El modelo TCP/IP fue desarrollado en el año 1970 por el departamento de defensa de los Estados Unidos y con el pasar del tiempo TCP/IP se convirtió en el principal estándar de todo el internet.

También debemos destacar que el modelo TCP/IP está basado en el modelo teórico OSI y su nombre radica en los 2 principales protocolos fundamentales para la comunicación de redes; el protocolo [[Protocolos#TCP (Transmission Control Protocol)|TCP]] y el protocolo [[Protocolos#IP (Internet Protocol)|IP]].
## Características
1. **Compatibilidad de dispositivos**: El modelo TCP/IP se ha convertido en el estándar de facto para la comunicación en redes de computadoras, por lo tanto, la mayoría de los dispositivos del planeta y sistemas operativos están diseñados para ser compatibles con TCP/IP, lo que facilita la comunicación entre diferentes proveedores.
2. **Interoperabilidad**: esto significa que una computadora con sistema operativo Windows, por ejemplo, puede comunicarse con una computadora con sistema operativo Linux utilizando el mismo conjunto de protocolos TCP/IP.
3. **Flexibilidad**: El modelo TCP/IP es muy flexible y puede admitir una amplia gama de aplicaciones y servicios. El modelo TCP/IP proporciona una base sólida para la navegación web, la transmisión de video o transferencia de archivos (por mencionar algunos servicios).
4. **Fiabilidad y control de errores**: Los principales protocolos de TCP/IP ofrecen múltiples mecanismos para garantizar una entrega confiable de los datos. TCP/IP ofrece a cada segmento enviado una enumeración, trazabilidad y seguimiento para que asegurarse de que todos los datos lleguen correctamente.

## Composición de capas del modelo TCP/IP

<div style="text-align: center;">
	<figure>
    <img src="https://miro.medium.com/v2/resize:fit:1100/format:webp/1*KbEducEG9i8GkZVMm0OWqA.png" alt="Texto alternativo de la imagen">
    <figcaption>Comparación de capas OSI / TCP/IP</figcaption>
    </figure>
</div>

# Capa de Aplicación (Application Layer)

Esta es la capa más alta del modelo TCP/IP y se ocupa de la interacción entre las aplicaciones y la red. Los protocolos que interactúan con esta capa tienen la finalidad de establecer reglas y formatos necesarios para que las aplicaciones puedan intercambiar información de manera efectiva, ofreciendo la interoperabilidad.

Todas las aplicaciones y servicios utilizan esta capa para enviar y recibir datos, destacando que, el usuario no interactúa directamente con esta capa, sino que el servicio o aplicación lo hace ocultando toda la complejidad que hay por detrás.

A su vez, cada protocolo de aplicación tiene funcionalidades específicas diseñadas para satisfacer las necesidades de una aplicación en particular. Los protocolos que podemos encontrar en esta capa son los siguientes:

- [[Protocolos#HTTP (Hypertext Transfer Protocol)|HTTP]] y [[Protocolos#HTTPS (Hypertext Transfer Protocol Secure)|HTTPS]]
- [[Protocolos#DNS (Domain Name System)|DNS]]
- [[Protocolos#DHCP (Dynamic Host Configuration Protocol)|DHCP]]
- [[Protocolos#SSH (Secure Shell)|SSH]]
- [[Protocolos#FTP (File Transfer Protocol)|FTP]]
- [[Protocolos#SMTP (Simple Mail Transfer Protocol)|SMTP]]
- Entre otros.

# Capa de Transporte (Transport layer)

En la capa de transporte, se gestionan las conexiones de extremo a extremo y se garantiza una entrega confiable de los datos. El Protocolo de Control de Transmisión (TCP) es el protocolo más comúnmente utilizado en esta capa y proporciona una entrega ordenada y confiable de los datos, control de flujo y control de congestión.

Debemos destacar que también existe el Protocolo de Datagramas de Usuario (UDP), que es más ligero y rápido, pero no garantiza la fiabilidad. Este protocolo se utiliza principalmente para consultas DNS, conexiones VPN y para el streaming de audio y vídeo.

Como se mencionó anteriormente, los protocolos que podemos encontrar en esta capa son los siguientes:

- [[Protocolos#TCP (Transmission Control Protocol)|TCP]]
- [[Protocolos#UDP (User Datagram Protocol)|UDP]]

# Capa de Internet (Internet Layer)

La capa de Internet es responsable del enrutamiento de los paquetes de datos a través de la red. Utiliza el Protocolo de Internet (IP) para asignar direcciones IP únicas a los dispositivos y encaminar los paquetes desde su origen hasta su destino a través de la red. Además, se encarga de dividir y ensamblar los datos en paquetes más pequeños para su transmisión.

El único protocolo que se encuentra en esta capa es el protocolo [[Protocolos#IP (Internet Protocol)|IP]], sub compuesto por [[Protocolos#ARP (Address Resolution Protocol)|ARP]], [[Protocolos#IGMP (Internet Group Management Protocol)|IGMP]] y [[Protocolos#ICMP (Internet Control Message Protocol)|ICMP]].

# Capa de interfaz de Red (Network Interface Layer)

Tambien conocida como **capa de acceso al medio**, encargada de la transmisión física de datos a través de un medio de red, como Ethernet, Wi-Fi o fibra óptica. Esta capa define los estándares para el enlace físico y la transmisión de bits. En esta capa, se especifican los detalles técnicos y los protocolos utilizados para la comunicación en la red local.

Los protocolos que podemos encontrar en esta capa son los siguientes:

- Ethernet.
- IEEE 802.3.
- Token-ring.
- Serial Line Internet Protocol.
- Loopback.
- FDDI.
- Serial Optical.
- [[Red Essentials#ATM (Asynchronous Transfer Mode)|ATM]]
- Entre otros.