
# Reserva y Paquete Turistico
En el contexto de modelado de negocio para una agencia de turismo en línea, **reserva** y **paquete turístico** son conceptos relacionados pero distintos. Aquí explico cada uno y sus diferencias clave:

| Concepto          | Descripción                                                                                                      |
|-------------------|------------------------------------------------------------------------------------------------------------------|
| **Reserva**       | Acción de apartar o asegurar un servicio o producto específico (como un vuelo, hotel o tour) para una fecha concreta. Puede referirse a la reserva individual de elementos que componen un viaje. |
| **Paquete turístico** | Conjunto de servicios y productos agrupados y vendidos como una oferta única. Normalmente incluye varios elementos como transporte, alojamiento, actividades y, en algunos casos, comidas o guías. |

### Diferencias clave

1. **Composición**:
   - Una **reserva** es específica y singular, como reservar un vuelo, una habitación de hotel o una excursión.
   - Un **paquete turístico** combina varias reservas (por ejemplo, vuelo + hotel + actividades) y se vende como un solo producto.

2. **Alcance**:
   - La **reserva** abarca un solo servicio o un componente específico del viaje.
   - El **paquete turístico** abarca múltiples servicios que están relacionados entre sí para formar una experiencia de viaje completa.

3. **Personalización**:
   - Las **reservas** suelen ser más flexibles y permiten al usuario seleccionar servicios individuales según sus preferencias.
   - Los **paquetes turísticos** vienen predefinidos con un conjunto de servicios, aunque algunos pueden permitir opciones de personalización limitada.

4. **Precio**:
   - Las **reservas** individuales se cotizan de forma independiente.
   - Los **paquetes turísticos** suelen ofrecer un precio global que puede ser más económico que la suma de los componentes reservados por separado, ya que aprovechan descuentos por volumen.

### Ejemplo
- **Reserva**: Un cliente visita la agencia en línea y reserva solo una habitación de hotel para el fin de semana.
- **Paquete turístico**: Un cliente compra un paquete de "Escapada de Fin de Semana" que incluye vuelo de ida y vuelta, 2 noches de hotel y un tour guiado por la ciudad.

Estos conceptos se complementan, ya que una agencia de turismo en línea puede ofrecer tanto la opción de hacer **reservas** individuales como la de comprar **paquetes turísticos** completos.


# Backend

## Archivo `pom.xml`
Esta configuración `pom.xml` es un archivo de Maven que define un proyecto de Spring Boot, estableciendo las dependencias y la estructura de construcción del proyecto. Aquí tienes una explicación detallada de cada sección:

### 1. Cabecera del Proyecto
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
```
- Define el esquema y la versión del modelo del proyecto que está siguiendo Maven (4.0.0).
- El `xmlns` y `xsi:schemaLocation` proporcionan la ubicación del esquema XML.

### 2. Definición del `parent`
```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>3.3.5</version>
    <relativePath/> <!-- lookup parent from repository -->
</parent>
```
- Establece el proyecto padre como `spring-boot-starter-parent`, lo que permite heredar configuraciones estándar de Spring Boot.
- La versión `3.3.5` se refiere a la versión de Spring Boot que se está utilizando.
- `<relativePath/>` hace que Maven busque el proyecto padre en el repositorio.

### 3. Información del Proyecto
```xml
<groupId>com.dirac</groupId>
<artifactId>sigepat</artifactId>
<version>0.0.1-SNAPSHOT</version>
<name>sigepat</name>
<description>Spring Boot SigepatBackend Project</description>
```
- `<groupId>`: Identificador único del proyecto (comúnmente el nombre de dominio invertido).
- `<artifactId>`: Nombre del proyecto.
- `<version>`: Versión del proyecto, `SNAPSHOT` indica que es una versión en desarrollo.
- `<name>` y `<description>`: Información básica del proyecto.

### 4. Propiedades
```xml
<properties>
    <java.version>17</java.version>
