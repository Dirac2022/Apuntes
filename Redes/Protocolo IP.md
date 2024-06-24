
[[Protocolos#IP (Internet Protocol)|IP]]
# Conceptos previos

## NAT (Network Address Translation)
Es un mecanismo utilizado en redes de computadoras para convertir direcciones IP privadas en direcciones IP públicas y viceversa. Su función principal es permitir que múltiples dispositivos en una red privada compartan una única dirección IP pública para acceder a internet.
### Funcionamiento de NAT
Cuando un dispositivo en una red privada envía un paquete a través de un router NAT para acceder a internet, el router modifica la dirección de origen del paquete (IP privada) con su propia dirección IP pública antes de enviarlo a través de internet. Cuando el paquete de respuesta llega al router NAT, este utiliza una tabla de traducción para determinar a qué dispositivo privado enviar la respuesta, modificando la dirección de destino (IP pública) por la dirección IP privada correspondiente.

# Encapsulamiento IP

El segmento que llega de la capa de transporte es procesado en la capa 3 o de red. IP le agrega un encabezado el cual contiene información para entregar el paquete al host de destino.
![[Pasted image 20240505110015.png]]

# Características de IP
- **No orientado a conexión**. IP no necesita un intercambio inicial de información de control para establecer una conexión completa para que se reenvíen los paquetes.
- ![[Pasted image 20240505113232.png]]
- **Entrega de servicio mínimo**. Si bien los paquetes IP se envían con información sobre la ubicación de entrega, no tienen información que pueda procesarse para informar al remitente si la entrega se realizó correctamente. Capas superiores se encargarán de ello.
- ![[Pasted image 20240505113505.png]]
- **Independencia de medios**. Los paquetes IP pueden ser señales electrónicas que se transmiten por cables de cobre, señales ópticas que se transmiten por fibra óptica o señales de radio inalámbricas.
- ![[Pasted image 20240505113629.png]]




# Protocolo IP

## Campos IPv4
![[Pasted image 20240505113656.png]]

| Campo                                     | Descripción                                                                                                                                                                                              |
| ----------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Versión                                   | Contiene un valor que lo identifica como IPv4, 0100.                                                                                                                                                     |
| Longitud del encabezado de internet (IHL) | 4 bits que identifica la cantidad de campos de 32 bits que tiene la cabecera.                                                                                                                            |
| Servicio Diferenciado (DS)                | Se utiliza para determinar la prioridad de cada paquete.                                                                                                                                                 |
| Longitud total                            | Longitud del paquete (16 bits), define el tamaño total del paquete (fragmento), incluidos el encabezado y los datos.                                                                                     |
| Identificación                            | Identifica de forma exclusiva el fragmento de un paquete IP original.                                                                                                                                    |
| Señalador                                 | Indica cómo se fragmenta el paquete. Usado para el reensamblado del paquete.                                                                                                                             |
| Desplazamiento de fragmentos              | Identifica el orden en que se debe colocar el fragmento del paquete en la reconstrucción del paquete original sin fragmentar.                                                                            |
| Tiempo de duración                        | 4 bits que se usa para delimitar el tiempo de vida de un paquete. El emisor del paquete establece el valor inicial de TTL (Time to Live) que se reduce en uno cada vez que un router procesa el paquete. |
| Protocolo                                 | Se utiliza para identificar el protocolo del siguiente nivel.                                                                                                                                            |
| Checksum del encabezado                   | Se utiliza para la verificación de errores del encabezado IP.                                                                                                                                            |
| IPv4 origen                               | Dirección Ipv4 origen del paquete                                                                                                                                                                        |
| IPv4 destino                              | Dirección IPv4 destino del paquete.                                                                                                                                                                      |

## Limitaciones IPv4
- **Agotamiento de direcciones IP**. Hay un número finito de direcciones IPv4 disponibles, y con el crecimiento constante de dispositivos conectados a internet, el suministro de direcciones IPv4 se está agotando rápidamente.
- **Expansión de tabla de routing de internet**. La tabla de enrutamiento de IPv4 en los routers de internet se está expandiendo constantemente. Esta expansión puede generar una sobrecarga en los routers, aumentando la complejidad de la gestión del enrutamiento y reduciendo la eficiencia de la red.
- **Falta de conectividad completa**. Puede haber problemas de conectividad en redes que utilizan direcciones IP privadas y necesitan acceder a recursos en internet o en otras redes

## IPv6
Las mejoras de IPv6 incluyen lo siguiente:

- **Mayor espacio de direcciones**: las direcciones IPv6 se basan en el direccionamiento jerárquico de 128 bits en comparación con los 32 bits de IPv4.
- **Mejor manejo de paquetes**: se redujo la cantidad de campos del encabezado de IPv6 para hacerlo más simple.
- **Se elimina la necesidad de NAT**: Al tener un número tan grande de direcciones IPv6 públicas, la [[#NAT (Network Address Translation)|NAT]] entre las direcciones IPv4 privadas y públicas ya no es necesaria. Esto evita algunos problemas de aplicación inducidos por NAT que tuvieron algunas aplicaciones que necesitan conectividad completa.
![[Pasted image 20240505120011.png]]

## Campos IPv6
![[Pasted image 20240505120035.png]]


| Campo                     | Descripción                                                                                                                                      |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| Versión                   | 4 bits que lo identifica como IPv6, 0110                                                                                                         |
| Clase de tráfico          | Equivalente a DS (Servicio diferenciado) de IPv4 que determinaba la prioridad de cada paquete.                                                   |
| Etiqueta de flujo         | Todos los paquetes con la misma etiqueta reciben el mismo trato por parte del router.                                                            |
| Longitud de contenido     | del paquete IPv6                                                                                                                                 |
| Encabezado siguiente      | Indica el tipo de contenido de datos que lleva el paquete, esto permite que se transmita la información al protocolo de capa superior apropiado. |
| Limite de saltos          | Campo de 8 bits que reemplaza al campo TTL de IPv4.                                                                                              |
| Dirección IPv6 de origen  | De donde proviene el paquete                                                                                                                     |
| Dirección IPv6 de destino | A donde va el paquete                                                                                                                            |

# Direcciones de Red IPv4


## Estructura de direcciones IPv4
- Cada IP esta compuesta por 32 bits divididos en 4 octetos separados por puntos. El espacio de direccionamiento es de $2^{32} = 4 \: 294 \: 967 \: 296$
- La representación binaria es compleja, por ende se usa notación decimal punteada.
- Un [[Conceptos en Redes#Host|host]] con conexión a varias redes debe tener por lo menos una dirección IP por cada interfaz.

- ![[Pasted image 20240505121020.png]]

## Porciones de Red y Host
Dentro de la secuencia de 32 bits, una porción de los bits identifica la red y la otra identifica el host.
- Los bits de la porción de red, también conocidos como **NetID**, deben ser idénticos en todos los dispositivos de la misma red. Estos son asignados por una autoridad global, como la [[Organizaciones#IANA (Internet Assigned Numbers Authority)|IANA]].
- Los bits de la porción de host, o **HostID**, deben ser únicos para identificar un host específico dentro de una red.
![[Pasted image 20240505125031.png]]

- **Dirección IP:** Una dirección IP es un identificador único asignado a cada dispositivo conectado a una red que utiliza el protocolo de Internet (IP). Esta dirección se compone de una parte que identifica la red y otra parte que identifica el host en esa red. Por ejemplo, en la dirección IP 192.168.1.100, "192.168.1" es la porción de red y "100" es la porción de host.

- **Dirección de Red:** La dirección de red es la parte de una dirección IP que identifica la red a la que pertenece un dispositivo. En una dirección IP, los bits correspondientes a la dirección de red son los bits que están fijos y no cambian entre diferentes dispositivos en la misma red. Por ejemplo, si una red utiliza direcciones IP del rango 192.168.1.0/24, la dirección de red sería "192.168.1.0".
## Mascara de subred
Una máscara es un número de 32 bits tal que al hacer una operación *AND* con una IP dada obtenemos la dirección de red que le corresponde.
![[Pasted image 20240505125151.png]]
### Caso práctico

![[Pasted image 20240505125643.png]]

Realizando operación *AND*
![[Pasted image 20240505125659.png]]

## Longitud de prefijo
Es el número de bits fijados en **1** en la máscara de subred. Se escribe mediante la *notación de barra diagonal*. Por tanto, se cuenta el número de bits en la máscara de subred y se antepone una barra diagonal.
![[Pasted image 20240505130212.png]]

## Cantidad de redes y hosts
La cantidad de redes se calcula a partir de la cantidad de bits de la porción de red. Siendo $N$ la cantidad de bits de la porción de red:
$$ \text{Cantidad de redes : } \quad 2^N $$
La cantidad de host se calcula a partir de la cantidad de bits de la porción de host. Siendo $K$ la cantidad de bits de la porción de host:
$$ \text{Cantidad de host : } \quad 2^K $$

## IPv4 Basado en clases

![[Pasted image 20240505130410.png]]
![[Pasted image 20240505130417.png]]


## Direcciones especiales
**Direcciones reservadas para redes privadas**
- Existe un conjunto de direcciones reservadas para uso privado.
- No son válidas para su uso en Internet.
	- Se pueden asignar a redes aisladas de Internet.
	- Se pueden asignar redes conectadas a través de un router que hace traducción de direcciones de red ([[#NAT (Network Address Translation)]]).
- Los rangos de direcciones IP privadas son
	- 10.0.0.0 - 10.255.255.255 $\sim$ 1 red privada de clase A
	- 172.16.0.0 - 172.31.255.255 $\sim$ 16 redes privadas de clase B.
	- 192.168.0.0 - 192.168.255.255 $\sim$ 256 redes privadas de clase C.

**Direcciones de loopback (127.x.y.z)**
- Direcciones de bucle interno (*loopback*)
- Casi todas las máquinas tienen como dirección de loopback la 127.0.0.1

**Direcciones broadcast (terminadas en 11...111)**
- Se utilizan para enviar un paquete a todas las máquinas de la red local.
- Formato de las direcciones broadcast
	- Todos los bits de identificador de host se ponen a valor1
	- Ultimo valor del rango de direcciones de la red.


## IPv4 sin clases
Los ISP (Proveedor de Servicios de Internet) ya no están limitados a una máscara de subred de /8, /16 o /24. Ahora pueden asignar espacio de direcciones de manera más eficiente mediante el uso de cualquier longitud de prefijo que empiece con /8. Utilizan los prefijos de red.

![[Pasted image 20240505132015.png]]

## Gateway predeterminado
Identifica la dirección IP del [[Red Essentials#Router (Enrutador)|router]] al que se debe enviar un paquete cuando el destino no está en la misma subred de la red local. Por lo general tienen como identificador de host 1 o 254.
![[Pasted image 20240505132225.png]]

## Direcciones de red, de host y de difusión

- **Dirección de red**: La porción de host solo son ceros.
- **Dirección de host (azules)**: la porción de host tiene 0 y 1.
- **Primera dirección de host (verde)**: Porción de host todos ceros menos el último.
- **Ultima dirección de host (rojo)**: Porción de host todos son 1 excepto el último.
- **Dirección de difusión**: La dirección de host se compone de puros 1.

![[Pasted image 20240505132534.png]]


## Asignación de IPv4 estática
La IPv4 no cambia. La asignación de la dirección IP, mascara y gateway (puerta de enlace) se ingresan a mano. Usado en impresoras, servidores y dispositivos de red.

![[Pasted image 20240505143751.png]] 

![[Pasted image 20240505143800.png]]

## Asignación de IPv4 dinámica
La dirección IP no permanece constante en el tiempo. El servidor [[Protocolos#DHCP (Dynamic Host Configuration Protocol)|DHCP]] proporciona una dirección IPv4, una máscara de subred, una puerta de enlace predeterminada y otra información de configuración. Este método es comúnmente utilizado en PC, tabletas y laptops de oficina

![[Pasted image 20240505144043.png]]

![[Pasted image 20240505144047.png]]


## Comunicación IPv4


| Tipo de comunicación | Destino                                                               | Intervalo de direcciones                                                                  |
| -------------------- | --------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| Unidifusión          | [[Conceptos en Redes#Host\|Host]] individual                          | **0.0.0.0  223.255.255.255**                                                              |
| Difusión             | Todos los host de la red                                              | La dirección de destino es **255.255.255.255**                                            |
| Multidifusión        | Un grupo seleccionado de host, probablemente en **diferentes redes**. | IPv4 reservó las direcciones **224.0.0.0 - 239.255.255.255** como rango de multidifusión. |


# Direcciones de red IPv6

## Estructura de IPv6

- Esta compuesto por 128 bits y se escribe en formato hexadecimal.
- Se le llama *hexteto* a un segmento de 16 bits.
- Toda la información adicional de nivel de red se codifica en cabeceras adicionales y se coloca entre la cabecera base y la carga del paquete.

![[Pasted image 20240505145035.png]]

Se pueden colocar de 3 formas

Notación hexadecimal con puntos (forma "oficial")
- **FEDC : BA98 : 7654 : 3210 : FEDC : BA98 : 7654 : 3210**
- **1080 : 0 : 0 : 0 : 8 : 800 : 200C : 417**

Se puede suprimir un **único grupo contiguo de 0s**
- **1080 : 0 : 0 : 0 : 8 : 800 : 200C : 417A** $\to$ **1080 : : 8 : 800 : 200C : 417A**
- **FF01 : 0 : 0 : 0 : 0 : 0 : 0 : 101** $\to$ **FF01 :: 101**
- **0 : 0 : 0 : 0 : 0 : 0 : 0 : 1** $\to$ **:: 1**

Se puede utilizar la forma IPv4
- **0 : 0 : 0 : 0 : 0 : 0 : 13.1.68.3** $\to$ **:: 13.1.68.3**
- **0 : 0 : 0 : 0 : FFFF : 129.144.52.38** $\to$ **:: FFFF : 129.144.52.38**
## Tipos de direcciones IPv6
### Unicast (unidifusión)
Una dirección para una única interfaz. Un paquete dirigido a una dirección *unicast* se entregará únicamente al host identificado con dicha dirección IP. Existen tres tipos: unicast global, de sitio local y de enlace local.
#### Unicast global
Tiene un alcance **ilimitado** en Internet y en todo el mundo. Los paquetes con la fuente global se dirigen a su destino elegido por los enrutadores de Internet, podemos compararlas con las direcciones públicas de IPv4. Es administrado por la [[Organizaciones#IANA (Internet Assigned Numbers Authority)|IANA]].

Abarca desde **2000 :: ** hasta **3FFF : FFFF : FFFF : FFFF : FFFF : FFFF : FFFF : FFFF**


**Formato**:
- **Prefijo Global de Encaminamiento (48 bits):** Los primeros tres bits son 001 y permiten $2^{45}$ organizaciones diferentes (ISP). Esta es la única parte relevante para el encaminamiento global.
- **Identificador de Subred (16 bits):** Permite 65536 subredes por organización.
- **Identificador de Host (64 bits):** Permite identificar hasta $2^{64}$ hosts en cada subred.

![[Pasted image 20240505151109.png]]
![[Pasted image 20240505151115.png]]


#### Unicast site local (Site-Local Address)
- Direcciones unicast privadas que pueden usarse en **intranets**.
- Nunca se encaminan fuera del sitio.

**Formato**:
- Prefijo de formato **fc00::/7**, y va desde **fc00** hasta **(feff : ffff : ...)**. Identificador de sitio (40 bits). Debe seleccionarse aleatoriamente para evitar colisiones.
- Identificador de subred (16 bits)
- Identificador de host (64 bits)

![[Pasted image 20240505152332.png]]

#### Unicast enlace local (Link-Local Address)
- Definen direcciones privadas unicast que se usan en intranets o para comunicarse con otros dispositivos en el mismo enlace local.
- Es un espacio de direcciones plano.
- Nunca se encamina fuera de la zona de ámbito del enlace.
- Permite la autoconfiguración y el descubrimiento de vecinos.

**Formato**:
- El prefijo de formato ocupa 10 bits: **1111 1110 10 (FE80::/10)**
- El resto de los primeros 64 bits (54 bits) son ceros.
- Identificador de host (64 bits).
![[Pasted image 20240505151734.png]]


## IPv6 Anycast
Identifican a un grupo de host. Un paquete dirigido a una dirección *anycast* se entrega a uno solo de los host identificados con esa dirección, normalmente al más cercano, en función de la métrica usada por el protocolo de routing.

![[Pasted image 20240505152638.png]]

- **Definición:** Anycast es un mecanismo de enrutamiento utilizado en IPv6 (y también en IPv4) donde una misma dirección de destino está asignada a múltiples nodos en diferentes ubicaciones de la red. Cuando se envía un paquete a una dirección anycast, la red enruta el paquete al nodo anycast más cercano en términos de métricas de enrutamiento, como la distancia o la latencia.

- **Uso:** Anycast se utiliza para servicios distribuidos geográficamente que pueden ser replicados en múltiples ubicaciones, como servidores DNS raíz, servidores de contenido web y servidores de CDN (Content Delivery Network). Al utilizar anycast, los clientes son automáticamente dirigidos al nodo anycast más cercano, lo que reduce la latencia y mejora la velocidad de acceso al servicio.

## IPv6 Multicast (Multidifusión)
Identifican a un grupo de host. Un paquete dirigido a una dirección *multicast* se entrega a todos los hosts identificados con esa dirección. Implementan también el tráfico broadcast.

![[Pasted image 20240505154442.png]]


## Autoconfiguración de direcciones IPv6

Una técnica de autoconfiguración de direcciones en IPv6 es un método que permite a los dispositivos IPv6 obtener automáticamente direcciones IP y otros parámetros de configuración de red sin intervención manual. Esto incluye métodos como **SLAAC** (Stateless Address Autoconfiguration) y **DHCPv6** (Dynamic Host Configuration Protocol for IPv6).
### SLAAC (Stateless Address Autoconfiguration)
Este método permite a los dispositivos IPv6 obtener automáticamente una dirección IPv6 y otros parámetros de configuración de red, como la máscara de subred y la puerta de enlace predeterminada, sin necesidad de un servidor DHCP. Utiliza la información de red local, como el prefijo de red anunciado por el router, para generar automáticamente la dirección IPv6.

### DHCPv6 (Dynamic Host Configuration Protocol for IPv6)
Similar al [[Protocolos#DHCP (Dynamic Host Configuration Protocol)|DHCP]] en IPv4, DHCPv6 permite a los dispositivos IPv6 obtener direcciones IPv6 y otros parámetros de configuración de un servidor DHCPv6 en la red. A diferencia de SLAAC, DHCPv6 puede proporcionar configuración adicional, como servidores DNS y otros parámetros de red.

### Manual Configuration (Configuración Manual)###
En este método, los administradores de red configuran manualmente las direcciones IPv6 y otros parámetros de configuración en cada dispositivo de la red. Aunque es menos común debido a su falta de automatización, puede ser útil en entornos donde se requiere un control total sobre la configuración de red.

