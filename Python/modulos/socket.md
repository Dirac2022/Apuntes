
### socket
Un **socket** es un punto de comunicación entre dos máquinas o procesos. En redes, esto significa que un mecanismo que permite a una aplicación comunicarse con otro a través de una red utilizando protocolos como  [[Protocolos#TCP (Transmission Control Protocol)|TCP]] (orientado a conexión) o [[Protocolos#UDP (User Datagram Protocol)|UDP]] (no orientado a conexión).

Los sockets permiten enviar y recibir datos entre programas, ya sean en la misma máquina o a través de una red (como Internet o una LAN).

### Modelo cliente-servidor
El modelo **cliente-servidor** es la base del uso de sockets.
- El servidor espera conexiones en un puerto específico
- El cliente inicia una conexión al servidor.
- Una vez conectadas, ambos pueden intercambiar mensajes.

Este modelo puede utilizar TCP o UDP.

## Módulo `socket`

```python
import socket

s = socket.socket(family=socket.AF_INET, type=socket.SOCK_STREAM, proto=0)
```



| Parámetro | Descripción                                                                                                       |
| --------- | ----------------------------------------------------------------------------------------------------------------- |
| `family`  | Especifica la familia de direcciones: `AF_INET` (IPv4), `AF_INET6` (IPv6), `AF_UNIX` (solo en sistemas Unix).     |
| `type`    | Tipo de socket: `SOCK_STREAM` (TCP), `SOCK_DGRAM` (UDP).                                                          |
| `proto`   | Protocolo. Casi siempre se deja como `0`- Python infiere el valor correcto con base en `type`                     |
| `fileno`  | Usado internamente para crear un socket desde un descriptor de archivo existente., Casi nunca se usa directamente |


Los objetos y funciones principales del módulo `socket` incluyen

| Elemento                         | Descripción                                     |
| -------------------------------- | ----------------------------------------------- |
| `socket.socket()`                | Crea un nuevo objeto socket                     |
| `socket.AF_INET`                 | Familia de direcciones IPv4                     |
| `socket.AF_INET6`                | Familia de direcciones IPv6                     |
| `socket.SOCK_STREAM`             | Protocolo TCP                                   |
| `socket.SOCK_DGRAM`              | Protocolo UDP                                   |
| `socket.gethostbyname(hostname)` | Traduce un nombre de dominio a una dirección IP |
| `socket.gethostname()`           | Devuelve el nombre del host actual              |
| `socket.getaddrinfo()`           | Obtiene info de una dirección (DNS)             |


### Métodos clave del objeto `socket`

**En un servidor TCP**
- [[#`bind(address)`|bind((host, port))]] : Asocia el socket a una dirección IP y puerto.
- [[#`listen(backlog)`|listen([backlog])]]: Comienza a escuchar conexiones entrantes
- [[#`accept()`|accept()]]: Acepta una conexión entrante. Devuelve un nuevo socket y la dirección del cliente.
- [[#`recv(bufsize)`|recv(bufsize)]]:  Recibe datos del socket.
- [[#`send(data)`|send(data)]]: Envía datos. Tambien usar [[#`sendall(data)`|sendall(data)]]
- [[#`close()`|close()]]: Cierra el socket.

**En un cliente TCP**
- [[#`connect(address)`|connect((host, port))]]:  Conecta con un servidor. 
- `send(data)` / `recv(bufsize)`:  
- `close()`: 

**En UDP**
- [[#`sendto()`|sendto(data, address)]]: Envía datos a una dirección.
- [[#`recvfrom(bufsize)`|recvfrom(bufsize)]]: Recibe datos de una dirección.


## 📚 Métodos del objeto `socket.socket`

### `bind(address)`

Asocia el socket a una dirección IP y puerto local.

```python
s.bind(('127.0.0.1'), 8000)
```

### `listen(backlog)`

Empieza a escuchar conexiones entrantes (modo servidor).

```python
s.listen(5)
```

`backlog`: Número máximo de conexiones en espera.

**Nota**
- No acepta conexiones aún, solo indica que está listo para aceptar.
- Requiere haber hecho `bind()` antes.

### `accept()`

Espera una conexión y la acepta.

```python
conn, addr = s.accept()
```

- `conn`: Un nuevo objeto `socket` para comunicar con el cliente.
- `addr`: Una tupla `(IP, puerto)` del cliente.

**Nota**
- Es **bloqueante**: espera hasta que alguien se conecte.
- El socket original (`s`) sigue escuchando, el nuevo socket (`conn`) es el que se usa para la comunicación.



### `connect(address)`

Conecta el socket (cliente) con un servidor.

```python
s.connect(('localhost', 8000))
```

`address`: una tupla `(host, port)`

**Notas**
- Bloquea hasta que la conexión se haya establecido
- Si el servidor no está disponible lanza una excepción `ConnectionRefusedError`

### `send(data)`

Envía datos a través del socket

```python
s.send(b"mensaje")
```


| Parámetro | Tipo  | Descripción                                                      |
| --------- | ----- | ---------------------------------------------------------------- |
| `data`    | bytes | Los datos deben estar codificados. (Ejemplo, usando `.encode()`) |

**Notas**
Puede no enviar todos los bytes de una sola vez. Para asegurar envío completo, usar `sendall()`.


### `sendall(data)`

Asegura el envío completo de los datos. No retorna hasta haber enviado todo.

```python
s.sendall(b"mensaje completo")
```

### `recv(bufsize)`

Recibe datos del socket

```python
data = s.recv(1024)
```

`bufsize`: Tamaño máximo de bytes a recibir. Ejemplo `1024` o `4096`.

**Notas**
- Retorna un objeto `bytes`. Usualmente se decodifica con `.decode()`
- Si la conexión se cerró, devuelve `b''`.


### `close()`

Cierra el socket y libera los recursos del sistema.

```python
s.close()
```


### `settimeout(seconds)`

Establece un tiempo de espera en segundos para operaciones bloqueantes como `recv()` o `accept()`.

```python
s.settimeout(10.0)
```


### `recvfrom(bufsize)`

Usado en sockets UDP. Recibe datos + dirección del emisor

```python
data, addr = s.recvfrom(1024)
```


### `sendto()`

Usado en sockets UDP. Envía datos a una dirección sin establecer una conexión.

```python
s.sendto(b"respuesta", addr)
```



## 🧩Funciones del módulo `socket`


### `socket.gethostbyname(hostname)`

Convierte un nombre de dominio en una IP.

```python
ip = socket.gethostbyname('www.google.com')
```


### `socket.gethostname()`

Devuelve el nombre del equipo local.

```python
hostname = socket.gethostname()
```


### `socket.inet_aton(ip_string)` / `inet_ntoa(packed_ip)`
Convierte IPs a/desde forma binaria. Más bajo nivel, usado rara vez.

## Tipos de direcciones y familias

- `AF_INET`: IPv4 (por ejemplo, `("127.0.0.1", 8080)`)
- `AF_INET6`: IPv6
- `AF_UNIX`: Sockets locales en Unix


## Protocolos de transporte
- `SOCK_STREAM`: Protocolo TCP (conexión establecida, orientado a conexión)
- `SOCK_DGRAM`: Protocolo UDP (no requiere conexión previa, más rápido, sin garantía de entrega)
- Otros `SOCK_RAW`, `SOCK_RDM`, `SOCK_SEQPACKET`


## Ejemplos

### Chat Cliente-Servidor con TCP

**Servidor `servidor_tcp.py`**

```python
import socket

# Crear socket TCP
server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# Enlazarlo al host y puerto
server_socket.bind(('127.0.0.1', 65432))
server_socket.listen(1)  # Solo una conexión

print("Servidor esperando conexión...")

# Aceptar conexión
conn, addr = server_socket.accept()
print(f"Conectado con: {addr}")

# Comunicación
while True:
    data = conn.recv(1024)
    if not data:
        break
    print("Cliente:", data.decode())
    msg = input("Servidor >> ")
    conn.send(msg.encode())

conn.close()
server_socket.close()

```


**Cliente `cliente_tcp.py`**

```python
import socket

# Crear socket
client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# Conectar al servidor
client_socket.connect(('127.0.0.1', 65432))

print("Conectado al servidor.")

while True:
    msg = input("Cliente >> ")
    client_socket.send(msg.encode())
    data = client_socket.recv(1024)
    print("Servidor:", data.decode())

client_socket.close()
```


### Servidor UDP tipo "eco"

**Servidor `servidor_udp.py`**

```python
import socket

# Crear socket UDP
udp_server = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
udp_server.bind(("0.0.0.0", 12345))

print("Servidor UDP esperando mensajes...")

while True:
    data, addr = udp_server.recvfrom(1024)
    print(f"Mensaje de {addr}: {data.decode()}")
    udp_server.sendto(data, addr)  # Eco: envía lo mismo
```

**Cliente `cliente_udp.py`**

```python
import socket

udp_client = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

while True:
    msg = input("Cliente >> ")
    udp_client.sendto(msg.encode(), ("127.0.0.1", 12345))
    data, addr = udp_client.recvfrom(1024)
    print("Respuesta del servidor:", data.decode())
```