</properties>
```
- Define la versión de Java que se usará (Java 17 en este caso).

### 5. Dependencias
```xml
<dependencies>
    <!-- Spring Data JPA para persistencia -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>

    <!-- Spring Web para desarrollar APIs REST -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>

    <!-- Herramientas de desarrollo (hot reload) -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-devtools</artifactId>
        <scope>runtime</scope>
        <optional>true</optional>
    </dependency>

    <!-- Controlador de base de datos PostgreSQL -->
    <dependency>
        <groupId>org.postgresql</groupId>
        <artifactId>postgresql</artifactId>
        <scope>runtime</scope>
    </dependency>

    <!-- Lombok para simplificar la escritura de código -->
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <optional>true</optional>
    </dependency>

    <!-- Dependencias de prueba -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>
</dependencies>
```
- **`spring-boot-starter-data-jpa`**: Para usar JPA y Hibernate para la persistencia de datos.
- **`spring-boot-starter-web`**: Para crear aplicaciones web y APIs REST.
- **`spring-boot-devtools`**: Proporciona recarga automática y otras herramientas de desarrollo.
- **`postgresql`**: Controlador JDBC para conectar con una base de datos PostgreSQL.
- **`lombok`**: Biblioteca para reducir el código repetitivo (e.g., getters, setters).
- **`spring-boot-starter-test`**: Para realizar pruebas unitarias e integradas.

### 6. Sección de `build` y Plugins
```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
            <configuration>
                <excludes>
                    <exclude>
                        <groupId>org.projectlombok</groupId>
                        <artifactId>lombok</artifactId>
                    </exclude>
                </excludes>
            </configuration>
        </plugin>
    </plugins>
</build>
```
- **`spring-boot-maven-plugin`**: Plugin que permite empaquetar la aplicación en un `jar` o `war` ejecutable.
- `<configuration>` permite personalizar cómo se ejecuta el plugin. Aquí, se excluye la dependencia de `lombok` al empaquetar el proyecto.

Este `pom.xml` configura un proyecto Spring Boot con dependencias comunes para desarrollo web, persistencia con JPA, conexión a PostgreSQL, herramientas de desarrollo, y soporte para pruebas.

# Conceptos

## JPA
JPA (Java Persistence API) es una especificación de Java que define un marco estándar para la gestión de datos relacionales en aplicaciones Java mediante la mapeo objeto-relacional (ORM). Es decir, JPA permite a los desarrolladores trabajar con bases de datos mediante la manipulación de objetos Java en lugar de escribir directamente consultas SQL.

### Conceptos Clave de JPA:
| Concepto        | Descripción                                                                          |
|-----------------|--------------------------------------------------------------------------------------|
| **Mapeo ORM**   | JPA permite mapear clases Java a tablas de la base de datos y atributos a columnas. |
| **Entity**      | Una clase Java que representa una tabla en la base de datos.                        |
| **EntityManager** | La interfaz principal de JPA para gestionar las operaciones de persistencia, como insertar, actualizar, eliminar y consultar datos. |
| **JPQL**        | Un lenguaje de consulta similar a SQL pero orientado a objetos, usado para trabajar con entidades JPA. |
| **Anotaciones** | Se usan anotaciones como `@Entity`, `@Table`, `@Id`, `@Column`, entre otras, para mapear clases y atributos a la estructura de la base de datos. |

### Ejemplo de una Clase con JPA:
```java
import javax.persistence.Entity;
import javax.persistence.Id;
import javax.persistence.Column;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;

