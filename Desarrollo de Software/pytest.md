
### 1. Filosofía y Arquitectura de pytest

**¿Por qué pytest?** pytest nace para simplificar la escritura de pruebas: aprovecha funciones Python normales, extiende `assert` para darte mensajes detallados y permite personalizar el proceso a través de fixtures y hooks.

Internamente, pytest realiza cuatro pasos principales:

1. **Discovery (Descubrimiento)**: escanea directorios en busca de archivos y nombres de pruebas según patrones (`test_*.py`).
    
2. **Collection (Colección)**: convierte cada función `test_` y cada método en un objeto de prueba (item).
    
3. **Setup/Call/Teardown**: antes de ejecutar la prueba, inyecta fixtures (`setup`), ejecuta la función (`call`) y limpia recursos (`teardown`).
    
4. **Reporting**: recopila los resultados, aplica la reescritura de `assert` para mejoras en mensajes y entrega un informe.
    

Este flujo te permite concentrarte en qué pruebas escribir, sin preocuparte por la mecánica de ejecución.

---

### 2. Instalación y Configuración Inicial

Para comenzar con pytest, instala el paquete y complementos de utilidad:

```bash
pip install pytest pytest-cov pytest-mock pytest-xdist
```

- **pytest**: motor principal.
- **pytest-cov**: plugin para medir cobertura de código.
- **pytest-mock**: atajos para integrar `unittest.mock`.
- **pytest-xdist**: ejecución en paralelo.
    

Una vez instalado, ejecuta `pytest --version` para confirmar la instalación. Crea un entorno virtual para aislar dependencias:

```bash
python -m venv .venv
source .venv/bin/activate
```

Puedes controlar opciones por defecto en un archivo `pytest.ini`:

```ini
[pytest]
addopts = -ra -q
testpaths = tests
```

Con esto, `pytest` usará `-ra -q` y buscará pruebas bajo la carpeta `tests`.

---

### 3. Estructura de Proyecto y Descubrimiento de Pruebas

Una buena estructura ayuda a mantener el proyecto organizado:

```
my_project/
├── src/             # Código de producción
│   └── my_module.py
└── tests/           # Código de prueba
    ├── conftest.py # Fixtures y hooks compartidos
    └── test_my_module.py
```

- **conftest.py**: define fixtures y hooks disponibles para todo el directorio.
- **test_*.py**: archivos de prueba.
- Cada función que empiece con `test_` será recogida y ejecutada.

---

### 4. Sintaxis Básica de Pruebas y Convenciones

En pytest, las pruebas son funciones normales. Para escribir una prueba:

1. Importa la función o clase a probar.
2. Define una función que empiece con `test_`.
3. Utiliza `assert` para comprobar resultados.

```python
from src.my_module import add

def test_add_two_positive_numbers():
    # Cuando sumamos 2 + 3
    result = add(2, 3)
    # pytest mostrará un mensaje claro si falla
    assert result == 5
```

**¿Qué ocurre si falla?** pytest reconstruye tu `assert` para desglosar la expresión y mostrar los valores intermedios, por ejemplo:

```
E   assert 4 == 5
E    +  where 4 = add(2, 2)
```

Así sabes tanto la expresión esperada como la real, sin tener que escribir manualmente mensajes en cada `assert`.

---

### 5. Patrón Arrange‑Act‑Assert (AAA)

Este patrón separa claramente tres fases en tu prueba:

1. **Arrange (Preparar)**: crea objetos, datos y estado necesario.
2. **Act (Actuar)**: invoca la función o método bajo prueba.
3. **Assert (Verificar)**: comprueba que el resultado coincide con lo esperado.

**Ejemplo completo:**

```python
from src.auth import AuthService, User
from src.db import InMemoryDB

def test_user_login_returns_valid_token(tmp_path):
    # Arrange: configurar base de datos en memoria
    db_file = tmp_path / 'db.sqlite'
    db = InMemoryDB(path=str(db_file))
    service = AuthService(db)
    user = User(username='bob', password='secret')
    db.save(user)

    # Act: realizar login
    token = service.login('bob', 'secret')

    # Assert: el token debe ser una cadena no vacía
    assert isinstance(token, str), 'El token debe ser string'
    assert token != '', 'El token no puede estar vacío'
```

