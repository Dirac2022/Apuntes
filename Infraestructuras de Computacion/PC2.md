**Mitchel Soto Cuya**
### 1. Creación de Políticas y Roles IAM:

*Crea una política IAM con permisos mínimos necesarios para que una instancia EC2 pueda interactuar con CloudWatch (enviar métricas y logs) y RDS (conectarse a la base de datos).*

Se creó la política IAM , con los permisos

Para **CloudWatch**
- `GetMetricStatistics`, `GetMetricData` en **Read**
- `PutMetricData` en **Write**


![[Pasted image 20251011084139.png]]

Para **CloudWatch Logs**

- `CreateLogGroup`, `CreateLogStream` y `PutLogEvents` en **Write**
- `DescribeLogStreams` en **List**

![[Pasted image 20251011084721.png]]

Para RDS

- `DescribeDBInstances` en **List**

![[Pasted image 20251011085434.png]]

Ya que son los permisos necesarios para enviar métricas, logs y conectarse a una base de datos.

Por ultimo, creo la política con nombre `Policy-PC2`

![[Pasted image 20251011085725.png]]


*Crea un rol IAM que utilice la política anterior y asócialo a futuras instancias EC2.*

- Seleccioné el servicio **EC2**

![[Pasted image 20251011090234.png]]

- Asocié al Rol mi política creada: `Policy-PC2`

![[Pasted image 20251011090336.png]]

- Nombre para el Rol: `Rol-PC2`

![[Pasted image 20251011090454.png]]



### 2. Lanzamiento de Instancia EC2

*Lanza una instancia EC2 (por ejemplo, t2.micro con Amazon Linux 2 AMI).*

- Se creo el grupo de Seguridad con trafico para `SSH` y `HTTP`

![[Pasted image 20251011092334.png]]

- Asocié el rol IAM creo `Rol-PC2`
- Agregue un volumen EBS con `10 GiB GP2`

![[Pasted image 20251011091658.png]]



*Conéctate a la instancia EC2 y monta el volumen EBS adicional. Instala un servidor web (Apache o Nginx) y PHP.*

- Me conecté a la instancia EC2:

![[Pasted image 20251011093459.png]]

- Monté el volumen EBS adicional

![[Pasted image 20251011094151.png]]

Instala un servidor web (Apache o Nginx) y PHP.*

- Instale un servidor Apache, a continuación detallo los comandos usados:

```sh
# Actualizando paquetes
sudo dnf update -y

# Instalacion Apache
sudo dnf install -y httpd

# Instalacion PHP y MySQL
sudo dnf install -y php php-mysqlnd

# Habilitando Apache
sudo systemctl enable --now httpd

# Verificacion
sudo systemctl status httpd
```

![[Pasted image 20251011094455.png]]


*Despliega una página web HTML/PHP de prueba simple que se conecte a una base de datos.*

- Se desplegó una pagina web de prueba

```php
<?php
echo "<h2>Servidor Web en EC2 funcionando correctamente</h2>";
?>
```

![[Pasted image 20251011095550.png]]

![[Pasted image 20251011095626.png]]






---

### 3. Configuración de RDS:

*Crea una instancia de base de datos RDS MySQL (por ejemplo, db.t2.micro con MySQL 8.x).*

- **DB instance identifier**: `db-pc2`
- **master username**: `admin`
- `db.t3.micro`
- `SSD gp2`
- `20 GiB`
- **Security group**: `SecurityGroup-RDS-PC2`
- **initial database**: `inventario_db`

![[Pasted image 20251011102820.png]]

Añadir algunas correcciones al grupo de seguridad para la base de datos:

![[Pasted image 20251011103140.png]]


El endpoint  de la bd es: `db-pc2.cwnucoeiajz0.us-east-1.rds.amazonaws.com`

![[Pasted image 20251011103330.png]]


*Conéctate a la instancia MySQL desde tu instancia EC2 y crea una base de datos y una tabla de ejemplo.*

- Primero instale la db, tuve problemas con MySQL, así que use MariaDB que es similar.

```sh
sudo dnf install -y mariadb105

```

- Me conecte a la base de datos

```sh
mysql -h db-pc2.cwnucoeiajz0.us-east-1.rds.amazonaws.com -u admin -p
```

![[Pasted image 20251011104705.png]]

- Se creó una tabla de ejemplo:

```mysql
USE inventorio_db;

CREATE TABLE products (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    qty INT
);

INSERT INTO products (name, qty)
VALUES ('Lapiz', 100), ('Cuaderno', 50), ('Borrador', 30);

SELECT * FROM products;

```

![[Pasted image 20251011105744.png]]

*Actualiza tu aplicación web en EC2 para conectarse a esta base de datos RDS.*

Se modifcó `index.php`

