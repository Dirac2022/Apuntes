

# Modelo OSI
## Capa de aplicación OSI
La capa de aplicación es la más cercana al usuario final. Es la capa que proporciona la interfaz entre las aplicaciones utilizadas para la comunicación y la red subyacente en la cual se transmiten los mensajes.

La capa de aplicación permite una comunicación eficaz y segura entre diferentes programas de aplicación dentro de una red. Ofrece varias funciones:
- Identificación
- Autenticación
- Análisis
- Supervisión

<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjX0KUUFmryoGe7j_Y_PZD6htuEwKe0aF701QG9TyQrnetTO8WsqoatCax62WcD0XHvYhBLf4tRPYzhPplGyDPjiC6NH250p4PIEugnd-3iqIwZ4usPTy1FY39lACwQbsS590t57cbWqTiB/s1600/Capa+de+aplicaci%25C3%25B3n.jpg" width=700>
    <figcaption></figcaption>
    </figure>
</div>


## Capa de presentación OSI
Se utiliza principalmente para traducir diferentes formatos de archivo entre el emisor y el receptor. La capa de presentación tiene tres funciones principales:
- Dar formato a los datos del dispositivo de origen, o presentarlos, en una forma compatible para que lo reciba el dispositivo de destino.
- Comprimir los datos de forma tal que los pueda descomprimir el dispositivo de destino.
- Cifrar los datos para la transmisión y descifrarlos al recibirlos. Usa protocolos [[Protocolos#SSL (Secure Sockets Layer)|SSL]] y  [[Protocolos#TLS (Transport Layer Security)|TLS]].
- Definir estándares de formatos de archivos como [[Formatos#MPEG Files|MPEG]], formato de intercambio de gficos (GIF) y formato de gráficos de red portátiles (PNG). 

<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhRfrfO4ohvnCvgeyYA51Uy74YNvwUz4CrAJDUq86AY-w6EH0EJlXmnNIwuE_i1HAgBrMF5xvcuzo5ZznwJyGPS_6AEfVUnYg67MPiLYfufUzyP1j4oCk7-MMDK0wRlAaOW2PM-MKrNsFcv/s1600/Capas+de+presentaci%25C3%25B3n+y+sesi%25C3%25B3n.jpg" width=700>
    <figcaption></figcaption>
    </figure>
</div>

## Capa de sesión OSI
Proporciona los mecanismos para controlar el diálogo entre las aplicaciones de los sistemas finales. En resumen inicial y terminar sesiones.

Además de organizar y controlar la comunicación, la capa de sesión tiene una segunda función muy importante: la sincronización del intercambio de datos. Su importancia se pone especialmente de manifiesto cuando una transmisión de datos se interrumpe inesperadamente y de forma involuntaria en la cuarta capa o en una inferior.

Resaltan los protocolos:
- [[Protocolos#RPC (Remote Procedure Call)|RPC]]
- [[Protocolos#SCP (Secure Copy Protocol)|SCP]]
- [[Protocolos#SAP (Session Announcement Protocol)|SAP]]

# Capa de aplicación TCP/IP
Las tres capas superiores del modelo OSI definen funciones de la capa de aplicación TCP/IP única.

<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi90abIsuEUiPyhDqHD5EpeIuAmBgXZQ7qIFd89J276Y64AM11XpFkVg8Mn7kUwBVVYYxakjulQkFPOdAAH-G4JLEQ8YAKsdPp723-muBll6g3f6TO8gw47JulZvzD-ZDLZHULo0SoWGPPy/s1600/Beneficios+del+uso+de+un+modelo+en+capas.jpg" width=700>
    <figcaption></figcaption>
    </figure>
</div>

## Protocolos de la capa de aplicación TCP/IP
Los protocolos de aplicación TCP/IP especifican el formato y la información de control necesarios para muchas funciones de comunicación comunes de Internet.

Los protocolos de capa de aplicación son utilizados tanto por los dispositivos de origen como de destino durante una sesión de comunicación. Para que las comunicaciones se lleven a cabo correctamente, los protocolos de capa de aplicación que se implementaron en los hosts de origen y de destino deben ser compatibles.

<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjZ5cbjRDss75uB_B9JvgQxIZoeBDtkJxm0qJs-T1hx5qjLDmJHHXORiqUfO7ziKnW8mVEZAtAUKnEiYhTph3EQ5Iocb9Yhqk2kFc2c2h_UxDQknN3wKAeo9C_8kGm2hrn2L5nWcbg9qg3R/s1600/Protocolos+de+capa+de+aplicaci%25C3%25B3n+TCP-IP.jpg" width=700>
    <figcaption></figcaption>
    </figure>
</div>


### Sistema de nombres de dominio (DNS)
[[Protocolos#DNS (Domain Name System)]]
Traduce los nombres de dominio como por ejemplo **uni.edu.pe** a direcciones IP. Hay 4 tipos de servidores DNS implicados:

#### DNS resolver
El solucionador recursivo actúa como intermediario entre un cliente y un servidor de nombres DNS. Tras recibir una consulta DNS de un cliente web, una solucionador recursivo responderá con datos almacenados en caché o enviará una solicitud a un servidor de nombres raíz.

#### DNS raíz
Se puede comparar a un índice en una biblioteca que apunta a diferentes estanterías de libros. Generalmente sirve como referencia de otras ubicaciones más específicas.

#### Servidor de nombres TLD
Un servidor de nombres de dominios de primer nivel mantiene información para todos los nombres de dominio que comparten una extensión de dominio común, tal como `.com`, `.net`, etc. Por ejemplo, un servidor de nombres de primer nivel `.com` contiene información para todos los sitios web que terminen en `.com`.

#### Servidor de nombres autoritativo
El servidor de nombres autoritativo es la última parada en la consulta del servidor de nombres. Si cuenta con acceso al registro solicitado, devolverá la dirección IP del nombre del servidor solicitado al recursor de DNS.



<div style="text-align: center;">
	<figure>
    <img src="https://almablog-media.s3.ap-south-1.amazonaws.com/003_a056b326f9.png" width=700>
    <figcaption></figcaption>
    </figure>
</div>

![[funcionamiento DNS.png]]


### Simple Mail Transfer Protocol (SMTP)
[[Protocolos#SMTP (Simple Mail Transfer Protocol)]]
Los formatos de mensajes SMTP necesitan un encabezado y un cuerpo de mensaje. Mientras que el cuerpo del mensaje puede contener la cantidad de texto que se desee, el encabezado debe contar con una dirección de correo electrónico de destinatario correctamente formateada y una dirección de emisor.

Cuando un cliente envía correo electrónico, el proceso SMTP del cliente se conecta a un proceso SMTP del servidor en el puerto bien conocido 25. Después de que se establece la conexión, el cliente intenta enviar el correo electrónico al servidor a través de esta. Una vez que el servidor recibe el mensaje, lo ubica en una cuenta local (si el destinatario es local) o lo reenvía a otro servidor de correo para su entrega, como se muestra en la figura.

El servidor de correo electrónico de destino puede no estar en línea, o estar muy ocupado, cuando se envían los mensajes. Por lo tanto, el SMTP pone los mensajes en cola para enviarlos posteriormente. El servidor verifica periódicamente la cola en busca de mensajes e intenta enviarlos nuevamente. Si el mensaje aún no se ha entregado después de un tiempo predeterminado de expiración, se devolverá al emisor como imposible de entregar.

<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEidAT_RqmiblBUQ5DdPXmFA-Bvgcoqc7l-UfC3b_SzZc6_EkzLrfSGZkR1XaAOU5V46rCnawjMk7-cMJMASWUPMPX7vUssZy0_EQJbcLd_bfhUX_P6LxeUekQyomfNudUDT1prlXMHvQCRI/s1600/Funcionamiento+de+SMTP.jpg" width=600>
    <figcaption></figcaption>
    </figure>
</div>

**Puertos SMTP**
- **Puerto 25**. Puerto de comunicación por defecto, no presenta encriptación.
- **Puerto 465**. Se designo inicialmente para SMTPS (SMTP sobre [[Protocolos#SSL (Secure Sockets Layer)|SSL]]). Muchos ISP y proveedores de alojamiento en la nube siguen admitiendo el puerto 465 para el envío SMTP.
- **Puerto 587**. Es el puerto principal que se utiliza para enviar emails a través de SMTP en la web moderna. Trabaja sobre [[Protocolos#TLS (Transport Layer Security)|TLS]].

La mayoría de aplicaciones cuando va a enviar correos utilizando el protocolo SMTP necesitan configurar los parámetros básicos para dicho envío, estos son:
- Servidor de correo saliente.
- Definir autenticación (Si/No).
- Protocolo de seguridad SMTP (SSL/TLS).
- Usuario SMTP.
- Contraseña.
- Puerto de salida SMTP.


**PHPmailer con Gmail**
```php
$mail = new PHPMailer(true);
// Server settings
$mail->SMTPDebug=0;
$mail->isSMTP();
$mail->Host       = 'smtp.gmail.com';
$mail->SMTPAuth   = true;
$mail->Username   = 'micorreo@gmail.com';
$mail->Password   = 'CONTRASEÑA_APLICACION';
$mail->SMTPSecure = PHPMailer::ENCRYPTION_STARTTLS;
$mail->Port       = 587;
$mail->CharSet = 'UTF-8';

// Recipients
$mail->setFrom('micorreo@gmail.com', 'Nombre Ejemplo');
$mail->addAddress($to);    // Añadir destinatiario

// Contenido
$mail->isHTML(true);
$mail->Subject = "MI ASUNTO PERSONALIZADO";
$mail->Body    = "EL CONTENIDO DE MI CORREO UTILIZADO PHPMAILER";

$mail->send();
```


**Configuración correo Moodle**
![[configuracion correo moodle.png]]


### Post Office Protocol (POP3)
Proporciona acceso a una bandeja de entrada almacenada en un servidor de email. Ejecuta las operaciones de descarga y eliminación de mensajes. Gracias a este protocolo, también puedes acceder a los mensajes localmente en modo fuera de línea. 
**Puertos**:
- 110 TCP
- 995 cifrado sobre TLS

**Aplicaciones que usan POP3**:
- Thunderbird
- Outlook Windows

Con POP, los mensajes de correo electrónico se descargan en el cliente y se eliminan del servidor, esto significa que no existe una ubicación centralizada donde se conserven los mensajes de correo electrónico. Como POP no almacena mensajes, no es una opción adecuada para una pequeña empresa que necesita una solución de respaldo centralizada.

Los clientes POP3 modernos le permiten guardar una copia de sus mensajes en el servidor si selecciona explícitamente esta opción.

<div style="text-align: center;">
	<figure>
    <img src="https://www.website.increasink.co.id/mode/uploads/2024/01/how-pop3-works-708x376-1.png" width=700>
    <figcaption></figcaption>
    </figure>
</div>

<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgM8Fnw1XX394POvGQcZFU6eq02K4xP420MsJf2SmlWlUu7LozH_LvBGZAs7uVNzEcDFUpIr-r_M4bQPt1T35KRhdJ8Qnv-fSuWunRaTtjALAa-i3sj51ZYBhFVoBrHDi6jf0_dKjDGZPPT/s1600/Funcionamiento+de+POP.jpg" width=650>
    <figcaption></figcaption>
    </figure>
</div>

### Internet Message Access Protocol (IMAP)
Permite acceder y administrar sus mensajes de email en el servidor de email. Este protocolo le permite manipular carpetas, eliminar permanentemente y buscar eficientemente a través de mensajes. Es el protocolo preferido para acceder a tu correo desde varias ubicaciones, y múltiples dispositivos. 

**Puertos**
- 143 TCP
- 993 cifrado sobre TLS

Se usa en el correo web.

<div style="text-align: center;">
	<figure>
    <img src="https://www.website.increasink.co.id/mode/uploads/2024/01/how-imap-works-1-708x414-1.png" width=700>
    <figcaption></figcaption>
    </figure>
</div>

<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEggbWbKwh4-pHZJ5dA6OR4OPCh0mm7Kshk3G9XgMgtJU4d9erq8DT2vnWXdQRV9XTyaWpRWgY1lm2KYfcaB4iPuZ8CG0AT1SWlM8BnpaiiX6R-BA9f4T3ZSIkTAQeIS079P5cLv3x6Sn6Ue/s1600/Funcionamiento+de+IMAP.jpg" width=700>
    <figcaption></figcaption>
    </figure>
</div>

### Dynamic Host Configuration Protocol (DHCP)
La asignación de direcciones con DHCP se basa en un modelo cliente-servidor: el terminal que quiere conectarse solicita la configuración IP a un servidor DHCP con información de conexión. Se siguen los siguientes pasos de configuración:
- El cliente DHCP envía un paquete **DHCPDISCOVER** a la dirección broadcast desde la dirección 0.0.0.0.
- Todos los servidores DHCP que escuchan peticiones en el puerto 67 y responden a la solicitud del cliente con un paquete **DHCPOFFER**, que contiene una dirección IP libre, la dirección MAC y máscara de subred, así como el ID del servidor.
- El cliente DHCP escoge un paquete y contacta con el servidor correspondiente con **DHCPREQUEST**. El resto de servidores también reciben este mensaje de forma que quedan informados de la elección. Se confirma la información.
- Se envía la información adicional al cliente con un paquete **DHCPACK**, que incluye datos de DNS, SMTP y/o POP.

<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjI2G-a9gUkumzQ8WxW9oHq_2rP2_wDWURYldXAyA7LGRtlsy9X1jPqHKba7l3DhdGH3ULh2jNx9w1WSpwRXadv8Ljq02WNrMJYhiAZPQyABWmhhj8dJQ3dFfMxHXuXnTHbrf05LpelNQeo/s1600/Funcionamiento+de+DHCP.jpg" width=700>
    <figcaption></figcaption>
    </figure>
</div>

### File Transfer Protocol (FTP)
FTP se desarrolló para permitir las transferencias de datos entre un cliente y un servidor. Un cliente FTP es una aplicación que se ejecuta en una computadora cliente y se utiliza para insertar y extraer datos en un servidor FTP. Requiere dos conexiones entre el cliente y el servidor, una para los comandos y las respuestas y otra para la transferencia de archivos.

Otras versiones FTPS y SFTP.
- La primera se basa en **FTP mediante SSL**: la conexión se establece en combinación con **SSL** y el intercambio de archivos es encriptado.
- La segunda usa **SSH** y un solo canal de comunicación.

<div style="text-align: center;">
	<figure>
    <img src="https://www.ionos.es/digitalguide/fileadmin/_processed_/a/f/csm_illustration-of-the-ftp-process_a028f88e14.webp" width=700>
    <figcaption></figcaption>
    </figure>
</div>

**Aplicación: FileZila**

### Hypertext Transfer Protocol (HTTP)
[[Protocolos#HTTP (Hypertext Transfer Protocol)]]
[[Protocolos#HTTPS (Hypertext Transfer Protocol Secure)]]
Cuando se escribe una dirección web o un localizador uniforme de recursos (URL) en un navegador web, el navegador establece una conexión con el servicio web que se ejecuta en el servidor mediante el protocolo HTTP. Los nombres que la mayoría de las personas asocia con las direcciones web son URL e identificadores uniformes de recursos (URI).

Para comprender mejor cómo interactúan el navegador web con el servidor web, podemos analizar cómo se abre una página web en un navegador. Para este ejemplo, utilice el URL http://www.cisco.com/index.html.

Primero, el navegador interpreta las tres partes del URL, como se muestra en la Figura 1:

1. **http** (el protocolo o esquema)
2. www.cisco.com (el nombre del servidor)
3. **index.html** (el nombre de archivo específico solicitado)

<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjMAia7-bbHb6sRoSGeMAxfKYpQ_DroKq00N_0N7Gi8NPobR3oz_9htdaZbonHs0axrenRw8_eV5mGWaJyTV9CekkklYPyVcst0mSKlWZpHqikRlS9od0UcNn5JF0Yf-XO-YkvYSYhueCnI/s1600/Protocolo+de+transferencia+de+hipertexto+y+lenguaje+de+marcado+de+hipertexto-1.jpg" width=700>
    <figcaption>Figura 1</figcaption>
    </figure>
</div>


- A continuación, el navegador se comunica con un servidor de nombres para convertir               www.cisco.com en una dirección IP numérica que utiliza para conectarse al servidor, como se muestra en la figura 2. 
- Mediante los requisitos de HTTP, el navegador envía una solicitud GET al servidor y solicita el archivo index.html . 

<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhHhOTXJSjOUI3kVcC29Du3XUe-6rbecFLa__jhTU95XZHZHzm5CSuzJPR-UWPj2kpO757DF3ZNGogXZrvOTdw_6cilwsQFeLPzCFrobXX00jfUGnRMRLoB-3CADSsxsXDsEFUKZqNvkKr-/s1600/Protocolo+de+transferencia+de+hipertexto+y+lenguaje+de+marcado+de+hipertexto-2.jpg" width=650>
    <figcaption>Figura 2</figcaption>
    </figure>
</div>

- El servidor envía el código HTML para esta página web al navegador, como se muestra en la figura 3. 

<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj0oeotodB3WwwBOWA9Emqiq6WC6U3JpaS9W2IJGG1m5sYOA96X6FUigcNzktQoO7Bw_DdpJeOwCN0j6xNF3wgohnThfxamJ8yiLHIZzLicS-s5ljcZKy382Stx9UAJVlKtZi_NvCEU9jkF/s1600/Protocolo+de+transferencia+de+hipertexto+y+lenguaje+de+marcado+de+hipertexto-3.jpg" width=650>
    <figcaption>Figura 3</figcaption>
    </figure>
</div>


 - Finalmente, el navegador descifra el código HTML y da formato a la página para que se pueda visualizar en la ventana del navegador, como se muestra en la figura 4.
<div style="text-align: center;">
	<figure>
    <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiHl_0y3Zt5Iqp8lQR5UU8Pp1bcvRLbT4GRXLefiNCpl9u0515tZdvxYo1K-pMw09E37YRUKBYCR7YnH5ldK4ad-x5z40ZLKw2dLDt0dpZxtqZPa_pSVpnRX66YsZIYIXFv3_ATOsqjVayf/s1600/Protocolo+de+transferencia+de+hipertexto+y+lenguaje+de+marcado+de+hipertexto-4.jpg" width=650>
    <figcaption>Figura 4</figcaption>
    </figure>
</div>

#### Ventajas y desventajas
**Ventajas**
- Consumo de recursos bajo debido a menos conexiones simultáneas.
- Tráfico de red TCP minoritario.
- Protocolo de enlace único.
- Reporte de errores online.
- Creación de canales.

**Desventajas**
- Requiere gran potencia para establecer la comunicación y transferir los datos.
- Seguridad.
- No optimizado en ciertos entornos.
- Integridad.
- Disponibilidad solo al cierre de la conexión.
#### Mensajes HTTP
En el protocolo HTTP existen 2 tipos de mensajes:
- **Peticiones HTTP (Request)**: Son los mensajes que el cliente envía al servidor para solicitar información o realizar una operación.
- **Respuestas HTTP (Responses)**: Son las respuestas que el servidor envía al cliente para responder a sus peticiones.

##### Petición HTTP
Toda petición HTTP está compuesta de
- **Método HTTP**: El tipo de operación que se quiere realizar (registro, consulta, modificación, etc.)
- **Ruta o path**: La ruta completa para identificar el recurso sobre el que se quiere operar.
- **Cabeceras**: Información adicional para el servidor que procesa la petición.
- **Cuerpo**: La información que se quiere enviar junto con la petición (sin contenido en operaciones GET). 

En una operación de registro, sería la información que se quiere registrar
<div style="text-align: center;">
	<figure>
    <img src="https://mdn.dev/archives/media/attachments/2016/08/09/13687/5d4c4719f4099d5342a5093bdf4a8843/HTTP_Request.png" width=600>
    <figcaption></figcaption>
    </figure>
</div>

##### Respuesta HTTP
Toda petición HTTP conlleva una respuesta, ya sea por haberse ejecutado ésta correctamente o bien para informar de un error. Estará compuesta de:

- **Código de estado**: Indica si la petición tuvo o no éxito y por qué.
- **Mensaje de estado**: Una descripción breve sobre el código de estado
- **Cabeceras**: Información adicional para el cliente que realizó la petición
- **Cuerpo**: La información que se quiere enviar al cliente. En una operación de consulta serían los datos que se solicitaron en la petición

<div style="text-align: center;">
	<figure>
    <img src="https://mdn.dev/archives/media/attachments/2016/08/09/13691/58390536967466a1a59ba98d06f43433/HTTP_Response.png" width=600>
    <figcaption></figcaption>
    </figure>
</div>

#### Códigos HTTP
Un código HTTP es un número de tres dígitos que genera un servidor en respuesta a la petición de un navegador.
<div style="text-align: center;">
	<figure>
    <img src="https://static.semrush.com/blog/uploads/media/f5/7c/f57c8f9295d20dc481e81ae1a782c13c/original.png" width=600>
    <figcaption></figcaption>
    </figure>
</div>

#### HTTP vs HTTPS
HTTPS protege las conexiones con un protocolo de seguridad que utiliza claves criptográficas para cifrar y validar datos. La forma más común para que los sitios web utilicen HTTPS y tengan un dominio seguro es obteniendo un certificado [[Protocolos#SSL (Secure Sockets Layer)|SSL]] o [[Protocolos#TLS (Transport Layer Security)|TLS]].

<div style="text-align: center;">
	<figure>
    <img src="https://www.hostinger.es/tutoriales/wp-content/uploads/sites/7/2022/11/ES-what-are-the-differences-between-http-and-https-1536x1102.png" width=600>
    <figcaption></figcaption>
    </figure>
</div>

