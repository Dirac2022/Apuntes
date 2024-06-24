
Se dice que dos computadoras están interconectadas si pueden intercambiar información. 

Hay confusión entre una red de computadoras y un sistema distribuido
- En un sistema distribuido un conjunto de computadoras independientes aparece frente a sus usuarios como un solo sistema coherente. Por ejemplo la World Wide Web. Un sistema distribuido es un sistema de software construido sobre una red.

Modelos de redes:
- Cliente - servidos
- Redes peer-to-peer


# Diferencia entre interfaz y protocolo

- **Interfaz**: En el contexto de la red, una interfaz se refiere a la conexión física o lógica a través de la cual los dispositivos se comunican entre sí. Ejemplos de interfaces incluyen puertos Ethernet en dispositivos de red, como conmutadores, routers y tarjetas de red en computadoras.

- **Protocolo**: Un protocolo de red define las reglas y los procedimientos que los dispositivos deben seguir para comunicarse entre sí. Ejemplos de protocolos en el contexto de Ethernet incluyen TCP/IP (Transmission Control Protocol/Internet Protocol), UDP (User Datagram Protocol), ICMP (Internet Control Message Protocol), etc


# Tecnologías de transmisión:
 
**Enlaces de difusión (broadcast)** 
En una red de difusión todas las máquinas en la red comparten el canal de comunicación;
los paquetes que envía una máquina son recibidos por todas las demás. Un campo de dirección
dentro de cada paquete especifica a quién se dirige. Cuando una máquina recibe un paquete, verifica el campo de dirección. Si el paquete está destinado a la máquina receptora, ésta procesa el paquete; si el paquete está destinado para otra máquina, sólo lo ignora. Por ejemplo: una red inalámbrica

**Enlaces de punto a punto**
Los enlaces de punto a punto conectan pares individuales de máquinas. Para ir del origen al destino en una red formada por enlaces de punto a punto, los mensajes cortos (paquetes) tal vez tengan primero que visitar una o más máquinas intermedias. Es importante encontrar la ruta más adecuada en las redes de punto a punto. A la transmisión punto a punto en donde sólo hay un emisor y un receptor se le conoce como unidifusión (*unicasting*). 

# Tipos de redes según la escala
## Redes de área personal (PAN)
Permiten a los dispositivos comunicarse dentro del rango de una persona. Un ejemplo común es una red inalámbrica que conecta a una computadora con sus periféricos.


## Redes de área local (LAN)
Son redes de propiedad privada que operan dentro de un solo edificio, como una casa, oficina o fábrica. Las redes LAN se utilizan ampliamente para conectar computadoras personales y electrodomésticos con el fin de compartir recursos (por ejemplo, impresoras) e intercambiar información. Cuando las empresas utilizan redes LAN se les conoce como redes empresariales.
La topología de muchas redes LAN alámbricas está basada en los enlaces de punto a punto. El estándar IEEE 802.3, comúnmente conocido como Ethernet, es hasta ahora el tipo más común de LAN alámbrica

## Redes de área metropolitana (MAN)
Una Red de Área Metropolitana, o MAN (Metropolitan Area Network), cubre toda una ciudad. El ejemplo más popular de una MAN es el de las redes de televisión por cable disponibles en muchas ciudades.

## Redes de área amplia (WAN)
Una Red de Área Amplia, o WAN (Wide Area Network), abarca una extensa área geográfica, por lo general un país o continente. En la mayoría de las redes WAN, la subred cuenta con dos componentes distintos: líneas de transmisión y elementos de conmutación. 

Las líneas de transmisión mueven bits entre máquinas. Se pueden fabricar a partir de alambre de cobre, fibra óptica o incluso enlaces de radio.

Los elementos de conmutación o switches son computadoras especializadas que conectan dos o más líneas de transmisión. Cuando los datos llegan por una línea entrante, el elemento de conmutación debe elegir una línea saliente hacia la cual reenviarlos (enrutador).

Muchas redes WAN son de hecho **interrredes** o redes compuestas formadas por más de una red.


#### Interredes
A menudo se confunden las subredes, las redes y las interredes. El término **subred** tiene más sentido en el contexto de una red de área amplia, en donde se refiere a la colección de enrutadores y líneas de comunicación que pertenecen al operador de red. Como analogía, el sistema telefónico está compuesto por oficinas de conmutación telefónica conectadas entre sí mediante líneas de alta velocidad y conectadas a los hogares y negocios mediante líneas de baja velocidad. Estas líneas y equipos, que pertenecen y son administradas por la compañía telefónica, forman la subred del sistema telefónico. Los teléfonos en sí (los hosts en esta analogía) no forman parte de la subred.

Una red se forma al combinar una subred y sus hosts. Sin embargo, la palabra “red” a menudo también se utiliza en un sentido amplio.

El nombre general para una máquina que realiza una conexión entre dos o más redes y provee
la traducción necesaria, tanto en términos de hardware como de software, es puerta de enlace        (**gateway**). Las puertas de enlace se distinguen por la capa en la que operan en la jerarquía de protocolos.