
- **Seguridad en red**: se encarga de proteger la usabilidad y la integridad de su red y sus datos. Involucra hardware y software.
- **Ciberseguridad**: involucra técnicas que ayudan y protegen diversos componentes digitales, redes, datos y sistemas informáticos, del acceso digital no autorizado. Incluyen los ataques a la pila OSI.
- **Seguridad de la información**: incluye las medidas, políticas, controles y normas para garantizar la confidencialidad, integridad y disponibilidad de los datos en un espacio virtual o real.

<div style="text-align: center;">
	<figure>
    <img src="https://media.geeksforgeeks.org/wp-content/cdn-uploads/20200330125125/Capture333.png" width=400>
    <figcaption></figcaption>
    </figure>
</div>
# Seguridad en redes
- La seguridad de la red es una sub parte de la ciberseguridad.
- Enfocado en temas de red y sus canales.
- Se enfoca en la seguridad de datos en movimiento.

Se tienen los siguientes tipos o recursos:
- Firewalls
- antivirus y antimalware
- segmentación de red
- control de acceso
- IPS
- IDS
- VPN
- Seguridad inalámbrica.

# Ciberseguridad
- La ciberseguridad es una sub parte de la seguridad de la información.
- La ciberseguridad garantiza la seguridad de todos los datos digitales.

Entre los principales ataques abarcados en el área de ciberseguridad se tiene:
- Malware
- ingeniería social (*pishing*)
- inyección SQL
- ataques de día cero
- ataques de intermediario
- scripts en sitios cruzados (XSS)
![[Pasted image 20240617151612.png]]

# Seguridad de la información
- Involucra e incluye a los conceptos anteriores.
- La seguridad de la información garantiza la protección del tránsito y de los datos digitales.
- Los cinco pilares son **integridad**, **confidencialidad**, **disponibilidad**, **autenticidad** y **legalidad**.
- **ISO 27001** es un estándar internacional que establece los requisitos para la implementación, mantenimiento y mejora continua de un Sistema de Gestión de la Seguridad de la Información.

![[Pasted image 20240617151944.png]]


# Servicios de seguridad X.800
Describe una arquitectura de seguridad básica en la transferencia de datos cuando se conecta una computadora a una red LAN o la Internet dentro del marco del modelo OSI y frente a ataques informáticos.

Tipos de ataques
**Ataques pasivos**
- Tiene como objetivo espiar o monitorear las transmisiones dentro de una red.
- Son de dos tipos: **obtención de contenidos y mensajes** y **análisis de tráfico**.

**Ataques activos**
- Tiene como objetivo la modificación de un flujo de datos o la creación de un flujo falso.
- Se clasifican en cuatro tipos: **suplantación**, **repetición**, **modificación del mensaje**, **interrupción del servicio**.

# Autenticación
- Hace referencia a la certeza de que una entidad es quien dice ser.
- Al inicio el servicio asegura que las entidades son las que deben estar en la comunicación y mantiene esta condición asegurando que la conexión no está intervenida y un tercero pueda suplantar a una de las dos entidades.
- Evitar intervención o realización de un transmisión o recepción no autorizada.
- Emplea medidas de seguridad diseñadas para establecer la validez de una transmisión, mensaje u organizador, o un medio para verificar la autorización de un individuo para recibir categorías específicas de información.

# Control de acceso
- Capacidad de limitar y controlar el acceso a terminales y aplicaciones mediante enlaces de comunicación.
- Cualquier entidad que desee acceder a otra entidad debe ser identificada y autenticada.
- Privilegios de acceso otorgados a un usuario, programa o proceso o el acto de otorgar esos privilegios.
# Confidencialidad
- El termino "confidencialidad" significa preservar las restricciones autorizadas de acceso y divulgación, incluidos los medios para proteger la privacidad personal y la información de propiedad exclusiva.
- La garantía de que la información no se divulgue a personas, procesos o dispositivos no autorizados. La confidencialidad cubre los datos almacenados, durante el procesamiento y en tránsito.
- En tránsito, este servicio protege los datos que son transmitidos usando conexiones TCP y protege el flujo frente al análisis de tráfico, para lo cual el atacante no puede ver la fuente, el destino, la frecuencia, la longitud, ni ninguna característica del tráfico en una comunicación.

# Integridad
- El termino "integridad" significa proteger contra la modificación inadecuada de la información e incluye garantizar el no repudio y la autenticidad de la información.
- La capacidad de detectar incluso cambios mínimos en los datos.
- La propiedad de que los datos o la información no han sido alterados o destruidos de forma no autorizada.
- Hace referencia a que los datos salientes de una terminal son exactamente iguales a los datos que recibe la terminal de destino. Su enfoque es la protección del flujo de datos.

# No repudio
- Garantía de que se proporciona al remitente de los datos un comprobante de entrega y al destinatario una prueba de la identidad del remitente, por lo que ninguno de los dos podrá negar posteriormente haber tratado los datos.
- Protección contra un individuo que niega falsamente haber realizado una acción particular. Proporciona la capacidad de determinar si un individuo determinado realizó una acción particular, como crear información, enviar un mensaje, aprobar información y recibir un mensaje.
- La incapacidad de negar la responsabilidad por la realización de un acto específico (*repudio con prueba de origen o de entrega)*.