- **tmp_path** es un fixture de pytest que proporciona un directorio temporal único.
- La división en secciones facilita la lectura y el mantenimiento.

---

### 6. Manejo de Excepciones con `pytest.raises`

Para verificar que cierta llamada lanza la excepción correcta, usamos un gestor de contexto.

**6.1. Verificar excepción básica**:

```python
import pytest
from src.calculator import divide

def test_divide_by_zero_raises():
    # divide() debe lanzar ZeroDivisionError
    with pytest.raises(ZeroDivisionError):
        divide(10, 0)
```

- Si `divide(10, 0)` no lanza la excepción, pytest marca la prueba como fallida.

**6.2. Inspeccionar el mensaje de la excepción**:

```python
with pytest.raises(ValueError) as exc_info:
    divide(-5, 2)
# exc_info.value es la instancia de ValueError
assert 'must be non-negative' in str(exc_info.value)
```

- Capturamos la excepción en `exc_info` para inspeccionar su contenido.
    

**6.3. Coincidencia con expresión regular (`match`)**:

```python
# Verifica que el mensaje cumpla un patrón concreto
with pytest.raises(ValueError, match=r"^Negative.* not allowed$"):
    divide(-1, 1)
```

- `match` simplifica la comprobación de mensajes largos o formateados.
    

**6.4. Excepciones en aplicaciones web**:

En frameworks como FastAPI, las excepciones incluyen códigos HTTP.

```python
from fastapi import HTTPException

def test_not_found_raises_http_exception(client):
    with pytest.raises(HTTPException) as exc:
        client.get('/no-existe')
    assert exc.value.status_code == 404, 'Se esperaba 404 para rutas no existentes'
```

- Aquí comprobamos tanto la excepción como su atributo `status_code`.
    

---

### 7. Fixtures: Creación y Uso

Los fixtures son funciones que preparan recursos y pueden hacer teardown automático.

**7.1. Definición básica**:

```python
import pytest

@pytest.fixture
def temp_file(tmp_path):
    file = tmp_path / 'data.txt'
    file.write_text('contenido inicial')
    return file
```

- Al pedir `temp_file` como argumento en un test, pytest ejecuta la función y pasa el valor retornado.


**7.2. Alcance (scopes)**:

- **function**: (por defecto) se crea una vez por cada función de test.
- **module**: se crea una vez por archivo de test.
- **session**: una sola vez por toda la ejecución.

```python
@pytest.fixture(scope='module')
def db_connection():
    conn = conectar_bd()
    yield conn
    conn.close()
```

**7.3. Fixtures automáticos**:

```python
@pytest.fixture(autouse=True)
def log_setup(caplog):
    caplog.set_level('INFO')
```

- `autouse=True` aplica el fixture sin incluirlo en la firma del test.
    

**7.4. Fixtures parametrizados (indirect)**:

```python
@pytest.fixture
def user(request):
    return User(name=request.param)

@pytest.mark.parametrize('user', ['alice','bob'], indirect=True)
def test_greeting(user):
    assert user.greet() == f"Hello, {user.name}!"
```

- Con `indirect=True`, pytest no pasa el valor directamente, sino que lo envía al fixture `user`.
    

---

### 8. Parametrización de Pruebas

Permite ejecutar el mismo test con múltiples entradas sin bucles internos.

**8.1. Básico**:

```python
import pytest

@pytest.mark.parametrize('input,expected', [(1,1),(2,4),(3,9)])
def test_square(input, expected):
    assert square(input) == expected
```

**8.2. IDs legibles**:

```python
@pytest.mark.parametrize(
    'n,expected',
    [(1,1),(2,4),(3,9)],
    ids=['uno','dos','tres']
)
def test_square(n, expected):
    assert square(n) == expected
```

