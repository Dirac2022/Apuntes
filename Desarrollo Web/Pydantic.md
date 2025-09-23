

Pydantic es una librería que utiliza las anotaciones de tipo de Python (`type hints`) para validar, serializar y deserializar datos. En esencia, te permite definir "schemas" de datos en clases de Python. Si los datos que recibe tu programa no cumplen con la estructura y los tipos definidos, Pydantic lanza errores claros y detallados. Esto reduce drásticamente el código repetitivo de validación y previene una gran cantidad de bugs.

Sus principales bondades son:

- **Menos código**: Define la forma de tus datos una vez y Pydantic se encarga de la validación.
    
- **Errores claros**: Cuando la validación falla, los errores te dicen exactamente qué campo falló y por qué.
    
- **Integración moderna**: Es la base de frameworks como FastAPI y es ampliamente usado para la gestión de configuraciones.
    
- **Rendimiento**: Es extremadamente rápido, ya que está construido sobre Rust.
    

---

## Instalación

Pydantic no viene con Python, por lo que debes instalarlo. La mejor práctica es hacerlo dentro de un entorno virtual.

Bash

```sh
# Instala la librería principal
pip install pydantic

# Instala el soporte para correos, URLs y otros tipos estrictos
pip install pydantic[email]

# Instala el soporte para la gestión de configuraciones (variables de entorno)
pip install pydantic-settings
```

---

## El Corazón de Pydantic: `BaseModel`

Para definir un schema de datos, creas una clase que hereda de `pydantic.BaseModel`. Los atributos de la clase, junto con sus `type hints`, se convierten en los campos del modelo.

**Ejemplo 1: Modelo Básico y Validación Automática**
Imagina que recibes datos de un nuevo usuario. Quieres asegurar que el `id` sea un número, el `nombre` un texto, y la fecha de registro sea válida.


```python
# Importamos las clases necesarias
from pydantic import BaseModel, ValidationError
from datetime import datetime

# Definimos nuestro modelo 'User'. Hereda de BaseModel.
# Cada atributo tiene un 'type hint' (anotación de tipo) que Pydantic usará para validar.
class User(BaseModel):
    id: int               # El ID debe ser un entero.
    name: str = 'John Doe'# El nombre debe ser un string. Tiene un valor por defecto.
    signup_ts: datetime | None # La fecha de registro puede ser un datetime o None.
    friends: list[int]    # 'friends' debe ser una lista de enteros.

# --- CASO 1: Datos correctos ---
# Creamos datos externos, como si vinieran de una petición JSON.
external_data = {
    'id': 123,
    'signup_ts': '2022-12-22 12:00', # Pydantic convierte automáticamente el string a datetime.
    'friends': [1, '2', 3]          # Pydantic convierte '2' (string) a 2 (int).
}

# Creamos una instancia del modelo User a partir de los datos.
# Pydantic valida y convierte los tipos automáticamente.
user = User(**external_data)

print(user)
# Salida esperada: id=123 name='John Doe' signup_ts=datetime.datetime(2022, 12, 22, 12, 0) friends=[1, 2, 3]

print(user.id) # Puedes acceder a los atributos como en una clase normal.
# Salida esperada: 123

# --- CASO 2: Datos incorrectos ---
# Ahora probamos con datos que no cumplen con el schema.
invalid_data = {
    'id': 'esto no es un numero',
    'signup_ts': 'fecha invalida',
    'friends': [1, 2, 'amigo']
}

try:
    # Intentamos crear la instancia. Esto fallará.
    User(**invalid_data)
except ValidationError as e:
    # Pydantic lanza una excepción 'ValidationError' con información muy detallada.
    print("\n--- ERRORES DE VALIDACIÓN DETECTADOS ---")
    print(e.json())
```

**Salida del `ValidationError`**:

JSON