```php
<?php
echo "<h2>Servidor Web en EC2 funcionando correctamente</h2>";

$host = 'db-pc2.cwnucoeiajz0.us-east-1.rds.amazonaws.com';
$user = 'admin';
$pass = 'admin12345$$';
$db   = 'inventario_db';

$conn = new mysqli($host, $user, $pass, $db);

if ($conn->connect_error) {
    die("<p style='color:red;'> Error al conectar a RDS: " . $conn->connect_error . "</p>");
} else {
    echo "<p style='color:green;'>Conexión exitosa a RDS.</p>";
}

$result = $conn->query("SELECT * FROM products");
if ($result->num_rows > 0) {
    echo "<h3>Inventario:</h3><ul>";
    while ($row = $result->fetch_assoc()) {
        echo "<li>{$row['name']} - {$row['qty']}</li>";
    }
    echo "</ul>";
} else {
    echo "<p>No hay productos.</p>";
}

$conn->close();
?>
```

Se reinició servidor:

```sh
sudo systemctl restart httpd
```


Se observa que la pagina correctamente esta conectada con la base de datos

![[Pasted image 20251011110516.png]]

### 4. Monitoreo con CloudWatch:

*Verifica las métricas predeterminadas de la instancia EC2 (CPU Utilization, Network In/Out) y la instancia RDS (CPU Utilization, Database Connections) en la consola de CloudWatch.*


Para **EC2**

- CPU Utilization
- Network In/Out

![[Pasted image 20251011111017.png]]

![[Pasted image 20251011111116.png]]

**RDS**

- CPU Utilization
- Database Connections


Crea una alarma de CloudWatch para la instancia EC2 que te notifique si la utilización de CPU excede el 80% durante 5 minutos.

![[Pasted image 20251011111330.png]]

- nombre: `Alarma-EC2-CPU-PC2`

![[Pasted image 20251011111809.png]]


Crea una alarma de CloudWatch para la instancia RDS que te notifique si el número de conexiones a la base de datos excede un umbral razonable (ej. 10 conexiones) durante 5 minutos.


![[Pasted image 20251011112254.png]]


![[Pasted image 20251011112331.png]]


- nombre: `Alarm-DB-PC2`

![[Pasted image 20251011112442.png]]



*Configura un tópico SNS y suscríbete a él para recibir notificaciones por correo electrónico cuando las alarmas se activen.*

Coloque mi correo: `casimiro.soto.c@uni.pe`

### Preguntas de Verificación

*1. ¿Qué permisos específicos incluiste en tu política IAM para la instancia EC2?*

En la política IAM que cree (Policy-PC2) puse los permisos mínimos para que la EC2 pueda enviar métricas y logs a CloudWatch, y también ver info básica de RDS.  

Para CloudWatch agregué:

- `PutMetricData`
- `GetMetricData`
- `GetMetricStatistics`

Y para CloudWatch Logs:

- `CreateLogGroup`
- `CreateLogStream`
- `PutLogEvents`
- `DescribeLogStreams`

Finalmente, para RDS puse:

- `DescribeDBInstances`

Con eso la instancia tiene los permisos justos para conectarse a la BD y mandar metricas sin darle acceso admin a todo AWS.

*2. ¿Cómo te asegurarías de que solo tu instancia EC2 pueda acceder a la base de datos RDS?*

Cree un grupo de seguridad aparte solo para RDS (SecurityGroup-RDS-PC2) y en sus reglas puse que el puerto 3306 (MySQL) solo acepte conexiones desde el **SecurityGroup-PC2** (el que usa la EC2). Solo las instancias EC2 que tengan ese grupo pueden conectarse al RDS, ni mi PC ni nadie más desde internet puede hacerlo.



*3. Si tu aplicación experimenta una alta carga, ¿cómo te alertaría CloudWatch y qué métricas monitorearías principalmente?*

CloudWatch mandaría una alerta por correo (SNS) si se pasa del 80% de CPU durante 5 minutos, porque configuré una alarma con ese umbral.  
También monitorearía las métricas de **CPUUtilization**, **NetworkIn/Out** en la EC2, y en la base de datos vería **DatabaseConnections** y **FreeStorageSpace**, por si hay muchas conexiones o si el disco se está llenando.


*4. ¿Cuál es el propósito del volumen EBS adicional y cómo lo prepararías para ser utilizado por tu aplicación?*

El volumen EBS adicional (de 10 GiB) lo agregué para guardar los datos de la app o logs sin usar el disco principal.  Primero lo formateé con ext4 usando `mkfs -t ext4`, después lo monté en `/mnt/appdata` y puse su UUID en `/etc/fstab` para que se monte solo al reiniciar.  
Así el sistema siempre tiene ese espacio listo y persistente, incluso si se apaga la instancia.


*5. ¿Qué diferencia hay entre un Security Group y una ACL de Red en el contexto de la seguridad de la red?*

El **Security Group** es como un firewall a nivel de instancia, o sea, controla qué tráfico entra o sale de una EC2 o RDS. En cambio la **ACL (Access Control List)** actúa a nivel de subred (VPC), antes de llegar al Security Group.  
