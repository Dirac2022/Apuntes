
# `Properties`
`java.util.Properties`

La clase `Properties` es una estructura de datos especializada en Java que:

1. **Hereda de** `Hashtable<Object,Object>` (pero se recomienda usar los métodos específicos de Properties)
2. **Almacena pares clave-valor** donde tanto la clave como el valor son Strings
3. **Está diseñada específicamente** para manejar configuraciones y parámetros
4. **Permite cargar/guardar** desde/hacia streams (flujos de entrada/salida)

## Características principales:

- **Persistencia**: Puede guardarse y cargarse desde archivos (normalmente .properties)
- **Jerarquía**: Soporta una propiedad "default" (por si no encuentra una clave)
- **Codificación**: Maneja automáticamente codificaciones de caracteres
- **Thread-safe**: Es segura para uso concurrente (por heredar de Hashtable)

## Ejemplos Prácticos

### 1. Creación y uso básico

```java
import java.util.Properties;

public class EjemploBasico {
    public static void main(String[] args) {
        // Crear instancia
        Properties config = new Properties();
        
        // Agregar propiedades
        config.setProperty("db.url", "jdbc:mysql://localhost:3306/mydb");
        config.setProperty("db.user", "admin");
        config.setProperty("db.password", "secret123");
        
        // Obtener valores
        String url = config.getProperty("db.url");
        System.out.println("URL de la base: " + url);
        
        // Valor por defecto si no existe
        String timeout = config.getProperty("db.timeout", "30");
        System.out.println("Timeout: " + timeout);
    }
}
```

### 2. Cargar desde archivo

**archivo config.properties:**
```
# Configuración de la aplicación
app.name=MiAplicacion
app.version=1.0.0
debug.mode=true
```

**Código Java:**
```java
import java.io.FileInputStream;
import java.util.Properties;

public class CargarProperties {
    public static void main(String[] args) {
        Properties props = new Properties();
        
        try (FileInputStream fis = new FileInputStream("config.properties")) {
            props.load(fis);
            
            System.out.println("Nombre: " + props.getProperty("app.name"));
            System.out.println("Versión: " + props.getProperty("app.version"));
            System.out.println("Modo debug: " + props.getProperty("debug.mode"));
        } catch (Exception e) {
            System.err.println("Error al cargar configuración: " + e.getMessage());
        }
    }
}
```

### 3. Guardar propiedades en archivo

```java
import java.io.FileOutputStream;
import java.util.Properties;

public class GuardarProperties {
    public static void main(String[] args) {
        Properties settings = new Properties();
        
        settings.setProperty("window.width", "800");
        settings.setProperty("window.height", "600");
        settings.setProperty("window.title", "Mi Ventana");
        
        try (FileOutputStream fos = new FileOutputStream("ui_settings.properties")) {
            // El segundo parámetro es un comentario que se incluye en el archivo
            settings.store(fos, "Configuración de la interfaz gráfica");
            System.out.println("Configuración guardada exitosamente");
        } catch (Exception e) {
            System.err.println("Error al guardar: " + e.getMessage());
        }
    }
}
```

### 4. Jerarquía de propiedades (defaults)

```java
import java.util.Properties;

public class PropiedadesJerarquicas {
    public static void main(String[] args) {
        // Propiedades por defecto
        Properties defaults = new Properties();
        defaults.setProperty("lenguaje", "es");
        defaults.setProperty("pais", "MX");
        
        // Propiedades principales (con defaults)
        Properties config = new Properties(defaults);
        
        // Sobreescribir una propiedad
        config.setProperty("pais", "US");
        
        System.out.println("Lenguaje: " + config.getProperty("lenguaje")); // Usa el default
        System.out.println("País: " + config.getProperty("pais")); // Usa el valor sobrescrito
        System.out.println("Región: " + config.getProperty("region", "N/A")); // Default del get
    }
}
```

## Casos de Uso Comunes

1. **Configuración de aplicaciones**: Parámetros de inicio, conexiones a BD
2. **Internacionalización**: Almacenamiento de cadenas para diferentes idiomas
3. **Persistencia simple**: Guardar preferencias de usuario
4. **Configuración de sistemas**: Como alternativa a archivos XML o JSON cuando se necesita simplicidad

## Ventajas sobre un HashMap convencional

- **Métodos específicos** para carga/guardado desde/hacia streams
- **Soporte nativo** para archivos .properties
- **Comentarios** en los archivos de configuración
- **Codificación automática** para caracteres especiales

La clase Properties es una herramienta sencilla pero poderosa para manejar configuraciones en Java, especialmente cuando necesitas persistencia en archivos.