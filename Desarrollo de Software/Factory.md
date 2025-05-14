
---

## 🧠 Teoría del Patrón de Diseño _Factory_

### ¿Qué es el patrón Factory?

El **Factory Pattern** es un patrón de diseño creacional que proporciona una interfaz para crear objetos en una superclase, pero permite a las subclases alterar el tipo de objetos que se crearán.

#### 🎯 Objetivo:

Evitar acoplamiento fuerte y permitir que el código que utiliza los objetos no sepa cómo se crean exactamente.

### Ejemplo conceptual (sin `factory_boy`):

```python
class Animal:
    def speak(self):
        raise NotImplementedError

class Dog(Animal):
    def speak(self):
        return "Woof!"

class Cat(Animal):
    def speak(self):
        return "Meow!"

def animal_factory(type_):
    if type_ == "dog":
        return Dog()
    elif type_ == "cat":
        return Cat()
    else:
        raise ValueError("Unknown animal type")

a = animal_factory("dog")
print(a.speak())  # Woof!
```

---

## 🧰 Introducción a `factory_boy`

`factory_boy` es una biblioteca que **automatiza la creación de objetos para pruebas** (test fixtures), especialmente útil cuando se trabaja con modelos complejos.

### ¿Por qué usarlo?

- Facilita la creación de datos realistas y válidos.
- Evita duplicación de código en pruebas.
- Se integra con ORM como SQLAlchemy, Django ORM, etc.
- Permite usar `Faker` para datos aleatorios.

---

## 🧱 Instalación

```bash
pip install factory_boy
```

---

## 🔧 Sintaxis y Componentes Básicos

### Estructura básica:

```python
import factory

class User:
    def __init__(self, name, email):
        self.name = name
        self.email = email

class UserFactory(factory.Factory):
    class Meta:
        model = User

    name = "John Doe"
    email = "john@example.com"

# Crear una instancia
user = UserFactory()
print(user.name)  # John Doe
```

---

## 🔍 Explorando `factory.Factory` y Faker

### Métodos importantes

|Método|Descripción|
|---|---|
|`build()`|Crea un objeto sin guardarlo (usado para objetos no persistentes).|
|`create()`|Crea un objeto y lo guarda (si el modelo lo permite, como en Django ORM).|
|`build_batch(n)`|Crea una lista de `n` objetos.|
|`create_batch(n)`|Igual que `build_batch` pero persistente.|

### Usando `Faker` (integrado con `factory_boy`):

```python
import factory
from factory import Faker

class UserFactory(factory.Factory):
    class Meta:
        model = User

    name = Faker('name')
    email = Faker('email')

u = UserFactory()
print(u.name, u.email)
```

📌 Faker utiliza datos aleatorios pero realistas como nombres, correos, direcciones, etc.

---

## 🧬 Campos Especiales en `factory_boy`

### `SubFactory`

Permite anidar fábricas. Ejemplo:

```python
class Profile:
    def __init__(self, user, bio):
        self.user = user
        self.bio = bio

class ProfileFactory(factory.Factory):
    class Meta:
        model = Profile

    user = factory.SubFactory(UserFactory)
    bio = Faker('sentence')
```

### `LazyAttribute`

Permite construir campos en función de otros:

```python
class UserFactory(factory.Factory):
    class Meta:
        model = User

    name = Faker('name')
    email = factory.LazyAttribute(lambda obj: f"{obj.name.replace(' ', '').lower()}@example.com")
```

### `Sequence`

Para generar valores únicos:

```python
class UserFactory(factory.Factory):
    class Meta:
        model = User

    id = factory.Sequence(lambda n: n + 1)
    name = Faker('name')
```

---

## 🏗️ Integración con Frameworks (Django y SQLAlchemy)

### Django (ejemplo):

```python
import factory
from myapp.models import User

class UserFactory(factory.django.DjangoModelFactory):
    class Meta:
        model = User

    username = Faker('user_name')
    email = Faker('email')
```

Con esto, `UserFactory.create()` guarda en la base de datos usando el ORM de Django.

---

## 🧪 Ejemplo completo con SubFactory y Faker

```python
class Address:
    def __init__(self, city, zipcode):
        self.city = city
        self.zipcode = zipcode

class Person:
    def __init__(self, name, address):
        self.name = name
        self.address = address

class AddressFactory(factory.Factory):
    class Meta:
        model = Address

    city = Faker('city')
    zipcode = Faker('postcode')

class PersonFactory(factory.Factory):
    class Meta:
        model = Person

    name = Faker('name')
    address = factory.SubFactory(AddressFactory)

person = PersonFactory()
print(person.name, person.address.city, person.address.zipcode)
```

---

## 🧰 Explorando Faker: Datos Disponibles

Algunos campos útiles:

- `name`, `first_name`, `last_name`
- `email`, `url`, `user_name`
- `address`, `city`, `postcode`, `country`
- `phone_number`
- `date`, `date_of_birth`, `time`
- `company`, `job`, `text`, `sentence`

Para ver todos los disponibles:  
📚 [https://faker.readthedocs.io/en/master/providers.html](https://faker.readthedocs.io/en/master/providers.html)

---

## 📘 Buenas prácticas

- Usa `SubFactory` para evitar dependencias manuales.
- Usa `LazyAttribute` para relaciones lógicas entre campos.
- No generes datos aleatorios directamente en los tests; centraliza en las fábricas.
- Usa `create_batch` para testear listas.
- Usa `Faker.seed(0)` para datos reproducibles.
    

---

## 🧾 Resumen Visual

```plaintext
FACTORY BOY
-----------
✔️ factory.Factory → base para objetos en memoria
✔️ factory.django.DjangoModelFactory → base para modelos Django
✔️ Faker → datos falsos (realistas)
✔️ SubFactory → objetos anidados
✔️ LazyAttribute → campos dependientes
✔️ Sequence → únicos incrementales
✔️ build(), create(), create_batch(), etc.
```

---
