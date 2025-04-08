
# Seguridad en Sistemas Informáticos

## Curso

**Nombre:** Seguridad en Sistemas Informáticos  
**Créditos:** 4  
**Horario:**

- **Teoría:** Viernes 15:00 - 18:00 (SALA 1)
    
- **Laboratorio:** Sábado 15:00 - 18:00 (SALA 2)
    

---

## Evaluación – Sistema G


## Introducción

- **La información** es fundamental para las empresas y la sociedad.
- La **seguridad informática** ha evolucionado hacia la **seguridad de la información**.
- La seguridad de la información es responsabilidad de todos los miembros de una organización, pero los administradores desempeñan un papel fundamental.

> 🔍 **Ejemplo:**  
> Un banco almacena datos financieros de sus clientes. Si no implementa medidas de seguridad adecuadas, un atacante podría robar información confidencial, afectando la reputación del banco y la confianza de los usuarios.

---

## ¿Qué es la Seguridad?

"The quality or state of being secure—to be free from danger"  
Significa estar protegido de los adversarios... de aquellos que harían daño, intencionadamente o no.

Es un concepto amplio, se refiere a la protección contra riesgos, amenazas o daños que puedan afectar a personas, bienes, sistemas, información o entornos.

- **Seguridad de la información**: Protección de datos contra accesos no autorizados, alteraciones o pérdidas.
- **Ciberseguridad**: Defensa de sistemas informáticos contra ataques digitales (*malware*, *pishing*, *ransomware*).



**Importancia de la seguridad**
- **Evita pérdidas económicas**: robos, multas por filtraciones de datos.
- **Protege la privacidad**: información personal o financiera.
- **Salva vidas**: protocolos de seguridad en fábricas
- **Fomenta la confianza**: clientes que confían en una plataforma de banca segura.


Una organización generalmente tiene múltiples capas de seguridad:

- **Seguridad física:** Protege los elementos físicos, objetos o áreas de una organización del acceso no autorizado y el uso indebido.
    
- **Seguridad personal:** Protege al individuo o grupo de individuos autorizados a acceder a la organización y sus operaciones.
    
- **Seguridad de las operaciones:** Protege los detalles de una operación o serie de actividades particulares.
    
- **Seguridad de las comunicaciones:** Protege los medios de comunicación, la tecnología y el contenido de una organización.
    
- **Seguridad de la red:** Protege los componentes, conexiones y contenidos de la red.
    
- **Seguridad de la información:** Protección de la información y sus elementos críticos, incluidos los sistemas y equipos que utilizan, almacenan y transmiten esa información.
    

> 📌 **Dato Importante** Para proteger la información y sus sistemas conexos del peligro, se necesitan herramientas como la política, la concienciación, la capacitación, la educación y la tecnología.

---

## Seguridad de la Información
Es el conjunto de medidas preventivas y reactivas implementadas por organizaciones y sistemas tecnológicos para proteger datos en cualquier formato (digital, físico, audiovisual, etc.)

Importancia
- **Cumplimiento legal**: Evita sanciones por leyes como GDPR
- **Protección de reputación**: Una filtración puede dañar la imagen de una empresa.
- C: Evita pérdidas económicas por ataques

- **Confidencialidad:** Solo las personas autorizadas pueden acceder a la información.
    
- **Integridad:** La información debe mantenerse exacta y sin alteraciones no autorizadas.
    
- **Disponibilidad:** La información debe estar accesible cuando se necesite.


> 🛡️ **Ejemplo:**  
> Un hospital almacena historiales clínicos de pacientes. Debe asegurarse de que solo médicos autorizados puedan ver estos registros (confidencialidad), que los datos no sean alterados por error o intención maliciosa (integridad), y que estén disponibles cuando se necesiten (disponibilidad).



**Seguridad de**

- **Hardware**: Protección física de dispositivos (servidores, routers, PCs). Control de acceso a salas de servidores, dispositivos antirobo.
- **Software**: Prevención de vulnerabilidades en aplicaciones y sistemas operativos, parches de seguridad, firewalls, antivirus.
- **Redes**: Defensa contra ataques en comunicaciones (Wi-Fi, Internet, LAN). VPN, sistemas de detección de intrusos (IDS).
- **Datos**: Cifrado, backups y control de acceso a información sensible. Encriptación de base de datos, políticas de retención de datos.



# Modelo Zero Trust
Es un **modelo de seguridad cibernética** que opera bajo el principio:
> [!cite] Never trust, always verify

A diferencia de los modelos tradicionales que asumen que todo **dentro de la red corporativa** es seguro, **Zero Trust** trata cada acceso como ==potencialmente malicioso==, sin importar su origen (interno o externo).

Desafíos
- **Complejidad**: Requiere reestructurar redes y políticas.
- **Costo**: Inversión en herramientas (IAM, SIEM, SDP).
- **Resistencia al cambio**: Usuarios acostumbrados a accesos sin restricciones.


## Principios Zero Trust

**Verificación explícita**
- Ningún usuario, dispositivo o aplicación se considera confiable por defecto.
- Cada acceso debe autenticarse y autorizarse.

