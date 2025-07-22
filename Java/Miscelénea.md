# Inicialización Estática en Java

La inicialización estática se refiere a la ejecución de código cuando una clase es cargada por el ``ClassLoader`` de Java, antes de que se cree cualquier instancia de la clase o se acceda a cualquier miembro estático.

## Sintaxis

Existen dos formas principales:

1. **Bloques de inicialización estática**:
```java
public class MiClase {
    static {
        // Código de inicialización estática
        System.out.println("Bloque estático ejecutado");
    }
}
```

2. **Asignación directa de variables estáticas**:
```java
public class MiClase {
    private static int contador = inicializarContador();
    
    private static int inicializarContador() {
        return 5 * 10;
    }
}
```

## Características clave

- Se ejecuta **una sola vez**, cuando la clase es cargada
- El orden de ejecución sigue el orden de aparición en el código
- Puede inicializar variables estáticas
- Puede lanzar excepciones (pero deben ser manejadas)
- Es thread-safe (la JVM garantiza que solo un hilo ejecute la inicialización)

## Ejemplo completo

```java
public class EjemploInicializacion {
    private static final String MENSAJE;
    private static int contador;
    
    // Bloque estático
    static {
        MENSAJE = "Hola Mundo";
        contador = 0;
        System.out.println("Bloque estático 1 ejecutado");
    }
    
    // Otro bloque estático (se ejecuta en orden)
    static {
        contador += 10;
        System.out.println("Bloque estático 2 ejecutado");
    }
    
    public static void main(String[] args) {
        System.out.println(MENSAJE);
        System.out.println("Contador: " + contador);
    }
}
```

Salida:
```
Bloque estático 1 ejecutado
Bloque estático 2 ejecutado
Hola Mundo
Contador: 10
```

La inicialización estática es muy útil para configuraciones que deben realizarse una vez por clase, como cargar bibliotecas nativas, inicializar recursos compartidos o configurar valores constantes complejos.



# ClassLoader

El **ClassLoader** es un componente fundamental del **Java Runtime Environment (JRE)** que forma parte integral de la **Java Virtual Machine (JVM)**. No es algo que necesites importar ni instanciar manualmente (aunque puedes interactuar con él), sino que es un mecanismo interno de Java que trabaja automáticamente.

## Conceptos clave:

1. **Propósito principal**:
   - Carga las clases (.class files) en memoria cuando son requeridas
   - Transforma el bytecode en representaciones internas ejecutables
   - Establece la jerarquía de namespaces para evitar conflictos

2. **Origen**:
   - Viene integrado en **cualquier implementación estándar de la JVM**
   - Es parte del núcleo de Java desde sus primeras versiones

3. **Jerarquía típica de ClassLoaders**:
   ```
   Bootstrap ClassLoader (nivel más alto)
      ↑
   Extension ClassLoader
      ↑
   System/Application ClassLoader (nivel visible normalmente)
   ```

## ¿Cómo funciona?

Cuando escribes:
```java
MiClase obj = new MiClase();
```

Detrás de escena ocurre:
1. La JVM pide al ClassLoader que cargue `MiClase` si no está ya cargada
2. El ClassLoader busca el archivo `.class` correspondiente
3. Verifica el bytecode y lo carga en memoria
4. La JVM puede entonces crear la instancia

## Ejemplo de interacción (aunque generalmente no es necesario):

```java
public class ClassLoaderDemo {
    public static void main(String[] args) {
        // Obtener el ClassLoader actual (el que cargó esta clase)
        ClassLoader loader = ClassLoaderDemo.class.getClassLoader();
        System.out.println("ClassLoader de esta clase: " + loader);
        
        // El ClassLoader de clases primitivas/core es null (Bootstrap ClassLoader)
        System.out.println("ClassLoader de String: " + String.class.getClassLoader());
    }
}
```

## Características importantes:

- **Carga bajo demanda**: Las clases se cargan solo cuando se necesitan
- **Delegación**: Los ClassLoaders siguen un modelo jerárquico (delegan a sus padres primero)
- **Visibilidad**: Un ClassLoader puede ver las clases de sus padres, pero no viceversa
- **Unicidad**: Una clase se identifica por su nombre completo + su ClassLoader

## ¿Cuándo interactuarías directamente con un ClassLoader?

Casos avanzados como:
- Carga dinámica de clases en tiempo de ejecución
- Implementación de plugins o módulos
- Creación de sandboxes de seguridad
- Hot-reloading de clases (como en servidores de aplicaciones)

El ClassLoader es una de las piezas más elegantes del diseño de Java, permitiendo características como la ejecución segura de código remoto y el aislamiento entre aplicaciones.


