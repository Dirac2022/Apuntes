Un sistema distribuido se define como una colección de computadoras separadas físicamente y conectadas entre sí por una red de comunicaciones; cada máquina posee sus componentes de hardware y software que el programador percibe como un solo sistema (no necesita saber qué cosas están en qué máquinas). el programador accede a los componentes de software (objetos) remotos, de la misma manera en que accedería a componentes locales, en un grupo de computadoras que usan un middleware entre los que destacan (RPC) y SOAP para conseguir un objetivo.

# Desafío de los Sistemas Distribuidos

## Heterogeneidad
La **Heterogeneidad** se aplica en los siguientes elementos:
- Redes
- Hardware de computadores
- Sistemas Operativos
- Lenguajes de Programación
- Implementaciones de diferentes desarrolladores

### Middleware
Es el estrato de software que provee una abstracción de programación, así como en enmascaramiento de la heterogeneidad subyacente de las redes, hardware, sistemas operativos y lenguajes de programación. Ejemplos: Corba, Java RMI

![1720220542927-XqFMjaYdhh.png (924×516)](https://assets.st-note.com/img/1720220542927-XqFMjaYdhh.png?width=1200)

>[!note] El middleware es una capa de software que simplifica la construcción de sistemas distribuidos al ocultar las complejidades de la comunicación entre diferentes componentes. El IDL es una herramienta que se utiliza para definir las interfaces que el middleware utiliza para facilitar esta comunicación


![A-distributed-system-organized.png (715×308)](https://www.researchgate.net/publication/346234101/figure/fig1/AS:961824929361922@1606328341829/A-distributed-system-organized.png)


>[!note] Las funciones del middleware son
>- **Abstraer la heterogeneidad**: El middleware oculta las diferencias entre los sistemas operativos y las computadoras, proporcionando una interfaz uniforme para las aplicaciones
>- **Facilitar la comunicación**: Permite que las aplicaciones se comuniquen entre sí, independientemente de dónde se encuentren o en que sistema operativo se ejecuten


**Heterogeneidad y código móvil**
Código que puede enviarse desde un computador a otro y ejecutarse en este último. El concepto de máquina virtual ofrece un modo de crear código ejecutable sobre cualquier hardware

## Extensibilidad
Es la característica que determina si el sistema puede extenderse de varias maneras. Un sistema puede ser abierto o cerrado con respecto a extensiones de hardware o de software. Para lograr la extensibilidad es imprescindible que las interfaces clave sean publicadas.

Los sistemas distribuidos abiertos pueden extenderse a nivel de hardware mediante la inclusión de computadoras a la red y a nivel de software por la introducción de nuevos servicios y la re implementación de los antiguos. Otro beneficio de los sistemas abiertos es su independencia de proveedores concretos.

## Seguridad

La seguridad tiene tres componentes
- **Confidencialidad** : protección contra individuos no autorizados
- **Integridad** : protección contra la alteración o corrupción
- **Disponibilidad** : protección contra la interferencia que impide el acceso a los recursos.

## Escalabilidad
Se dice que un sistema es escalable si conserva su efectividad cuando ocurre un incremento significativo en el número de recursos y en el número de usuarios.

## Tolerancia a Fallas

### Detección de fallos
Por ejemplo, se pueden utilizar sumas de comprobación (**checksums**) para detectar datos corruptos en un mensaje.

> Imagina que envías un archivo grande a través de la red. Antes de enviarlo, calculas su checksum. Al recibirlo, el destinatario calcula el checksum del archivo recibido. Si los checksums coinciden, es muy probable que el archivo no haya sido alterado. Si no coinciden, sabes que hubo un error.

![What-are-checksums-How-to-find-the-checksum-of-a-file-All-you-need-to-know.jpg (566×443)](https://www.how2shout.com/wp-content/uploads/2019/03/What-are-checksums-How-to-find-the-checksum-of-a-file-All-you-need-to-know.jpg)

### Enmascaramiento de fallos

Por ejemplo, los mensajes pueden retransmitirse, replicar los datos
El objetivo aquí es ocultar los fallos a los usuarios o a otras partes del sistema, de modo que el sistema pueda seguir funcionando como si no hubiera ocurrido ningún error.

- **Retransmisión de mensajes** : Si un mensaje no se entrega correctamente, se vuelve a enviar
- **Replicación de datos**: Si un servidor falla, se puede acceder a una copia de los datos en otro servidor.


>  Piensa en un servidor web que tiene varias réplicas. Si un servidor falla, el tráfico se redirige automáticamente a las réplicas restantes, y los usuarios no notan la interrupción

### Tolerancia de fallos
Los programas clientes de los servicios pueden diseñarse para tolerar ciertos fallos. Esto implica que los usuarios tendrán también que tolerarlos.

Diseñar el sistema para que pueda seguir funcionando correctamente incluso en presencia de fallos. Esto a menudo significa que los usuarios también deben estar preparados para aceptar ciertas limitaciones o degradaciones en el servicio.

> Un servicio de streaming de video que puede reducir la calidad del video si la conexión de red es deficiente, en lugar de interrumpir la reproducción por completo.


### Recuperación de fallos
Implica el diseño de software en el que, tras una caída del servidor, el estado de los datos puede reponerse o retractarse (rollback) a una situación anterior.

Restaurar el sistema a un estado consistente después de que ha ocurrido un fallo.

> Si una transacción falla, se revierten los cambios realizados hasta el último punto de control válido

### Redundancia
Emplear componentes redundantes.
Utilizar componentes duplicados o adicionales para aumentar la fiabilidad del sistema.

> - Servidores redundantes, fuentes de alimentación redundantes, discos duros redundantes (RAID)
> - En las redes, tener caminos redundantes, para que en caso de que un camino falle, exista otro alternativo.

## Concurrencia

Existe la posibilidad de acceso concurrente a un mismo recurso. La concurrencia en los servidores se puede lograr a través de threads. Cada objeto que represente un recurso compartido debe responsabilizarse de garantizar que opera correctamente en un entorno concurrente. Para que un objeto sea seguro en un entorno concurrente, sus operaciones deben sincronizarse de forma que sus datos permanezcan consistentes.
## Transparencia

- **Transparencia de acceso**: Permite acceder a los recursos locales y remotos empleando operaciones idénticas.

- **Transparencia de ubicación**: Permite acceder a los recursos sin conocer su localización.

- **Transparencia de concurrencia**: Permite que varios procesos operen concurrentemente sobre recursos compartidos sin interferencia mutua.

- **Transparencia de replicación**: Permite replicar los recursos sin que los usuarios y los programadores necesiten su conocimiento.

- **Transparencia frente a fallos**: Permite ocultar fallos.

- **Transparencia de movilidad**: Permite la reubicación de recursos  y clientes en un sistema sin afectar la operación de los usuarios y los programas.

- **Transparencia de rendimiento**: Permite reconfigurar el sistema para mejorar el desempeño según varíe su carga.

- **Transparencia al escalado**: Permite al sistema y a las aplicaciones expandirse en tamaño sin cambiar la estructura del sistema o los algoritmos de aplicación.