- Los IDs aparecen en los reportes en lugar de índices numéricos.
    

**8.3. Marcando casos con `pytest.param`**:

```python
@pytest.mark.parametrize(
    'a,b,expected',
    [
        pytest.param(1,0,None, marks=pytest.mark.xfail(reason='bug#1')),
        pytest.param(2,2,4)
    ]
)
def test_divide(a,b,expected):
    assert divide(a,b) == expected
```

- Permite tratar algunos casos como fallidos esperados (`xfail`).
    

**8.4. Combinando decoradores**:

Aplicar varias veces `@parametrize` crea el producto cartesiano de valores.

```python
@pytest.mark.parametrize('x',[1,2])
@pytest.mark.parametrize('y',[10,20])
def test_sum(x,y):
    assert sum([x,y]) == x+y
```

---

### 9. Marcadores y Ejecutando Condicionalmente

Los marcadores sirven para etiquetar tests y controlarlos desde la línea de comandos.

**9.1. Skip (Omitir test):**

- Útil cuando una funcionalidad aún no está implementada.

```python
import pytest

@pytest.mark.skip(reason='Funcionalidad no implementada')
def test_future_feature():
    # Este test no se ejecutará
    pass
```

**Explicación**: Al ejecutar pytest, este test se muestra como omitido con la razón indicada.

**9.2. Skipif (Omitir según condición):**

- Omite un test si se cumple una condición en tiempo de ejecución.
    

```python
@pytest.mark.skipif(
    sys.platform == 'win32',
    reason='Solo aplicable en Unix'
)
def test_unix_only():
    # Lógica específica de Unix
    pass
```

**9.3. XFail (Fallo esperado):**

- Marca tests que fallarán debido a bugs conocidos.

```python
@pytest.mark.xfail(
    strict=True,
    reason='Bug #123: división incorrecta'
)
def test_known_bug():
    assert divide(1,0) is None
```

**9.4. Marcadores personalizados:**

En `pytest.ini` definimos nueva categoría:

```ini
[pytest]
markers =
    slow: marca pruebas lentas para ejecutarlas con '-m slow'
```

Luego en código:

```python
@pytest.mark.slow
def test_heavy_computation():
    # Cálculos intensivos
    pass
```

---

### 10. Hooks y Plugins

pytest expone puntos de extensión (hooks) que podemos usar en `conftest.py` o en un plugin separado.

**Ejemplo de hook en `conftest.py`:**

```python
### conftest.py

def pytest_runtest_logreport(report):
    if report.failed:
        print(f"  >>> Test fallido: {report.nodeid} ({report.when})")
```

- `report.nodeid`: identificador del test (archivo y nombre).
- `report.when`: fase (`setup`, `call`, `teardown`).
    

Para crear un plugin independiente, define un paquete con un `entry_point` en `setup.py` bajo `pytest11`.

---

### 11. Archivos de Configuración

- **pytest.ini**: configura opciones, marcadores, rutas.
- **pyproject.toml**: sección `[tool.pytest.ini_options]` equivalente.
- **conftest.py**: define fixtures y hooks locales.

```ini
# pytest.ini
[pytest]
addopts = --maxfail=2 --disable-warnings
testpaths = tests
markers =
    integration: pruebas de integración
```

---

### 12. Comandos de Línea de Comandos (CLI)

Además de `pytest` básico, estas opciones te ayudan a filtrar, depurar y optimizar:

- `pytest -v`: muestra el nombre completo de cada prueba.
- `pytest -q`: salida minimalista.
- `pytest -k 'expresión'`: ejecuta solo tests cuyo nombre o marca coincida.
- `pytest -m 'slow'`: solo tests marcados como `slow`.
- `pytest --maxfail=1`: detiene al primer fallo.
- `pytest --disable-warnings`: oculta advertencias.
- `pytest --collect-only`: muestra qué pruebas se descubrirían sin ejecutarlas.
- `pytest --fixtures`: lista fixtures disponibles.
- `pytest --durations=5`: reporta los 5 tests más lentos.
- `pytest -x`: detiene al primer fallo (`--exitfirst`).
- `pytest --lf`: vuelve a ejecutar solo los tests fallidos en la última ejecución.
- `pytest -n 4`: ejecuta tests en paralelo usando 4 procesos (`xdist`).
- `pytest --cov=src --cov-report=html`: mide cobertura y genera reporte HTML (`pytest-cov`).
- `pytest --random-order`: para ejecutar las pruebas en un orden aleatorio.

