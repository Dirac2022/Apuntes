# Resumen

La computación en la nube es un tipo de computación donde los servicios informáticos como aplicaciones, almacenamiento, infraestructura y capacidad de procesamiento son alojados por algunos proveedores (proveedores de nube) a través de Internet y entregados a los usuarios según demanda. Una empresa puede beneficiarse de la computación en la nube en el sentido de que pueden alquilar acceso a cualquier cosa, desde aplicaciones hasta almacenamiento y capacidad de procesamiento, en lugar de poseer su propia infraestructura de TI. Al utilizar servicios de computación en la nube, las empresas pueden evitar los diversos costos y complejidades asociados con poseer y mantener su propia infraestructura de TI, ya que todo es atendido por los proveedores de servicios. La computación en la nube es un paradigma en el que tanto los usuarios como los proveedores de servicios se benefician. Los proveedores de servicios se benefician enormemente de la computación en la nube al proporcionar servicios en la nube a una amplia gama de clientes. **El objetivo principal de este documento es proporcionar una visión general de la computación en la nube, abarcando sus características, los pros y los contras de la computación en la nube y los desafíos que conlleva**. Además, este documento también presenta una lista de preocupaciones de seguridad en la computación en la nube que obstaculizan la adopción generalizada de la computación en la nube, lo que motiva a los investigadores a idear soluciones competentes para abordar estos problemas de seguridad en curso.
Palabras clave: IaaS, proveedor de servicios en la nube, PaaS, SaaS, DoS.

# Introducción

La computación en la nube está ganando mucha popularidad entre diferentes empresas y tiene el potencial de cambiar la forma en que operan los negocios. Es la nueva tendencia y ha tomado el mercado por asalto. La computación en la nube ofrece aplicaciones y capacidades de TI como un servicio a través de Internet utilizando terceros. Los recursos (CPU, almacenamiento, etc.) se entregan como utilidades generales que son arrendadas y liberadas por el usuario a través de Internet en una base de pago según el uso y bajo demanda. Es muy atractivo para los propietarios de negocios que pueden comenzar desde pequeños y aumentar los recursos solo si hay un aumento en la demanda del servicio. Muchas empresas y organizaciones diferentes han adoptado el concepto de la computación en la nube. La computación en la nube permite a los consumidores y empresas utilizar aplicaciones sin necesidad de instalación y pueden acceder a sus archivos en cualquier computadora a través de Internet [1]. Actualmente, muchas empresas de Tecnologías de la Información (TI) como Google, Yahoo, Amazon, etc., están proporcionando servicios en la nube a los usuarios [2].

Hay algunos requisitos para los servicios en la nube:
- Para acceder a cualquier dato o servicio, el proveedor de servicios en la nube (CSP) debe especificar las políticas de control de acceso.
- Para proporcionar un recurso solicitado al usuario, debe haber un mapeo de políticas de acceso entre el CSP y las organizaciones con los recursos disponibles. Siempre existe la posibilidad de violar el mapeo de políticas. Por lo tanto, la aplicación de más políticas de acceso por parte de la organización es beneficiosa en lo que respecta al acceso seguro a los recursos.
- El Propietario de Datos (DO) debe ofrecer todo tipo de servicios de datos a los consumidores [2].

## Características de la Computación en la Nube

- **Servicio bajo demanda**: los recursos informáticos como almacenamiento, potencia de procesamiento, aplicaciones, etc., se proporcionan a los usuarios cuando se necesitan y solo pagan por lo que usan.
- **Trabajo desde cualquier lugar**: siempre que los usuarios tengan acceso a Internet, los usuarios de la nube pueden acceder a la nube y trabajar en ella desde cualquier ubicación.
- **Ahorro de costos**: al usar servicios en la nube, una empresa puede evitar costos iniciales y las complejidades de poseer y mantener su propia infraestructura de TI porque ya no es necesario comprar su propio hardware, sino usar servicios basados en web.
- **Actualizaciones**: las actualizaciones de software y otros problemas técnicos ya no son un dolor de cabeza para los consumidores, ya que todo es atendido por los proveedores de servicios.
- **Escalabilidad**: los servicios en la nube son altamente escalables y los consumidores pueden escalar sus recursos hacia arriba y hacia abajo según sea necesario según sus requisitos.

## Ventajas de la Computación en la Nube