@Entity
public class Cliente {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false)
    private String nombre;

    @Column(nullable = false)
    private String apellido;

    // Getters y setters
}
```

### Ventajas de Usar JPA:
- **Simplificación del código**: Reduce la cantidad de código necesario para manejar la persistencia de datos.
- **Portabilidad**: Es independiente del proveedor de JPA (por ejemplo, Hibernate, EclipseLink, etc.), lo que permite cambiar de proveedor con menor esfuerzo.
- **Mantenimiento**: Facilita el mantenimiento de la aplicación al utilizar un modelo orientado a objetos.

### Relación con Spring Data JPA:
En el contexto de un proyecto Spring Boot (como el que mencionaste con el `pom.xml`), se suele usar **Spring Data JPA**, que es un proyecto de Spring que simplifica aún más el uso de JPA proporcionando métodos de repositorio predefinidos para acceder y gestionar entidades.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

La dependencia `spring-boot-starter-data-jpa` que está en tu archivo `pom.xml` incluye todo lo necesario para trabajar con JPA de manera sencilla en un proyecto Spring Boot.

# Conexion a base de datos
- Render: es un poco más lento
- Neon: Lo usa la profesora

## Credenciales Neon

```
postgresql://sigepat-bd_owner:Ulxwnb3rj8Rz@ep-orange-bird-a5o6nkrk.us-east-2.aws.neon.tech/sigepat-bd?sslmode=require
```


- host: ep-orange-bird-a5o6nkrk.us-east-2.aws.neon.tech
- username: sigepat-bd_owner
- password: Ulxwnb3rj8Rz
- bd: sigepat-bd



# Distribucion de autos

Basándome en tu descripción, aquí está la lógica para insertar autos en la tabla `auto` según el contexto de las ciudades y aeropuertos. Asignaremos cantidades de autos dependiendo de cuán comercial o turística sea la ciudad.

---

### **Distribución de autos**
- **Aeropuertos comerciales (más autos):**
  - **Jorge Chávez (Lima)**: 40 autos.
  - **Alejandro Velasco Astete (Cuzco)**: 30 autos.
  - **Alfredo Rodríguez Ballón (Arequipa)**: 25 autos.
  - **Capitán FAP Carlos Martínez de Pinillos (Trujillo)**: 20 autos.

- **Aeropuertos con pocos autos:**
  - **Capitán FAP Guillermo Concha Iberico (Piura)**: 15 autos.
  - **Mayor General FAP Armando Revoredo Iglesias (Cajamarca)**: 10 autos.

- **Aeropuertos sin autos:**
  - **Francisco Carlé (Jauja)**.
  - **Internacional Capitán FAP David Abensur Rengifo (Pucallpa)**.

---

### **Aeropuertos sin autos**
Los aeropuertos **Francisco Carlé (Jauja)** y **Internacional Capitán FAP David Abensur Rengifo (Pucallpa)** no tendrán autos. Por tanto, no se ejecutarán comandos de inserción para estos.


# Convenciones

Insomia usa la convención camelCase, si tus campos de clase los has definido con convencion PascalCase en Java, estos no se reflejaran en Insomia.

**Java**
```java
private Long IdPersona
```

**Insomia (JSON)**
```json
{
"idPersona": 1
}
```


# Solicitudes HTTP
Las solicitudes HTTP (Hypertext Transfer Protocol) son mensajes que los clientes, como los navegadores web, envían a un servidor para pedir información. Las solicitudes HTTP se componen de varios elementos, entre ellos un método HTTP, que es un verbo o nombre que describe la acción que se solicita: 

- **GET**
    
    Se utiliza para recuperar datos del servidor. Es un método de lectura. 
    
- **POST**
    
    Se utiliza para enviar datos al servidor, creando o modificando un recurso. Es un método de creación. 
    
- **PUT**
    
    Se utiliza para actualizar o reemplazar un recurso existente. Es un método de actualización completa. 
    
- **PATCH**
    
    Se utiliza para actualizar una entrada de datos enviando solo los datos a cambiar al servidor. Es un método de actualización parcial. 
    
- **DELETE**
    
    Se utiliza para eliminar un recurso especificado por medio de un ID (URI). Es un método de eliminación. 
    

Las solicitudes HTTP también incluyen: 

- La versión del protocolo HTTP 
    
- Cabeceras de solicitud, que proporcionan información adicional sobre la transacción 
    
- El cuerpo del mensaje, que contiene los datos que se están enviando o recibiendo 
    
- La dirección del recurso pedido 
    

El servidor responde a las solicitudes HTTP con un código HTTP que indica el estado de la respuesta.

# Capas

Las cuatro clases asociadas a la entidad `Alojamiento` se deben a un patrón de diseño común en aplicaciones Spring Boot que organiza el código en capas lógicas. Este patrón promueve la separación de responsabilidades, lo que facilita la escalabilidad, el mantenimiento y las pruebas de la aplicación.

Aquí te explico el propósito de cada clase y su rol en el diseño de tu aplicación:

---

### 1. **Clase en el paquete `Model`**

Esta clase representa la entidad principal de negocio, directamente relacionada con la base de datos.

**Propósito**:

- Mapea la tabla `alojamiento` de la base de datos a un objeto Java (utilizando anotaciones como `@Entity` y `@Table`).
- Define los atributos (columnas) de la tabla en forma de propiedades del objeto.
- Utiliza anotaciones de JPA (Jakarta Persistence API) para manejar la persistencia.

**Ejemplo**:

```java
@Entity
@Table(name="alojamiento")
public class Alojamiento {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long idAlojamiento;
    private double precio;
    private boolean cancelable;
    private boolean modificable;
    private String nombre;
    private String ciudad;
    private String direccion;
    private int clasificacion;
    private int habIndDisponibles;
    private int habDobDisponibles;
}
```

**Responsabilidad**:

- Solo maneja el modelo de datos.
- No contiene lógica de negocio ni interacción directa con la base de datos.

---

### 2. **Clase en el paquete `Repository`**

Esta clase actúa como un puente entre la aplicación y la base de datos.

**Propósito**:

- Realiza consultas a la base de datos utilizando Spring Data JPA.
- Proporciona métodos para operaciones CRUD (crear, leer, actualizar, eliminar).
- Permite definir consultas personalizadas si es necesario (por ejemplo, mediante `@Query`).

**Ejemplo**:

```java
@Repository
public interface AlojamientoRepository extends JpaRepository<Alojamiento, Long> {
    // Métodos personalizados opcionales
    List<Alojamiento> findByCiudad(String ciudad);
}
```

**Responsabilidad**:

- Interactúa directamente con la base de datos.
- No contiene lógica de negocio.

---

### 3. **Clase en el paquete `Service`**

Esta capa contiene la lógica de negocio y orquesta las interacciones entre el controlador y el repositorio.

**Propósito**:

- Valida los datos antes de enviarlos al repositorio.
- Contiene reglas de negocio (por ejemplo, verificar la disponibilidad de habitaciones antes de guardar un alojamiento).
- Aísla la lógica de negocio de la implementación de la base de datos.

**Ejemplo**:

```java
@Service
public class AlojamientoService {
    @Autowired
    private AlojamientoRepository alojamientoRepository;

