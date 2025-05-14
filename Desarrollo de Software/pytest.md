
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

**¿Qué ocurre si falla?** pytest recruye tu `assert` para desglosar la expresión y mostrar los valores intermedios, por ejemplo:

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
- `pytest -x`: detiene al primer fallo (-`exitfirst`).
- `pytest --lf`: vuelve a ejecutar solo los tests fallidos en la última ejecución.
- `pytest -n 4`: ejecuta tests en paralelo usando 4 procesos (`xdist`).
- `pytest --cov=src --cov-report=html`: mide cobertura y genera reporte HTML (`pytest-cov`).

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
