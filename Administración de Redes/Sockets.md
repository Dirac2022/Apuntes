

# WebSockets
WebSockets es un protocolo de comunicación que permite la transmisión de datos bidireccional y en tiempo real entre un cliente (generalmente un navegador web) y un servidor. A diferencia del protocolo HTTP, que requiere que el cliente inicie la comunicación cada vez, WebSockets establece una conexión persistente que se mantiene abierta, permitiendo la comunicación continua y eficiente.

### Características principales de WebSockets:

| Característica             | Descripción                                                                                   |
|----------------------------|-----------------------------------------------------------------------------------------------|
| Comunicación bidireccional | Permite el envío y recepción de mensajes entre cliente y servidor sin necesidad de nuevas solicitudes. |
| Baja latencia              | Ideal para aplicaciones en tiempo real como chats, juegos online y sistemas de notificaciones. |
| Conexión persistente       | La conexión permanece abierta, evitando la sobrecarga de establecer nuevas conexiones.        |
| Basado en TCP              | Funciona sobre el protocolo TCP, garantizando una transmisión de datos confiable.             |
| Reducción de tráfico       | No hay intercambio constante de encabezados HTTP, lo que reduce el uso de ancho de banda.     |

### ¿Cómo funcionan los WebSockets?

1. **Handshake inicial**: La comunicación comienza con una solicitud HTTP del cliente al servidor, que luego se "actualiza" para establecer la conexión WebSocket.
2. **Conexión abierta**: Una vez que se completa el handshake, la conexión permanece abierta, permitiendo la transmisión de datos en ambos sentidos.
3. **Transmisión de datos**: Cliente y servidor pueden enviar mensajes sin restricciones y de manera independiente.
4. **Cierre de conexión**: Cuando ya no se necesita la comunicación, cualquiera de las partes puede cerrar la conexión.

### Ejemplo de uso

- **Chats en tiempo real**: Los mensajes enviados por un usuario se transmiten instantáneamente a otros usuarios sin recargar la página.
- **Aplicaciones de trading**: Permite actualizar los precios de acciones y otros activos de forma continua.
- **Juegos multijugador en línea**: Facilita la interacción en tiempo real entre jugadores.

WebSockets son una herramienta poderosa para cualquier aplicación que requiera actualizaciones rápidas y comunicación interactiva entre cliente y servidor.

# ayncio y aiohttp
`asyncio` y `aiohttp` son herramientas en Python que facilitan la programación asincrónica, permitiendo la ejecución concurrente de tareas para mejorar la eficiencia y el rendimiento de aplicaciones que requieren múltiples operaciones de entrada/salida (E/S), como servidores web y clientes que manejan grandes volúmenes de peticiones.

### `asyncio`

`asyncio` es una biblioteca estándar de Python que permite la programación asincrónica mediante la definición de corutinas, que son funciones especiales que pueden pausarse y reanudarse, permitiendo que otras tareas se ejecuten mientras esperan.

#### Características principales de `asyncio`:

| Característica                | Descripción                                                                                     |
|-------------------------------|-------------------------------------------------------------------------------------------------|
| Ejecución de corutinas        | Permite definir y ejecutar corutinas, funciones con la palabra clave `async def`.              |
| Bucle de eventos              | Gestiona y coordina la ejecución de corutinas y tareas asincrónicas.                           |
| Tareas y futuros              | Permite crear tareas (`asyncio.create_task()`) y manejar futuros que representan resultados pendientes. |
| Manejo de E/S asincrónica     | Ideal para operaciones de E/S como acceso a bases de datos, llamadas a API, etc.               |

#### Ejemplo de uso de `asyncio`:
```python
import asyncio

async def saludar():
    print("Hola")
    await asyncio.sleep(1)
    print("Adiós")

asyncio.run(saludar())
```

### `aiohttp`

`aiohttp` es una biblioteca basada en `asyncio` que se usa para realizar peticiones HTTP de manera asincrónica y para construir servidores web. Permite manejar tanto el cliente HTTP como el servidor con un enfoque asincrónico.

#### Características principales de `aiohttp`:

| Característica             | Descripción                                                                                     |
|----------------------------|-------------------------------------------------------------------------------------------------|
| Cliente HTTP asincrónico   | Permite realizar solicitudes HTTP (`GET`, `POST`, etc.) de manera asincrónica.                 |
| Servidor web asincrónico   | Facilita la creación de servidores web que manejan múltiples solicitudes concurrentemente.      |
| Manejo de sesiones         | Soporte para sesiones persistentes mediante `ClientSession`.                                   |
| Streaming de datos         | Permite la transmisión de grandes cantidades de datos de forma eficiente.                      |

#### Ejemplo de uso de `aiohttp` (cliente):
```python
import aiohttp
import asyncio

async def fetch(url):
    async with aiohttp.ClientSession() as session:
        async with session.get(url) as response:
            print(await response.text())

asyncio.run(fetch('https://www.example.com'))
```

#### Ejemplo de uso de `aiohttp` (servidor):
```python
from aiohttp import web

async def handle(request):
    return web.Response(text="Hola, mundo")

app = web.Application()
app.add_routes([web.get('/', handle)])

web.run_app(app, port=8080)
```

### Comparación entre `asyncio` y `aiohttp`:

| Aspecto                      | `asyncio`                                 | `aiohttp`                                              |
|------------------------------|-------------------------------------------|--------------------------------------------------------|
| Propósito                    | Biblioteca estándar para programación asincrónica general. | Librería para cliente/servidor HTTP asincrónico basada en `asyncio`. |
| Enfoque                      | Ejecutar corutinas y manejar tareas asincrónicas.         | Manejar solicitudes y respuestas HTTP de forma eficiente. |
| Nivel de abstracción         | Más bajo, requiere implementación de más detalles.       | Más alto, enfocado en peticiones HTTP y servidores web.  |

`asyncio` es ideal para manejar la lógica asincrónica de Python en general, mientras que `aiohttp` se especializa en la gestión de solicitudes y respuestas HTTP, tanto para clientes como para servidores. 


