

## ✅ Introducción

### ¿Qué es `requests`?

`requests` es una **biblioteca HTTP** en Python diseñada para que puedas enviar **solicitudes HTTP/1.1** de forma **sencilla, legible y humana**.

> "Requests es HTTP para humanos" – eslogan oficial del módulo.

Es ampliamente usada en:

- Consumo de APIs REST.
    
- Web scraping.
    
- Automatización de interacciones con servicios web.
    
- Testing de endpoints HTTP.
    

### Instalación

```bash
pip install requests
```

---

## 🧠 Fundamentos del protocolo HTTP

Antes de usar `requests`, es vital entender qué es HTTP:

- HTTP (HyperText Transfer Protocol) es un protocolo de **cliente-servidor**.
    
- Los **clientes** envían solicitudes al **servidor**, que responde con datos.
    

### Métodos HTTP más comunes

|Método|Descripción|
|---|---|
|GET|Solicita datos del servidor (lectura)|
|POST|Envía datos al servidor (crear)|
|PUT|Actualiza datos existentes|
|DELETE|Elimina recursos|
|PATCH|Actualiza parcialmente un recurso|
|HEAD|Igual que GET, pero sin el cuerpo de respuesta|

---

## 🔧 Primeros pasos con `requests`

Importamos el módulo:

```python
import requests
```

---

## 📘 Ejemplo 1: Solicitud GET simple

```python
import requests  # Importamos el módulo requests

# Enviamos una solicitud HTTP GET al servidor (en este caso, httpbin.org)
response = requests.get("https://httpbin.org/get")

# Imprimimos el código de estado de la respuesta HTTP (200 = OK)
print("Código de estado:", response.status_code)

# Imprimimos el cuerpo (contenido) de la respuesta
print("Cuerpo de respuesta:", response.text)
```

### 🔍 ¿Qué pasó aquí?

- `requests.get(url)`: envía una solicitud `GET`.
    
- `response`: es un objeto de tipo `Response` que contiene toda la información devuelta por el servidor.
    
- `response.text`: devuelve el contenido del cuerpo de la respuesta como cadena (texto plano).
    
- `response.status_code`: nos da el código de estado HTTP (por ejemplo, 200, 404, etc).
    

---

## 📘 Ejemplo 2: GET con parámetros (query strings)

```python
import requests

# Definimos los parámetros que queremos pasar a la URL (como en ?nombre=Ana&edad=30)
params = {
    "nombre": "Ana",
    "edad": 30
}

# Enviamos la solicitud GET con los parámetros
response = requests.get("https://httpbin.org/get", params=params)

# Mostramos la URL generada con los parámetros incluidos
print("URL generada:", response.url)

# Mostramos la respuesta
print("Respuesta JSON:", response.json())  # La respuesta ya es un diccionario
```

### ℹ️ `.json()`

- Si el servidor devuelve una respuesta en formato JSON (como hacen las APIs), puedes usar `response.json()` para convertirlo directamente a un diccionario de Python.
    

---

## 📘 Ejemplo 3: POST con datos (formulario)

```python
import requests

# Definimos los datos que vamos a enviar al servidor
data = {
    "usuario": "mitchel",
    "clave": "12345"
}

# Enviamos una solicitud POST
response = requests.post("https://httpbin.org/post", data=data)

# Mostramos el cuerpo de la respuesta en JSON
print("Respuesta JSON:", response.json())
```

### 📌 Diferencias:

- `GET`: envía los datos en la **URL**.
    
- `POST`: los envía en el **cuerpo** de la solicitud (más seguro).
    

---

## 📘 Ejemplo 4: Enviar encabezados personalizados (headers)

```python
import requests

# Definimos encabezados HTTP personalizados
headers = {
    "User-Agent": "MiAplicacionPython/1.0",
    "Authorization": "Bearer 123abc456"
}

response = requests.get("https://httpbin.org/headers", headers=headers)

print("Encabezados recibidos:", response.json())
```

---

## 📘 Ejemplo 5: Enviar datos JSON

```python
import requests

# Diccionario con los datos que queremos enviar como JSON
json_data = {
    "producto": "laptop",
    "precio": 1200
}

# Enviamos una solicitud POST con JSON
response = requests.post("https://httpbin.org/post", json=json_data)

# Mostramos el JSON recibido por el servidor
print("Datos enviados (JSON):", response.json())
```