**Acceso con privilegios mínimos**
- Los usuarios solo obtienen permisos estrictamente necesarios para su rol.

**Microsegmentación**
- La red se divide en zonas pequeñas y asiladas para limitar el movimiento lateral de atacantes.

**Monitoreo continuo**
- Analizar el comportamiento en tiempo real para detectar anomalías.

**Protección de datos**
- Cifrado, enmascaramiento y control estricto de transferencias.

**Zero Trust** no es un producto,  sino una **estrategia integral** que combina tecnologías, políticas y cultura organizacional. Es esencial en un mundo donde el **perímetro tradicional ya no existe** (cloud, IoT, trabajo remoto).




---


# Qué es Ciberseguridad  
La **ciberseguridad es la práctica de** defender, con tecnologías o prácticas ofensivas, las computadoras, los servidores, los dispositivos móviles, los sistemas electrónicos, las redes y los datos de ataques maliciosos llevados a cabo por cibercriminales.  

- Seguridad de red  
- Seguridad de las aplicaciones  
- Seguridad de la información  
- Seguridad operativa  
- Recuperación ante desastres y continuidad del negocio  
- Capacitación del usuario final  

---

# Pilares de la Seguridad de la Información  
- **Confidencialidad**  
- **Integridad**  
- **Disponibilidad**  

---

# Confidencialidad - Confidentiality   --

Protección de la información para impedir que entidades no autorizadas accedan a los activos de información

