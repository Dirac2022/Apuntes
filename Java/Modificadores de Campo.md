

# Modificadores de Acceso

### `public`
Acceso desde cualquier clase

```java
public class Account {
    public String accountNumber;  // Accesible desde cualquier clase
    
    public Account(String number) {
        this.accountNumber = number;
    }
}

// Uso desde otra clase
Account acc = new Account("123456");
System.out.println(acc.accountNumber);  // Acceso directo permitido
```

### `private`
Acceso solo dentro de la clase

```java
public class BankAccount {
    private double balance;  // Solo accesible dentro de BankAccount
    
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;  // Acceso permitido
        }
    }
    
    public double getBalance() {
        return balance;  // Método público para acceso controlado
    }
}

// Uso desde otra clase
BankAccount account = new BankAccount();
// account.balance = 1000;  // Error: balance tiene acceso private
account.deposit(1000);  // Forma correcta
```

### `protected`
Acceso desde el mismo paquete y subclases

```java
package banking;

public class FinancialInstrument {
    protected String instrumentId;  // Accesible por subclases y clases del mismo paquete
    
    protected void validate() {
        System.out.println("Validating instrument " + instrumentId);
    }
}

package banking;

public class Stock extends FinancialInstrument {
    public void setup(String id) {
        instrumentId = id;  // Acceso permitido por ser subclase
        validate();  // Método protected accesible
    }
}
```

### (default/package-private)
Acceso solo desde el mismo paquete

```java
package utilities;

class Logger {
    String logPrefix;  // Modificador default (sin especificar)
    
    void log(String message) {
        System.out.println(logPrefix + ": " + message);
    }
}

// Solo accesible desde otras clases en el paquete 'utilities'
```

## Modificadores de No-Acceso

### `static` 

Pertenece a la clase, no a la instancia.

```java
public class Employee {
    private static int employeeCount = 0;  // Compartido por todas las instancias
    private String name;
    
    public Employee(String name) {
        this.name = name;
        employeeCount++;
    }
    
    public static int getEmployeeCount() {
        return employeeCount;  // Método static que accede a campo static
    }
}

// Uso
System.out.println(Employee.getEmployeeCount());  // 0
Employee e1 = new Employee("John");
Employee e2 = new Employee("Alice");
System.out.println(Employee.getEmployeeCount());  // 2
```

### `final`

Valor no modificable después de la inicialización

```java
public class Constants {
    public static final double PI = 3.141592653589793;
    public final String creationDate;
    
    public Constants(String date) {
        this.creationDate = date;  // Solo se puede asignar una vez
    }
    
    public void tryChange() {
        // creationDate = "2023-01-01";  // Error: no se puede modificar
    }
}

// Uso
System.out.println(Constants.PI);  // 3.141592653589793
Constants c = new Constants("2023-01-01");
// c.creationDate = "2023-01-02";  // Error
```

### `transient` 

Excluido de la serialización

```java
import java.io.*;

public class UserSession implements Serializable {
    private String userId;
    private transient String sessionToken;  // No se serializará
    private transient long tokenExpiry;  // Tampoco se serializará
    
    public UserSession(String userId, String token, long expiry) {
        this.userId = userId;
        this.sessionToken = token;
        this.tokenExpiry = expiry;
    }
    
    // Control manual de serialización para campos transient
    private void writeObject(ObjectOutputStream out) throws IOException {
        out.defaultWriteObject();
        out.writeLong(tokenExpiry);  // Serializamos manualmente
    }
    
    private void readObject(ObjectInputStream in) throws IOException, ClassNotFoundException {
        in.defaultReadObject();
        this.tokenExpiry = in.readLong();  // Deserializamos manualmente
        this.sessionToken = generateNewToken();  // Generamos nuevo token
    }
    
    private String generateNewToken() {
        return "TKN-" + System.currentTimeMillis();
    }
    
    @Override
    public String toString() {
        return "UserSession{userId='" + userId + "', token='" + sessionToken + "', expires=" + tokenExpiry + "}";
    }
}

// Uso
UserSession session = new UserSession("user123", "oldToken123", System.currentTimeMillis() + 3600000);

// Serialización
try (ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("session.dat"))) {
    out.writeObject(session);
}

// Deserialización
try (ObjectInputStream in = new ObjectInputStream(new FileInputStream("session.dat"))) {
    UserSession restored = (UserSession) in.readObject();
    System.out.println(restored);  // Muestra nuevo token generado
}
```

### `volatile`

Garantiza visibilidad entre hilos