> ✅ El parámetro `json=...` convierte el diccionario automáticamente en JSON y establece el header `Content-Type: application/json`.

---

## 📘 Ejemplo 6: Manejo de errores (status codes)

```python
import requests

response = requests.get("https://httpbin.org/status/404")  # Forzamos error 404

if response.status_code == 200:
    print("Todo bien.")
elif response.status_code == 404:
    print("Recurso no encontrado.")
else:
    print("Algo salió mal. Código:", response.status_code)
```

---

## 📘 Ejemplo 7: Subir archivos

```python
import requests

# Abrimos un archivo en modo binario
with open("archivo.txt", "rb") as f:
    archivos = {"archivo": f}
    response = requests.post("https://httpbin.org/post", files=archivos)

print("Respuesta del servidor:", response.json())
```

---

## 📘 Ejemplo 8: Autenticación básica

```python
import requests
from requests.auth import HTTPBasicAuth

# Enviamos usuario y contraseña en la cabecera de la solicitud
response = requests.get("https://httpbin.org/basic-auth/usuario/clave",
                        auth=HTTPBasicAuth("usuario", "clave"))

print("Código de estado:", response.status_code)
print("Respuesta:", response.json())
```

---

## 📘 Ejemplo 9: Manejo de cookies

```python
import requests

# Primera solicitud: el servidor nos envía cookies
response = requests.get("https://httpbin.org/cookies/set/curso/python")

# Ahora obtenemos esas cookies
response2 = requests.get("https://httpbin.org/cookies", cookies=response.cookies)

print("Cookies almacenadas:", response2.json())
```

---

## 📘 Ejemplo 10: Redirecciones

```python
import requests

response = requests.get("https://httpbin.org/redirect/1")  # Redirige una vez

print("URL final:", response.url)
print("Historial de redirecciones:", response.history)
```

---

## ⚠️ Timeouts y excepciones

```python
import requests

try:
    # Si el servidor no responde en 2 segundos, lanza Timeout
    response = requests.get("https://httpbin.org/delay/3", timeout=2)
    print("Respuesta:", response.text)
except requests.Timeout:
    print("¡Tiempo de espera excedido!")
except requests.RequestException as e:
    print("Error general de solicitud:", e)
```

---

## 📦 Otras funciones útiles de `Response`

```python
response = requests.get("https://httpbin.org/get")

print("Código de estado:", response.status_code)
print("Encabezados:", response.headers)
print("Tipo de contenido:", response.headers.get("Content-Type"))
print("Texto:", response.text)
print("Contenido en bytes:", response.content)
print("JSON:", response.json())
```

---

## 🎯 Sesiones: mantener conexiones

```python
import requests

# Creamos una sesión para mantener cookies, headers, etc.
session = requests.Session()

# Definimos headers comunes para todas las solicitudes
session.headers.update({"User-Agent": "MiAppPython/2.0"})

# Primera solicitud (guarda cookies)
session.get("https://httpbin.org/cookies/set/idioma/es")

# Segunda solicitud (reutiliza cookies automáticamente)
response = session.get("https://httpbin.org/cookies")

print("Cookies mantenidas:", response.json())
```

---

## 🧪 Testing de APIs reales (opcional)

Puedes probar `requests` con cualquier API pública como:

- [https://jsonplaceholder.typicode.com](https://jsonplaceholder.typicode.com/)
    
- [https://pokeapi.co](https://pokeapi.co/)
    
- [https://api.github.com](https://api.github.com/)
    

Ejemplo:

```python
response = requests.get("https://api.github.com/users/octocat")
print(response.json()["bio"])
```

---

## 🧠 Resumen

|Tema|Descripción|
|---|---|
|`get`, `post`, `put`, `delete`|Métodos HTTP|
|`params`, `data`, `json`|Enviar datos|
|`headers`, `cookies`, `auth`|Encabezados, cookies, autenticación|
|`status_code`, `text`, `json()`|Leer respuesta|
|`Session()`|Mantener conexión|
|`Timeout`, `exceptions`|Control de errores|

---

## 🏁 Conclusión

El módulo `requests` es una herramienta poderosa, simple y versátil para trabajar con HTTP en Python. Es **imprescindible** para cualquier desarrollador backend, analista de datos o entusiasta de la automatización de tareas web.

¿Te gustaría que preparemos un mini-proyecto práctico usando `requests`, como un **cliente para una API REST pública** o un **web scraper simple**?