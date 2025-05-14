
# Remote Procedure Call (RPC)

Es una forma de comunicación en [[Conceptos en Redes#Sistemas distribuidos|sistemas distribuidos]]  basada en extender el uso de llamadas a procedimientos para invocar servicios sobre objetos o recursos remotos en lugar de mensajes.
- Permiten a los programas llamar procedimientos localizados en otras máquinas.
- Un proceso **X** en una máquina **A** (cliente), puede llamar un procedimiento localizado en una máquina B (servidor)

![[rpc rep grafica 1.png]]


La llamada a procedimiento remoto, o RPC, es un protocolo utilizado por un programa para solicitar un servicio de otro programa que podría estar ubicado en otra computadora o red. El programa no necesita entender los detalles de la red al usar RPC. Una llamada a procedimiento también se conoce como llamada a función o llamada a subrutina.

### ¿Cómo funciona RPC?
Cuando se realiza una llamada remota, el entorno de llamada o entorno del cliente se suspende. Los parámetros del procedimiento se transfieren al entorno en el que se ejecutará el procedimiento. El procedimiento se ejecuta entonces en ese entorno.
Una vez que el procedimiento se completa, los resultados se envían de vuelta al entorno de llamada.

<div style="text-align: center;">
	<figure>
    <img src="https://miro.medium.com/v2/resize:fit:828/format:webp/1*1xog-vJ7bpdEoKYnz1fVUA.jpeg" width=600>
    <figcaption></figcaption>
    </figure>
</div>

## Características de RPC
- **Bases del paradigma cliente/servidor**. Es una técnica para el desarrollo de aplicaciones distribuidas basadas en el paradigma cliente/servidor.
- **Se basa en el empaquetado**. La información puede llevarse del proceso invocador al invocado dentro de los parámetros de envío y respuesta.
- **Transparencia**. Ningún mensaje u operación de E/S es visible para el programador.

**Desventajas**
- **El servidor no esta disponible**: fallo del servidor.
- El cliente no puede localizar el servicio.

Un sistema basado en RPC tiene tres componentes.
- El cliente
- El servidor
- El middleware


![[componentes rpc.png]]

### Cliente
Es el proceso que realiza la **llamada** a una función.
1. Envía los parámetros de la petición.
2. Queda en **espera** del resultado.
3. Recibe el resultado.

### Servidor
Debe estar escuchando, es decir, esta en espera de una petición.
1. **Recibe** un mensaje, que consiste de uno o varios argumentos.
2. Los argumentos son usados para llamar a un **procedimiento** en el servidor.
3. El resultado del procedimiento se envía al middleware.

### Middleware
- **Empaqueta** los argumentos a petición del cliente.
- **Envía** el paquete por el canal de comunicación al servidor.
- **Recibe** la respuesta del servidor, empaqueta el resultado y se envía de regreso al cliente por el canal de comunicación.
Algunos paquetes RPC ya manejan el middleware de manera transparente.


## Stub de cliente
**Es un programa o código auxiliar que actúa como reemplazo temporal o representante de un servicio u objeto remoto del servidor**. Permite que la aplicación cliente acceda a un servicio como si fuera local, mientras oculta los detalles de la comunicación de red subyacente.

La funcionalidad del stub del cliente es la siguiente:
- Empaquetar los parámetros (proceso de serialización de datos) en un mensaje (*parameter marshalling*). 
- Enviar el mensaje al servidor.
- Esperar la respuesta - Desempaquetar (proceso de deserialización de datos) la respuesta cuando llega (*unmarshalling*).

## Stub del servidor
**Es un programa o código auxiliar que actúa como reemplazo del cliente en el servidor**. Permite que el servidor pueda ejecutar la información enviada por el cliente como si fuera local, mientras oculta los detalles de la comunicación de red subyacente.

La funcionalidad del stub del servidor es la siguiente:
- Análogas funcionalidades del stub de cliente.
- **Creación de hilos**. En caso de servidor con múltiples hilos, crea un hilo para gestionar cada invocación.
- **Dispatching**: seleccionar el procedimiento remoto solicitado (si hay varios) e invocarlo, actuando como hilo representante del cliente.

>[!info]
>El dispatching es el proceso mediante el cual el sistema RPC determina y ejecuta el procedimiento adecuado en el servidor en respuesta a una solicitud de procedimiento remoto (RPC) del cliente. Esto incluye la identificación del método solicitado, la deserialización de los parámetros, la ejecución del método y el envió de la respuesta de vuelta al cliente.


![[stub-cliente stub-servidor.png]]


<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Redes\imgs\arquitectura RPC.png">
    <figcaption>Arquitectura de un sistema basado en RPC</figcaption>
    </figure>
</div>


![[ejemplo arquitectura rpc.png]]

## Servicio Binding

El binding es el mecanismo mediante el cual un servidor registra una implementación de un servicio remoto en un directorio o registro, y los clientes utilizan este directorio para localizar y acceder al servicio remoto. Este proceso es crucial para permitir que los clientes encuentren los servicios de manera dinámica y eficiente.


- **Responsable de la transparencia de localización**: el servicio de binding permite que los clientes invoquen procedimientos remotos sin tener que preocuparse por la ubicación física del servidor. Esto se conoce como **transparencia de localización**.

- **Servicio auxiliar que complementa a stub cliente y servidor**: el servicio de binding actúa como un intermediario adicional que facilita la interacción entre los stubs del cliente y del servidor.

- **Gestiona la asociación entre el nombre del procedimiento remoto con su localización en la máquina servidor**: el servicio de binding gestiona la asociación entre el nombre simbólico del procedimiento remoto (y su versión) y su localización física en la máquina del servidor (incluyendo dirección, puerto y stub del servidor).

- Realiza la búsqueda del stub servidor de la implementación concreta del procedimiento remoto llamado por un cliente. El servicio de binding es responsable de encontrar el stub del servidor correspondiente a la implementación concreta del procedimiento remoto solicitado por el cliente.

- **Selecciona stub servidor + servidor que atiende a la llamada remota**: el servicio de binding no solo identifica el stub del servidor adecuado, sino que también selecciona el servidor que estará disponible para atender la llamada remota del cliente.


![[Pasted image 20240617131958.png]]

# Objetos distribuidos
Tienen por objetivo diseñar e implementar sistemas distribuidos que se estructuren como colecciones de componentes modulares (objetos) que puedan ser manejados fácilmente y organizados en capas para ocultar la complejidad del diseño.

- Posibilidad de invocar y pasar como argumento diferentes **comportamientos**.
- Posibilidad de aplicar patrones de diseño orientados a objetos  en la implementación del sistema distribuido.
- Idea base: extender el concepto RPC para su uso en un modelo de computación distribuida orientado a objetos.

## Interfaces remotas

**Interfaz remota**
Define el comportamiento del objeto remoto.
- Conjunto de definiciones de métodos accesibles por los demás objetos del sistema.
- Separación entre *definición* de la interfaz remota e *implementación* del comportamiento.

**Alternativas**
1. Mismo lenguaje para definición e implementación (ej.: Java RMI).
2. Uso de un IDL (*interface definition language*) independiente del lenguaje de implementación (ej.: CORBA).

Generación automática de elementos complementarios a partir de la definición del interfaz (stubs, código de partida para las implementaciones).

**Objetos remotos residen en la máquina que los crea**
- Es donde almacenan su estado (atributos).
- Es donde ejecutan su comportamiento (métodos).

**En los procesos cliente se manejan referencias remotas a esos objetos**
- Determinan de forma unívoca la ubicación de un objeto en el sistema distribuido
- $\approx$ *puntero* que referencia un objeto distribuido residente en otra máquina.

**Información típica asociada a una referencia remota**
- Dirección IP de la máquina donde reside el objeto remoto.
- N° de puerto de escucha asignado por el sistema de objetos.
- Identificador único del objeto (único dentro de la máquina que lo crea).

**Normalmente su contenido no es accesible directamente**, es gestionado por los stub de los clientes y por el servicio de *binding*.

**Uso de las referencias remotas**
- En la invocación remota de los métodos exportados por el objeto remoto.
- Como argumento que se pasa en una invocación a otro objeto.

**Utilización de las referencias a objetos**: si "X" es una referencia a un objeto remoto, entonces se pueden utilizar de los siguientes modos:
- Invocación estática de métodos remotos: `X.method1(arg1, arg2, ...)`;
- Pasar la referencia a otro objeto: `Y.method3(X);`


![[referencia a objetos remotos.png]]


## Invocación a métodos remotos

### Modelos de invocación
- **Invocación estática**: la interfaz del objeto remoto es conocida en tiempo de compilación.
	- Basado en la generación / uso de representantes (stubs y skeleton).
	- Cliente invoca el *stub* correspondiente, que gestiona la invocación *real* del objeto remoto.
- **Invocación dinámica**: la interfaz del objeto remoto no es conocida en tiempo de compilación.
	- Requiere una serie de pasos previos para descubrir el interfaz.

### Paso de parámetros 
- **Para tipos básicos**: paso por valor (copia-restauración).
- **Para objetos locales**: paso por valor de objetos serializados (copia-restauración).
	1. **Serializar**: convertir objeto en una cadena de bytes.
	2. **Transferir** copia serializada del objeto.
	3. **Deserializar**: reconstruir el objeto en la máquina de destino.
- **Para objetos remotos**: paso de referencias remotas.

### Ubicación de objetos remotos (binding)
- **Necesidad de mecanismos para obtener referencias remotas**.
	- *Binding* estático: en tiempo de compilación.
		- La ubicación del objeto remoto es fija y conocida a priori.
		- El compilador genera directamente la referencia remota.
	- *Binding* dinámico: en tiempo de ejecución.
		- El objeto remoto tiene asociado un nombre.
		- La referencia remota se recupera de un servidor de nombres.
- **Binding dinámico** $\to$ uso de servicios de nombres.
	- Mantiene una B.D con pares *(nombre objeto, referencia remota)*.
	- Funciones básicas:
		- Registrar pares *nombre-referencia* (bind()).
		- Localizar referencia asociada a un nombre (lookup())
	- Nombres pueden ser
		- Transparentes a la ubicación.
		- No transparentes a la ubicación.
	- Espacio de nombres puede ser
		- Plano
		- Jerárquico (en árbol).


# Java RMI
Java RMI (Remote Method Invocation) es una API que permite la invocación de métodos que operan en objetos ubicados en diferentes máquinas virtuales Java (JVM), facilitando la comunicación y ejecución de métodos de manera remota.

El objetivo principal de Java RMI es facilitar la programación distribuida permitiendo que los métodos de objetos puedan ser invocados desde diferentes JVM como si fueran métodos locales.

La arquitectura RMI esta dividida en cuatro capas.

- **Primera capa**: corresponde con la implementación real de las aplicaciones cliente y servidor. Los métodos disponibles en red deben estar en una interfaz que extienda *java.rmi.Remote* y luego los objetos deben ser exportados con *UnicastRemoteObjetct*.
- **Segunda capa**: todas las llamadas a objetos remotos y acciones junto con sus parámetros y retorno de objetos tienen lugar en esta capa.
- **Tercera capa**: responsable del manejo de la parte semántica de las invocaciones remotas. También es responsable de la gestión de la replicación de objetos y realización de tareas específicas de la implementación con los objetos remotos.
- **Cuarta capa**: el protocolo de transporte subyacente para RMI es JRMP (*Java Remote Method Protocol*), que solamente es *comprendido* por programas Java. Relacionado a la capa de transporte.

## Java RMI componentes
Toda aplicación RMI normalmente se descompone en dos partes:
- **Un servidor**, que crea algunos objetos remotos, crea referencias para hacerlos accesibles, y espera a que el cliente los invoque.
- **Un cliente**, que obtiene una referencia a objetos remotos en el servidor, y los invoca.

Para crear un objeto remoto, se define una *interfaz*, y el objeto remoto será una clase que implemente dicha interfaz. Se toma en cuenta:
- La interfaz debe ser pública.
- Debe heredar de la interfaz *java.rmi.Remote*, para indicar que puede llamarse desde cualquier equipo.
- Cada método remoto debe lanzar la excepción *java.rmi.RemoteException* en su cláusula *throws*, además de las excepciones que pueda manejar.
