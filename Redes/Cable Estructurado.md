
# Cableado de cobre
Los datos se transmiten en cables de cobre como impulsos eléctricos.

| Ventajas                        | Limitaciones                                |
| ------------------------------- | ------------------------------------------- |
| Barato                          | Atenuación proporcional a la distancia      |
| Fáciles de instalar             | Interferencia electromagnética (EMI)        |
| Baja resistencia a la corriente | Interferencia de radio frecuencia RFI       |
|                                 | [[Conceptos en Redes#Crosstalk\|Crosstalk]] |
![[Pasted image 20240503155115.png]]

## Tipos de cableado de cobre
Par trenzado, dos hilos de cobre aislado y trenzados entre si. Usan los estándar TIA 568A y TIA 568B.

- Par trenzado no blindado ( Unshlelded Twisted Pair UTP)
- Par trenzado blindado (Shlelded Twisted Pair STP)
- Coaxial

### Cable UTP (Unshlelded Twisted Pair)
![[Pasted image 20240503182227.png]]

| Tipo de cable             | Estandár                             | Aplicación                                                                                                                                      |
| ------------------------- | ------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| Cable directo de Ethernet | Ambos extremos son T568A o T568B     | Conexión de un host de red a un dispositivo como un [[Red Essentials#Switch (conmutador)\|switch]] o [[Red Essentials#Concentrador (Hub)\|hub]] |
| Cruzado Ethernet          | Un extremo T568A, otro extremo T568B | Conecta dos host de red, conecta dos dispositivos de red intermediarios                                                                         |
| De consola                | Propietario de Cisco                 | Conecta el puerto serial de una estación de trabajo al puerto de consola de un router utilizando un adaptador                                   |
![[Pasted image 20240503191347.png]]

#### Categorías de cable UTP
| Categoría    | Velocidad de hasta | Frecuencia hasta | Descripción                                                             |
| ------------ | ------------------ | ---------------- | ----------------------------------------------------------------------- |
| Categoría 1  |                    |                  | Usa el estándar EIA/TIA 568B. Comunicaciones telefónicas                |
| Categoría 2  | 4 Mbps             |                  | Comunicaciones telefónicas y datos de baja capacidad                    |
| Categoría 3  | 10 Mbps            | 16 MHz           | Se usa en redes 10BaseT. Usado para redes ethernet y líneas telefónicas |
| Categoría 4  | 16 Mbps            | 20 MHz           | Usado para ethernet 10BaseT y IEEE 802.5 Token Ring                     |
| Categoría 5  | 100 Mbps           | 100 MHz          | Usado en redes ethernet y fast ethernet                                 |
| Categoría 5e | 1000 Mbps          |                  | Fast ethernet y gigabit ethernet                                        |
| Categoría 6  | 1000 Mbps          | 250 MHz          | Gigabit ethernet                                                        |
| Categoría 6a | 10000 Mbps         | 500 MHz          | Usado en redes 10 gigabit ethernet                                      |

# Fibra óptica
Es un hilo flexible, pero extremadamente delgado y transparente de vidrio muy puro. Los bits se codifican en la fibra como impulsos de luz. 
Actualmente es usado en redes empresariales, FTTH, largo alcance y redes submarinas.
## Diseño interno

- Envoltura
- Material de refuerzo
- Búfer
- Cubierta
- Núcleo

![[Pasted image 20240504001135.png]]
![[Pasted image 20240504001150.png]]

## Tipos de fibra

### Monomodo
![[Pasted image 20240504095038.png]]

### Multimodo
![[Pasted image 20240504095133.png]]

| Monomodo                              | Multimodo                        |
| ------------------------------------- | -------------------------------- |
| Transporta hasta 10 km.               | Longitudes de hasta 550 m        |
| Velocidad de 100 Gbps o más           | Velocidades de 10 Gbps           |
| Normalmente color amarillo (TIA-598C) | Normalmente color naranja o aqua |

## Transceiver
Dispositivo que permite la transmisión y recepción de datos a través de cables de fibra óptica
Como elegir un transceiver:
- Compatibilidad
- Distancia
- Velocidad y ancho de banda
- Tipo de fibra

<div style="text-align: center;">
    <img src="https://intellinetnetwork.eu/cdn/shop/products/10-gigabit-fiber-sfp-optical-transceiver-module-507462-1.jpg?v=1678740877" width=300 height=300>
</div>

# Monomodo vs Multimodo en Fibra óptica
Monomodo y multimodo son dos tipos de fibras ópticas que se utilizan en redes de comunicación para transmitir señales de luz a través de cables de fibra. La principal diferencia entre ambas radica en la forma en que la luz viaja a través de la fibra y en sus características de ancho de banda y alcance.
La fibra monomodo se utiliza para transmisiones a larga distancia y alta velocidad, mientras que la fibra multimodo es más adecuada para distancias cortas y aplicaciones locales donde no se requiere una transmisión de alta velocidad y larga distancia.


# UTP vs Fibra

| Cuestión de implementación     | Cableado UTP  | Cableado Fibra |
| ------------------------------ | ------------- | -------------- |
| Velocidad de transferencia     | Hasta 10 Gbps | 100 Gbps o más |
| Distancia                      | 1 a 100 m     | 1 m a 100 km   |
| Inmunidad EMI y RFI            | Baja          | Alta (total)   |
| Inmunidad peligros eléctricos  | Baja          | Alta (total)   |
| Costo de medio de comunicación | Más baja      | Más alta       |
| Habilidades de instalación     | Más baja      | Más alta       |
| Precauciones de seguridad      | Más baja      | Más alta       |

# Cableado estructurado

| Componente                                          | Descripción                                                                                                                                                                                                   |
| --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1. Cableado de área de trabajo                      | Elementos para la conexión entre los dispositivos o equipo y la salida deinformación. Cables UTP fáciles de cambiar.                                                                                          |
| 2. Cableado Horizontal                              | Cableado que recorre entre el piso y techo. Se debe usar cables UTP, STP o fibra multimodo                                                                                                                    |
| 3. Armario de cableado y cableado de administración | Soporte metálico destinado a alojar equipamiento electrónico, informático y de comunicaciones para un piso.                                                                                                   |
| 4. Cableado vertical                                | Interconexión entre los armarios de cables, [[Conceptos en Redes#Data Center (Centro de datos)\|data center]] y central de comunicaciones. Admite uso de cables cables UTP, STP y fibra multimodo o monomodo. |
| 5. Cableado del centro de datos                     | Cableado en sala de servidores, precauciones de instalación. Uso de cables UTP, STP o fibra multimodo                                                                                                         |
| 6. Centro de comunicaciones                         | Se conoce así a la sala en la que se alojan y centralizan todos los elementos que componen el sistema de telecomunicaciones. Conecta el edificio con el exterior                                              |
| 7. Cableado de campus                               | Conecta al edificio con el exterior, en la actualidad usa conexión fibra monomodo.                                                                                                                            |
![[Pasted image 20240504100304.png]]