    public List<Alojamiento> getAlojamientos() {
        return alojamientoRepository.findAll();
    }

    public Alojamiento insertAlojamiento(Alojamiento alojamiento) {
        // Lógica adicional antes de guardar
        return alojamientoRepository.save(alojamiento);
    }
}
```

**Responsabilidad**:

- Proporciona métodos reutilizables para manejar la lógica del negocio.
- Simplifica el controlador al delegar las operaciones complejas.

---

### 4. **Clase en el paquete `Controller`**

Esta clase maneja las solicitudes HTTP y coordina las respuestas de la aplicación.

**Propósito**:

- Recibe las solicitudes desde el cliente (por ejemplo, navegador o aplicaciones frontend).
- Llama a la capa de servicio para procesar la solicitud.
- Devuelve una respuesta HTTP con el estado correspondiente.

**Ejemplo**:

```java
@RestController
@RequestMapping("/api/v1/alojamiento")
public class AlojamientoController {
    @Autowired
    private AlojamientoService alojamientoService;

    @GetMapping
    public ResponseEntity<List<Alojamiento>> getAlojamientos() {
        return ResponseEntity.ok(alojamientoService.getAlojamientos());
    }
}
```

**Responsabilidad**:

- Maneja la interacción con los clientes (usuarios).
- No contiene lógica de negocio ni detalles de persistencia.

---

### Resumen: Roles de las clases

|Clase|Propósito|Ejemplo de Responsabilidad|
|---|---|---|
|**Model** (`Alojamiento`)|Representar datos (tabla en BD).|Definir propiedades como `idAlojamiento`, `precio`.|
|**Repository**|Acceso directo a la base de datos.|`findAll()`, `save()`, consultas personalizadas.|
|**Service**|Lógica de negocio y validación.|Verificar condiciones antes de guardar un registro.|
|**Controller**|Manejo de solicitudes HTTP y respuestas.|`@GetMapping`, `@PostMapping`, devolver `ResponseEntity`.|

---

### Ventajas de esta arquitectura

1. **Modularidad**: Cada capa tiene una responsabilidad única, lo que facilita los cambios.
2. **Reusabilidad**: La lógica de negocio en `Service` puede ser reutilizada por otros controladores o servicios.
3. **Facilidad para pruebas**:
    - Puedes probar `Service` y `Repository` de forma independiente.
    - Simulas respuestas en pruebas unitarias para evitar dependencias innecesarias.
4. **Escalabilidad**: Si más adelante necesitas agregar validaciones complejas, lógica adicional o servicios externos, cada capa puede extenderse sin afectar las demás.

¿Tienes alguna duda sobre este diseño o necesitas profundizar en alguna de las capas?


# Patrón DTO
El patrón **DTO (Data Transfer Object)** es un diseño utilizado en programación para transferir datos entre procesos o capas de una aplicación de forma eficiente. Su objetivo principal es reducir el número de llamadas entre componentes al agrupar información en un único objeto. Es muy común en aplicaciones con arquitecturas distribuidas o multicapa, como las basadas en servicios REST o arquitecturas orientadas a microservicios.

### Características principales del DTO:

|**Característica**|**Descripción**|
|---|---|
|**Propósito**|Agrupar datos para transferirlos de manera eficiente entre procesos o capas.|
|**Inmutabilidad**|Usualmente, se diseñan como objetos inmutables para mayor seguridad.|
|**Sin lógica**|No contiene lógica de negocio; solo sirve para almacenar y transportar datos.|
|**Independencia**|Está diseñado para ser independiente de la capa de dominio o de la base de datos.|

### Ejemplo de uso:

Imagina que tienes una aplicación que gestiona usuarios, y necesitas enviar datos del usuario desde la capa del servidor al cliente. En lugar de enviar un objeto de dominio (que puede contener datos adicionales o sensibles), creas un DTO específico.

**Clase DTO:**

```java
public class UsuarioDTO {
    private String nombre;
    private String correo;
    private int edad;

    // Constructor
    public UsuarioDTO(String nombre, String correo, int edad) {
        this.nombre = nombre;
        this.correo = correo;
        this.edad = edad;
    }

    // Getters
    public String getNombre() { return nombre; }
    public String getCorreo() { return correo; }
    public int getEdad() { return edad; }
}
```

**Conversión de un objeto de dominio al DTO:**

```java
public UsuarioDTO convertirADTO(Usuario usuario) {
    return new UsuarioDTO(usuario.getNombre(), usuario.getCorreo(), usuario.getEdad());
}
```

### Ventajas del patrón DTO:

|**Ventaja**|**Explicación**|
|---|---|
|**Optimización de datos**|Reduce la cantidad de información enviada al incluir solo lo necesario.|
|**Desacoplamiento**|Separa los datos que se transfieren de la lógica interna de la aplicación.|
|**Mejor seguridad**|Evita exponer información sensible de los objetos de dominio.|
|**Facilidad de mantenimiento**|Cambios en la capa de dominio no afectan directamente a los clientes.|

¿Te interesa algún detalle en particular o quieres otro ejemplo práctico?