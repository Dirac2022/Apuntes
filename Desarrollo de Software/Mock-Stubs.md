

> Los **test doubles** se utilizan para aislar unidades de código sustituyendo dependencias reales por objetos controlados. Se dividen en cinco tipos principales: **Dummy**, **Fake**, **Stub**, **Spy** y **Mock**. Mientras los _stubs_ devuelven datos predefinidos para verificar el **estado**, los _mocks_ comprueban **interacciones** entre componentes. Python ofrece la biblioteca estándar `unittest.mock` (con `Mock`, `MagicMock`, `patch`, etc.) y, en pytest, el fixture `mocker` para crearlos. Veremos desde la teoría de Meszaros y Fowler hasta ejemplos avanzados (métodos encadenados, side_effect, context managers, asincronía) y cómo aplicarlos en proyectos reales, evitando sobre-mocking y siguiendo buenas prácticas de mantenibilidad.

---

## Taxonomía de los Test Doubles

### ¿Qué es un Test Double?

Un **test double** es cualquier objeto que reemplaza a una dependencia real durante una prueba para **aislar** la unidad bajo test ([Wikipedia](https://en.wikipedia.org/wiki/Test_double?utm_source=chatgpt.com "Test double")). Se inspiran en dobles de acción (“stunt doubles”) en cine ([Wikipedia](https://it.wikipedia.org/wiki/Test_double?utm_source=chatgpt.com "Test double")) y siguen la clasificación propuesta por Gerard Meszaros ([Coding Horror](https://blog.codinghorror.com/test-doubles-a-taxonomy-of-pretend-objects/?utm_source=chatgpt.com "Test Doubles: A Taxonomy of Pretend Objects - Coding Horror")).

### Tipos de Test Doubles

Según Meszaros (y recogido por Fowler), existen cinco categorías principales:

- **Dummy**: se pasa como parámetro pero nunca se usa.
- **Fake**: implementación simplificada (por ejemplo, base de datos en memoria).
- **Stub**: devuelve respuestas programadas para controlar el flujo de ejecución.
- **Spy**: además de devolver datos, registra información sobre las llamadas recibidas.
- **Mock**: similar al spy, pero también verifica **expectativas** predefinidas sobre esas llamadas ([martinfowler.com](https://martinfowler.com/articles/mocksArentStubs.html?utm_source=chatgpt.com "Mocks Aren't Stubs - Martin Fowler")).

Cada categoría tiene su propósito: los _fakes_ son útiles para pruebas de integración sin componentes externos, mientras los _stubs_ y _mocks_ se enfocan en pruebas unitarias rigurosas ([droidcon](https://www.droidcon.com/2022/05/29/the-definitive-guide-to-test-doubles-on-android-part-1-theory/?utm_source=chatgpt.com "The definitive guide to test doubles on Android — Part 1: Theory")).

### Estado vs. Comportamiento

- **State Verification (Stubs)**: comprobamos que, dado un retorno específico, el código produce el estado esperado.
    
- **Behavior Verification (Mocks)**: comprobamos que el código **interactúa** correctamente con sus dependencias (métodos llamados, argumentos, orden) ([Stack Overflow](https://stackoverflow.com/questions/25073561/stubbing-vs-mocking-in-python?utm_source=chatgpt.com "Stubbing vs Mocking in Python - unit testing - Stack Overflow")).

---

## Diferencias conceptuales: Stubs vs. Mocks

### ¿Qué es un Stub?

Un **stub** es un objeto preconfigurado que **sólo devuelve** valores fijos en función de las llamadas recibidas, sin fallar el test por interacciones inesperadas ([Developer Purpose](https://blog.developerpurpose.com/mocking-stubs-spies-in-your-unit-tests-b37b0c7fdd8d?utm_source=chatgpt.com "Mocking, stubs, & spies in your unit tests | by Bennett Garner")). Se usa para simular respuestas de APIs, bases de datos, etc., y **facilitar** escenarios difíciles de reproducir (errores, latencia) ([zencoder.ai](https://zencoder.ai/blog/effective-unit-tests-mocking-stubbing?utm_source=chatgpt.com "Mocking and Stubbing for Effective Unit Test Generation - Zencoder")).

### 2.2 ¿Qué es un Mock?

Un **mock** es un stub con **expectativas**: lanza errores si no se cumplen (cantidad de llamadas, parámetros) ([Python documentation](https://docs.python.org/3/library/unittest.mock.html?utm_source=chatgpt.com "unittest.mock — mock object library — Python 3.13.3 documentation")). Es ideal para **verificar** que un servicio invoque a otro con exactitud, p. ej., un logger recibiendo el mensaje correcto ([Medium](https://medium.com/%40moraneus/the-art-of-mocking-in-python-a-comprehensive-guide-8b619529458f?utm_source=chatgpt.com "The Art of Mocking in Python: A Comprehensive Guide | by Moraneus")).

### 2.3 Comparativa

|Característica|Stub|Mock|
|---|---|---|
|Retorno de datos|Valores predefinidos ([XUnit Patterns](https://xunitpatterns.com/Mocks%2C%20Fakes%2C%20Stubs%20and%20Dummies.html?utm_source=chatgpt.com "Mocks, Fakes, Stubs and Dummies at XUnitPatterns.com"))|Valores predefinidos|
|Verificación de interacciones|❌ No|✅ Sí (assert_called_…) ([Python documentation](https://docs.python.org/3/library/unittest.mock.html?utm_source=chatgpt.com "unittest.mock — mock object library — Python 3.13.3 documentation"))|
|Falta de llamadas inesperadas|Acepta|Falla el test|
|Enfoque|State verification|Behavior verification|

---

## Implementación en Python con `unittest.mock`

### Creando Stubs con `Mock`

```python
from unittest.mock import Mock

# 1. Definimos un stub que siempre devuelve 42
stub = Mock(return_value=42)       # Mock con return_value :contentReference[oaicite:12]{index=12}
assert stub() == 42                # State verification
```

1. `Mock(return_value=…)` genera un objeto callable que devuelve el valor indicado.
2. No verifica interacciones: cualquier llamada es aceptada ([Python documentation](https://docs.python.org/3/library/unittest.mock.html?utm_source=chatgpt.com "unittest.mock — mock object library — Python 3.13.3 documentation")).


### 3.2 Mocks básicos

```python
from unittest.mock import Mock

# 1. Creamos un mock para un servicio de email
email_service = Mock()             # Mock sin return_value :contentReference[oaicite:14]{index=14}

# Llamada simulada
email_service.send('a@b.com', 'Hola')  
# 2. Verificamos la interacción
email_service.send.assert_called_once_with('a@b.com', 'Hola')  # Behavior verification :contentReference[oaicite:15]{index=15}
```

1. `assert_called_once_with()` comprueba que el método se llamó exactamente una vez con esos argumentos.
    
2. Fallará si no se cumple la expectativa.

### 3.3 Uso de `patch()`

```python
from unittest.mock import patch

# 1. Reemplazamos get_data() durante esta prueba
@patch('mi_modulo.get_data')
def test_procesar(mock_get_data):
    mock_get_data.return_value = {'x': 1}  # Stub dentro del patch :contentReference[oaicite:16]{index=16}
    resultado = mi_modulo.procesar()
    assert resultado == 'Procesado 1'
    mock_get_data.assert_called_once()     # Behavior verification
```

- `@patch('modulo.funcion')` recibe el **punto de uso**, no el de definición ([Medium](https://medium.com/%40moraneus/the-art-of-mocking-in-python-a-comprehensive-guide-8b619529458f?utm_source=chatgpt.com "The Art of Mocking in Python: A Comprehensive Guide | by Moraneus")).
- Dentro de la función de test, `mock_get_data` es el stub/mocK que sustituye a la función real.

---

## pytest y `pytest-mock`

### 4.1 Configuración del fixture `mocker`

Con `pip install pytest-mock` obtienes el fixture `mocker`, envoltorio de `unittest.mock` ([Software Engineering Stack Exchange](https://softwareengineering.stackexchange.com/questions/415958/how-deep-should-i-mock-dependencies-in-unit-tests?utm_source=chatgpt.com "How deep should I mock dependencies in unit tests")).

### 4.2 Ejemplo de Stub y Mock en pytest

```python
def test_servicio_usuario(mocker):
    # 1. Stub de función externa
    mocker.patch('app.api.obtener_usuario', return_value={'id':1,'nombre':'Ana'})
    # 2. Mock de servicio de notificaciones
    svc_notif = mocker.Mock(name='notif_svc')
    
    from app import servicio
    servicio.notificar_usuario(1, svc_notif)
    
    # 3. Verificaciones
    svc_notif.enviar.assert_called_once_with('Ana')  # Behavior
```

1. `mocker.patch()` crea un stub para `obtener_usuario` ([Software Engineering Stack Exchange](https://softwareengineering.stackexchange.com/questions/415958/how-deep-should-i-mock-dependencies-in-unit-tests?utm_source=chatgpt.com "How deep should I mock dependencies in unit tests")).
2. `mocker.Mock(name='…')` nombra el mock para diagnósticos más claros.
3. Se combinan state y behavior verification.

---

## ## 5. Ejemplos avanzados

### 5.1 `side_effect` para secuencias o excepciones

```python
from unittest.mock import Mock

# Secuencia de retornos
stub = Mock(side_effect=[1,2,3])
assert [stub(), stub(), stub()] == [1,2,3]  # side_effect secuencial:contentReference[oaicite:20]{index=20}

# Excepción en ciertas llamadas
def falla(x):
    raise ValueError("Error")
stub_exc = Mock(side_effect=falla)
try:
    stub_exc(0)
except ValueError as e:
    assert str(e) == "Error"
```

- `side_effect` puede ser lista o función que lanza excepciones.

### MagicMock y encadenamiento

```python
from unittest.mock import MagicMock

api = MagicMock()  
# Simular llamadas encadenadas: api.servicio().recurso().get()
api.servicio.return_value.recurso.return_value.get.return_value = {'ok':True}
assert api.servicio().recurso().get()['ok']  # Chained mocks :contentReference[oaicite:21]{index=21}
```

- `MagicMock` incluye métodos mágicos (e.g., `__len__`, `__iter__`) listos para usar.

### 5.3 Context managers y asincronía

```python
from unittest.mock import patch, AsyncMock

# Context manager
with patch('mod.api.fetch') as mock_fetch:
    mock_fetch.return_value = {'data':42}
    assert api.procesar() == 42

# AsyncMock para corutinas
async def test_async(mocker):
    m = mocker.AsyncMock(return_value=5)
    assert await m() == 5
```

- `AsyncMock` gestiona `await` y funciones `async def`.

---

## Buenas prácticas y anti-patrones

### Evita el sobre-mocking

Mocks excesivos hacen tests frágiles y difíciles de mantener. Prefiere **fakes** o stubs escritos a mano cuando haya múltiples tests que compartan la misma sustitución ([Enterprise Craftsmanship](https://enterprisecraftsmanship.com/posts/stubs-vs-mocks/?utm_source=chatgpt.com "Stubs vs Mocks - Enterprise Craftsmanship")).

### Nombres descriptivos

Usar `name='email_svc'` facilita la lectura de errores de tests.

### Verifica solo lo relevante

No asserts en llamadas internas irrelevantes; céntrate en la **interfaz pública** del módulo.

### Agrupa configuraciones comunes en fixtures

En pytest, define fixtures que preparen tus stubs/mocks para evitar duplicación.

---

## Aplicaciones en proyectos reales

En proyectos a gran escala (Django, Flask, microservicios):

- **APIs externas**: stubs que devuelvan JSON de ejemplo, evitando llamadas reales.
    
- **Bases de datos**: fakes en memoria (SQLite o bibliotecas específicas) para pruebas de integración rápida ([InfoWorld](https://www.infoworld.com/article/2164759/mocks-and-stubs-understanding-test-doubles-with-mockito.html?utm_source=chatgpt.com "Mocks And Stubs – Understanding Test Doubles With Mockito")).
    
- **Mensajería y colas**: mocks de cola para verificar que se publiquen eventos correctamente.
    
- **Paquetes de terceros**: patch de librerías complejas (e.g., boto3, requests) para simular errores y medir cobertura de excepciones.
    

---
