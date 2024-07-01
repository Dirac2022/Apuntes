
- **Seguridad en red**: se encarga de proteger la usabilidad y la integridad de su red y sus datos. Involucra hardware y software.
- **Ciberseguridad**: involucra técnicas que ayudan y protegen diversos componentes digitales, redes, datos y sistemas informáticos, del acceso digital no autorizado. **Incluyen los ataques a la pila OSI**.
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
- **Firewalls**: Actúan como barrera de seguridad entre redes confiables e internet no confiable, controlando el tráfico entrante y saliente según reglas configuradas.
- **Antivirus y antimalware**: Software diseñado para detectar, bloquear y eliminar programas maliciosos como virus, gusanos, y spyware que pueden comprometer la seguridad de una red.
- **Segmentación de red**: Divide una red en segmentos más pequeños para limitar el acceso entre ellos, reduciendo así el impacto de posibles compromisos de seguridad.
- **Control de acceso**: Regula quién puede acceder a qué recursos en la red. Implementa políticas y tecnologías como autenticación, autorización y gestión de identidades.
- **IPS (Intrusion Prevention System)**: Monitorea y analiza el tráfico de red en tiempo real para detectar y responder automáticamente a posibles intentos de intrusión o actividades maliciosas.
- **IDS (Intrusion Detection System)**: Detecta y alerta sobre posibles intrusiones o actividades inusuales en la red, ayudando a los administradores a responder rápidamente a amenazas potenciales.
- **VPN**: Crea un túnel seguro y encriptado sobre una red pública, permitiendo a usuarios remotos acceder a recursos de red de manera segura como si estuvieran localmente conectados.
- **Seguridad inalámbrica**: Protege las comunicaciones y accesos a redes Wi-Fi mediante técnicas como encriptación de datos, autenticación de usuarios y monitoreo de tráfico para evitar intrusiones no autorizadas.



# Ciberseguridad
- La ciberseguridad es una sub parte de la seguridad de la información.
- La ciberseguridad garantiza la seguridad de todos los datos digitales.

Entre los principales ataques abarcados en el área de ciberseguridad se tiene:
- **Malware**: Es software malicioso diseñado para infiltrarse o dañar un sistema de computadora sin el consentimiento del usuario. Puede incluir virus, gusanos, troyanos, ransomware, entre otros.
- **Ingeniería social (*pishing*)**: Es un método de engaño diseñado para obtener información confidencial como nombres de usuario, contraseñas y detalles de tarjetas de crédito haciéndose pasar por una entidad confiable en comunicaciones electrónicas.
- **Inyección SQL**: Es una técnica de hacking que se aprovecha de vulnerabilidades en aplicaciones web al insertar código SQL malicioso en campos de entrada para ejecutar comandos no autorizados en la base de datos subyacente.
- **Ataques de día cero**: Se refieren a vulnerabilidades de seguridad recién descubiertas en software o hardware que aún no tienen una solución o parche disponible. Los atacantes aprovechan estas vulnerabilidades antes de que los desarrolladores puedan mitigarlas.
- **Ataques de intermediario**: También conocidos como ataques "Man-in-the-Middle" (MITM), implican a un tercero que intercepta y potencialmente modifica la comunicación entre dos partes sin que ninguna de ellas lo sepa.
- **Scripts en sitios cruzados (XSS)**: Es una vulnerabilidad de seguridad en aplicaciones web donde los atacantes pueden insertar scripts maliciosos en páginas web visualizadas por otros usuarios. Estos scripts pueden robar información de sesión, redirigir a sitios maliciosos, entre otros.

>[!info]
>El "phishing" hace referencia a un intento de robar información confidencial, normalmente en forma de nombres de usuario, contraseñas, números de tarjetas de crédito, información de cuentas bancarias u otros datos importantes para utilizar o vender la información robada. Al hacerse pasar por una fuente de confianza con una solicitud atractiva, el atacante tienta a la víctima para engañarla, de forma similar a como un pescador utiliza el cebo para pescar. Ejemplos: estafa nigeriana, estafa de desactivación de cuenta, estafa de falsificación de sitio web.