Cada opción puede combinarse para construir pipelines de CI rápidas y claras.

---

### 13. Integración en Proyectos Medianos y Buenas Prácticas

- **Organiza tests** por funcionalidades y capas (unit, integration).
- **Centraliza fixtures** en `conftest.py`.
- **Usa marcadores** para agrupar tests lentos o de integración.
- **Parametriza** casos repetitivos para evitar código duplicado.
- **Mide rendimiento** con `--durations`.
- **Automatiza en CI**: añade `pytest --cov` en tu pipeline.
- **Genera reportes** (`pytest-html`) para revisiones de equipo.


¡Perfecto! Siguiendo tu razonamiento y preferencia por un enfoque **profundo, explicativo y bien documentado**, te presento la clase con un nuevo título adecuado y un enfoque **educativo, técnico y claro**, paso a paso.

---

## 🎓 Pruebas Parametrizadas con `@pytest.mark.parametrize`


Las pruebas parametrizadas son una técnica para **ejecutar una misma función de prueba múltiples veces** con **diferentes entradas y salidas esperadas**.

Esto **evita escribir funciones repetidas** como:

```python
def test_suma_1(): assert sumar(1, 2) == 3
def test_suma_2(): assert sumar(2, 3) == 5
...
```

En lugar de eso, se **define una sola función** y se pasa una tabla de casos de prueba.

---

**¿Qué problema resuelven?**

✔️ Eliminan **duplicación de código**  
✔️ Hacen el test **más claro y mantenible**  
✔️ Aumentan la **cobertura** al probar más casos  
✔️ Son más **explícitas y legibles**

---

**Sintaxis general**

```python
@pytest.mark.parametrize("arg1, arg2, ..., expected", [
    (valor1, valor2, ..., esperado),
    ...
])
def test_func(arg1, arg2, ..., expected):
    assert funcion(arg1, arg2, ...) == expected
```

- Los nombres de los parámetros entre comillas deben **coincidir exactamente** con los argumentos de la función de test.
    
- Cada **tupla** en la lista representa **un caso de prueba**.
    
- `pytest` ejecutará la función de test **una vez por cada fila** de datos.
    

---

### Ejemplo

Supongamos que queremos testear esta función:

 📄 `calculadora.py`

```python
def sumar(a, b):
    """
    Retorna la suma de dos números.
    """
    return a + b
```


Ahora veamos cómo se testea esa función usando pruebas parametrizadas.

📄 `test_calculadora.py`

```python
import pytest  # Importamos pytest
from calculadora import sumar  # Importamos la función que vamos a testear

# 🔽 Aquí empieza la prueba parametrizada
# Declaramos los parámetros que usará el test: a, b y resultado esperado
# Cada tupla del segundo argumento representa un caso de prueba

@pytest.mark.parametrize("a, b, esperado", [
    (1, 2, 3),        # 1 + 2 = 3
    (0, 0, 0),        # caso trivial con ceros
    (-1, 1, 0),       # suma con negativo
    (100, 200, 300),  # números grandes
    (-5, -5, -10),    # ambos negativos
])
def test_sumar(a, b, esperado):
    """
    Este test será ejecutado 5 veces, una por cada combinación (a, b, esperado).
    """
    # 💡 Pytest pasa automáticamente los valores de cada tupla a los parámetros
    resultado = sumar(a, b)  # Ejecutamos la función a testear con los parámetros actuales

    # 📌 Comprobamos que el resultado es igual al esperado
    assert resultado == esperado
```