Los beneficios de usar la computación en la nube son:

- **Beneficios de costos**: dado que la computación en la nube elimina la necesidad de poseer y mantener hardware físico e infraestructura de TI, un usuario puede ahorrar costos de capital significativos. Además, la computación en la nube es un servicio de pago por uso, por lo que el usuario paga solo por lo que ha utilizado.
- **Actualizaciones y mantenimiento**: todas las actualizaciones y mantenimientos son realizados por el proveedor de servicios, por lo que el usuario no necesita perder tiempo en el mantenimiento del sistema.
- **Accesibilidad fácil**: los servicios en la nube son fácilmente accesibles desde cualquier lugar siempre que se tenga una conexión a Internet estable.
- **Alta disponibilidad**: los servicios en la nube son altamente disponibles y confiables, con la mayoría de ellos disponibles con un tiempo de actividad de 24x7.
- **Altamente escalable**: los servicios en la nube son altamente escalables, por lo que los consumidores pueden agregar recursos o descartarlos según sus necesidades.
- **Alta confiabilidad**: la nube se ejecuta en múltiples servidores, por lo que incluso en el caso de que un servidor falle, se realiza fácilmente una copia de seguridad y los recursos se obtienen de otros servidores asegurando un funcionamiento suave e ininterrumpido.

## Desventajas de la Computación en la Nube
- **Seguridad**: La seguridad de los datos y la privacidad es una de las principales desventajas de la computación en la nube. Al usar servicios en la nube, un usuario está almacenando todos sus datos en la nube, que básicamente es la computadora de otra persona. Algunos datos son demasiado sensibles para ser colocados en la nube, por lo que siempre existe una preocupación por la privacidad de los datos.
- **Tiempo de inactividad**: esto significa el tiempo en que la nube está inactiva debido a que los proveedores de servicios enfrentan dificultades como pérdida de energía, problemas técnicos y mantenimiento del servidor.
- **Dependencia de la conectividad**: la computación en la nube depende de la conexión a Internet y requiere que las empresas o usuarios tengan una conectividad a Internet estable para usar sus servicios. Además, cuando el proveedor de servicios experimenta pérdida de conectividad, no pueden tener lugar transacciones.
- **Control limitado**: Cuando una empresa o un individuo trasladan sus datos a la nube, tienen un control limitado sobre ellos debido a que todas las actividades de backend son gestionadas por el proveedor de servicios y el usuario solo tiene control sobre el frontend de las aplicaciones.

# Modelos de implementación en la nube

Generalmente, hay cuatro tipos de nubes; son nube privada, nube pública, nube híbrida y nube comunitaria. La implementación depende de quién controla la infraestructura y dónde reside.

### Nube Privada:
Una nube privada es una infraestructura en la nube que es propiedad y ==está operada por una sola organización. No está disponible para el público en general y solo la organización que la posee y sus miembros pueden acceder a sus recursos==. También se llama nube interna/corporativa por esta razón. Una nube privada es más segura, confiable y mantiene la privacidad ya que solo las personas autorizadas pueden acceder a ella.

**Ventajas:**
- Altamente segura y confiable.
- Ofrece un alto nivel de personalización.

**Desventajas:**
- Para usar una nube privada, una empresa tiene que gastar considerables gastos en hardware, software y capacitación del personal.

### Nube Pública:
Como su nombre lo sugiere, la nube pública está ==disponible para el público en general==. En la nube pública, el proveedor de servicios en la nube proporciona los recursos, como la red, el servidor, etc. La infraestructura del servidor pertenece al proveedor y, por lo tanto, los usuarios/empresas no necesitan comprar y mantener su propio hardware individual. Aquí, los usuarios pueden pagar por la cantidad que han utilizado la nube pública. ==En la nube pública, los clientes o usuarios de muchas organizaciones están mezclados y utilizan la misma nube o red==.

**Ventajas:**
- Es altamente escalable.
- Es rentable ya que los usuarios pagan solo por lo que usan.
- Administración de infraestructura sin complicaciones ya que todas las actualizaciones y mantenimientos se realizan en el lado del servidor por parte del proveedor de servicios.

**Desventajas:**
- La seguridad de los datos es una preocupación.
- Menos confiable.