<div style="text-align: center;">
	<figure>
    <img src="https://www.cloudflare.com/img/learning/security/threats/phishing-attack/diagram-phishing-attack.png" width=600>
    <figcaption></figcaption>
    </figure>
</div>



# Seguridad de la información
- Involucra e incluye a los conceptos anteriores.
- La seguridad de la información garantiza la protección del tránsito y de los datos digitales.
- Los cinco pilares son **integridad**, **confidencialidad**, **disponibilidad**, **autenticidad** y **legalidad**.
- **ISO 27001** es un estándar internacional que establece los requisitos para la implementación, mantenimiento y mejora continua de un Sistema de Gestión de la Seguridad de la Información.
<div style="text-align: center;">
	<figure>
    <img src="https://www.normas-iso.com/wp-content/uploads/2012/02/SGSI.png" width=600>
    <figcaption></figcaption>
    </figure>
</div>

Existen numerosas metodologías estandarizadas de evaluación de riesgos. Aquí explicaremos la metodología sugerida en la Norma.

Las fases de esta metodología son los siguientes:

1.  Identificar los **Activos de Información** y sus responsables, entendiendo por activo todo aquello que tiene valor para la organización, incluyendo soportes físicos (edificios o equipamientos), intelectuales o informativas (Ideas, aplicaciones, proyectos ...) así como la marca, la reputación etc.
2. Identificar las **Vulnerabilidades** de cada activo: aquellas debilidades propias del activo que lo hacen susceptible de sufrir ataques o daños.
3. Identificar las **amenazas:** Aquellas cosas que puedan suceder y dañar el activo de la información, tales como desastres naturales, incendios o ataques de virus, espionaje etc.
4. Identificar los **requisitos legales** y contractuales que la organización está obligada a cumplir con sus clientes, socios o proveedores.
5. **Identificar los riesgos:** Definir para cada activo, la probabilidad de que las amenazas o las vulnerabilidades propias del activo puedan causar un daño total o parcial al activo de la información, en relación a su disponibilidad, confidencialidad e integridad del mismo.
6. **Cálculo del riesgo:** Este se realiza a partir de la probabilidad de ocurrencia del riesgo y el impacto que este tiene sobre la organización (Riesgo = impacto x probabilidad de la amenaza). Con este procedimiento determinamos los riesgos que deben ser controlados con prioridad.
7. **Plan de tratamiento del riesgo:** En este punto estamos preparados para definir la política de tratamiento de los riesgos en función de los puntos anteriores y de la política definida por la dirección. En este punto, es donde seleccionaremos los controles adecuados para cada riesgo, los cuales irán orientados a :
	- Asumir el riesgo.
	- Reducir el riesgo.
	- Eliminar el riesgo.
	- Transferir el riesgo.


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

# Control de acceso (autorización)
- Capacidad de limitar y controlar el acceso a terminales y aplicaciones mediante enlaces de comunicación.
- Cualquier entidad que desee acceder a otra entidad debe ser identificada y autenticada.
- Privilegios de acceso otorgados a un usuario, programa o proceso o el acto de otorgar esos privilegios.


<div style="text-align: center;">
	<figure>
    <img src="https://miro.medium.com/v2/resize:fit:828/format:webp/0*XnpV_RpU49wHg-jb.png" width=600>
    <figcaption></figcaption>
    </figure>
</div>


>[!info]
>- **Autenticación:** verifica las identidades, por diferentes métodos (algo que sabemos, algo que tenemos, algo que somos).
>- **Autorización**: verifica los permisos que corresponden a cada identidad.

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

>[!info]
>El no repudio asegura que una entidad no pueda negar la realización de una acción una vez que ha ocurrido. Por ejemplo, una firma digital en una transacción asegura que el emisor no pueda negar haberla enviado, proporcionando una prueba irrefutable de la autenticidad y responsabilidad de la acción.
