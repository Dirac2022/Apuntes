La arquitectura cliente-servidor es un **modelo de diseño de software**. en este modelo las tareas se reparten entre los proveedores de recursos o servicios, llamados **servidores**, y los demandantes, llamados **clientes**.

<div style="text-align: center;">
	<figure>
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/1/1c/Cliente-Servidor.png/375px-Cliente-Servidor.png" width=600>
    <figcaption></figcaption>
    </figure>
</div>

# Ventajas y desventajas

## Ventajas
- **Administración centralizada**, donde todos los recursos se encuentran en un solo lugar y es accedidos por todos.
- **Control de acceso global bien administrado**.
- Un solo servidor para varios clientes con capacidad de aumento.
- **Mejora la escalabilidad**, ya que permite actualizar y ampliar ambos entornos por separado tanto en la parte del cliente como la parte del servidor.

## Desventajas
- Están expuestos en una red, pudiendo haber más posibles ataques de seguridad.
- Requieren el uso de una red para funcionar.
- Vulnerable a caídas masivas.


# Web como cliente-servidor

En el contexto de la web, el modelo cliente-servidor es un paradigma fundamental en el que las aplicaciones y servicios se estructuran para distribuir las tareas entre proveedores de servicios (servidores) y solicitantes de servicios (clientes). A continuación, te explico los componentes y funcionamiento de este modelo en la web.

### Componentes del Modelo Cliente-Servidor

1. **Cliente**:
   - **Navegador Web**: Los clientes son típicamente navegadores web como Google Chrome, Mozilla Firefox, Safari, etc. Estos se utilizan para acceder y visualizar contenido web.
   - **Aplicaciones Cliente**: También pueden ser aplicaciones específicas (apps) que se conectan a servicios web para obtener datos y funcionalidad.

2. **Servidor**:
   - **Servidor Web**: Los servidores web son programas que manejan solicitudes HTTP/HTTPS de los clientes. Ejemplos de servidores web incluyen Apache, Nginx y Microsoft IIS.
   - **Servidor de Aplicaciones**: Procesa la lógica de negocio de la aplicación web. Puede ser el mismo que el servidor web o estar separado.
   - **Servidor de Base de Datos**: Almacena datos persistentes para la aplicación web, que pueden ser consultados y manipulados a través de lenguajes como SQL. Ejemplos incluyen MySQL, PostgreSQL y MongoDB.

### Funcionamiento del Modelo Cliente-Servidor

1. **Solicitud (Request) del Cliente**:
   - El cliente (por ejemplo, un navegador web) envía una solicitud HTTP/HTTPS al servidor web. Esto puede ser una solicitud para una página web, un archivo, o cualquier recurso web.
   - Las solicitudes se realizan típicamente mediante métodos HTTP como GET (para obtener datos) y POST (para enviar datos).

2. **Procesamiento del Servidor**:
   - El servidor web recibe la solicitud y la procesa. Si es una solicitud simple para un archivo estático (como una imagen o un HTML), el servidor web puede manejarla directamente.
   - Para solicitudes más complejas que requieren lógica de negocio (por ejemplo, autenticación de usuario, procesamiento de formularios), el servidor web puede pasar la solicitud a un servidor de aplicaciones.

3. **Acceso a la Base de Datos**:
   - Si la solicitud implica operaciones con datos persistentes, el servidor de aplicaciones interactúa con el servidor de base de datos. 
   - Se ejecutan consultas SQL u otras operaciones de bases de datos para recuperar o manipular datos necesarios.

4. **Respuesta (Response) del Servidor**:
   - Una vez que el servidor web o de aplicaciones ha procesado la solicitud, genera una respuesta HTTP que incluye el código de estado (como 200 OK, 404 Not Found), cabeceras y el cuerpo de la respuesta (que puede ser HTML, JSON, XML, etc.).
   - La respuesta es enviada de vuelta al cliente.

