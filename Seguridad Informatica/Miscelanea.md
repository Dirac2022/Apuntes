
# No repudio
Garantiza que una entidad no pueda negar haber realizado una acción. En otras palabras, asegura que un usuario o sistema no pueda rechazar haber enviado un mensaje, realizado una transacción o ejecutado una acción específica.

El no repudio se implementa mediante técnicas criptográficas como firmas digitales, certificados digitales y registros de auditoría inalterables. Su propósito es proporcionar evidencia irrefutable de la participación de una entidad en una operación determinada.

El no repudio se basa en dos aspectos clave:
1. **No repudio del origen**: el remitente de un mensaje o la entidad que realiza una acción no puede negar su autoría.
2. **No repudio de la recepción**: el destinatario de un mensaje o la entidad que recibe una acción no puede negar haberla recibido.

Esto se logra mediante:
- **Firmas digitales**: cuando un usuario firma digitalmente un mensaje o documento, se usa una clave privada que solo él posee. La firma puede ser verificada con la clave pública correspondiente.

- **Infraestructura de Clave Pública (PKI):** el uso de certificados digitales emitidos por una Autoridad de Certificación (CA) confiable garantiza la autenticidad del firmante.

- **Registros de auditoría seguros:** los sistemas deben mantener logs protegidos contra alteraciones para registrar eventos críticos.

- **Técnicas de Blockchain:** en algunos casos, la inmutabilidad de la cadena de bloques puede garantizar que los registros de transacciones no sean alterados.

## Ejemplos

**1. Firmas Digitales en Correos Electrónicos**
Si un usuario envía un correo electrónico firmado digitalmente con su clave privada, el receptor puede verificar la autenticidad con la clave pública del remitente. De esta forma, el remitente no puede negar haber enviado el correo.

**2. Transacciones Bancarias**

Cuando una persona realiza una transferencia bancaria en línea, el banco genera registros digitales y notificaciones. Si la transacción requiere autenticación de dos factores (2FA) o una firma digital, el cliente no puede negar haberla realizado.

**3. Comercio Electrónico**
Cuando un usuario compra un producto en línea y recibe un comprobante de pago con una firma digital del proveedor, este último no puede negar que la transacción se realizó.

**4. Contratos Electrónicos**
Los contratos firmados digitalmente con certificados de una Autoridad de Certificación son legalmente vinculantes. Un firmante no puede negar que aceptó los términos del contrato.

**5. Blockchain y Criptomonedas**
Las transacciones en blockchain quedan registradas de manera inmutable y firmadas digitalmente por las claves privadas de los participantes. Un usuario no puede negar haber realizado una transacción con criptomonedas.


# VNP (Virtual Private Network)
Una **VPN** es una tecnología que permite establecer una conexión segura y cifrada entre un dispositivo y una red privada a través de Internet. Su propósito es proteger la privacidad del usuario y evitar el espionaje de datos.

> **Ejemplo**
> Un trabajador remoto usa una VPN para conectarse a la red interna de su empresa desde casa, asegurando que la información transmitida no pueda ser interceptada por atacantes.

# IDS Intrusion Detection System
Es un sistema que monitorea el tráfico de red o actividades en un sistema en busca de comportamientos sospechosos o ataques cibernéticos. Puede generar alertas cuando detecta intentos de intrusión.
- **IDS basado en red (NIDS)**: Monitorea el tráfico de la red en busca de amenazadas.
- **IDS basado en host (HIDS)**: Analiza actividades dentro de un sistema específico.

> **Ejemplo**
> Un IDS detecta un escaneo de puertos desde una dirección IP desconocida e informa al administrador de seguridad para que tome medidas.

# Firewalls
Es un sistema de seguridad que controla y filtra el tráfico de red, permitiendo o bloqueando conexiones según reglas de seguridad predefinidas. Puede ser de **software** (Windows Defender Firewall) o de **hardware** (firewall físico en una empresa).

> **Ejemplo**
> Un firewall bloquea todas las conexiones entrantes a un servidor web, excepto aquellas provenientes de direcciones IP autorizadas.

# Parches de seguridad
Los **parches de seguridad** son actualizaciones de software diseñadas para corregir vulnerabilidades o fallos en sistemas operativos y aplicaciones. Instalar parches reduce el riesgo de explotación por parte de atacantes.

