
# Regiones AWS

- Perú ya cuenta con un data center propio.



VPC (Virtual Private Cloud)

# Grupo de seguridad en AWS
- Controla el tráfico al que se permite llegar y dejar los recursos a los que está asociado.
- Al crear un VPC, incluye un grupo de seguridad predeterminado.
- Generalmente especifica origen, destino, puerto y protocolo.

# AWS: Elastic Compute Cloud (EC2)

Es un servicio de computación en la nube que permite crear y administrar servidores virtuales (instancias) bajo demanda. Se usa para hospedar aplicaciones, ejecutar bases de datos, realizar procesamiento de datos y más. 

Características: 
- **Servicio informático bajo demanda y con la flexibilidad de un entorno virtual**. AWS EC2 ofrece capacidad informática bajo demanda a través de instancias virtuales, permitiendo a los usuarios lanzar servidores virtuales con diversas configuraciones según las necesidades específicas de recursos computacionales.
- **Configuración de instancias temporales**. Las instancias en EC2 pueden ser configuradas como temporales, lo que significa que pueden iniciarse y detenerse según sea necesario. Esto proporciona flexibilidad para optimizar costos y recursos, especialmente en entornos de desarrollo y pruebas.
- **Seguro, redimensionable y escalable**. EC2 proporciona un entorno seguro mediante el uso de controles de acceso y configuraciones de seguridad configurables. Las instancias pueden escalar verticalmente (redimensionarse para más recursos) y horizontalmente (agregar más instancias) para manejar cargas de trabajo cambiantes y escalables.
- **Máquinas virtuales preconfiguradas**. Las Amazon Machine Images (AMI) permiten a los usuarios lanzar instancias con sistemas operativos y software preconfigurados. Esto facilita la rápida implementación de entornos de aplicación sin la necesidad de configuraciones manuales extensas.
- **Uso de VPC, Subredes y Seguridad**. EC2 utiliza Virtual Private Cloud (VPC) para proporcionar un entorno de red aislado y controlado por el usuario. Las subredes dentro de VPC permiten segmentar recursos y aplicar políticas de acceso específicas. La seguridad se gestiona mediante grupos de seguridad, que actúan como firewalls virtuales para controlar el tráfico de red hacia y desde las instancias EC2.
- **Escalamiento en función del tráfico entrante de la aplicación**. EC2 es compatible con el Auto Scaling, lo que permite ajustar automáticamente la cantidad de instancias según el tráfico entrante. Esto asegura que la aplicación pueda manejar picos de carga sin intervención manual, mejorando la disponibilidad y la eficiencia de costos.

Estas características hacen de AWS EC2 una solución poderosa para desplegar y gestionar aplicaciones en la nube de manera flexible, segura y eficiente.



# AWS: Elastic Block Store (EBS)

#### Escalamiento rápido
AWS Elastic Block Store (EBS) proporciona almacenamiento en bloques que puede escalarse rápidamente para adaptarse a las necesidades cambiantes de las aplicaciones. Los volúmenes EBS pueden aumentarse en tamaño sin necesidad de tiempo de inactividad. Esto permite a las empresas responder ágilmente a las demandas crecientes de almacenamiento. 
**Ejemplo:** Una aplicación de comercio electrónico experimenta un aumento en la cantidad de datos debido a una campaña de ventas. Con EBS, el administrador puede aumentar rápidamente el tamaño del volumen de almacenamiento para manejar el aumento de transacciones y datos de clientes sin interrumpir el servicio.

#### Alto rendimiento
EBS ofrece varios tipos de volúmenes, como los volúmenes SSD de propósito general (gp3) y los volúmenes IOPS provisionados (io2), que están diseñados para proporcionar un alto rendimiento en términos de velocidad de lectura y escritura. Estos volúmenes son ideales para aplicaciones que requieren tiempos de respuesta rápidos y consistentes.
**Ejemplo:** Una base de datos relacional que respalda una aplicación crítica requiere acceso rápido a los datos. Utilizando volúmenes io2, la base de datos puede lograr altos niveles de IOPS (Operaciones de Entrada/Salida por Segundo), asegurando que las consultas se ejecuten rápidamente y la aplicación mantenga un rendimiento óptimo.

#### Optimización de costos
EBS permite optimizar costos al ofrecer diferentes tipos de volúmenes con distintos niveles de rendimiento y precios. Los volúmenes gp3, por ejemplo, proporcionan un equilibrio entre costo y rendimiento. Además, EBS Snapshot permite hacer copias de seguridad incrementales, reduciendo los costos de almacenamiento.
**Ejemplo:** Una empresa puede utilizar volúmenes gp3 para entornos de desarrollo y pruebas, donde los requisitos de rendimiento son menores, y reservar volúmenes io2 para producción. Además, pueden utilizar snapshots para realizar copias de seguridad de los datos críticos, pagando solo por los cambios incrementales desde el último snapshot.