```json
[
  {
    "type": "int_parsing",
    "loc": ["id"],
    "msg": "Input should be a valid integer, unable to parse string as an integer",
    "input": "esto no es un numero"
  },
  {
    "type": "datetime_parsing",
    "loc": ["signup_ts"],
    "msg": "Input should be a valid datetime, invalid character in year",
    "input": "fecha invalida"
  },
  {
    "type": "int_parsing",
    "loc": ["friends", 2],
    "msg": "Input should be a valid integer, unable to parse string as an integer",
    "input": "amigo"
  }
]
```

Como puedes ver, los errores son increíblemente específicos, indicando el campo (`loc`), el tipo de error (`type`) y el valor que falló (`input`).

---

## Campos Avanzados con `Field` y Tipos Especiales

Para validaciones más complejas (límites numéricos, longitud de strings, etc.) o para configurar alias (cuando el nombre en el JSON es diferente al de tu modelo), usamos la función `Field`.

**Ejemplo 2: Modelo de Producto con Validaciones y Alias**

Supongamos que un sistema externo te envía datos de productos donde el campo para el precio se llama `"item-price"`. Además, quieres asegurar que el precio sea siempre positivo y el nombre tenga una longitud máxima.


```python
from pydantic import BaseModel, Field, HttpUrl
from typing import Annotated # Necesario para usar Field en versiones más recientes

# Definimos un modelo de producto con validaciones más estrictas.
class Product(BaseModel):
    # Usamos Annotated para combinar el tipo con la configuración de Field.
    # gt=0 significa 'greater than 0' (mayor que 0).
    # alias='item-price' mapea el campo JSON 'item-price' a nuestro atributo 'price'.
    price: Annotated[float, Field(gt=0, description="Precio del producto, debe ser positivo.")]

    # min_length y max_length definen la longitud permitida para el string.
    name: Annotated[str, Field(min_length=3, max_length=50, description="Nombre del producto.")]
    
    # Pydantic tiene tipos especiales. HttpUrl valida que el string sea una URL válida.
    image_url: HttpUrl | None = None # Este campo es opcional.

# Datos de entrada que usan el alias 'item-price'.
product_data = {
    'item-price': 29.99,
    'name': 'Teclado Mecánico RGB',
    'image_url': 'https://example.com/images/keyboard.jpg'
}

# Creamos la instancia. Pydantic usa el alias para encontrar el precio.
product = Product(**product_data)

print(product)
# Salida: price=29.99 name='Teclado Mecánico RGB' image_url=Url('https://example.com/images/keyboard.jpg')

# Exportar el modelo a un diccionario usando el alias.
print(product.model_dump(by_alias=True))
# Salida: {'item-price': 29.99, 'name': 'Teclado Mecánico RGB', 'image_url': 'https://example.com/images/keyboard.jpg'}
```

---

## Modelos Anidados

La verdadera potencia de Pydantic brilla cuando trabajas con estructuras JSON complejas. Puedes anidar modelos dentro de otros.

**Ejemplo 3: Modelo de un Pedido con Varios Productos**

Un pedido contiene información del comprador y una lista de productos. Podemos modelar esto componiendo los modelos que ya tenemos.


```python
from pydantic import BaseModel
from typing import List

# (Asumiendo que las clases User y Product de los ejemplos anteriores están definidas aquí)

class Order(BaseModel):
    order_id: int
    customer: User  # ¡Anidamos el modelo User! Pydantic espera un dict con la estructura de User.
    items: List[Product] # Una lista donde cada elemento debe cumplir con el modelo Product.

# Datos complejos que representan un pedido completo.
order_data = {
    "order_id": 9876,
    "customer": { # Este diccionario se validará contra el modelo User.
        "id": 123,
        "signup_ts": "2022-12-22 12:00",
        "friends": [1, 2, 3]
    },
    "items": [ # Esta lista de diccionarios se validará contra el modelo Product.
        {"item-price": 29.99, "name": "Teclado Mecánico RGB"},
        {"item-price": 15.50, "name": "Mouse Gamer"}
    ]
}

# Creamos la instancia del pedido.
# Pydantic recursivamente valida y crea instancias de User y Product.
order = Order(**order_data)

print(order)
# Puedes ver que 'customer' es ahora una instancia de User y 'items' una lista de Products.

# Acceder a datos anidados es intuitivo y seguro.
print(f"Cliente del pedido: {order.customer.name}") # Salida: Cliente del pedido: John Doe
print(f"Nombre del primer producto: {order.items[0].name}") # Salida: Nombre del primer producto: Teclado Mecánico RGB
```