---

### 🧠 Flujo de ejecución interno en Pytest

**¿Qué hace Pytest al encontrar `@pytest.mark.parametrize`?**

1. ✅ Cuando detecta este decorador, **Pytest expande la función de test** en **varias instancias**, una por cada conjunto de datos.
    
2. ✅ Cada instancia es ejecutada como un test separado.
    
3. ✅ Si una falla, solo esa combinación aparece como fallida, lo que ayuda a **diagnosticar problemas concretos**.
    
4. ✅ Pytest genera un **nombre automático para cada caso**, como:
    
    ```
    test_sumar[1-2-3]
    test_sumar[0-0-0]
    ...
    ```
    

---

**¿Cómo sabe Pytest qué valores usar?**

Gracias a la combinación:

```python
@pytest.mark.parametrize("a, b, esperado", [(1, 2, 3), ...])
```

Pytest:

- Lee `"a, b, esperado"` como **nombres de argumentos**.
    
- Lee `[(1, 2, 3), ...]` como **valores de entrada/salida esperada**.
    
- Por cada tupla, **llama a `test_sumar` con esos valores**.
    

---

### Casos avanzados

**Parametrización con un solo argumento**

```python
@pytest.mark.parametrize("x", [1, 2, 3])
def test_es_positivo(x):
    assert x > 0
```

➡️ Ejecuta `test_es_positivo(1)`, `test_es_positivo(2)`, `test_es_positivo(3)`.

---

**Usar `ids` para nombrar los tests**

```python
@pytest.mark.parametrize("a, b, esperado", [
    (1, 2, 3),
    (0, 0, 0),
], ids=["caso_simple", "caso_ceros"])
def test_sumar(a, b, esperado):
    assert sumar(a, b) == esperado
```

➡️ Pytest mostrará los nombres personalizados como:

```
test_sumar[caso_simple]
test_sumar[caso_ceros]
```

---

**Parametrizar varias veces (producto cartesiano)**

```python
@pytest.mark.parametrize("x", [1, 2])
@pytest.mark.parametrize("y", [10, 20])
def test_producto(x, y):
    assert x * y >= 0
```

➡️ Genera 4 combinaciones:

- x=1, y=10
- x=1, y=20
- x=2, y=10
- x=2, y=20

---

### Errores comunes

| Error                                   | Explicación                                                     |
| --------------------------------------- | --------------------------------------------------------------- |
| ❌ Faltan parámetros en la función       | `parametrize("a,b", [(1,2)])` pero `def test(a):`               |
| ❌ Olvidar que la lista necesita tuplas  | `[(1,2)]` ✅ vs `[1,2]` ❌                                        |
| ❌ Nombres incorrectos                   | `"x,y"` pero la función recibe `def test(a,b)`                  |
| ❌ Usar `=` en lugar de `==` en `assert` | Python permite `assert x == y`, pero `assert x = y` lanza error |

---

###  🧼 Buenas prácticas

✅ Nombra bien tus parámetros  
✅ Usa `ids` para mayor claridad  
✅ Evita probar muchos casos en un solo test (divide si es necesario)  
✅ Mantén los valores alineados con el objetivo del test  
✅ Documenta cada caso (comentarios al lado de cada tupla)

---

---
---

## `mocker.patch` en Pytest con `pytest-mock`


### 🧠 `pytest-mock`

`pytest-mock` es **un plugin para pytest** que te da un _fixture_ llamado `mocker`.  
Este fixture **simplifica** el uso de `unittest.mock` (que forma parte de la librería estándar).

> 🔧 Con `mocker`, puedes hacer **mocks**, **patches**, **spies**, etc., de manera más sencilla, sin tener que usar decoradores como `@patch()` o context managers como `with patch(...)`.

---

### 🧪`mocker`

Es un **fixture de pytest** (como `tmp_path`, `monkeypatch`, `caplog`, etc.) que se inyecta automáticamente si lo pones como argumento en tu test:

