- El objetivo principal de la capa de red es el encaminamiento es decir, llevar paquetes desde el origen hasta el destino a través de la subred
- Es necesario que la capa de red tenga información de la topología de la red para elegir la ruta más adecuada
- También se encarga de la interconexión de redes heterogéneas formando inter redes


# Procesos básicos

- **Direccionamiento de terminales**: Asignar a cada terminal una dirección IP única para identificarlo en la red.
- **Encapsulamiento**: Encapsula la información de la capa de transporte (segmento) en paquetes. Adiciona las direcciones IP de origen y destino.
- **Enrutamiento**: Envía paquetes a un host de destino en otra red, a través del procesamiento de un router Se sigue el proceso de tomar el mejor camino, proceso denominado **routing**. Se denomina salto de paquete cuando atraviesa un router en el camino.
- **Desencapsulamiento**: Cuando llega un paquete a un destino este revisa si la IP de destino coincide con la suya De ser así, des encapsula la información (segmento) y lo envía a las capas superiores.

# Componentes
- [[Red Essentials#Switch core|Switch core]]
- [[Red Essentials#Switch (conmutador)|Switch]]
- [[Red Essentials#Router (Enrutador)|Router]]
- **Equipos terminales**: Cualquier equipo o dispositivo al final de la red en el sentido del usuario, pueden ser PC, impresoras, etc.
# Enrutamiento
Cada enrutador posee una tabla de enrutamiento. Indica que interfaz de salida elegir para llegar a cada uno de los enrutadores de las otras subredes. Existen diversos algoritmos de enrutamiento.

Cada vez que un paquete llega al un enrutador:
- **Almacena** el paquete.
- **Comprueba** la **suma de verificación**.
- **Elige la interfaz de salida** en base a la tabla de enrutamiento y dirección de destino.
- **Reenvía el paquete** por la interfaz elegida.

# Tipos de enrutamiento

## Enrutamiento estático
En el enrutamiento estático, se utiliza tablas estáticas para configurar y seleccionar manualmente las rutas de red, la información se carga en los enrutadores previamente. El enrutamiento estático es útil cuando los parámetros de la red permanecen constantes. Es vulnerable a inconvenientes esperados, como la congestión de la red, el enrutamiento estático generalmente disminuye la adaptabilidad y la flexibilidad de las redes.

En el ámbito del enrutamiento de redes, existen múltiples estrategias que los dispositivos pueden utilizar para determinar cómo enviar paquetes a través de una red. Dos de estos métodos son el **enrutamiento por ruta más corta** y el **enrutamiento por inundación**

### Enrutamiento por ruta más corta
Se siguen los siguientes pasos:
- Se forma un grafo no ponderado no dirigido con la estructura de la red donde los enrutadores son los nodos y los arcos son las líneas de comunicación.
- Cada nodo se etiqueta con la distancia al nodo origen a través de la mejor ruta, al inicio de temporales y una vez determinada la ruta posible se vuelven permanentes.
- Se busca la ruta más corta al destino.
![[Pasted image 20240504205353.png]]

### Enrutamiento por inundación
- Cada paquete recibido se reenvía por todas las interfaces de salida excepto por donde vino.
- Muy eficaz pero muy ineficiente. Genera una gran cantidad de tráfico.
- Para evitar que los paquetes se muevan indefinidamente, se hace uso de un contador de vida o registro de paquetes procesados o un registro de nodos visitados.
- Tiene como principales ventajas la robustez o seguridad de llegar al destino y llegada por la ruta más corta en el sentido de comparación.
- Mejorado: **Inundación selectiva**.

![[Pasted image 20240504210328.png]]

## Enrutamiento dinámico
En el enrutamiento dinámico, los enrutadores crean y actualizan las tablas de enrutamiento en tiempo de ejecución según las condiciones reales de la red. Intentan encontrar la ruta más rápida desde el origen hasta el destino mediante un protocolo de enrutamiento dinámico, que es un conjunto de reglas que crean, mantienen y actualizan la tabla de enrutamiento dinámico. La mayor ventaja del enrutamiento dinámico es que se adapta a las condiciones cambiantes de la red, incluidos el volumen de tráfico, el ancho de banda y las fallas de la red.

### Enrutamiento por vector distancia
- Cada enrutador mantiene una tabla que indica la mejor distancia conocida a cada nodo de la subred y la interfaz de salida.
- La tabla se actualiza intercambiando información entre nodos.
- El enrutador sabe o puede calcular la distancia a sus vecinos.
- Utiliza algoritmos de ruta más corta, destacando el de Bellman-Ford.
- Tiene la limitación de convergencia lenta y no toma en cuenta el ancho de banda para elegir la ruta.
![[Pasted image 20240504211544.png]]

### Enrutamiento por estado del enlace
Los protocolos de estado de enlace, como OSPF (Open Shortest Path First), crean un mapa completo de la red al intercambiar información sobre todos los enlaces conocidos con todos los routers dentro de una misma área de enrutamiento. Utilizan el algoritmo de Dijkstra para calcular la ruta más corta.

- Cada router contacta con sus vecinos y mide la distancia o el coste entre ellos.

- Se construye un paquete **LSP** (Link State Packet), que incluye:
    - Identidad del emisor.
    - Lista de vecinos y sus respectivas distancias (coste de enlaces directos).

- Envía su **LSP** por inundación controlada a todos los routers de la red.
    - Los **LSP** solo se envían cuando hay cambios en la red.
    - Los **LSP** se numeran secuencialmente y tienen un tiempo de vida limitado.
    - Se evita enviar cualquier LSP por el mismo camino por donde se recibió.
    - Cada LSP recibido se compara con el que mantiene el nodo. Si es duplicado, se rechaza y no se retransmite.

- Recopila los LSP de todos los demás nodos.

- Calcula las rutas más óptimas utilizando diferentes algoritmos.
 
![[Pasted image 20240504212652.png]]
![[Pasted image 20240504212707.png]]
![[Pasted image 20240504212713.png]]
![[Pasted image 20240504212725.png]]
![[Pasted image 20240504212731.png]]
![[Pasted image 20240504212745.png]]
![[Pasted image 20240504212751.png]]
![[Pasted image 20240504212757.png]]
![[Pasted image 20240504212803.png]]



### Enrutamiento jerárquico
El enrutamiento jerárquico divide la red en diferentes áreas jerárquicas para simplificar la administración y optimizar el rendimiento. Esto permite a los routers concentrarse solo en la información de enrutamiento que es relevante para su área específica, reduciendo la cantidad de información de enrutamiento necesaria en cada dispositivo

- Los nodos de la red se agrupan en grupos y estos, a su vez, se dividen en subgrupos con niveles de jerarquización.
- Cada grupo o subgrupo pertenece a un nivel dentro de la jerarquía, y cada nodo puede pertenecer a un nivel distinto dentro de la jerarquía de la red.
- Para conectar los grupos entre sí se definen los denominados nodos jerárquicos o pasarelas, que serán los encargados de gestionar el tráfico hacia o desde los grupos.
- Dentro de cada grupo, cada nodo de conmutación sabe cómo encaminar paquetes al resto de los nodos del grupo, pero no conoce la estructura interna de los demás grupos.
- Al encaminar entre diferentes grupos de nodos, se considera a cada grupo como una región independiente.
- Para encaminar tráfico entre nodos de diferentes regiones, los nodos jerárquicos deben encontrar rutas entre sí.
- En redes más grandes se necesitan más niveles de jerarquía: áreas o subregiones, zonas, grupos.
#### Ventajas

- Favorece a la escalabilidad de la red.
- Aislamiento entre zonas o regiones jerárquicas y otras.

#### Desventajas

- Fallos en los nodos jerárquicos.
- Rutas desaprovechadas.
- Rutas jerárquicas no siempre óptimas.
- Configuración y diseño de red más complejos.

![[Pasted image 20240504223324.png]]
![[Pasted image 20240504223335.png]]


### Enrutamiento por difusión
El enrutamiento por difusión envía la misma información a todos los nodos de la red. Este método es común en aplicaciones donde cada nodo necesita recibir la misma información simultáneamente, como en transmisiones de multimedia.

El origen brinda una copia a cada destino por alguna de estas formas:
- Usando inundación
- **Enrutamiento en base a un árbol de sumidero** con el origen al enrutador actual. Todos los enrutadores deben conocer todos los árboles de sumidero.
- **Reenvío de ruta invertida** donde el paquete se reenvía solo si llegó por la mejor ruta.

### Enrutamiento multicast
El enrutamiento Multicast es similar a la difusión, pero más eficiente, ya que dirige la información solo a los nodos que han solicitado explícitamente unirse a un grupo multicast específico.

- El enrutamiento Multicast requiere administración de grupos, crear y destruir grupos y añadir y quitar [[Conceptos en Redes#Host|host]] o destinos de ellos.
- Los enrutadores deben saber a que grupos pertenecen sus host.
- Los enrutadores propagan dicha información a sus vecinos recursivamente.
- Cuando un encaminador recibe un paquete Multicast de uno de sus host examina su árbol de expansión y lo recorta.
# Protocolos de enrutamiento
Es un conjunto de reglas que especifican cómo los enrutadores identifican y reenvían paquetes a lo largo de una ruta de red. Los protocolos de enrutamiento se agrupan en dos categorías distintas: **protocolos de puerta de enlace interior** y **protocolos de puerta de enlace exterior**.

## Protocolos de puerta de enlace interior
Son aquellos protocolos utilizados para encaminar el trafico dentro de un [[#Sistemas autónomos|sistema autónomo]] o dentro de la infraestructura de una misma empresa.

### Protocolo RIP (Routing Information Protocol)
Es un protocolo de enrutamiento que se basa en el número de saltos para decidir cuál es la mejor ruta hacia una red de destino. Utiliza los algoritmos o métodos del [[#Enrutamiento por vector distancia|vector distancia]].
![[Pasted image 20240504225226.png]]

### Protocolo OSPF (Open Shortest Path First)
Recopila información de todos los demás enrutadores del sistema autónomo para identificar la ruta más corta y rápida hacia el destino de un paquete de datos en base al ancho de banda. Utiliza el método de [[#Enrutamiento por estado del enlace|estado de enlace]] con el **Algoritmo de Dijkstra** para encontrar la ruta más corta entre nodos.

**Tipos de paquetes**.

- **Hello**: estos paquetes se envían periódicamente y contienen información sobre el enrutador emisor, como su identificación de router (Router ID) y el ID de área.

- **Descripción de BD**: se utilizan para intercambiar resúmenes de la base de datos de enrutamiento entre vecinos OSPF. Estos resúmenes permiten a los enrutadores sincronizar su base de datos de estado de enlace.

- **Actualización LSU (Link State Update)**: contienen información detallada sobre el estado de enlace de los enrutadores vecinos. Estos paquetes se utilizan para informar a otros enrutadores sobre cambios en la topología de la red.

- **Solicitud LSR (Link State Request)**: se utilizan para solicitar información específica sobre el estado de enlace de otros enrutadores. Cuando un enrutador necesita más detalles sobre ciertos enlaces, envía paquetes LSR a sus vecinos.

- **Acuse de recibo LSAck (Link State Acknowledgement)**. se utilizan para confirmar la recepción de paquetes LSU. Cuando un enrutador recibe un paquete LSU, responde con un paquete LSAck para indicar que ha recibido la actualización correctamente.

## Sistemas autónomos
Un sistema autónomo (AS) es un conjunto de redes IP administradas por uno o más operadores de red, en la que se **utiliza la misma política de enrutamiento**. Comúnmente cada AS es gestionado por una única organización, como un proveedor de acceso a internet (ISP), una gran empresa tecnológica, una universidad o una agencia gubernamental. Cada ordenador o dispositivo que se conecta a Internet está conectado a un AS.
![[Pasted image 20240504230556.png]]

#### Características de Sistemas Autónomos

- Los sistemas autónomos (AS) se comunican entre sí utilizando el protocolo de enrutamiento BGP.
- Cada sistema autónomo posee un número que lo identifica.
- La representación textual de los números de los sistemas autónomos está definida en la RFC 5396.
- Los números de sistemas autónomos son asignados por la [[Organizaciones#IANA (Internet Assigned Numbers Authority)|IANA]] y van desde 0 hasta 65353
- Cada sistema autónomo controla un conjunto específico de direcciones IP, denominado rango de direcciones IP.
- Dentro de un sistema autónomo se utiliza un protocolo de enrutamiento interior IGP mientras que entre sistemas autónomos se utiliza el protocolo de enrutamiento exterior EGP.

## Espacio de direcciones IP
Un grupo o rango específico de direcciones IP se llama **espacio de direcciones IP**. Cada AS controla una cierta cantidad de espacio de direcciones IP. Un grupo de direcciones IP también se conoce como **bloque** de direcciones IP.

| Rango de direcciones           | Clase   |
| ------------------------------ | ------- |
| 10.0.0.0 - 10.255.255.255      | Clase A |
| 172.16.0.0 - 172.31.255.255    | Clase B |
| 192.168.0.0  - 192.168.255.255 | Clase C |
**Este rango de direcciones esta limitado para el uso privado**.

## Protocolos de puerta de enlace externa
Son aquellos utilizados para encaminar el trafico entre diferentes **sistemas autónomos**.

### Protocolo BGP(Border Gateway Protocol)
- Considerados protocolos tipo vector distancia con mejoras: actualizaciones fiables, solo en casos de cambio de topología y con atributos adicionales.
- Los nodos vecinos BGP usan el puerto TCP 179 para enviar actualizaciones
- Puede ser usado como IGP (eBGP) o EGP (eBGP).
- Se le conoce como protocolo de enrutamiento de internet.
- Su protocolo EGP es del tipo vector de ruta (*path vector*) con varios atributos en base a los cuales se decide la ruta más corta.
- Su versión más reciente es la BGPv4 normado en la RFC 4271..
- Tiene una distancia administrativa de 20 (eBGP) y 200 (iBGP).
- Diseñado para ser robusto y no tan rápido.
- Por defecto se comporta de manera similar al RIP entre AS.

#### Mensajes BGP
| Tipo de Mensaje | Descripción                                                                                                                                                                             |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| OPEN            | Se envía tras el establecimiento de la conexión TCP. Su función es básicamente informar a los routers vecinos información del BGP usado, número de sistemas autónomos e Id del proceso. |
| KEEPALIVE       | Son mensajes que sirven para mantener la conexión, son la respuesta al mensaje OPEN.                                                                                                    |
| NOTIFICATION    | Notifican apertura y cierre de la conexión BGP y TCP.                                                                                                                                   |
| UPDATE          | Son usados para intercambiar información de enrutamiento como atributos, prefijos de redes y longitud de cada ruta y las eliminadas. Se envían cuando hay cambio de topología-          |

#### Atributos del vector de ruta BGP

![[Pasted image 20240505003028.png]]
![[Pasted image 20240505003048.png]]
![[Pasted image 20240505003054.png]]

### Criterios de selección de rutas
- Rutas con mayor valor **Local preference**.
- Rutas que el propio router originó, es decir, **de origen local**.
- Rutas con **AS-Path más corto**.
- Rutas con el atributo Origin sea del menor tipo (IGP < EGP < Incomplete)


# ¿Como arma las rutas el host?

Se tiene tres destinos posibles:
- A sí mismo
- A una PC o nodo local. Los equipos comparten la misma dirección de red.
- A un módulo E/S. El equipo esta un una red remota. No se comparte la misma dirección de red. Entran a tallar los routers y el routing.
![[Pasted image 20240505003802.png]]

## Gateway predeterminado
El gateway predeterminado es el dispositivo de red que puede enrutar el tráfico a otras redes. Es el router el que puede enrutar el tráfico fuera de la red local, Si se piensa en una red como si fuera una habitación, el gateway predeterminado es como la puerta.
![[Pasted image 20240505003922.png]]

# Tablas de routing
Al introducir el comando **netstat -r** o su comando equivalente **route print**, se muestran tres direcciones relacionadas:
- **Lista de interfaces**: Muestra una lista de las direcciones de control de acceso a los medios (MAC) y el número de interfaz asignado a cada interfaz.
- **Tablas de rutas IPv4**: Es una lista de todas las rutas IPv4 conocidas, incluidas las conexiones directas, las redes locales y las rutas locales predeterminadas.
- **Tabla de rutas IPv6**: Es una lista de todas las rutas IPV6 conocidas, incluidas las conexiones directas, las redes locales y las rutas locales predeterminadas.

![[Pasted image 20240505004331.png]]

# Enrutamiento

La tabla de routing de un router almacena información sobre lo siguiente:

- **Rutas conectadas directamente**: Estas rutas provienen de interfaces de router activas. Los routers agregan una ruta conectada directamente cuando una interfaz se configura con una dirección IP y se activa. Cada una de las interfaces del router está conectada a un segmento de red diferente.
- **Rutas remotas**: Estas rutas provienen de redes remotas conectadas a otros routers. El administrador de redes puede configurar las rutas a estas redes manualmente en el router local o dichas rutas pueden configurarse de manera dinámica al permitir que el router local intercambie información routing con otros routers mediante el protocolo de routing dinámico.
![[Pasted image 20240505004706.png]]
