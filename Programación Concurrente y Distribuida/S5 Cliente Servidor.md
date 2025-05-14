
## 🧠 PARTE 1: El Modelo Cliente-Servidor

### 📘 Teoría

El modelo **Cliente-Servidor** es la arquitectura base de la mayoría de sistemas distribuidos. Implica dos roles:

- **Cliente**: solicita servicios.
- **Servidor**: proporciona servicios relacionados con recursos. 

La comunicación es iniciada por el cliente. Esto puede hacerse de diferentes formas:

- **Sockets** (nivel bajo)
    
- **RPC** (Remote Procedure Call, nivel medio)
    
- **RMI/CORBA** (nivel alto, orientado a objetos)
    

---

### 💡 Ejemplo real

- **Cliente**: navegador web
    
- **Servidor**: servidor web como Apache o Nginx
    
- El navegador solicita una página → el servidor devuelve el HTML.
    

---

### 🔧 Implementación con Sockets

#### 🟡 Python - Cliente y servidor básicos (TCP)

**Servidor (`tcp_server.py`)**:

```python
import socket

# Creamos el socket del servidor (IPv4, TCP)
server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# Enlazamos el socket a una IP y puerto
server_socket.bind(('localhost', 12345))

# Escuchamos conexiones entrantes
server_socket.listen()
print("Servidor escuchando en el puerto 12345...")

# Aceptamos una conexión
conn, addr = server_socket.accept()
print("Conectado por", addr)

# Recibimos datos (hasta 1024 bytes)
data = conn.recv(1024)
print("Mensaje recibido:", data.decode())

# Enviamos respuesta
conn.sendall("Hola, cliente!".encode())

# Cerramos conexión
conn.close()
```

**Cliente (`tcp_client.py`)**:

```python
import socket

# Creamos el socket cliente
client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# Nos conectamos al servidor
client_socket.connect(('localhost', 12345))

# Enviamos mensaje
client_socket.sendall("Hola, servidor!".encode())

# Recibimos respuesta
response = client_socket.recv(1024)
print("Respuesta del servidor:", response.decode())

# Cerramos
client_socket.close()
```

---

### 🔷 Java - Cliente y servidor básicos (TCP)

**Servidor (`ServidorTCP.java`)**:

```java
import java.net.*;
import java.io.*;

public class ServidorTCP {
    public static void main(String[] args) throws IOException {
        ServerSocket servidor = new ServerSocket(12345); // Crea el servidor
        System.out.println("Servidor esperando conexión...");

        Socket cliente = servidor.accept(); // Acepta la conexión
        System.out.println("Cliente conectado desde: " + cliente.getInetAddress());

        BufferedReader entrada = new BufferedReader(new InputStreamReader(cliente.getInputStream()));
        PrintWriter salida = new PrintWriter(cliente.getOutputStream(), true);

        String mensaje = entrada.readLine(); // Lee mensaje
        System.out.println("Cliente dice: " + mensaje);

        salida.println("Hola, cliente!"); // Responde

        cliente.close();
        servidor.close();
    }
}
```

**Cliente (`ClienteTCP.java`)**:

```java
import java.net.*;
import java.io.*;

public class ClienteTCP {
    public static void main(String[] args) throws IOException {
        Socket socket = new Socket("localhost", 12345); // Se conecta al servidor

        PrintWriter salida = new PrintWriter(socket.getOutputStream(), true);
        BufferedReader entrada = new BufferedReader(new InputStreamReader(socket.getInputStream()));

        salida.println("Hola, servidor!"); // Envía mensaje

        String respuesta = entrada.readLine(); // Recibe respuesta
        System.out.println("Servidor dice: " + respuesta);

        socket.close(); // Cierra conexión
    }
}
```

---

## 🧠 PARTE 2: RPC (Remote Procedure Call)

### 📘 Teoría

Un **RPC** permite a un programa invocar funciones que están en otra máquina, como si fueran locales.

**Ventaja clave**: oculta la complejidad de la red.

### 🔄 Stubs

- El **stub cliente** empaca los argumentos y envía la solicitud.
    
- El **stub servidor** desempaqueta, ejecuta y responde.
    

---

### 💡 Ejemplo real

- Sistemas de archivos distribuidos como **NFS** usan RPC para acceder a archivos en servidores remotos.
    

---

### 🔧 Implementación simple de "RPC" simulado con sockets (Python)

**Servidor RPC**:

```python
import socket
import json

def sumar(a, b):
    return a + b

server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server_socket.bind(('localhost', 5000))
server_socket.listen()

print("Servidor RPC esperando...")

conn, addr = server_socket.accept()
data = json.loads(conn.recv(1024).decode())

# Simula dispatching RPC
if data["funcion"] == "sumar":
    resultado = sumar(data["args"][0], data["args"][1])
    conn.sendall(json.dumps({"resultado": resultado}).encode())

conn.close()
```

**Cliente RPC**:

```python
import socket
import json

client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client_socket.connect(('localhost', 5000))

# Llamamos remotamente a la función "sumar"
mensaje = json.dumps({"funcion": "sumar", "args": [10, 15]})
client_socket.sendall(mensaje.encode())

respuesta = json.loads(client_socket.recv(1024).decode())
print("Resultado remoto:", respuesta["resultado"])

client_socket.close()
```

---

## 🧠 PARTE 3: RMI (Java) y CORBA (Multilenguaje)

### 📘 RMI - Java Remote Method Invocation

Permite invocar **métodos de objetos remotos**. Es una forma orientada a objetos de hacer RPC.

**Componentes**:

- `Remote`: interfaz remota
    
- `Stub` / `Skeleton`: manejan la comunicación
    
- `rmiregistry`: catálogo de servicios
    

---

### 💡 Ejemplo real

- Aplicaciones distribuidas Java que comparten lógica en red como sistemas bancarios o chat colaborativo.
    

---

### 🔧 Ejemplo sencillo en Java RMI

Te lo preparo en detalle si quieres que avancemos con RMI o CORBA. Ambos necesitan múltiples archivos y configuración (RMI registry, IDL en CORBA, etc.).

---

¿Te gustaría que siga con la parte de **RMI (Java)** o **CORBA** (con IDL)? ¿O prefieres más ejemplos con RPC, cliente-servidor o sockets multicliente/multihilo? Puedo profundizar en cualquier dirección.