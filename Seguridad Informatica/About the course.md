
contraseña: [HackMyVM | Settings](https://hackmyvm.eu/): `12345%%`


# Sabado 12/04/2025

kali
configuracion
red
adaotador 1 - adaptador solo anfrition (elegir #2) y aceptar


# Sabado 03/05/2025 Semana 6

# Ataque

```plaintext
Ataque = motivo(objetivo) + método  + vulnerabilidad
```

- El motivo se origina en el valor del sistema o proceso objetivo, llegando a despertar ==el interés del atacante.==
- Los atacantes utilizan ==herramientas y técnicas== de ataque para explotar las vulnerabilidades del sistema, las políticas o controles de seguridad con el fin de cumplir sus objetivos.
## Motivos de los ataques a la seguridad de la información
- Interrumpir la continuidad del negocio
- Realizar robos de información
- Manipular datos
- Crear miedo y caos al interrumpir la infraestructura crítica
- Provocar pérdidas económicas al objetivo
- Exigir un rescate
- Vengarse
- Dañar la reputación del objetivo
- Objetivos militares de un estado
- Propagar creencias religiosas o políticas.


## Superficie de ataque

La **superficie de ataque** se refiere a todos los puntos de entrada o vulnerabilidades potenciales que un atacante podría explotar para infiltrarse en un sistema, red, aplicación o dispositivo.

**Tipos de superficies de ataque**
- Superficie de ataque física
- Superficie de ataque digital
- Superficie de ataque humana

## Vector de ataque
Un **vector de ataque** es un método utilizado por un actor malicioso para vulnerar la superficie de ataque y toma muchas formas, incluido ransomware, credenciales comprometidas, ==phishing== y ==malware==.

**Tipos de vectores de ataque**
- Malware
- Ransomware
- Sistemas mal configurados
- Sistemas sin parches
- Credenciales comprometidas


# Clasificación de ataques - IATF


| Tipos de ataque        | Descripción                                                                                                                                                                                                                                                                                                                |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Ataque pasivo          | No manipulan los datos y consisten en interceptar y supervisar el tráfico de red y el flujo de datos en la red objetivo. Ejemplo: sniffer (captura y analiza el tráfico de red) y eavesdropping (escuchar/registrar comunicaciones ajenas sin autorización).                                                               |
| Ataque activo          | Manipulan los datos en tránsito o interrumpen la comunicación o los servicios entre sistemas para eludir o penetrar en los sistemas seguros. Ejemplo: Dos, Man in the Middle, Session hijacking (roba o toma el control de una sesión activa de un usuario legítimo) y SQL Injection.                                      |
| Ataque de proximidad   | Se realiza cuando el atacante está en estrecha proximidad física con el sistema o la red de destino con el fin de recopilar, modificar o interrumpir el acceso a la información. Ejemplo: ingeniería social, eaves dropping, el shoulder sufing (Mirar por encima del hombro) y el dumpster diving (búsqueda en la basura) |
| Ataque interno         | Hacen uso de acceso privilegiado para violar las reglas o causar intencionalmente una amenaza a los sistemas de información de una organización. Ejemplo: Robo de dispositivos físicos y Colocación de keyloggers, backdoors y malware.                                                                                    |
| Ataque de distribución | Se producen cuando los atacantes manipulan el hardware o el software antes de su instalación, en su origen o en tránsito.                                                                                                                                                                                                  |




# APT (Advanced Persistent Threat)
Es un **ataque sofisticado, prolongado y dirigido**, generalmente ejecutado por grupos organizados (patrocinados por estados o crimen organizado) para robar información sensible, espiar o sabotear sistemas.


✅ **Avanzado
- Usa técnicas de alto nivel (zero-day exploits, malware personalizado, ingeniería social avanzada).
- Evita detección con herramientas antimalware comunes.

✅ **Persistente**
- Permanece meses o años en la red de la víctima sin ser detectado.
- Se reactiva después de reinicios o limpiezas parciales.

✅ **Dirigido**
- Objetivos específicos (gobiernos, empresas tecnológicas, infraestructura crítica).
- Investigación previa sobre la víctima (reconocimiento).


# Metodología cyber kill chain
Utilizado para conocer y entender los patrones de comportamiento de los actores de amenazas permite comprender cómo planean y ejecutan los ciberataques.

Estudiar cada etapa bajo distintos escenarios, obtenemos una visión amplia y estructurada de los controles necesarios para prevenir estos ataques.

<img src="https://infosec.cs.umass.edu/sites/default/files/mitre_course_graphic.png" >


## 🕵️‍♂️ Reconocimiento (Reconnaissance): Identificar el objetivo

### 👨‍💻 El atacante

- Planifican sus operaciones mediante la recolección de información para identificar y seleccionar sus objetivos. Este proceso incluye el análisis de redes, sistemas, estructuras organizacionales y empleados.
	
- Reconocimiento es fundamental, permite determinar las vulnerabilidades existentes, definir el alcance del ataque, evaluar la superficie de exposición y planificar las acciones posteriores a la explotación.
	
- Recoger direcciones de correo electrónico.
	
- Identificar a los empleados en las redes sociales.
	
- Recoger comunicados de prensa adjudicaciones de contratos, listas de asistentes a conferencias.
	
- Descubrir servidores con acceso a Internet.


### 🛡️ La defensa

- Actúa utilizando técnicas de análisis preventivo para aumentar sus posibilidades de detección, intentando revelar las intenciones del atacante sobre algún activo cibernético.
- Recoge los registros de visitantes al sitio web para alertas y realizar búsquedas históricas
- Los administradores de la web realizan análisis de la navegación existente.
- Construir detectores de comportamientos de navegación (machine learning).
- Priorizar las defensas en torno a determinadas tecnologías o personas en función de la actividad de reconocimiento.


## 🧪Preparación (Weaponization): Preparación del ataque

### 👨‍💻 El atacante

- Analiza los datos recolectados, identifica las vulnerabilidades, prepara la forma de ataque tomando en cuenta que ya tiene claro el objetivo.
	
- Ejm: utiliza un troyano que tome provecho de una vulnerabilidad existente en los sistemas.
	
- Obtener un weaponizer (armamento) ya sea interno u obtenido a través de canales púbicos o privados.
	
- Los atacantes seleccionan cuidadosamente el documento señuelo que presentarán a la víctima.
	
- Eligen el implante de puerta trasera más adecuado y configuran la infraestructura de C2 necesaria para la operación.
	
- Asignan un identificador de misión específico que incrustan directamente en el código del malware.
	
- Finalmente proceden a compilar el backdoor y preparar la carga útil maliciosa que será desplegada.


### 🛡️La defensa

- Los controles de seguridad deben mantenerse actualizados para proteger los sistemas contra vulnerabilidades conocidas y posibles exploits de malware.	
	
- Realizar un análisis exhaustivo del malware, examinando tanto su carga útil como los métodos operativos que emplea durante la ejecución del ataque.
	
- Desarrollar detectores de armamento especializados e identificar nuevas variantes de carga útil maliciosa.
	
- Realizar un análisis temporal que establezca la correlación entre la fecha de creación del malware y su primer uso en ataques reales.
	
- Recopilación sistemática de archivos y sus metadatos asociados, servirán como base para investigaciones forenses.
	
- Determinar qué artefactos de armamento son característicos de las APT, ya que estos patrones permiten mejorar los sistemas de detección y respuesta.


## 🚚 Entrega (Delivery): Llevar a cabo la operación

### 👨‍💻 El atacante

- Utiliza un método de ataque definido para llevar a cabo la operación introduciendo, por ejemplo, el malware al objetivo.
- Entrega controlada de malware por el atacante.
- Correo electrónico malicioso.
- Malware en una memoria USB
- Interacciones en las redes sociales
- El sitio web es infectado con malware.


### 🛡️ La defensa

- Representa la primera y más crucial oportunidad para evaluar la efectividad de las defensas en la interrupción de un ataque. La información recopilada en etapas anteriores, junto con datos de referencia de ataques previos, permite implementar acciones oportunas para romper la cadena de ataque.
	
- Analizar a profundidad el vector de entrega utilizado, lo que implica comprender detalladamente la infraestructura de entrada empleada por los atacantes. El análisis proporciona insights valiosos para fortalecer los mecanismos de protección.
	
- Comprender los servidores, las personas, sus funciones y responsabilidades disponible.
	
- Inferir la intención del adversario basándose en los objetivos.
	
- Analizar la hora y el día en que comenzó la operación.
	
- Recoger los registros de correo electrónico y web para la reconstrucción forense.
	
- En una intrusión, los defensores deben ser capaces de determinar cuándo y cómo comenzó la entrega.



## Aprovechamiento (Exploitation)

### 👨‍💻 El atacante

- Busca aprovechar las vulnerabilidades para ganar acceso a los sistemas.
- A veces se aprovecha vulnerabilidades de tipo **zero-day** (desde fábrica), las cuales consisten en explotar fallos de seguridad desconocidos tanto para los fabricantes como para los usuarios finales. Estos exploits permiten a los atacantes obtener acceso no autorizado a los sistemas antes de que pueda implementarse algún parche de protección.
- ==Vulnerabilidad de software, hardware o humana==
- Adquirir o desarrollar un exploit de **zero-day**.
- Explotación de ls vulnerabilidades del servidor por el atacante.
- Explotación desencadenada por la víctima.
- Abrir el archivo adjunto de un correo electrónico malicioso.
- Hacer clic en un enlace malicioso.


## 🛡️La defensa
- Implementar diversas medidas de protección. Fortalecimiento de los mecanismos de autenticación mediante credenciales robustas. Mantener un estricto protocolo de actualizaciones del sistema que permita parchear vulnerabilidades conocidas.
- Fomentar entre los usuarios una cultura de seguridad cibernética que incluya el uso consciente de redes y herramientas digitales.
- Concienciación de los usuarios.
- Formación en codificación segura para los desarrolladores web.
- Escaneo regular de vulnerabilidades y pruebas de penetración.
- Medidas de endurecimiento de los `endopoints`.
- Restringir los privilegios de administrador.
- Reglas personalizadas para bloquear la ejecución de `shellcode`.
- Auditoría de los procesos de los `endpoints` para realizar forense.


## Instalación (Installation)
### El atacante

- Instalan accesos ocultos (**backdoors**) en el entorno de la víctima para mantener el acceso de forma persistente.
- La intrusión prolongada puede materializarse mediante dos método principales: la instalación de una `webshell` en el servidor web vulnerable o la implantación de un `backdoor` directamente en el sistema cliente comprometido.
- Establecer puntos de persistencia en los sistemas comprometidos mediante la creación de servicios maliciosos o la modificación de claves de registro que permiten la ejecución automática del malware.
- Evadir la detección, los adversarios suelen camuflar los archivos maliciosos, diseñándolos para que se asemejen a componentes legítimos del sistema operativo.

### La defensa

- Utilizar mecanismos técnicos (antivirus) y de gestión (procedimientos que incluyan revisión y verificación del origen del software) que supervisen instalaciones de software autorizadas o no.
- Alertar o bloquear rutas de instalación, por ejemplo, `RECYCLER`.
- Comprobar si el malware requiere privilegios de administrador o de usuario.
- Auditoría de procesos de `endpoints` para descubrir archivos anormales.
- Extrae certificados de cualquier ejecutable firmado.
- Comprender el tiempo de compilación del malware para determinar si es antiguo o nuevo.



## Comando y Control - C2: Implantar control remoto

### El atacante

- Utiliza malware para establecer un canal de comunicación remota, lo que le permite tomar el control total del equipo objetivo. Esta técnica proporciona acceso privilegiado al sistema comprometido, facilitando la ejecución de comandos de forma remota.
- Abre un canal de comunicación bidireccional con la infraestructura C2.
- Los canales C2 más comunes son a través de protocolos web, DNS y correo electrónico




### La defensa

Fase crítica, las defensas tiene la última oportunidad para interrumpir la cadena de ataque, impidiendo el establecimiento del canal de Comando y Control (C2).

Emplear mecanismos avanzados como  **Network Intrusion Prevention Systems (NIPS), Network Intrusion Detection Systems (NIDS)**, firewalls de última generación y otras herramientas similares, cuyo propósito fundamental es neutralizar los intentos del atacante y evitar que alcance sus objetivos en esta etapa del compromiso.

- Descubrir la infraestructura C2 mediante el análisis del malware.
- Endurecer configuración de la red.
- Exigir proxies para todo tipo de tráfico (HTTP, DNS).
- Personalizar los bloques de protocoles C2 en los proxies web.
- Bloqueos de categorías de proxy.
- Envenenamiento del servidor de nombres DNS.
- Realizar investigaciones de código abierto para descubrir nuevas infraestructuras C2 de los adversarios.


## Acciones sobre objetivos (Actions on Objectives)

![[Pasted image 20250503172007.png]]

### El atacante

Logra el objetivo, tomando control sobre el sistema; lo que pase luego depende del conocimiento, las habilidades y las intenciones del atacante. Por lo general, los objetivos pueden ser: El robo de la información, violación de la integridad de los datos, tomar el control del sistema, inhabilitar sistemas instrumentados de seguridad, etc.

- Recoger las credenciales del usuario.
- Escalada de privilegios.
- Reconocimiento interno.
- Movimiento lateral a través del entorno.
- Recoger y ex-filtrar datos.
- Destruir sistemas.
- Sobrescribir o corromper datos.
- Modificar subrepticiamente los datos


### La defensa

- Aplicar medidas de respuestas ante ataques, tomando en cuenta que mientras mayor tiempo se encuentra en este estado, mayores serán los daños o consecuencias desfavorables ocasionadas por el atacante. Las medidas van desde aislamiento del activo cibernético bajo ataque hasta detener el proceso. Estas medidas deben ser revertidas.
	
- Establecer un manual de respuesta a incidentes, que incluya un plan de comunicación y compromiso ejecutivo.
	
- Detectar la filtración de datos, el movimiento lateral y el uso de credenciales no autorizadas.
	
- Respuesta inmediata de los analistas a todas las alertas.
	
- Agentes forenses pre desplegados en los puntos finales para un rápido triaje (escoger, separar o clasificar).



# Tácticas Técnicas Procedimientos TTP

---

que es mitre? encargada de los cvss??

---

Utilizado para describir el *modus operandi*, comportamiento, patrones, actividades y métodos de un agente de amenaza, ayuda a analizar las amenazas y el perfil de agente, usado para fortalecer la seguridad.


<img src="https://www.optiv.com/sites/default/files/styles/image/public/images/Overarching-TTPs_Seer-SEO-Takeaways-Content%20Updates_Blog%20Images-100.jpg.webp?itok=Ic6K6d_Y"
>

| Tactics/Tools                                                          | Techniques                                                                             | Procedures                                                                           |
| ---------------------------------------------------------------------- | -------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| Una táctica es la descripción de más alto nivel de este comportamiento | Brindan una descripción más detallada del comportamiento en el contexto de una táctica | Implican una descripción de menor nivel, muy detallada en el contexto de una técnica |

## Las tácticas
Representan los lineamientos estratégicos que describen cómo un atacante planifica y ejecuta un ciberataque desde su fase inicial hasta la finalización. Este enfoque abarca diversas acciones coordinadas, que incluyen la recolección de información previa, la explotación de vulnerabilidades iniciales, la escalada de privilegios dentro del sistema, el movimiento lateral a través de la red y el establecimiento


- **Explotación inicial**:
	- Envían un correo de pishing personalizado (suplantando al proveedor) con un archivo Excel malicioso.
	- El documento explota una vulnerabilidad zero-day en macros (CVE-2022-30125).
- **Escalada de privilegios**: Usan *Mimikatz* para extraer credenciales de administrador del equipo infectado.
- **Movimiento lateral**:
	- Se mueven a servidores críticos usando RDP (Protocolo de Escritorio Remoto) con las credenciales robadas.
- **Acceso persistente**:
	- Crean tareas programadas en Windows para ejecutar malware cada 24 horas.
	- Instalan una puerta trasera (*backdoor*) en el servidor de backups.
- **Resultado**: Mantiene acceso a la red durante 9 meses, robando datos financieros sensibles.


## Las técnicas
Representan los métodos específicos que emplean los atacantes para lograr objetivos intermedios durante un compromiso de seguridad. Estas acciones especializadas abarcan desde la explotación inicial de vulnerabilidades hasta el establecimiento de canales de comunicación encubiertos con servidores de mando y control, la infiltración en infraestructuras críticas y la eliminación sistemática de evidencias tras completar la ex-filtración de datos.

**Ejemplo concreto**
El atacante podría utilizar la técnica de "Pass-the-Hash" (T1550.002 en MITRE ATT&CK) para moverse lateralmente en una red corporativa. Tras comprometer inicialmente un equipo mediante phishing, los atacantes recolectan hashes de credenciales NTLM mediante herramientas como  *Mimikatz*. Estos hashes les permiten autenticarse en otras sistemas sin necesidad de descifrar contraseñas, manteniendo acceso persistente mientras evitan la detección al no generar tráfico de red sospechoso.


## Los procedimientos



## Que utilidad tiene TTPs

- La rápida clasificación y contextualización de un evento o incidente mediante su correlación con las TTPs de actores relacionados con un ataque.
- Apoyar el proceso de investigación proporcionando rutas probables para la investigación, basándose en las TTPs anteriores utilizadas en un ataque.
- Apoyar la identificación de posibles fuentes o vectores de ataque.
- Apoyar los procesos de respuesta a incidentes y de identificación y mitigación de amenazas, ayudando a identificar los sistemas que probablemente estén comprometidos.
- Apoyar los ejercicios de modelado de amenazas ayudando a analizar e integrar los controles para defenderse de las TTPs conocidas de los actores de las amenazas.



# 09-05-2025



Un protocolo de red son un conjunto de reglas que gobiernas la comunicación


## Modelo OSI





## Principios de diseño seguro - arquitectura de red

- Modelo de amenazas
- Mínimos Privilegios
- Defensa de seguridad
- Valores predeterminados seguros
- Fallar de forma segura
- Separación de funciones
- Mantenlo simple
- Confianza cero
- Confiar pero verificar
- Responsabilidad compartida

# Ataque a la capa 2 - Data Link
En la capa enlace, **los dispositivos intercambian *tramas* utilizando las direcciones MAC de origen y destino**, los actores de las amenazas explotan este método de comunicación.

- ARP poisoning
- MAC flooding



### ARP poisoning

Suplantación de direcciones MAC (MAC spoofing) el hacker busca en la red direcciones MAC válidas originales para eludir las medidas de control de acceso.

Evadir las comprobaciones de autenticación. Ejm: *El haclker puede suplantar el gateway por defecto y puede copiar los datos transmitidos al Gateway sin ser identificado*.

- Protección de la privacidad.
- Prevención del robo de identidad.
- Acceso a aplicaciones de software de pago.

Evitar la suplantación
- Examinar el tráfico de red.
- Firewall con herramientas MAC SPOOFING.

### MAC Flooding


### MAC Cloning

Los actores de la amenaza generalmente realizan los siguientes pasos.

- Descubren


### MACsec, Media Access Control (MAC) Security

Es un estándar definido en IEEE 802.1AE, específica