5. **Renderizado en el Cliente**:
   - El navegador web del cliente recibe la respuesta y la procesa. Si es HTML, el navegador renderiza la página web para que el usuario la vea.
   - Si es JSON o XML (en el caso de aplicaciones web o SPA - Single Page Applications), el navegador puede usar JavaScript para procesar los datos y actualizar la interfaz de usuario dinámicamente.

### Ejemplo Simplificado

Supongamos que un usuario desea acceder a una página web:

1. El usuario escribe una URL en el navegador (por ejemplo, `https://www.example.com`).
2. El navegador envía una solicitud HTTP GET al servidor web de `example.com`.
3. El servidor web recibe la solicitud y determina qué recurso debe servir. Si es una página HTML estática, el servidor web devuelve el archivo HTML directamente.
4. El navegador recibe el archivo HTML y lo renderiza, mostrando la página web al usuario.

Si la solicitud fuera más compleja, como enviar un formulario de registro:

1. El usuario completa un formulario de registro y lo envía.
2. El navegador envía una solicitud HTTP POST al servidor con los datos del formulario.
3. El servidor web pasa la solicitud al servidor de aplicaciones que maneja la lógica de registro.
4. El servidor de aplicaciones interactúa con el servidor de base de datos para almacenar los datos del nuevo usuario.
5. El servidor de aplicaciones genera una respuesta (por ejemplo, una página de confirmación) y la envía de vuelta al navegador.
6. El navegador muestra la página de confirmación al usuario.

### Ventajas del Modelo Cliente-Servidor

- **Escalabilidad**: Los servidores pueden manejar múltiples solicitudes simultáneamente y distribuir la carga entre varios servidores.
- **Mantenimiento y Actualización**: Es más fácil actualizar y mantener aplicaciones en el servidor sin necesidad de modificar el cliente.
- **Seguridad**: Los datos sensibles y la lógica de negocio se mantienen en el servidor, lo que puede ser más seguro que distribuirlos a los clientes.

### Desventajas del Modelo Cliente-Servidor

- **Dependencia de la Red**: El modelo requiere una conexión de red fiable entre el cliente y el servidor.
- **Puntos Únicos de Falla**: Si el servidor falla, los clientes no pueden acceder a los recursos o servicios.

El modelo cliente-servidor es la base de cómo funciona la web hoy en día, permitiendo una amplia gama de aplicaciones desde simples sitios web hasta complejas aplicaciones web interactivas.

<div style="text-align: center;">
	<figure>
    <img src="https://i.blogs.es/392246/los-protocolos-que-se-usan-en-internet/1366_2000.jpg" width=600>
    <figcaption></figcaption>
    </figure>
</div>


# Framework
- Un framework incluye compiladores, programas de soporte, conjuntos de herramientas, bibliotecas de código y API que facilitan el desarrollo de un proyecto, proporcionando una estructura estándar y reutilizable.
- Las principales ventajas de utilizar un framework son el ahorro de tiempo, la capacidad de crear código escalable y la mejora en la seguridad.
- Los frameworks frontend se enfocan en la parte de la aplicación o sitio web con la que los usuarios interactúan directamente, mejorando la experiencia de usuario y facilitando el diseño de interfaces atractivas y funcionales.
- Los frameworks backend ofrecen herramientas que simplifican tareas complejas como la autorización de usuarios, la seguridad, el enrutamiento de URL y la interacción con bases de datos, permitiendo a los desarrolladores centrarse en la lógica de negocio.


# Fronted vs Backend
El front-end es todo lo que el navegador puede leer, mostrar o iniciar. Es decir, estos son HTML, CSS y Javascript. Este es el desarrollo de una interfaz de usuario y funciones, trabajando en un lado del cliente del sitio web o aplicación. Incluye todo lo que el usuario ve al abrir la página web. Los desarrolladores front-end cooperan con otros programadores, diseñadores y UX análisis para crear un producto conveniente y buscado. 

El back-end es todo lo que opera en el servidor, a saber, no en el navegador o computadora, que responde a otros mensajes de computadora. Esta es una parte de hardware del servicio. El back-end es un conjunto de herramientas, con la ayuda de las cuales se implementa la lógica de los sitios web. Esto es lo que está oculto a los ojos de los usuarios y sucede fuera de la computadora o el navegador. Uno puede usar cualquier lenguaje de programación para el back-end, incluyendo 
Ruby, PHP, Java, Javascript o Node.