```python
def test_algo(mocker):  # mocker se pasa automáticamente gracias a pytest-mock
    ...
```

Detrás de escena, `mocker` es un **wrapper** alrededor de `unittest.mock` y te permite usar:

- `mocker.patch()`
- `mocker.Mock()`
- `mocker.spy()`

---

### 🧩 ¿Qué hace `mocker.patch()`?

La función `mocker.patch("modulo.objeto")` reemplaza **temporalmente** un objeto (una función, clase, variable, método, etc.) por un **mock**, **durante la ejecución del test**.

Es como decir:

> “Durante esta prueba, quiero que cuando se llame a `objeto`, en lugar de ejecutar el original, se use este falso”.

---

**Sintaxis**

```python
mocker.patch("ruta.al.objeto.que.quieres.parchear")
```

📌 Esta ruta debe ser una **cadena de texto (string)** que indique:

```
"módulo.donde_se_usa.objeto"
```

✅ No es donde se **define** el objeto.  
✅ Es donde se **usa** (importa y se llama).

---

### ⚠️ Ejemplos

Supongamos esto:

---

 📄 `calculadora.py`

```python
from math import sqrt  # <--- Importas sqrt aquí

def raiz_cuadrada(x):
    return sqrt(x)
```

Ahora, quieres testear `raiz_cuadrada(x)`, pero simular que `sqrt(x)` devuelve siempre 999, sin importar lo que se le pase.

**❌ Error común:**

```python
# INCORRECTO: parchar "math.sqrt" directamente NO FUNCIONA
mocker.patch("math.sqrt", return_value=999)
```

Porque **calculadora.py no usa `math.sqrt`**, usa la versión ya importada `sqrt`.

---

**✅ Correcto:**

```python
# CORRECTO: parcheas donde se USA: en calculadora.sqrt
mocker.patch("calculadora.sqrt", return_value=999)
```

---

## 🧪 Test completo con mocker

### 📄 `test_calculadora.py`

```python
import pytest
from calculadora import raiz_cuadrada

def test_raiz_cuadrada_mock(mocker):
    # 🔧 Parchar la función 'sqrt' que se usa dentro del módulo 'calculadora'
    mock_sqrt = mocker.patch("calculadora.sqrt", return_value=999)

    resultado = raiz_cuadrada(4)

    assert resultado == 999
    mock_sqrt.assert_called_once_with(4)  # Verifica que se llamó con el argumento correcto
```

---

### 🧠 ¿Qué está haciendo mocker.patch internamente?

1. Lee la cadena `"calculadora.sqrt"` y encuentra el objeto que debe reemplazar.
    
2. Reemplaza **temporalmente** ese objeto con un **mock**.
    
3. Devuelve el mock para que puedas configurar o inspeccionar (como `mock.return_value`, `mock.assert_called()`).
    
4. Al terminar la prueba, restaura el objeto original.
    

---

## 🧠 ¿Qué pasa si quiero parchear una función de Python como `open`, `input`, `print`?

### Debes usar `"builtins.open"` porque `open` está en el módulo `builtins`.

```python
mocker.patch("builtins.open")
```

✅ Esto hace que **cualquier uso de `open()`** en el código que estás testeando sea reemplazado por un mock.

---

## 🔍 Ejemplo: testear función que lee un archivo

### 📄 `lector.py`

```python
def leer_archivo(nombre):
    with open(nombre, "r") as f:
        return f.read()
```

### 📄 `test_lector.py`

```python
def test_leer_archivo(mocker):
    # Creamos un mock para open()
    mock_open = mocker.patch("builtins.open", mocker.mock_open(read_data="contenido"))

    resultado = leer_archivo("archivo.txt")

    assert resultado == "contenido"
    mock_open.assert_called_once_with("archivo.txt", "r")
```

---

## 🧠 ¿Qué diferencia hay entre `patch` (de `unittest.mock`) y `mocker.patch`?