### Nube Comunitaria:
La nube comunitaria es un esfuerzo colaborativo en el que la infraestructura y los recursos son compartidos por varias organizaciones con antecedentes e intereses similares. Estas nubes generalmente se basan en un acuerdo entre organizaciones empresariales relacionadas y son administradas conjuntamente por todas estas organizaciones o por un tercero.

**Ventajas:**
- Es eficiente en costos.
- Ofrece fácil intercambio de datos y colaboración.

**Desventajas:**
- El costo es más alto en comparación con el modelo público.
- Compartir responsabilidades entre organizaciones es difícil.

### Nube Híbrida:
La nube híbrida es una combinación de los modelos de implementación mencionados anteriormente (pública, privada, comunitaria) que explota las mejores características de cada modelo. Por ejemplo, una empresa que utiliza una nube híbrida puede almacenar sus datos críticos en una nube privada y almacenar los menos sensibles en una nube pública. La nube híbrida proporciona un control más seguro de los datos y las aplicaciones y permite que varias partes accedan a la información a través de Internet.

**Ventajas:**
- Ofrece una mejor seguridad y privacidad.
- Tiene una escalabilidad mejorada y ofrece flexibilidad.

**Desventajas:**
- El costo inicial de configuración es alto.
- Problemas de compatibilidad.

![[Pasted image 20240505211744.png]]
Figure 1. Comparative analysis on Cloud Deployment Models
## Modelos de servicio en la nube

Los modelos de nube son de tres tipos, a saber, SaaS (Software como Servicio), IaaS (Infraestructura como Servicio) y PaaS (Plataforma como Servicio). Cada uno de estos modelos tiene sus propios beneficios que pueden ser utilizados para satisfacer diferentes requerimientos empresariales.

### Software como Servicio (SaaS):
El modelo de servicio más conocido y líder de una adopción más extendida de la computación en la nube ha sido el SaaS. Este es un modelo bajo demanda donde el usuario solicita al proveedor de servicios diversas aplicaciones y programas de software. Proporciona al usuario acceso rápido a aplicaciones web basadas en la nube. SaaS es un modelo de entrega de software que permite a los proveedores de servicios en la nube alojar y mantener diversas aplicaciones web sobre Internet para ser accedidas y utilizadas por los usuarios finales. **Un ejemplo de SaaS es, estos días puedes optar por usar Microsoft Office alquilándolo al proveedor de servicios en una base de pago por uso en lugar de comprar su licencia e instalarlo en tu sistema**, lo cual es mejor en términos de flexibilidad y lo suficientemente asequible para cualquier presupuesto.

**Ventajas:**
- Es escalable.
- Accesibilidad fácil.
- Rentable.

**Desventajas:**
- Requiere una conexión a Internet estable ya que SaaS es un servicio basado en web.
- Preocupaciones de seguridad y privacidad.

### Plataforma como Servicio (PaaS):
En este modelo, el proveedor de servicios en la nube proporciona un entorno/plataforma de desarrollo al usuario. **La diferencia entre SaaS y PaaS es que SaaS solo aloja aplicaciones en la nube completadas, mientras que PaaS ofrece una plataforma de desarrollo tanto para aplicaciones en la nube completadas como en progreso**. PaaS es un entorno de desarrollo e implementación en la nube donde se les dan a los usuarios los recursos para desarrollar e implementar varias aplicaciones, desde simples basadas en la nube hasta sofisticadas. Estos recursos de desarrollo de aplicaciones se compran a los proveedores de servicios en una base de pago por uso. La plataforma, similar a SaaS, se entrega a través de la web y todos los mantenimientos, actualizaciones y servidores son gestionados por los proveedores de servicios.

**Ventajas:**
- Es escalable y rentable.
- La disponibilidad es alta.

**Desventajas:**
- La seguridad de los datos es un problema.
- Dependencia del proveedor.

### Infraestructura como Servicio (IaaS):
Las ofertas de IaaS son recursos informáticos como procesamiento o almacenamiento que pueden obtenerse como un servicio. Es un servicio de computación en la nube donde los usuarios finales arriendan recursos de almacenamiento, cómputo y almacenamiento de los proveedores de servicios. Permite a las empresas alquilar infraestructura en lugar de poseer y gestionar su propia infraestructura. El modelo de IaaS cambia la forma en que los desarrolladores implementan sus aplicaciones. En lugar de pasar tiempo con sus propios centros de datos o empresas de alojamiento administrado, simplemente pueden seleccionar uno de los proveedores de IaaS, obtener un servidor virtual en funcionamiento en pocos minutos y pagar solo por los recursos que usan.

