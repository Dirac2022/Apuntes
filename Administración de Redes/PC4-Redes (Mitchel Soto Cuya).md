# Pregunta 1. [7 puntos]

 Usted administra una red que experimenta congestión de tráfico en determinadas horas del día. Necesita implementar QoS en una interfaz específica para garantizar que el tráfico de voz tenga prioridad sobre el tráfico de datos. Utilizará Postman para enviar comandos RESTCONF con formato YANG XML al router y configurará las políticas QoS necesarias.

## Pasos: 1. Configurar las clases de tráfico

Obtuve la dirección IP del router en mi máquina DEVASC

![[Pasted image 20241130155001.png]]

En mi caso es **10.0.2.1**

-            Con esta información tengo el URL para configurar el POSTMAN

-            Creo una nueva solicitud **PUT** ya que deseamos configurar un recurso

![A screenshot of a computer
Description automatically generated](file:///C:/Users/mitch/AppData/Local/Temp/msohtmlclip1/01/clip_image004.png)


-            Agregué un encabezado (**Header**) de tipo **Content-Type** con el valor de **application/yang+json**

![A screenshot of a computer
Description automatically generated](file:///C:/Users/mitch/AppData/Local/Temp/msohtmlclip1/01/clip_image006.png)

Por último, inserté el código XML brindado

```xml
<config xmlns="urn:ietf:params:xml:ns:yang:ietf-qos">
  <qos>
    <policy-map name="voice-priority">
      <class-map match="ip-dscp" match-value="af41">
        <priority>10</priority>
      </class-map>
      <class-map match="ip-dscp" match-value="default">
        <priority>5</priority>
      </class-map>
      <policy-statement name="voice-priority-statement">
        <output>
          <police rate="64 kbps" burst-size="128 bytes">
            <conform-to priority="10"/>
            <exceed non-conform-to priority="5"/>
          </police>
        </output>
      </policy-statement>
    </policy-map>
  </qos>
</config>
```

![[Pasted image 20241130155424.png]]



# Pregunta 2. [5 puntos]

En una solución típica basada en YANG, el cliente y el servidor son impulsados por el contenido de los módulos YANG. El servidor incluye las definiciones de los módulos como metadatos que están disponibles para el motor NETCONF / RESTCONF. Este motor procesa las solicitudes entrantes, utiliza los metadatos para analizar y verificar la solicitud, realiza la operación solicitada y devuelve los resultados al cliente, como se muestra en la siguiente figura.

![[Pasted image 20241201121124.png]]

Los módulos YANG, que modelan un dominio de problema específico, se cargan, compilan o codifican en el servidor. 
**Explique la secuencia de eventos para la interacción típica cliente / servidor NETCONF.**
## Solución
Para explicar la secuencia de eventos primero especificaré los componentes involucrados:
- **Cliente (Aplicación)**: es la entidad que inicia la comunicación. Envía solicitudes al servidor usando el protocolo `NETCONF` encapsuladas en elementos `rpc` (Remote Procedure Call). Recibe respuestas del servidor encapsuladas en elementos `rpc-reply`.
- **Servidor (Device)**: es el dispositivo de red que se esta gestionando (router, switch, etc.). Tiene un motor NETCONF/RESTCONF que procesa las solicitudes recibidas. Almacena la configuración del dispositivo en una base de datos de configuración. Tiene componentes de software específicos que implementan las funcionalidades definidas en los módulos YANG.
- **Módulos YANG**: Son modelos de datos que describen la configuración y el estado del dispositivo de red. Definen una estructura jerárquica para representar los datos de configuración como interfaces, rutas, VLAN, etc. Son utilizados por el motor NETCONF/RESTCONF para validar solicitudes y generar respuestas.

La secuencia de eventos en una interacción típica **cliente/servidor** NETCONF es la siguiente:

1. **El cliente (aplicación) genera una solicitud**
	- El cliente, que puede ser una aplicación, genera una solicitud específica utilizando el protocolo `NETCONF` o `RESTCONF` (encapsulada en un elemento `rpc`). 
	- La solicitud se envía al servidor.
2. **El servidor recibe la solicitud**
	- El motor `NETCONF/RESTCONF` del servidor entra en acción. Este motor es el encargado de procesar las solicitudes y utilizar los metadatos para analizar y verificar su validez.
3. **El motor NETCONF/RESTCONF analiza la solicitud**
	- El motor utiliza los metadatos de los módulos YANG cargados en el servidor para analizar la solicitud.
	- Los metadatos contienen información sobre la estructura de los datos que el servidor puede gestionar, así como las operaciones permitidas.
	- El motor verifica que la solicitud sea sintácticamente correcta y que los datos especificados en la solicitud sean válidos según los modelos YANG.
4. **El motor ejecuta la operación solicitada**
	- Si la solicitud es válida, el motor precede a ejecutar la operación solicitada.
	- Esta operación puede implicar modificar la configuración del dispositivo, obtener información del estado actual o realizar alguna otra acción.
5. **El servidor envía una respuesta al cliente
	- Una vez que la operación se ha completado, el servidor genera una respuesta y la envía al cliente (encapsulada en un elemento `rpc-reply)`.
	- La respuesta indica si la operación se ha realizado correctamente o si ha habido algún error.
	- Si la operación ha sido exitosa, la respuesta puede incluir información sobre los cambios realizados o los datos solicitados.



# Pregunta 3. [8 puntos]
Desplegar 3 contenedores en Docker, similar al laboratorio de Microservicios desarrollado en clase, en este caso no será necesario desplegar el frontend de la app. El primer contenedor tendrá desplegada una API, al igual que el segundo contenedor, mientras que el tercer contenedor será una base de datos.

Cree 3 carpetas dentro de mi area de trabajo: **api1**, **api2** y **db**

En el mismo nivel de las carpetas esta  **docker-compose.yml**
```yml
version: '3.7'

services:
  api1:
    build:
      context: ./api1
      dockerfile: Dockerfile
    ports:
      - "5000:5000"
    depends_on:
      - api2
    environment:
      - API2_URL=http://api2:5001
    networks:
      - app_network

  api2:
    build:
      context: ./api2
      dockerfile: Dockerfile
    ports:
      - "5001:5001"
    depends_on:
      - db
    environment:
      - DB_HOST=db
      - DB_PORT=5432
      - DB_USER=mitchel
      - DB_PASSWORD=12345
      - DB_NAME=db_prueba_redes
    networks:
      - app_network

  db:
    build:
      context: ./db
      dockerfile: Dockerfile
    environment:
      POSTGRES_DB: db_prueba_redes
      POSTGRES_USER: mitchel
      POSTGRES_PASSWORD: 12345
    ports:
      - "5432:5432"
    volumes:
      - ./db/initdb.d:/docker-entrypoint-initdb.d
    networks:
      - app_network

networks:
  app_network:
    driver: bridge

```
## **En api1**
Se crearon los siguientes archivos
- app1.py
```python
import requests

def count_user(user):
    response = requests.post('http://api2:5001/count', json={'user': user})
    return response.json()['count']
```
- Dockerfile
```dockerfile
# Dockerfile_api2 (API 2)
FROM python:3.8-slim-buster

WORKDIR /app

COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt

COPY . .

CMD ["python", "app2.py"]

```


## **En api2**
- app2.py
```python
from flask import Flask, request, jsonify
import psycopg2

app = Flask(__name__)

conn = psycopg2.connect(
    database="db_prueba_redes",
    user="mitchel",
    password="12345",
    host="db"
)

```

- Dockerfile
```dockerfile
# Usa una imagen base de Debian slim
FROM debian:bookworm-slim

# Establece el directorio de trabajo en /app
WORKDIR /app

# Actualiza apt y agrega las dependencias necesarias
RUN apt-get update && apt-get install -y \
    gnupg \
    curl \
    build-essential \
    libpq-dev \
    python3 \
    python3-pip \
    python3-dev

# Copia el archivo requirements.txt al contenedor
COPY requirements.txt /app/

# Instala las dependencias de Python
RUN pip3 install --no-cache-dir -r requirements.txt

# Copia el código fuente al contenedor
COPY . /app/

# Exponemos el puerto que se utilizará en la aplicación
EXPOSE 5001

# Comando por defecto para ejecutar la aplicación
CMD ["python3", "app2.py"]

```



## En **db**
- Dockerfile
```dockerfile
# Usar una imagen base oficial de PostgreSQL
FROM postgres:14.15

# Copiar los scripts de inicialización de la base de datos
COPY initdb.d /docker-entrypoint-initdb.d

# Exponer el puerto de la base de datos
EXPOSE 5432
```
- init.sql
```sql
CREATE TABLE users (
    user_name TEXT PRIMARY KEY
);
```


**Para la ejecucion**

```bash
curl -X POST http://localhost:5000/start -H "Content-Type: application/json" -d '{"user": "Carlos"}'
```