```java
public class TaskRunner {
    private volatile boolean running = true;  // Visible inmediatamente para todos los hilos
    
    public void stop() {
        running = false;
    }
    
    public void run() {
        while (running) {
            // Ejecutar tarea
            System.out.println("Running...");
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
        }
        System.out.println("Stopped");
    }
}

// Uso en entorno multi-hilo
TaskRunner runner = new TaskRunner();
new Thread(runner::run).start();

// Después de 5 segundos, detener
new Thread(() -> {
    try {
        Thread.sleep(5000);
        runner.stop();
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
}).start();
```

## Combinación de Modificadores

Los modificadores pueden combinarse (con algunas restricciones):

```java
public class Example {
    // Constante pública accesible globalmente
    public static final int MAX_CONNECTIONS = 100;
    
    // Contador interno del paquete
    static int instanceCount = 0;
    
    // Campo protegido para subclases, no serializable
    protected transient String internalState;
    
    // Bloqueo para sincronización entre hilos
    private volatile Object lock = new Object();
    
    // Método que usa varios modificadores
    public static synchronized void incrementCount() {
        instanceCount++;
    }
}
```

## Reglas y Buenas Prácticas

1. **Principio de mínimo acceso**: Usa siempre el modificador de acceso más restrictivo posible (prefiere `private`).

2. **Campos `static final`** para constantes:
   ```java
   public static final double EARTH_GRAVITY = 9.807;
   ```

3. **`transient` para seguridad**: Marca como `transient` cualquier campo que contenga información sensible.

4. **`volatile` para flags**: Ideal para variables bandera en entornos multi-hilo.

5. **Inicialización de `final`**:
   - Debe inicializarse en la declaración o en todos los constructores
   ```java
   public class FinalExample {
       private final int value;
       
       public FinalExample(int v) {
           this.value = v;  // Inicialización obligatoria
       }
   }
   ```

6. **Serialización con `transient`**:
   - Considera implementar `Serializable` con `serialVersionUID`:
   ```java
   private static final long serialVersionUID = 1L;
   ```

## Ejemplo Completo Integrado

```java
import java.io.*;

public class ServerConfiguration implements Serializable {
    private static final long serialVersionUID = 1L;
    
    // Configuración básica (serializable)
    private final String serverName;
    private final int port;
    
    // Credenciales (no serializables)
    private transient String adminUsername;
    private transient String adminPassword;
    
    // Estado del servidor (no serializable, compartido entre hilos)
    private volatile boolean isRunning;
    
    // Contador de instancias (compartido)
    private static int instanceCount = 0;
    
    public ServerConfiguration(String name, int port, String user, String pass) {
        this.serverName = name;
        this.port = port;
        this.adminUsername = user;
        this.adminPassword = pass;
        this.isRunning = false;
        instanceCount++;
    }
    
    // Método para serialización personalizada
    private void writeObject(ObjectOutputStream out) throws IOException {
        out.defaultWriteObject();
        // No serializamos las credenciales, pero podríamos hacer hash
    }
    
    private void readObject(ObjectInputStream in) throws IOException, ClassNotFoundException {
        in.defaultReadObject();
        // Requerir nueva autenticación al deserializar
        this.adminUsername = null;
        this.adminPassword = null;
    }
    
    public void startServer() {
        isRunning = true;
        System.out.println(serverName + " started on port " + port);
    }
    
    public void stopServer() {
        isRunning = false;
        System.out.println(serverName + " stopped");
    }
    
    public static int getInstanceCount() {
        return instanceCount;
    }
    
    @Override
    public String toString() {
        return "ServerConfig{" +
               "name='" + serverName + '\'' +
               ", port=" + port +
               ", running=" + isRunning +
               ", instances=" + instanceCount +
               '}';
    }
}

// Uso
public class Main {
    public static void main(String[] args) {
        ServerConfiguration config = new ServerConfiguration("MyServer", 8080, "admin", "secret");
        
        // Serialización
        try (ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("server.config"))) {
            out.writeObject(config);
        } catch (IOException e) {
            e.printStackTrace();
        }
        
        // Deserialización
        try (ObjectInputStream in = new ObjectInputStream(new FileInputStream("server.config"))) {
            ServerConfiguration loaded = (ServerConfiguration) in.readObject();
            loaded.startServer();
            System.out.println(loaded);
            System.out.println("Total instances: " + ServerConfiguration.getInstanceCount());
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

Este ejemplo integrado muestra cómo usar todos los modificadores de campo en un contexto realista, con serialización, control de acceso, seguridad de hilos y gestión de estado.