**Ventajas:**
- Es rentable.
- Es el modelo más flexible.

**Desventajas:**
- La seguridad de los datos es un problema.
- Si hay una falla/interrupción en el lado del proveedor, interrumpiría la actividad del consumidor.

![[Pasted image 20240505211721.png]]
Figure 2. Types of Cloud Computing Service Models

# Desafíos de la computación en la nube

La computación en la nube es una tecnología muy popular y emergente hoy en día, adoptada por muchas empresas e individuos, pero tan popular como pueda ser, tiene su parte justa de desafíos. En esta sección abordamos los diversos desafíos enfrentados por la computación en la nube.

### Privacidad y Seguridad de los Datos:
La privacidad de los datos se trata de asegurar la información personal identificable (**Personal Identifiable Information PII**) de los usuarios. La información personal identificable (PII) es cualquier información que podría usarse para identificar a un individuo en particular. PII puede ser sensible o no sensible. La PII no sensible es información que puede transmitirse en una forma no oculta. La PII se encuentra fácilmente en los servicios de computación en la nube debido a problemas de privacidad. Una vez que un proveedor de la nube conoce la PII (nombre, número de estudiante, ID de personal, dirección, correo electrónico, etc.), se convierte en un problema para el usuario. Uno de los problemas más desafiantes que disminuyen la tasa de confiabilidad y eficiencia en los entornos de computación en la nube es garantizar la seguridad y privacidad de los recursos almacenados. La seguridad de la computación en la nube se ha convertido en un tema importante en la industria y la investigación académica y se ha convertido en la principal causa que obstaculiza su desarrollo. Entonces, a menos que el proveedor garantice la seguridad y confidencialidad de los datos mediante la implementación de rigurosas medidas de seguridad, no se espera que la computación en la nube sea adoptada por muchos.

### Interoperabilidad:
**Esta es la capacidad de dos o más sistemas para trabajar juntos con el fin de intercambiar información y utilizar esa información intercambiada**. Muchas redes de nubes públicas están configuradas como sistemas cerrados y no están diseñadas para interactuar entre sí. La falta de integración entre estas redes dificulta que las organizaciones combinen sus sistemas de TI en la nube y obtengan ganancias de productividad y ahorros de costos. Para superar este desafío, deben desarrollarse estándares industriales para ayudar a los proveedores de servicios en la nube a diseñar plataformas interoperables y permitir la portabilidad de datos.

### Protección de Datos:
La protección de datos en la nube es la práctica de asegurar los datos de una empresa en un entorno de nube. La seguridad de los datos es un elemento crucial que merece un escrutinio. Las empresas son reacias a comprar una garantía de seguridad de datos comerciales de los proveedores. Temen perder datos ante la competencia y la confidencialidad de los datos de los consumidores. En muchos casos, la ubicación real de almacenamiento no se divulga, lo que aumenta las preocupaciones de seguridad de las empresas. En los modelos existentes, los cortafuegos en los centros de datos protegen esta información sensible. En el modelo de nube, los proveedores de servicios son responsables de mantener la seguridad de los datos y las empresas tendrían que confiar en ellos.

### Portabilidad:
La portabilidad significa transferir las aplicaciones que se ejecutan en una plataforma de nube a otra. Sin embargo, las aplicaciones desplegadas en una plataforma de nube, incluidos los datos y recursos, son difíciles de mover entre nubes debido a las diferencias en las plataformas, lo que lleva a problemas de portabilidad.

### Rendimiento:
Cuando una empresa se traslada a la nube, se vuelve dependiente de los proveedores de servicios. Los siguientes desafíos prominentes de mudarse a la computación en la nube amplían esta asociación. Sin embargo, esta asociación a menudo proporciona a las empresas tecnologías innovadoras a las que de otro modo no podrían acceder. Por otro lado, el rendimiento del BI de la organización y otros sistemas basados en la nube también está vinculado al rendimiento del proveedor de la nube cuando falla. Cuando su proveedor está fuera de servicio, usted también lo está.

# Problemas de seguridad en la computación en la nube