<div style="text-align: center;">
	<figure>
    <img src="https://qubit-labs.com/wp-content/webp-express/webp-images/uploads/2021/04/Front-end-VS-Back-end-768x846.png.webp" width=650>
    <figcaption></figcaption>
    </figure>
</div>

La interacción entre el Front-end y el Back-end ocurre de manera cíclica:

- El Front-end envía los datos del usuario al Back-end.
- La información es procesada.
- Regresa en una forma comprensible.

Además, existen varias arquitecturas principales que definen la manera en que tu Front-end y Back-end interactuarán, incluyendo:

- Aplicaciones basadas en servidor.
- Conexión usando AJAX.
- Aplicaciones del lado del cliente (de una sola página).
- Aplicaciones universales/isomórficas.

Así, la interfaz de usuario y toda la interactividad constituyen el Front-end, y los datos y la lógica de negocio ─ el Back-end.


# Arquitectura general de una web
La arquitectura de una web implica varios componentes que trabajan juntos para crear una experiencia de usuario fluida y funcional. 

<div style="text-align: center;">
	<figure>
    <img src="https://pythones.net/wp-content/uploads/2020/11/LAMP-WAMP-min.png" width=600>
    <figcaption></figcaption>
    </figure>
</div>


A continuación, se detallan los elementos principales de esta arquitectura:
## Clientes
Los clientes son los dispositivos y aplicaciones que actúan como intermediarios entre los usuarios finales y los servidores web. Pueden ser tanto hardware (como computadoras, teléfonos inteligentes, tablets) como software (navegadores web, aplicaciones móviles y de escritorio).

- **Descripción**: Los clientes son dispositivos utilizados por los usuarios para acceder a la web, como computadoras, teléfonos inteligentes, tablets, etc.
- **Funciones**: Los clientes solicitan recursos web y muestran el contenido al usuario final. Utilizan navegadores web para interpretar y renderizar HTML, CSS y JavaScript.
- **Ejemplos**: Google Chrome, Mozilla Firefox, Safari, Microsoft Edge.

<div style="text-align: center;">
	<figure>
    <img src="https://tecnosoluciones.com/wp-content/uploads/2023/02/que-navegador-usar-en-internet.png" width=400>
    <figcaption></figcaption>
    </figure>
</div>

### Funcionalidades principales de los clientes:

1. **Solicitud de Recursos**: Los clientes envían solicitudes HTTP/HTTPS al servidor web para acceder a recursos como páginas web, imágenes, archivos, videos, entre otros. Utilizan métodos HTTP como GET, POST, PUT, DELETE para especificar la acción deseada.

2. **Interpretación de Respuestas**: Una vez que el servidor web responde a la solicitud del cliente, el cliente interpreta y procesa la respuesta. Por ejemplo, un navegador web interpreta el HTML, CSS y JavaScript recibido para renderizar una página web interactiva y visualmente atractiva.

3. **Presentación al Usuario**: Los clientes son responsables de presentar el contenido recibido al usuario final de manera legible y atractiva. Esto incluye la disposición de elementos visuales, el manejo de eventos de interacción (como clics y desplazamientos) y la ejecución de scripts para la funcionalidad dinámica.

### Tipos de Clientes:

- **Navegadores Web**: Son aplicaciones que interpretan y renderizan contenido web para los usuarios finales. Ejemplos populares incluyen Google Chrome, Mozilla Firefox, Safari, Microsoft Edge, entre otros.
  
- **Aplicaciones Móviles y de Escritorio**: Estas aplicaciones utilizan API y servicios web para interactuar con los servidores y ofrecer funcionalidades específicas a los usuarios. Pueden ser tanto nativas (desarrolladas para una plataforma específica) como basadas en tecnologías web (utilizando WebView para mostrar contenido HTML).

### Evolución y Tecnologías Relacionadas:

- **Interfaces de Programación de Aplicaciones (API)**: Permiten que las aplicaciones cliente accedan y utilicen servicios y datos específicos proporcionados por el servidor web.
  
- **Frameworks Frontend**: Como Angular, React, Vue.js, que facilitan la creación de interfaces de usuario dinámicas y complejas en aplicaciones web.



<div style="text-align: center;">
	<figure>
    <img src="https://conversisconsulting.com/wp-content/uploads/2018/08/sitio-web.png" width=600>
    <figcaption></figcaption>
    </figure>
</div>




## Servidor Web
Los servidores web (también conocidos como servidores HTTP) son un tipo de servidores utilizados para la **distribución (entrega) de contenido web** en redes internas o en Internet.
Destacan:
- Apache2
- Nginx
- IIS

### Descripción
El servidor web es el componente que maneja las solicitudes HTTP/HTTPS de los clientes y les proporciona los recursos solicitados.
### Funciones
  - Responder a las solicitudes del navegador enviando archivos HTML, CSS, JavaScript, imágenes y otros recursos.
  - Puede alojar aplicaciones web dinámicas mediante la ejecución de scripts del lado del servidor.


<div style="text-align: center;">
	<figure>
    <img src="https://lh3.googleusercontent.com/9022tEdFf4OjUeDifHyqS4EyLHDpJ0imOhnQUetQbnoiFKD5PlYTBMKTHOtjeHldaOUH2frTOBModl4pgn2vAw1EZP70SECtxLfg-pBk0RUhMs196bisvIJnHiDPJmetA2I_2rXbpFyQTSodcu2vN_v4PBjRoRHIQc6vup7TXGM0AsmsvWamutVliklNZ9jImpErhuIwqh2cAscQn2d_S8Am7tCuRdD25nN3L4yVZ4ND_FpQE5z8pwfFkDM56BzSgEdhmDc-Gx1zdnNe01P-WbT1VnashccOnqOmmuqBxLw-GM_8PeA37gA105L_gbhe4ga-Um8DA5puXz5tTSpQRZZrjVqt3l66E1WW_1AfFO8oRVPS2FywbrBuWbhlCLLYIu-SCDcLabd3Ro6jYtpzN0jbURjzsaUDj0AZOdiBmVkXYGdwm8empyHZaV3dBenJSXjFuWlnygw8QKIgsZ_qaOK01T_GMgoVhGM8zPY-F69abnMTvo-79ypkVDT9ZTQHd5byRxVq9jLbofgilyNldTnS9fef1tDhDWQPVVjWSGYI_tr4KFjmAKSKdgo-ih9wf0ifbUdrv177SnFydsfKqFUD29rBofUySDhKE0zp-P8i_jst9mxC=w463-h255-no" width=500>
    <figcaption></figcaption>
    </figure>
</div>
<div style="text-align: center;">
	<figure>
    <img src="https://miro.medium.com/v2/resize:fit:828/format:webp/0*mjG1YdoT7xPcnznN.jpg" width=500>
    <figcaption></figcaption>
    </figure>
</div>

<div style="text-align: center;">
	<figure>
    <img src="https://www.websentra.com/wp-content/uploads/Microsoft-IIS.png" width=300>
    <figcaption></figcaption>
    </figure>
</div>



## Lenguaje de Programación para Desarrollo Web


### Descripción
Los lenguajes de programación se utilizan para desarrollar la lógica de las aplicaciones web, tanto en el lado del cliente (frontend) como en el lado del servidor (backend).

### Funciones
 - **Frontend**: Crear interfaces de usuario interactivas y dinámicas. Ejemplos de lenguajes: HTML, CSS, JavaScript.
 - **Backend**: Manejar la lógica del negocio, procesar solicitudes, interactuar con bases de datos y gestionar la autenticación y autorización de usuarios. Ejemplos de lenguajes: Python, PHP, Java, Ruby, Node.js.
- **Frameworks**: Angular, React, Vue.js (frontend); Django, Flask, Laravel, Spring, Express.js (backend).