#### Características adicionales de AWS EBS

- **Snapshots y backup:** Permiten hacer copias de seguridad incrementales de los volúmenes EBS para recuperación ante desastres.
- **Encriptación:** Los volúmenes EBS pueden encriptarse para proteger los datos en reposo, proporcionando seguridad adicional para datos sensibles.
- **Replicación:** AWS EBS soporta replicación entre zonas de disponibilidad (AZ) para mejorar la durabilidad y la disponibilidad de los datos.

# AWS: Amazon Simple Storage Service (S3)
Es un servicio de almacenamiento en la nube que permite guardar y recuperar cualquier tipo de archivo. Es altamente escalable y seguro, con diferentes opciones de almacenamiento según la frecuencia de acceso a los datos. 

Características

- **Servicio de almacenamiento simple de archivos de diferentes tipos, como fotos, audio y videos como objetos**. Amazon S3 permite almacenar y recuperar cualquier cantidad de datos en cualquier momento y desde cualquier lugar. Los datos se almacenan como objetos dentro de cubos (*buckets*). Cada objeto está compuesto por datos, metadatos y una clave única dentro del cubo.
> **Ejemplo:** Una empresa de medios puede almacenar fotos, archivos de audio y videos en S3. Cada archivo multimedia se guarda como un objeto en un cubo específico, lo que facilita su acceso y gestión a través de URLs únicas.

- **Escalabilidad, seguridad y recuperación de información**. S3 es altamente escalable, lo que permite a las aplicaciones crecer sin necesidad de aprovisionar más infraestructura. Además, S3 ofrece una seguridad robusta con ==cifrado en reposo y en tránsito==, y políticas de acceso detalladas para controlar quién puede acceder a qué datos. S3 también garantiza la durabilidad de los datos mediante la replicación en múltiples ubicaciones.
> **Ejemplo:** Una aplicación web que crece rápidamente puede seguir almacenando grandes volúmenes de datos de usuario en S3 sin preocuparse por la capacidad de almacenamiento. Además, puede aplicar cifrado a los datos para asegurar su confidencialidad y establecer permisos específicos para que solo ciertos usuarios o servicios puedan acceder a ellos.


>[!Note] Cifrado en reposo y tránsito
>- **Cifrado en reposo**: Protege los datos cuando están almacenados, asegurando que, aunque alguien acceda físicamente al almacenamiento, no pueda leer la información sin la clave de cifrado.
>- **Cifrado en tránsito**: Protege los datos mientras se transfieren entre redes, evitando que sean interceptados o modificados por terceros durante la transmisión.
### Usos

#### Almacenamiento de datos
S3 se utiliza ampliamente para almacenar datos de manera duradera y accesible. Es ideal para almacenar datos sin estructura, como archivos multimedia, documentos, y datos de respaldo.
**Ejemplo:** Una startup de análisis de datos puede usar S3 para almacenar grandes conjuntos de datos sin estructura que luego se analizarán utilizando herramientas de análisis de datos.

#### Copia de seguridad y recuperación
S3 es una opción popular para las copias de seguridad y la recuperación de datos debido a su durabilidad y disponibilidad. Las organizaciones pueden crear copias de seguridad automáticas de sus datos críticos en S3.
**Ejemplo:** Un proveedor de servicios de TI puede configurar copias de seguridad automáticas de las bases de datos de sus clientes en S3, asegurando que los datos estén protegidos contra pérdidas y sean fácilmente recuperables en caso de desastre.

#### Archivo de datos: la integración del servicio Amazon Glacier
Amazon Glacier es un servicio de almacenamiento a largo plazo para el archivado y la copia de seguridad de datos a costos muy bajos. S3 se integra con Glacier para mover automáticamente los datos menos utilizados a Glacier para almacenamiento a largo plazo.
**Ejemplo:** Una institución financiera puede archivar datos de transacciones antiguas en Amazon Glacier a través de S3, reduciendo los costos de almacenamiento y cumpliendo con los requisitos de retención de datos a largo plazo.

#### Big Data Analytics
S3 se integra con diversas herramientas de análisis de datos y big data, como Amazon EMR (Elastic MapReduce), AWS Glue y Amazon Athena, para analizar grandes volúmenes de datos directamente desde S3.
**Ejemplo:** Una empresa de marketing digital puede almacenar datos de interacción de usuarios en S3 y luego usar Amazon Athena para ejecutar consultas SQL directamente sobre esos datos sin necesidad de moverlos, obteniendo insights valiosos de manera eficiente y rápida.