[[Conceptos de seguridad#Confidencialidad|Confidencialidad]]

**Proporciona confidencialidad mediante**:
- Cifrado de datos en reposo (todo el disco, BD)
- Cifrado de datos en tránsito (IPSec, TLS, PPTP, SSH)
- Clasificación de datos
- Control de Acceso
- Seguridad Física

**Objetivos**:
- Garantiza un nivel de secreto.
- Evita la divulgación no autorizada.



> **Ejemplo:** Cifrado de emails con PGP garantiza que solo el destinatario legítimo pueda leerlos.  

---

1. **Cifrado:**  
   - Clave de cifrado/descifrado (ejemplo: AES-256).  
   - Proceso: Remitente (encrypt) → Canal (ciphertext) → Destinatario (decrypt).  

2. **Control de acceso:**  
   - Basado en identidad (ejemplo: credenciales) o función (ejemplo: rol "Administrador").  

3. **Seguridad física:**  
   - Jaulas de Faraday para bloquear señales electromagnéticas.  

---

# Integridad - Integrity  
Garantiza que los datos no sean alterados o eliminados sin autorización.  

**Controles:**  
- Hashes (ejemplo: SHA-256 para verificar archivos).  
- Códigos de corrección (ejemplo: RAID para recuperar datos).  

**Ataques comunes:** Inyección SQL, envenenamiento de DNS.  

> **Ejemplo:** Firmas digitales en contratos electrónicos aseguran que no se modifiquen.  

---

# Disponibilidad - Availability  
Asegura que los sistemas y datos estén accesibles cuando se necesiten.  

**Controles:**  
- RAID y clústeres (ejemplo: Kubernetes para alta disponibilidad).  
- Copias de seguridad (ejemplo: backups automatizados en la nube).  

> **Ejemplo:** Cloudflare protege sitios web contra ataques DDoS que afectan la disponibilidad.  

---

# Triada CID y sus Opuestos  
| Pilar          | Amenaza          |  
|----------------|------------------|  
| Confidencialidad| Divulgación      |  
| Integridad     | Alteración       |  
| Disponibilidad | Pérdida/Destrucción |  

**Conceptos adicionales:**  
- Autenticidad (ejemplo: certificados SSL).  
- No repudio (ejemplo: firmas digitales en transacciones bancarias).  

---

# Autenticación y Autorización  
- **Identificación:** Declarar identidad (ejemplo: usuario y contraseña).  
- **Autenticación:** Verificar identidad (ejemplo: huella dactilar + token).  
- **Autorización:** Asignar permisos (ejemplo: rol "Editor" en WordPress).  

> **Ejemplo:** Google Workspace usa MFA (algo que sabes + algo que tienes).  

---

# Auditoría y No Repudio  
- **Auditoría:** Registro de logs (ejemplo: SIEM como Splunk).  
- **No repudio:** Pruebas irrefutables (ejemplo: blockchain en contratos).  

---

# Mecanismos de Protección  
1. **Seguridad en capas:** Firewall + Antivirus + Cifrado.  
2. **Abstracción:** Roles grupales (ejemplo: "Departamento de Finanzas").  
3. **Ocultar datos:** APIs con autenticación OAuth.  

> **Advertencia:** "Seguridad por oscuridad" (ejemplo: ocultar puertos) no es confiable.  

---

# Desafíos de la Seguridad  
- Complejidad vs. Usabilidad (ejemplo: banca en línea).  
- Costo vs. Beneficio (ejemplo: empresas que solo actúan tras un ciberataque).  


----


----- 



-----

# Qué es Ciberseguridad  
La **ciberseguridad es la práctica de** defender sistemas digitales contra ataques maliciosos.  

> **🔍 Profundizando: Ámbitos de acción**  
> - **Seguridad de red:** Firewalls y sistemas IDS/IPS (ej: Cisco Firepower).  
> - **Seguridad de apps:** Análisis estático/dinámico de código (ej: SonarQube).  
> - **Recuperación ante desastres:** Planes de contingencia documentados (ej: AWS Backup).  
> *Caso real: El ataque a Colonial Pipeline (2021) mostró la necesidad de proteger redes OT/IT.*  

---

# Pilares de la Seguridad de la Información  

> **🔍 Triada CID en profundidad**  
> ```mermaid  
> graph TD  
>   A[Confidencialidad] -->|Cifrado| B[AES-256]  
>   C[Integridad] -->|Hash| D[SHA-3]  
>   E[Disponibilidad] -->|Redundancia| F[RAID 6]  
> ```  
> *Ejemplo médico: Historiales clínicos requieren los 3 pilares: cifrados (C), con checksums (I), y accesibles 24/7 (D).*  

---

# Confidencialidad  

> **🔍 Cifrado avanzado**  
> - **En reposo:** LUKS (Linux) o BitLocker (Windows) para discos.  
> - **En tránsito:** Perfect Forward Secrecy en TLS 1.3.  
> *Ejemplo práctico: Signal usa cifrado E2E con PFS para mensajería.*  

> **🔍 Control de acceso físico**  
> - **Biometría multifactorial:** Huella + reconocimiento facial (ej: iPhone Face ID).  
> - **Jaulas Faraday:** Usadas en centros de examen para bloquear señales.  

---

# Integridad  

> **🔍 Técnicas de verificación**  
> | Método          | Caso de uso                  |  
> |-----------------|------------------------------|  
> | Hashes SHA-256  | Verificación de ISO descargadas |  
> | Firmas GPG      | Paquetes de software Linux   |  
> *Ejemplo de ataque: Stuxnet alteró código PLC sin detectarse con hashes válidos.*  

> **🔍 Sistemas anti-tampering**  
> - **WORM storage:** Discos write-once para compliance financiero.  
> - **Blockchain:** Registros inmutables (ej: land registry en Suecia).  

---

# Disponibilidad  

> **🔍 Redundancia crítica**  
> ```mermaid  
> graph LR  
>   A[Servidor principal] -->|Heartbeat| B[Servidor secundario]  
>   B -->|Failover automático| C[Balanceador de carga]  
> ```  
> *Ejemplo real: Netflix Chaos Monkey prueba caídas aleatorias en AWS.*  

> **🔍 Backup 3-2-1**  
> - 3 copias totales  
> - 2 medios diferentes (ej: NAS + cinta)  
> - 1 copia offsite (ej: AWS Glacier)  

---

# Autenticación & Autorización  

> **🔍 MFA en profundidad**  
> | Factor           | Ejemplo                      | Vulnerabilidad           |  
> |------------------|------------------------------|--------------------------|  
> | Algo que sabes   | Contraseña + PIN             | Phishing                 |  
> | Algo que tienes  | Yubikey + TOTP (Google Auth) | SIM swapping             |  
> | Algo que eres    | Reconocimiento de iris       | Deepfakes                |  

> **🔍 Modelo Zero Trust**  
> - "Never trust, always verify"  
> - Microsegmentación (ej: Google BeyondCorp)  

---

# Auditoría & No Repudio  

> **🔍 SIEM avanzado**  
> - **Reglas de correlación:** Detección de lateral movement (ej: Sigma rules).  
> - **Forensics:** Timeline analysis con ELK Stack.  
> *Caso: SolarWinds hack detectado mediante anomalías en logs.*  

> **🔍 No repudio legal**  
> - **Firmas digitales cualificadas** (eIDAS UE).  
> - **Registros timestamped:** RFC 3161 (Time-Stamp Protocol).  

---

# Mecanismos de Protección  

> **🔍 Defense in Depth**  
> ```mermaid  
> graph BT  
>   A[Cap 5: Datos] -->|Cifrado| B[Cap 4: App]  
>   B -->|WAF| C[Cap 3: Red]  
>   C -->|Firewall| D[Cap 2: Física]  
>   D -->|Políticas| E[Cap 1: Humana]  
> ```  

> **🔍 Criptografía post-cuántica**  
> - Lattice-based (Kyber)  
> - Hash-based (XMSS)  
> *Ejemplo: NIST está estandarizando algoritmos resistentes a quantum.*  

---

# Desafíos Actuales  

> **🔍 Paradoxes de seguridad**  
> - **Usabilidad vs Protección:** CAPTCHAs vs accesibilidad.  
> - **Innovación vs Riesgo:** IoT médico (ej: marcapasos hackeables).  

> **🔍 Futuro: IA en seguridad**  
> - **Blue team:** Darktrace detecta anomalías con IA.  
> - **Red team:** GPT-4 para generar ataques simulados.  