Algunos lenguajes de programación:
- Javascript
- Python
- PHP
- NodeJS
- Angular
- Ruby

<div style="text-align: center;">
	<figure>
    <img src="https://cdn-galmn.nitrocdn.com/GSQzEdMFdIGgicqYAambSetFochNVMes/assets/images/optimized/rev-cf20688/www.goodcore.co.uk/blog/wp-content/webp-express/webp-images/uploads/2019/12/Popular-programming-languages-and-frameworks.png.webp" width=600>
    <figcaption></figcaption>
    </figure>
</div>


## Base de Datos

### Descripción
La base de datos almacena de forma estructurada la información que necesita la aplicación web, como datos de usuario, contenidos, configuraciones y transacciones.

### Funciones
  - Almacenar y recuperar datos según sea necesario para el funcionamiento de la aplicación web.
  - Permitir consultas eficientes y seguras.

### Tipos
  - **Relacionales**: Utilizan SQL para gestionar datos estructurados en tablas. Ejemplos: MySQL, PostgreSQL, Oracle.
  - **NoSQL**: Utilizan diversos modelos de datos como documentos, grafos, clave-valor. Ejemplos: MongoDB, Redis, Cassandra.
### MySQL
Ideal para webs de media a gran escala y se encuentra disponible en casi todas las plataformas hosting e inclusive en la nube.

<div style="text-align: center;">
	<figure>
    <img src="https://hoplasoftware.com/wp-content/uploads/2021/07/1024px-MySQL.ff87215b43fd7292af172e2a5d9b844217262571.png" width=300>
    <figcaption></figcaption>
    </figure>
</div>

### MariaDB
Brinda facilidades de flexibilidad ofreciendo varios motores de almacenamiento eficaces para que pueda adaptar el sistema de base de datos a sus necesidades y también soporte para transacciones , almacenamiento de alto rendimiento.

<div style="text-align: center;">
	<figure>
    <img src="https://pbs.twimg.com/profile_images/1675860982025920515/fQVwLMze_400x400.jpg" width=300>
    <figcaption></figcaption>
    </figure>
</div>

### Postgres
Es el más robusto de los anteriores, dado que su sistema de indexación ofrece mejor rendimiento para trabajos a gran escala

<div style="text-align: center;">
	<figure>
    <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTdlBufQ8ULluU5e4OwfB1zttUn3kVf-MIziBQM-QxkAvOnRCA4GtsVt5jwypTIiig-YQ4" width=300>
    <figcaption></figcaption>
    </figure>
</div>



## Página Web

### Descripción
La página web es el documento o conjunto de documentos que se presentan al usuario final.

### Funciones
  - Proporcionar contenido y funcionalidades a través de una interfaz de usuario.
  - Utilizar HTML para la estructura, CSS para el diseño y JavaScript para la interactividad.

### Tipos
  - **Estáticas**: Contenido fijo que no cambia con la interacción del usuario. Son rápidas y fáciles de desplegar.
  - **Dinámicas**: Contenido generado en tiempo real en respuesta a las acciones del usuario o las solicitudes del cliente. Requieren más procesamiento del servidor y pueden interactuar con bases de datos.

### Sitios web estáticos vs dinámicos

####  Web estática

Son aquellos sitios cuyo contenido no cambia mediante la ejecución del programa y solo el administrador puede modificar. Generalmente, usan HTML puro.

#### Web dinámica

Son aquellos sitios que permiten cambios en su contenido, el cual es almacenado en la base de datos. Nos permiten crear aplicaciones dentro de la página web, como votaciones, libros de visitas, inicios de sesión, entre otros. Tienen una continua interacción con lenguajes de programación web y la base de datos.


<div style="text-align: center;">
	<figure>
    <img src="https://elblogpython.com/wp-content/uploads/2023/07/diferencias-entre-paginas-estaticas-y-dinamicas-en-el-desarrollo-web-con-python.jpg" width=600>
    <figcaption></figcaption>
    </figure>
</div>


Instalar y configurar un servidor web completo:
https://pythones.net/instalar-servidor-web-completo-mysql/