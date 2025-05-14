
# Control de acceso al medio (MAC)

El control de acceso al medio **MAC** es el conjunto de mecanismos y protocolos de comunicaciones a través de los cuales varios *interlocutores* (dispositivos en una red, como computadores, teléfonos móviles, etc.) se ponen de acuerdo para compartir un **medio de transmisión** común (cable eléctrico o [[Cable Estructurado#Fibra óptica|fibra óptica]] o comunicaciones inalámbricas).

Equivalente al control de acceso vehicular a una autopista mediante un conjunto de reglas. Formado por reglas de ingreso de las tramas a la red física.

Depende de
- Topología: Como se muestra la conexión de nodos
- Compartición de medios: Como se comparte la información entre nodos

# Topología de red
https://techriders.tajamar.es/topologia-fisica-vs-topologia-logica/
Cada topología de red lleva asociada una **topología física y lógica**, la primera es la que define la **estructura física** (la manera en que se organizan los cables) de la red. Mientras que la topología lógica define el **conjunto de reglas para la gestión de transmisión** de datos en la red.
<div style="text-align: center;">
    <img src="https://farm5.staticflickr.com/4461/37683530836_2ab63da521_b.jpg" alt="Texto alternativo de la imagen">
</div>
<div style="text-align: center;">
    <img src="https://farm5.staticflickr.com/4477/37022302574_46d1424d3b_b.jpg" alt="Texto alternativo de la imagen">
</div>


## Topología física
La topología de una red de computadoras se refiere a la disposición física de los dispositivos (nodos) y las conexiones de comunicación (enlaces) entre ellos. Esta configuración es crucial porque afecta el rendimiento, la capacidad de administración y la escalabilidad de la red.


### Punto a Punto
La topología punto a punto consiste en una conexión directa entre dos dispositivos o nodos. Los nodos no tienen que compartir los medios con otros [[Conceptos en Redes#Host|hosts]] . Es la forma más sencilla de red y se utiliza comúnmente para conectar un dispositivo a otro, como en el caso de un enlace directo entre dos computadoras o entre un cliente y un servidor. Usado en redes WAN.
![[Pasted image 20240504122833.png]]

#### Ventajas
- Simplicidad en la configuración y el mantenimiento.
- Bajo costo, ya que solo requiere el hardware necesario para conectar dos dispositivos.
- Eficiencia en la comunicación debido a la ausencia de dispositivos intermediarios.

#### Desventajas
- Escalabilidad limitada, ya que cada conexión solo involucra dos dispositivos.
- No adecuada para redes más grandes donde múltiples dispositivos necesitan interconectarse.


### Bus
En una topología de bus, todos los dispositivos están conectados a un único cable conductor, llamado bus o troncal. Los datos enviados por cualquier dispositivo son recibidos por todos los otros, pero solo el destinatario correcto los procesa. Usado en redes LAN.

<div style="text-align: center;">
    <img src="https://gustavo2792.wordpress.com/wp-content/uploads/2012/01/bus1.jpg?w=241&h=181" alt="Texto alternativo de la imagen">
</div>

#### Ventajas
- Facilidad de instalación.
- Costo reducido ya que requiere menos cableado.

#### Desventajas
- Difícil de diagnosticar y aislar fallas.
- Limitación en el número de dispositivos debido a señales que pueden debilitarse con la longitud del bus.

### Estrella
En la topología de estrella, cada dispositivo se conecta directamente a un concentrador central (hub) o un switch. Si un dispositivo quiere enviar datos a otro, envía los datos al hub, que luego los retransmite al destino final. Usado en redes LAN.
<div style="text-align: center;">
    <img src="https://gustavo2792.wordpress.com/wp-content/uploads/2012/01/estrella.jpg" alt="Texto alternativo de la imagen">
</div>

#### Ventajas
- Fácil de manejar y localizar problemas.
- Adición o eliminación de dispositivos sin afectar al resto de la red.

#### Desventajas
- Dependencia del punto central; si el hub falla, toda la red se cae.
- Requiere más cable que la topología de bus.

### Estrella Extendida
Tiene como base la topología en estrella pero interconecta a varias de estas, en donde cada dispositivo intermedio de las diferentes estrellas unitarias se conectan a un nuevo punto central . Usado en redes. En esta configuración, una estrella central se conecta a una o más estrellas secundarias. Cada nodo en cada estrella secundaria está conectado a un concentrador o switch local, y estos concentradores o switches secundarios se conectan a un concentrador o switch central.
<div style="text-align: center;">
    <img src="https://gustavo2792.wordpress.com/wp-content/uploads/2012/01/estrella-extendida.jpg" alt="Texto alternativo de la imagen">
</div>

#### Ventajas
- Escalabilidad: Permite la expansión de la red agregando más estrellas secundarias.
- Gestión y diagnóstico de problemas facilitados, manteniendo la independencia de cada segmento de la estrella.

#### Desventajas
- Dependencia de múltiples concentradores o switches, aumentando el riesgo de fallo centralizado.
- Mayor coste y complejidad en el cableado comparado con una simple estrella.


### Anillo
En una topología de anillo, cada dispositivo está conectado exactamente a otros dos dispositivos, formando un circuito cerrado (anillo). La información se transmite en una dirección alrededor del anillo, de nodo a nodo. A diferencia de la topología de bus, no necesita tener una terminación. Usado en redes LAN.
<div style="text-align: center;">
    <img src="https://gustavo2792.wordpress.com/wp-content/uploads/2012/01/anillo.jpg" alt="Texto alternativo de la imagen">
</div>

#### Ventajas
- No requiere un servidor central para gestionar la conexión.
- Menos tráfico de red que en una topología de estrella.

#### Desventajas
- Una falla en cualquier cable o dispositivo puede afectar a toda la red.
- La adición o eliminación de dispositivos puede afectar la red.


### Malla
En una topología de malla, cada dispositivo tiene una conexión punto a punto con todos los otros dispositivos. Esto puede ser completo, donde cada nodo está conectado a cada otro nodo, o parcial, donde algunos nodos están conectados a todos los demás y otros no. Usado en redes LAN
<div style="text-align: center;">
    <img src="https://gustavo2792.wordpress.com/wp-content/uploads/2012/01/malla.jpg" alt="Texto alternativo de la imagen">
</div>

#### Ventajas
- Ofrece la máxima redundancia; si una conexión falla, hay múltiples caminos para mantener la red operativa.
- Ideal para aplicaciones críticas donde la fiabilidad es primordial.

#### Desventajas
- Alta cantidad de cableado y puertos de red necesarios, lo que aumenta el costo.
- Complejidad en la gestión y configuración de la red.

### Árbol
La topología de árbol es una variante de la topología de estrella que permite múltiples niveles jerárquicos. Un nodo central se conecta a uno o varios nodos, que a su vez se conectan a otros nodos, formando una estructura de árbol.
<div style="text-align: center;">
    <img src="https://gustavo2792.wordpress.com/wp-content/uploads/2012/01/arbol.jpg?w=445&h=235" alt="Texto alternativo de la imagen">
</div>

#### Ventajas
- Permite expandir fácilmente la red.
- Adecuada para grandes redes distribuidas.

#### Desventajas
- Dependencia del nodo raíz y de los nodos intermedios.
- Más compleja de configurar que las topologías más simples.


## Topología Lógica
La topología lógica de una red se refiere a cómo los datos fluyen entre los dispositivos de la red, independientemente de su configuración física.

### Punto a Punto
Los nodos de los extremos que se comunican en una red conectados físicamente a través de una
cantidad de dispositivos intermediarios. Ello no afecta la topología lógica. Usado en redes WAN.

### Punto a Punto
La topología lógica de punto a punto representa una comunicación directa entre dos dispositivos. En esta topología, cada conexión se establece individualmente entre pares de nodos. Es común en tecnologías como PPP (Protocolo Punto a Punto) utilizadas para conexiones de acceso remoto. Usado en redes WAN.
![[Pasted image 20240504130439.png]]

#### Ventajas
- Configuración simple y directa.
- Alta fiabilidad y seguridad en la conexión ya que solo involucra dos dispositivos.

#### Desventajas
- No escalable para grandes redes sin la incorporación de técnicas adicionales como enrutamiento o conmutación.
- Requiere una gestión individualizada de cada conexión.


### Acceso Múltiple
Las topologías lógicas de acceso múltiple, como Ethernet, permiten que múltiples dispositivos compartan el mismo medio de transmisión. Utilizan mecanismos de control de acceso al medio como **CSMA/CD** (Carrier Sense Multiple Access with Collision Detection) o **CSMA/CA** (Carrier Sense Multiple Access with Collision Avoidance) para regular cómo los dispositivos transmiten datos.
<div style="text-align: center;">
    <img src="https://farm5.staticflickr.com/4471/37710504586_37e43050dd_z.jpg" alt="Texto alternativo de la imagen">
</div>
#### Ventajas
- Eficiencia en costes al compartir un medio común.
- Flexibilidad y facilidad de expansión de la red.

#### Desventajas
- Riesgo de colisiones en redes con alto tráfico, especialmente en CSMA/CD.
- La eficiencia de la red disminuye con el aumento del número de dispositivos en el mismo segmento de red.

### Anillo Lógico
En esta tipología para poder controlar el acceso a la red se transmite un token a cada equipo. Cada equipo al recibir ese token tiene derecho a enviar datos por la red, si no tiene nada que enviar sencillamente envía el token al siguiente equipo. Esta topología es típicamente utilizada en redes que implementan la tecnología Token Ring.
<div style="text-align: center;">
    <img src="https://farm5.staticflickr.com/4494/37710504626_43b222e3f0.jpg">
</div>

#### Ventajas
- No hay colisiones de datos, ya que el token (un paquete especial de datos) controla quién puede transmitir.
- Consistente en el rendimiento, independientemente del número de dispositivos.

#### Desventajas
- Una falla en cualquier dispositivo o conexión puede afectar toda la red.
- Más compleja de configurar y mantener en comparación con la topología de bus.


# Métodos de control de acceso al medio
Las redes de acceso múltiple comparten el medio entre nodos. Es necesario tener reglas que rijan la forma de compartir los medios físicos.

## Acceso basado en la contención
En los métodos de acceso basado en la contención, todos los dispositivos en la red tienen igual derecho a intentar enviar datos a través del medio compartido. No hay una coordinación central que determine qué dispositivo puede hablar en un momento dado, lo que puede llevar a colisiones si dos dispositivos transmiten simultáneamente.



# Métodos de Control de Acceso al Medio (MAC)

El control de acceso al medio (MAC) se refiere a los protocolos utilizados en redes de comunicaciones para determinar cómo los dispositivos en una red tienen derecho a acceder al medio compartido para la transmisión de datos. Este control puede ser clasificado principalmente en dos categorías: acceso basado en la contención y acceso controlado.

![[Pasted image 20240504151905.png]]
![[Pasted image 20240504151918.png]]


## Acceso Basado en la Contención
En los métodos de acceso basado en la contención, todos los dispositivos en la red tienen igual derecho a intentar enviar datos a través del medio compartido. No hay una coordinación central que determine qué dispositivo puede hablar en un momento dado, lo que puede llevar a colisiones si dos dispositivos transmiten simultáneamente.

### CSMA/CD
**Carrier Sense Multiple Access with Collision Detection**: Utilizado en redes Ethernet tradicionales. Los dispositivos verifican si el medio está libre antes de transmitir. Si detectan una colisión, detienen la transmisión y reintentan después de un tiempo aleatorio. Usado principalmente en
LAN Ethernet de half duplex se utiliza este proceso de acceso múltiple Primero se determina si el
medio esta libre, la trama se envía a todos los extremos y el que es el destino recibe y copia la
trama enviada
![[Pasted image 20240504152627.png]]
![[Pasted image 20240504152640.png]]


### CSMA/CA
**Carrier Sense Multiple Access with Collision Avoidance**. 
Utilizado en redes inalámbricas como Wi-Fi. Los dispositivos intentan evitar colisiones mediante el uso de señales para anunciar intenciones de transmisión antes de enviar los datos reales. Usado principalmente en las WLAN. Cada dispositivo que transmite incluye la duración que necesita para la transmisión. Todos los demás dispositivos inalámbricos reciben esta información y saben por cuanto tiempo el medio no estará disponible.
![[Pasted image 20240504152300.png]]



### Ejemplos Comunes
- 
- **CSMA/CA (Carrier Sense Multiple Access with Collision Avoidance)**: 


## Acceso Controlado

### Descripción
En los métodos de acceso controlado, un dispositivo o protocolo central coordina el acceso al medio, dictaminando qué dispositivo puede transmitir en qué momento. Esto reduce o elimina las colisiones y hace un uso más eficiente del medio.

### Ejemplos Comunes
- **Token Ring**: Los dispositivos en la red pasan un "token" de un nodo a otro. Solo el dispositivo que posee el token puede transmitir datos, lo que evita colisiones.
- **Polling**: Un controlador maestro "llama" a cada dispositivo secuencialmente para permitirle transmitir, asegurando que solo un dispositivo transmita en cualquier momento.

### Ventajas
- Eficaz en redes con alto tráfico, minimizando las colisiones y maximizando el uso del medio.

### Desventajas
- Mayor complejidad y coste de implementación.
- Dependencia en el dispositivo o protocolo de control, cuyo fallo puede afectar toda la red.

### Ejemplo de Implementación
```networking
1. En una red Token Ring, configure el servidor o switch principal para generar y controlar la circulación del token entre los dispositivos.
2. En el caso de polling, programe el controlador maestro para que realice encuestas regulares a cada dispositivo, otorgando ventanas de tiempo específicas para la transmisión.
```

### Consideraciones Adicionales
- La elección entre acceso basado en la contención y acceso controlado depende del tamaño de la red, los patrones de tráfico esperados, y los requisitos de rendimiento y confiabilidad.
- Con las tecnologías modernas, como Wi-Fi y Ethernet de alta velocidad, los métodos de control de acceso han evolucionado para optimizar aún más estos aspectos, integrando técnicas avanzadas de gestión del tráfico y evitación de colisiones.