Cuando se trata de la nube, los datos se almacenan en el lado del proveedor de servicios y se accede a ellos a través de Internet. El usuario tiene un control limitado sobre sus datos y la visibilidad se vuelve restringida. También surge la pregunta de qué tan seguros están almacenados y gestionados estos datos. Los problemas de seguridad en la nube son compartidos tanto por el proveedor como por el cliente. El proveedor de servicios debe asegurarse de que los servicios proporcionados sean seguros, y el cliente debe asegurarse de que el servicio que está utilizando sea seguro.

En esta sección analizaremos los diversos desafíos de seguridad enfrentados por la computación en la nube.

### Violación de Datos:
La violación de datos es una preocupación clave de seguridad que se encuentra en la computación en la nube. Es un incidente donde datos sensibles y confidenciales se liberan en un entorno no autorizado. Las violaciones de datos pueden ocurrir debido a una variedad de razones; podría ser intencional o no intencional. Podría ser no intencional a través de fugas de datos, filtraciones de información o intencional a través de robo.

### Secuestro de Cuentas:
El secuestro de cuentas es una situación en la que la cuenta de un usuario de la nube ha sido comprometida por un atacante. Es una forma de robo de identidad donde el atacante ha adquirido con éxito las credenciales del usuario de la nube y utiliza la cuenta robada para llevar a cabo actividades maliciosas. Los atacantes obtienen cuentas de usuario a través de phishing enviando correos electrónicos falsos, páginas web a usuarios específicos o mediante el uso de software malicioso.

### Ataque Interno:
El ataque interno, también conocido como "turn cloak", es un ataque donde alguien de la organización intenta acceder maliciosamente a información confidencial. Los ataques internos son la materialización del riesgo para las empresas, sus datos, sus socios comerciales y su futuro a largo plazo causado por personas dentro de la organización que se vuelven maliciosas y actúan en consecuencia. Estos ataques son orquestados o ejecutados por personas que son confiables con diversos niveles de acceso a los sistemas y facilidades de una empresa, y que tienen un conocimiento íntimo de la infraestructura de la empresa que un atacante externo tardaría un período significativo de tiempo en desarrollar.

### Ataques de Denegación de Servicio (DoS)
A diferencia de otras formas de ataques que intentan secuestrar información sensible, la denegación de servicio es un ataque destinado a cerrar un sitio web o servidores, volviéndolos inútiles para usuarios legítimos. En la computación en la nube, un ataque de denegación de servicio (DoS, por sus siglas en inglés) puede describirse como un ataque diseñado para evitar que algún servicio o recurso de computación en la nube proporcione su servicio normal durante un período de tiempo. Los ataques de DoS comprometen la disponibilidad de los recursos y servicios en la nube y a menudo se dirigen al ancho de banda o la conectividad de las redes informáticas. El atacante apaga los servidores, redes y máquinas de las organizaciones objetivo, volviéndolos inaccesibles para sus usuarios legítimos al inundarlos con tráfico no deseado.

### Pérdida de Datos:
La pérdida de datos es una situación en la que los sistemas de información que almacenan información son destruidos, lo que conduce a la pérdida de información vital. Los sistemas de información pueden ser destruidos como resultado de negligencia, manejo incorrecto, desastres naturales y ataques maliciosos o debido a un borrado de datos por parte del proveedor de servicios de manera intencional o no intencional. Esto podría afectar gravemente a las empresas que no tienen un plan de recuperación. Amazon sufrió pérdida de datos en 2011 al destruir mucha de la información de sus clientes. Google es otra organización que sufrió una pérdida masiva de datos cuando su red eléctrica fue alcanzada por un rayo.

# Conclusión
La computación en la nube es una de las áreas de más rápido crecimiento en el campo de la tecnología de la información hoy en día, ofreciendo enormes beneficios a clientes de todo tipo y tamaño. Es uno de los principales habilitadores para muchas empresas y organizaciones. La computación en la nube es tan popular hoy en día porque ofrece una amplia gama de servicios a tarifas asequibles y las soluciones en la nube son mucho más simples de adquirir, no requieren contratos a largo plazo y pueden escalarse según sea necesario. A pesar de todos los beneficios que ofrece, la computación en la nube también tiene sus propias desventajas y desafíos, y actualmente se están llevando a cabo investigaciones activas para abordar los diversos problemas que enfrenta.