|Característica|`unittest.mock.patch()`|`mocker.patch()`|
|---|---|---|
|Parte del estándar|✅ Sí|❌ No, requiere instalar `pytest-mock`|
|Se usa como decorador o `with`|✅ Sí|❌ No (solo llamado directo)|
|Devuelve mock|✅ Sí|✅ Sí|
|Se integra con fixtures de `pytest`|❌ No|✅ Sí|
|Requiere `import patch`|✅ Sí|❌ No, solo `mocker`|

---


### 🧠 Cómo usar correctamente `mocker.patch()` — Casos prácticos reales

> **Siempre parcheas el objeto en el módulo donde se USA, no donde se DEFINE.**

---

#### 📦 CASO 1 — Función importada directamente

### 📄 `modulo.py`

```python
from math import sqrt

def calcular_raiz(x):
    return sqrt(x)
```

**❌ Incorrecto:**

```python
# No funciona porque sqrt fue importado directamente.
mocker.patch("math.sqrt", return_value=0)
```


 **✅ Correcto:**

```python
# Porque se usa sqrt en modulo.py
mocker.patch("modulo.sqrt", return_value=0)
```

---

#### 📦 CASO 2 — Función usada sin importación directa

** 📄 `modulo.py`**

```python
import math

def calcular_raiz(x):
    return math.sqrt(x)
```

✅ En este caso **sí puedes** parchear `"math.sqrt"`:

```python
mocker.patch("math.sqrt", return_value=123)
```

O también:

```python
mocker.patch("modulo.math.sqrt", return_value=123)
```

Ambos funcionan porque **`modulo` accede a `sqrt` como atributo de `math`**, no como una función importada directamente.

---

#### 📦 CASO 3 — Parchear `open()` (función integrada de Python)

📄 `lector.py`

```python
def leer(nombre_archivo):
    with open(nombre_archivo) as f:
        return f.read()
```

✅ Correcto:

```python
mocker.patch("builtins.open", mocker.mock_open(read_data="hola"))
```

Porque `open()` es parte del módulo **`builtins`**, que contiene funciones nativas como `open`, `input`, `print`.

---

#### 📦 CASO 4 — Parchear `input()` para evitar interacción humana

 📄 `usuario.py`

```python
def preguntar_nombre():
    nombre = input("¿Cómo te llamas? ")
    return nombre.upper()
```

**✅ Correcto:**

```python
mocker.patch("builtins.input", return_value="Mitchel")
```

---

#### 📦 CASO 5 — Parchear `datetime.now()` (clase y método)

📄 `fechas.py`

```python
from datetime import datetime

def obtener_hora():
    return datetime.now()
```

**❌ Incorrecto:**

```python
# No funciona si se importó directamente
mocker.patch("datetime.datetime.now", ...)  # ❌
```

**✅ Correcto:**

```python
mocker.patch("fechas.datetime", autospec=True)
```

O más específico:

```python
mocker.patch("fechas.datetime.now", return_value=fake_datetime)
```

> 🔍 Porque se importó directamente `from datetime import datetime`, debes parchar `fechas.datetime`.

---

#### 📦 CASO 6 — Parchear método de clase

📄 `auth.py`

```python
class AuthService:
    def login(self, user, password):
        # ... lógica real de autenticación
        return True
```

📄 `main.py`

```python
from auth import AuthService

def ejecutar_login():
    servicio = AuthService()
    return servicio.login("admin", "1234")
```

**✅ Correcto (parcheas método dentro de la clase):**

```python
mocker.patch("auth.AuthService.login", return_value=False)
```

➡️ Esto hace que _cualquier instancia_ de `AuthService` retorne `False` al llamar `login`.

---

#### 📦 CASO 7 — Parchear función en un submódulo

**Estructura de archivos:**

```
miapp/
├── api/
│   └── cliente.py
└── servicios/
    └── procesador.py
```

 📄 `api/cliente.py`

```python
def obtener_datos():
    return {"data": "real"}
```

📄 `servicios/procesador.py`

```python
from api.cliente import obtener_datos

def procesar():
    datos = obtener_datos()
    return datos["data"].upper()
```

