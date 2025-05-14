

# Lecturas complementarias


# Tipos de interfaces de red

Las interfaces de red son los puntos a través de los cuales un dispositivo se conecta a una red. Existen varios tipos de interfaces de red que permiten la conexión de dispositivos, cada uno con características y configuraciones específicas. 

## Interfaz Ethernet (LAN)
La interfaz Ethernet es una de las más comunes para redes de área local (LAN). Utiliza el protocolo Ethernet para la transmisión de datos entre dispositivos dentro de una misma red. Se caracteriza por ser una conexión cableada y de alta velocidad.

### Ejemplo de configuración en un router Cisco:
```bash
interface FastEthernet0/0
description Conectado a la red local
ip address 192.168.1.1 255.255.255.0
no shutdown
```

#### Explicación de comandos:
- `interface FastEthernet0/0`: Selecciona la interfaz FastEthernet en el router.
	- **FastEthernet** significa que se esta usando el estándar Ethernet de 100 Mbps
	- **0/0** indica número de interfaz ranura / número de puerto
- `description Conectado a la red local`: Añade una descripción para identificar la interfaz.
- `ip address 192.168.1.1 255.255.255.0`: Asigna la dirección IP 192.168.1.1 con una máscara de subred 255.255.255.0.
- `no shutdown`: Activa la interfaz (sin este comando, la interfaz estaría apagada). Si este comando no se ejecuta, la interfaz permanecerá deshabilitada, aunque tenga configuración de IP o descripción.



## Interfaz WAN (Wide Area Network)
La interfaz WAN se utiliza para conectar redes que están geográficamente separadas. Este tipo de conexión es común para vincular redes LAN a través de Internet o para interconectar oficinas en distintas ubicaciones.

### Ejemplo de configuración en un router Cisco:
```bash
interface Serial0/0
description Conectado a la red WAN
ip address 10.0.0.1 255.255.255.0
clock rate 64000
no shutdown
```

#### Explicación de comandos:
- `interface Serial0/0`: Selecciona la interfaz serial, típica en conexiones WAN.
	- Los datos se transmiten de forma secuencial a través de una conexión punto a punto
	- [Router A] ---- [Línea serial] ---- [Router B]
- `clock rate 64000`: Establece la tasa de reloj de la interfaz (necesario en conexiones seriales).
	- El comando `clock rate 64000` establece la velocidad de la interfaz en **64 Kbps**.
	- Los datos se transmiten de forma secuencial, un bit a la vez. El dispositivo que proporciona la tasa de reloj define la frecuencia de transmisión. Esto asegura que ambos extremos de la comunicación estén sincronizados.


## Interfaz Wi-Fi
La interfaz Wi-Fi es una conexión inalámbrica que permite la transmisión de datos a través de ondas de radio. Es utilizada para conectar dispositivos sin necesidad de cables, creando redes LAN inalámbricas.

### Ejemplo de configuración en un router Cisco:
```bash
interface Dot11Radio0
description Conectado a la red inalámbrica
encapsulation dot1Q 1 native
no shutdown
bridge-group 1
bridge-group 1 subscriber-loop-control
bridge-group 1 block-unknown-source
no bridge-group 1 source-learning
bridge-group 1 unicast-flooding
bridge-group 1 spanning-disabled
!
```

#### Explicación de comandos:
- `interface Dot11Radio0`: Selecciona la interfaz de radio inalámbrica en el router. (Estándar IEEE 802.11)
- `encapsulation dot1Q 1 native`: 
	- **dot1Q**: Configura la VLAN con encapsulación 802.1Q (dot1Q). El estándar 802.1Q permite encapsular varias VLANs en una misma interfaz física.
	- **1**: Es el identificador de la VLAN
	- **native**: La VLAN 1 es la VLAN nativa, significa que todos los paquetes que no tengan una etiqueta de VLAN específica se asignarán a esta VLAN de forma predeterminada.
- `bridge-group 1`: Asigna esta interfaz al grupo de puente 1.
	- Es una función que permite agrupar varias interfaces en un mismo grupo de puente para que funcionen como si estuvieran en la misma red local (LAN)
- `subscriber-loop-control`: El control de bucles detecta y previene la creación de bucles de red (donde los paquetes podrían circular indefinidamente).
- `block-unknown-source`: Impide que el bridge-group 1 reenvíe paquetes cuyo origen sea desconocido.
- `source-learning`: Al desactivar el aprendizaje de direcciones, el puente no memoriza las direcciones de origen de los paquetes que recibe.
- `unicast-flooding`
	- **Unicast**: Es un tipo de comunicación donde un dispositivo envía paquetes directamente a otro dispositivo específico, usando su dirección MAC (Media Access Control) como identificador.
	- **Flooding de unicast** significa que el switch o router no sabe a que puerto enviar el paquete, por tanto, lo envía por todas las interfaces (excepto por la interfaz de entrada). Este proceso se conoce como *flooding* (inundación).
- `spanning-disabled`: El protocolo STP se usa para prevenir bucles en la red. En algunos casos puede resultar beneficioso
	- Si una red es simple y pequeña, no es necesario tener STP activo porque no hay riesgo de bucles de red
	- STP introduce una pequeña latencia al revisar constantemente la topología de la red para buscar bucles. En redes sencillas se puede evitar esta latencia
- `!` separador que indica el final de una sección en la configuración

Adicionalmente, se puede configurar una red para invitados, como en este ejemplo:
```bash
interface Dot11Radio0.1
description Red inalámbrica de invitados
encapsulation dot1Q 1
ip address 10.0.0.1 255.255.255.0
no shutdown
```
Aquí se crea una subinterfaz virtual para la red de invitados y se le asigna una dirección IP y una VLAN separada.