> **Ejemplo**
> Microsoft lanza un parche de seguridad para Windows que soluciona una vulnerabilidad crítica detectada en su sistema operativo.

# Políticas de Retención de datos
Establecen cuánto tiempo y en qué condiciones se almacena los datos antes de ser eliminados o archivados. Son importantes para cumplir con regulaciones legales y optimizar el almacenamiento.

> **Ejemplo**
> Una empresa financiera mantiene los registros de transacciones durante 5 años antes de eliminarlos, en cumplimiento con la normativa legal.


# Debido ciudado
Hya que proteget esa informacion

devbia diligencia, debo diligenciar para que ese dato sea seguro
- planificar, hacer analisis de riesgos, proyectarme, como proteer esos datos




# CVSS

CVSS (Common Vulnerability Scoring System) es un **sistema estándar** para evaluar la **gravedad de vulnerabilidades de seguridad** en software y sistemas informáticos. Fue desarrollado por el **FIRST (Forum of Incident Response and Security Teams)** y es ampliamente usado en la industria de la ciberseguridad para priorizar la atención a vulnerabilidades.

---

### 🎯 ¿Para qué sirve CVSS?

CVSS proporciona una **puntuación numérica** (de 0.0 a 10.0) que indica qué tan grave es una vulnerabilidad. Cuanto más alta es la puntuación, mayor es el riesgo.

Esta puntuación ayuda a:

- Determinar la **urgencia de aplicar parches**.
- Priorizar los esfuerzos de mitigación.
- Comunicar el nivel de riesgo a personal técnico y no técnico.

---

### 🧱 Componentes de CVSS

CVSS se divide en **tres grupos métricos**:

#### 1. **Base Metrics (Métricas base)** – _Qué tan grave es la vulnerabilidad en sí misma._

Incluye factores como:

- **Attack Vector (AV)**: Cómo se puede explotar (por red, físicamente, etc.)
- **Attack Complexity (AC)**: ¿Es fácil de explotar?
- **Privileges Required (PR)**: ¿Qué permisos necesita el atacante?
- **User Interaction (UI)**: ¿Se necesita que la víctima haga algo?
- **Confidentiality/Integrity/Availability Impact (C/I/A)**: ¿Qué tanto afecta a la confidencialidad, integridad y disponibilidad del sistema?

Ejemplo:

> Una vulnerabilidad explotable por red, sin privilegios, sin interacción del usuario y que compromete totalmente la confidencialidad, integridad y disponibilidad, tendrá una puntuación base muy alta (cercana a 10.0).

#### 2. **Temporal Metrics** – _Cómo cambia la gravedad con el tiempo._

Evalúa:

- Disponibilidad de soluciones.
- Confianza en el reporte.
- Nivel de explotación actual.

#### 3. **Environmental Metrics** – _Qué tan relevante es la vulnerabilidad en tu entorno específico._

Permite ajustar la puntuación según:

- La importancia de los sistemas afectados.
- Las medidas de seguridad existentes.

---

### 📌 Ejemplo práctico

Supón que se descubre una vulnerabilidad en un servidor web que:

- Se puede explotar remotamente (AV: Network),
- No requiere privilegios especiales (PR: None),
- No necesita que el usuario haga nada (UI: None),
- Permite ejecutar código arbitrario (impacto crítico en C, I y A).

Esta vulnerabilidad podría tener una **puntuación base CVSS de 9.8**, que indica **riesgo crítico**.

---

### 🛠 Herramientas para calcular CVSS

Puedes usar calculadoras en línea como:

- [NVD CVSS Calculator](https://nvd.nist.gov/vuln-metrics/cvss)
    
- [FIRST CVSS Calculator](https://www.first.org/cvss/calculator/3.1)
    

---

### 🔍 ¿Dónde se ve en la práctica?

CVSS es común en bases de datos como:

- **NVD (National Vulnerability Database)**: [https://nvd.nist.gov/](https://nvd.nist.gov/)
    
- **CVE Details**: [https://www.cvedetails.com/](https://www.cvedetails.com/)
    

Cada vulnerabilidad (CVE) listada incluye su **puntuación CVSS**, como:

> CVE-2021-44228 (Log4Shell) — CVSS 10.0 (CRÍTICO)

---



# PoC (Proof of Concept)

### 🔍 ¿Qué es un PoC (Proof of Concept) en Seguridad Informática?

Un **Proof of Concept (PoC)** en seguridad informática es una **demostración funcional** que **prueba la existencia de una vulnerabilidad o amenaza** en un sistema, aplicación o infraestructura.  
No necesariamente se trata de un ataque completo, pero sí lo suficiente para **probar que la falla es real y explotable**.

---

### 📌 ¿Por qué es importante un PoC?

- ✅ **Valida una vulnerabilidad**: Sirve como prueba de que el fallo no es solo teórico.
    
- ⚠️ **Muestra el impacto potencial**: Puede simular cómo un atacante podría aprovechar la falla.
    
- 🔧 **Guía la remediación**: Ayuda a los desarrolladores o administradores a entender qué corregir.
    

---

### 📎 Características clave de un PoC

1. **Controlado**: Se ejecuta en un entorno de prueba o con autorización.
    
2. **No malicioso**: El objetivo es probar, no dañar.
    
3. **Documentado**: Incluye pasos claros, código o comandos utilizados, y resultados esperados.
    
4. **Reproducible**: Otros pueden verificarlo y replicarlo para confirmar la falla.
    

---

### 🧠 Ejemplo real 1: PoC de una vulnerabilidad XSS (Cross-site Scripting)

Supón que alguien encuentra que en un formulario web (por ejemplo, un buscador interno de una web), el sitio no limpia correctamente el contenido ingresado.

🔍 **PoC:**

```html
<script>alert('XSS PoC')</script>
```

- El investigador ingresa ese código en el buscador del sitio.
    
- Al cargar la página de resultados, aparece el `alert()` con el mensaje “XSS PoC”.
    
- Esto demuestra que el sitio permite la ejecución de scripts no autorizados → prueba de que hay una vulnerabilidad XSS.
    

---

### 🧠 Ejemplo real 2: PoC de ejecución remota de código (RCE)

Una vulnerabilidad crítica en Apache Struts (como la de **CVE-2017-5638**) permitía a los atacantes ejecutar código remoto en servidores web.

🔍 **PoC:** Un investigador envió un `Content-Type` modificado con un payload especial al servidor.

```bash
curl -X POST "http://victima.com" -H "Content-Type: %{(#nike='multipart/form-data').(#dm=@ognl.OgnlContext@DEFAULT_MEMBER_ACCESS)...}"
```

Este comando, al ejecutarse con éxito, por ejemplo hacía que el servidor respondiera con una shell o ejecutara comandos arbitrarios. No era un ataque completo, pero **demostraba que el servidor era vulnerable**.

---

### 🧠 Ejemplo real 3: PoC de vulnerabilidad en dispositivos IoT

Un investigador encuentra que una cámara IP de uso doméstico permite el acceso remoto sin autenticación.

🔍 **PoC:** Con un simple script en Python, accede al feed de video:

```python
import requests

url = "http://192.168.1.105/video"
response = requests.get(url)
with open("output.mp4", "wb") as f:
    f.write(response.content)
```

Eso bastaba para demostrar que **cualquier persona en la red podía espiar la cámara** sin login → grave problema de seguridad.

---

### 🧰 Herramientas comunes usadas para PoC

- `curl`, `wget`, `nmap`, `Metasploit`, `Burp Suite`, `Python`, `PowerShell`
    
- Scripts personalizados
    
- Documentación técnica (Markdown, PDF, video, captura de pantalla)
    

---

### 👨‍💻 ¿Quién crea PoCs?

- Investigadores de seguridad
    
- Hackers éticos (pentesters, red team)
    
- Desarrolladores que descubren errores
    
- Grupos como ZDI, Project Zero, etc.
    

---

### 🔐 PoC ≠ Exploit

Un **PoC** demuestra que la vulnerabilidad existe.  
Un **exploit** ya es una herramienta o código totalmente desarrollado para **explotar** esa vulnerabilidad, muchas veces con fines ofensivos o maliciosos.

---

### ✅ En resumen:

|PoC (Proof of Concept)|Exploit|
|---|---|
|Demuestra que una vulnerabilidad existe|Aprovecha esa vulnerabilidad para causar daño|
|Controlado y con fines éticos|Puede ser malicioso o ilegal|
|No siempre automatizado|Automatizado para facilitar el ataque|

---

¿Quieres que te muestre un ejemplo de código real de PoC para alguna vulnerabilidad específica?



# Groups

En esencia, los **grupos** en Linux y Unix son una forma de **gestionar y controlar los permisos de acceso a los recursos del sistema (principalmente archivos y directorios) para múltiples usuarios de manera colectiva**. Imagínalos como etiquetas que puedes poner a un conjunto de usuarios, y luego puedes decir "este archivo puede ser leído por cualquier usuario con la etiqueta 'desarrolladores'".

Aquí tienes los aspectos clave para entender los grupos:

**1. Agrupación de Usuarios:**

- Un **grupo** es una colección de cuentas de usuario.
- Un usuario puede pertenecer a **uno o varios grupos**.
- Cada usuario tiene un **grupo primario** (que generalmente se asigna cuando se crea el usuario) y puede ser miembro de **grupos secundarios o suplementarios**.

**2. Permisos a Nivel de Grupo:**

- Cada archivo y directorio en el sistema tiene asociado un **propietario** (un usuario) y un **grupo propietario**.
- Cuando se definen los permisos para un archivo o directorio, se especifican tres conjuntos de permisos:
    - **Permisos del propietario (user):** Qué puede hacer el usuario propietario del archivo.
    - **Permisos del grupo (group):** Qué pueden hacer los usuarios que son miembros del grupo propietario del archivo.
    - **Permisos de otros (others):** Qué pueden hacer los usuarios que no son el propietario ni miembros del grupo propietario.
- Estos permisos típicamente incluyen la capacidad de **leer (r)**, **escribir (w)** y **ejecutar (x)** el archivo o acceder al directorio.

**3. Propósito y Beneficios:**

- **Simplificación de la Administración:** En lugar de tener que otorgar o revocar permisos individualmente a cada usuario para cada archivo, puedes asignar un archivo a un grupo y luego simplemente añadir o eliminar usuarios de ese grupo para controlar su acceso. Esto es especialmente útil en entornos con muchos usuarios que necesitan acceder a los mismos recursos.
- **Colaboración:** Los grupos facilitan la colaboración entre usuarios. Por ejemplo, si varios desarrolladores están trabajando en el mismo proyecto, puedes crear un grupo "desarrolladores" y dar a ese grupo permisos de lectura y escritura en los archivos del proyecto. Cualquier usuario que sea miembro de este grupo podrá acceder y modificar los archivos.
- **Seguridad:** Los grupos ayudan a implementar políticas de seguridad coherentes. Puedes restringir el acceso a archivos sensibles a solo los miembros de un grupo específico, asegurando que usuarios no autorizados no puedan acceder a ellos.
- **Organización:** Los grupos proporcionan una forma lógica de organizar a los usuarios según sus roles, proyectos o responsabilidades dentro del sistema.

**4. Identificación de Grupos:**

- Cada grupo tiene un **nombre** (por ejemplo, `users`, `admin`, `developers`, `hidden`, `friends`).
- Cada grupo también tiene un **identificador numérico único** llamado **GID (Group Identifier)**. El sistema operativo utiliza el GID internamente para identificar los grupos.

**Ejemplos:**

Imagina que tienes un directorio llamado `proyecto_secreto`. Podrías hacer lo siguiente:

1. Crear un grupo llamado `equipo_alpha`.
2. Añadir a las usuarias Ana y Bruno al grupo `equipo_alpha`.
3. Cambiar el grupo propietario del directorio `proyecto_secreto` a `equipo_alpha`.
4. Establecer los permisos del directorio para que el propietario tenga lectura, escritura y ejecución (rwx), el grupo `equipo_alpha` tenga lectura y escritura (rw), y otros no tengan ningún acceso (---).

De esta manera, solo el propietario del directorio y cualquier usuario que sea miembro del grupo `equipo_alpha` (Ana y Bruno) podrán leer y escribir en los archivos dentro de `proyecto_secreto`. Otros usuarios no tendrán permiso para acceder a él.