---

## Gestión de Configuración con `BaseSettings`

Otra gran utilidad es gestionar la configuración de tu aplicación (claves de API, conexiones a bases de datos, etc.) leyéndolas desde variables de entorno.

**Ejemplo 4: Configuración de una Base de Datos**

En lugar de escribir las credenciales en el código, las leemos del entorno del sistema. Esto es más seguro y flexible.



```python
# Necesitas `pydantic-settings` instalado: pip install pydantic-settings
from pydantic_settings import BaseSettings, SettingsConfigDict

class DatabaseSettings(BaseSettings):
    # Pydantic buscará automáticamente variables de entorno con estos nombres (insensible a mayúsculas).
    # Por ejemplo, para 'db_host', buscará una variable de entorno llamada DB_HOST.
    db_host: str
    db_port: int = 5432 # Valor por defecto si no se encuentra la variable.
    db_user: str
    db_password: str
    
    # Configuración para leer desde un archivo .env si existe.
    model_config = SettingsConfigDict(env_file='.env', env_file_encoding='utf-8')

# Para probar esto, crea un archivo llamado '.env' en el mismo directorio con este contenido:
# DB_HOST=localhost
# DB_USER=myuser
# DB_PASSWORD=supersecret

# Ahora, simplemente instancia la clase. No necesitas pasarle datos.
# Pydantic hace el trabajo de leer las variables de entorno o el archivo .env.
settings = DatabaseSettings()

print("Configuración de la Base de Datos:")
print(f"Host: {settings.db_host}")
print(f"Usuario: {settings.db_user}")

# La contraseña se lee pero por seguridad no la imprimimos directamente.
# print(settings.model_dump_json(indent=2)) # Muestra toda la config en formato JSON
```

Este enfoque te permite tener diferentes configuraciones para desarrollo, pruebas y producción simplemente cambiando las variables de entorno o el archivo `.env`.

---

## Serialización: Convertir Modelos a JSON/Dict

Una vez que tienes tus datos validados en un objeto Pydantic, es muy fácil convertirlos de vuelta a un diccionario o a un string JSON, por ejemplo, para enviarlos como respuesta en una API.

**Ejemplo 5: Exportando un Modelo**

Usaremos el modelo anidado `Order` del ejemplo 3.


```python
# (Asumiendo que la variable 'order' del ejemplo 3 existe)

# Convertir la instancia del modelo a un diccionario de Python.
order_dict = order.model_dump()
print("\n--- MODELO A DICCIONARIO ---")
print(order_dict)

# Convertir la instancia del modelo directamente a un string JSON.
# 'indent=2' formatea el JSON para que sea legible.
order_json = order.model_dump_json(indent=2)
print("\n--- MODELO A JSON ---")
print(order_json)
```

**Salida JSON:**

JSON

```json
{
  "order_id": 9876,
  "customer": {
    "id": 123,
    "name": "John Doe",
    "signup_ts": "2022-12-22T12:00:00",
    "friends": [
      1,
      2,
      3
    ]
  },
  "items": [
    {
      "price": 29.99,
      "name": "Teclado Mecánico RGB",
      "image_url": null
    },
    {
      "price": 15.5,
      "name": "Mouse Gamer",
      "image_url": null
    }
  ]
}
```