**❌ Esto fallará:**

```python
mocker.patch("api.cliente.obtener_datos")  # ❌
```

**✅ Lo correcto es:**

```python
mocker.patch("servicios.procesador.obtener_datos", return_value={"data": "mock"})
```

> Porque `procesador.py` importó directamente la función.

---

**📦 CASO 8 — Simular una excepción**

📄 `archivo.py`

```python
def abrir(nombre):
    with open(nombre, "r") as f:
        return f.read()
```

**✅ Parchar para simular que el archivo no existe:**

```python
mocker.patch("builtins.open", side_effect=FileNotFoundError)
```

---

### 🧠 Resumen

| Código fuente                       | Cómo se usa en el código | ¿Qué debes poner en `mocker.patch()`? |
| ----------------------------------- | ------------------------ | ------------------------------------- |
| `from x import y`                   | Usas `y()` directamente  | `"modulo_donde_se_usa.y"`             |
| `import x`                          | Usas `x.y()`             | `"x.y"` o `"modulo.x.y"`              |
| Función de Python (`open`, `input`) | `open(...)`              | `"builtins.open"`                     |
| Método de clase                     | `obj.metodo()`           | `"modulo.Clase.metodo"`               |
| Clase importada                     | `Clase()`                | `"modulo.Clase"`                      |

---


# **setup.cfg**

Este es un archivo de configuración para pytest y coverage, que personaliza cómo se ejecutan las pruebas y cómo se recopila el informe de cobertura de código. 

- `[tool:pytest]` Esto indica que las configuraciones que siguen son para la herramienta pytest, el marco de pruebas en Python.

- `addopts = -v --tb=short --cov=stack --cov-report=term-missing`
    - `-v`: Ejecuta pytest en modo detallado (verbose mode), lo que proporciona información adicional sobre qué pruebas están siendo ejecutadas y sus resultados.
    - `--tb=short`: Muestra solo el rastro de la pila acortado (short traceback) cuando se produce un error. Esto es útil para evitar la salida excesiva de texto en caso de errores o fallos de pruebas.
    - `--cov=stack`: Indica que pytest debe calcular la cobertura de código para el módulo o archivo stack.py. stack es el nombre del archivo o paquete para el cual se recopilará la cobertura.
    - `--cov-report=term-missing`: Muestra el informe de cobertura en la terminal e incluye las líneas faltantes que no están siendo cubiertas por las pruebas. Esto es útil para identificar qué partes del código no han sido probadas.
- `[coverage:run]` Este bloque contiene configuraciones específicas para el comando coverage run, que ejecuta las pruebas y recopila datos de cobertura.

  - `branch = True`: Esta opción indica que el análisis de cobertura debe incluir la cobertura de ramas (branch coverage), no solo de líneas de código. Esto asegura que se analicen todas las ramas condicionales (por ejemplo, si tienes un if en tu código, se verifica si ambas ramas —verdadera y falsa— han sido cubiertas por las pruebas).
  - `omit =`: Este parámetro especifica qué archivos o directorios omitir del informe de cobertura. En este caso:

    - */tests/*: Omite cualquier archivo o directorio bajo un directorio llamado tests.
    - */test_*: Omite archivos que comiencen con test_. Esto es útil para excluir los propios archivos de prueba del análisis de cobertura, ya que no es necesario incluirlos en el informe de cobertura de código.
- `[coverage:report]`Este bloque define cómo se debe generar el informe de cobertura de código después de ejecutar las pruebas.

    - `show_missing = True` Esta opción asegura que el informe muestre qué líneas de código están faltando en la cobertura, es decir, aquellas que no fueron ejecutadas por las pruebas. Esto te ayuda a identificar fácilmente las partes del código que no han sido probadas y donde podrías necesitar agregar más casos de prueba.

Este tipo de configuración es útil para obtener información clara sobre qué partes del código han sido probadas, y al mismo tiempo te permite ver qué partes del código aún requieren más cobertura de pruebas.
