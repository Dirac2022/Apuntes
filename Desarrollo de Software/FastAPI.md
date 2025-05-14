# 📦 `fastapi`

**¿Qué es?**  
FastAPI es un framework para construir APIs web modernas, rápidas y eficientes con Python. Está basado en **Starlette** para la parte web y en **Pydantic** para validación de datos.

**¿Por qué es popular?**

- Es **muy rápido** (casi tan rápido como Node.js o Go).
- Usa **async/await**, lo que permite manejar muchas peticiones al mismo tiempo sin bloquear el servidor.
- Tiene **documentación automática** (Swagger y ReDoc) apenas levantas el servidor.

🔧 Ejemplo:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
async def read_root():
    return {"Hello": "World"}
```



# TestClient

Es una utilidad proporcionada por FastAPI para facilitar la escritura de pruebas de integración para tu API. Te permite simular peticiones HTTP (GET, POST, PUT, DELETE, etc.) a tus endpoints sin necesidad de levantar un servidor HTTP real. Recibe una instancia de tu aplicación FastAPI (`app`) y te permite interactuar con ella como si fuera un cliente HTTP real, pero de forma más rápida y controlada dentro de tus pruebas.