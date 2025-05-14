
## Capítulo 1: Filosofía de los Test Doubles (Ampliado)
### Definición y Clasificación
Los **Test Doubles** (dobles de prueba) son sustitutos de componentes reales usados en testing. El término fue popularizado por Gerard Meszaros en su libro *xUnit Test Patterns*. Se clasifican en:

1. **Dummy**: Objeto vacío usado para rellenar parámetros (no tiene funcionalidad).
   ```python
   # Ejemplo: Un logger que no hace nada.
   dummy_logger = None
   ```
2. **Stub**: Proporciona **respuestas predefinidas** a llamadas durante la prueba.
   ```python
   stub = Mock()
   stub.get_value.return_value = 42  # Siempre devuelve 42.
   ```
3. **Spy**: Registra información sobre cómo fue llamado (como un mock básico).
   ```python
   spy = Mock()
   spy.method()  # Llamada real.
   spy.method.assert_called_once()  # Verificación.
   ```
4. **Mock**: Preprogramado con **expectativas** (qué métodos deben llamarse y con qué argumentos).
   ```python
   mock = Mock()
   mock.expects(once()).method("param")  # Configura expectativa.
   ```
5. **Fake**: Implementación simplificada pero funcional (ej: base de datos en memoria).
   ```python
   class FakeDB:
       def __init__(self):
           self.data = {}
       def save(self, key, value):
           self.data[key] = value
   ```

### Principio de Sustitución de Liskov (LSP)
Los Test Doubles deben ser sustituibles por sus equivalentes reales. Si un stub de una API no replica el contrato mínimo (ej: formato de respuesta), las pruebas pueden dar falsos positivos.

---
	 
## Capítulo 2: Stubs en Python: Teoría y Práctica (Ampliado)
### ¿Qué Problema Resuelven?
Imagina un servicio que depende de una API externa de clima. En pruebas:
- **No podemos depender** de la disponibilidad de la API real.
- **No queremos** pagar costos por llamadas excesivas.
- **Necesitamos** simular respuestas específicas (ej: error 500).

### Implementación con `unittest.mock`
```python
from unittest.mock import Mock

# Creación de un Stub para una API de Clima
def test_clima_service():
    # Paso 1: Crear el stub que simula la API
    stub_clima_api = Mock()
    
    # Configurar el stub para devolver una temperatura específica
    stub_clima_api.obtener_temperatura.return_value = 25.5
    
    # Paso 2: Inyectar el stub en el servicio bajo prueba
    servicio = ClimaService(stub_clima_api)
    
    # Paso 3: Ejecutar el método bajo prueba
    resultado = servicio.obtener_temperatura_actual("Madrid")
    
    # Paso 4: Verificar el resultado basado en el stub
    assert resultado == 25.5, "La temperatura debe ser 25.5"
    
    # Opcional: Verificar interacción (esto ya es más propio de un mock)
    stub_clima_api.obtener_temperatura.assert_called_once_with("Madrid")
```

#### Análisis Detallado:
- **Configuración del Stub**: `return_value` fija el valor de retorno. Aquí, `obtener_temperatura` siempre devuelve 25.5.
- **Inyección de Dependencias**: El servicio recibe el stub en su constructor, siguiendo el principio de inversión de dependencias.
- **Aserciones**: Aunque los stubs no suelen requerir verificaciones, aquí mixturamos con un mock para demostrar flexibilidad.

---

## Capítulo 3: Mocks en Python: Más Allá de las Expectativas (Ampliado)
### Diferencias Clave con Stubs
- **Mocks se enfocan en el comportamiento**: No solo devuelven valores, sino que **verifican** cómo se usan.
- **Ejemplo de Uso Real**:
  - Asegurar que un método que envía emails **fue llamado exactamente una vez**.
  - Verificar que los parámetros de una llamada HTTP son correctos.

### Ejemplo: Sistema de Pagos con Mocks
```python
from unittest.mock import Mock

class ProcesadorPagos:
    def __init__(self, pasarela):
        self.pasarela = pasarela  # Dependencia externa (ej: Stripe)
    
    def realizar_pago(self, monto, tarjeta):
        if not self.pasarela.esta_activa():
            raise Exception("Pasarela inactiva")
        return self.pasarela.cobrar(monto, tarjeta)

def test_procesador_pagos():
    # Paso 1: Crear un mock de la pasarela de pagos
    mock_pasarela = Mock()
    
    # Configurar el mock para devolver True en esta_activa()
    mock_pasarela.esta_activa.return_value = True
    
    # Configurar el mock para simular un cobro exitoso
    mock_pasarela.cobrar.return_value = {"exito": True, "id": "123"}
    
    # Paso 2: Inyectar el mock en el ProcesadorPagos
    procesador = ProcesadorPagos(mock_pasarela)
    
    # Paso 3: Ejecutar el método bajo prueba
    resultado = procesador.realizar_pago(100, "4242-4242-4242-4242")
    
    # Paso 4: Verificar el resultado
    assert resultado["exito"] is True
    
    # Paso 5: Verificar interacciones con el mock
    mock_pasarela.esta_activa.assert_called_once()  # ¿Se llamó a esta_activa?
    mock_pasarela.cobrar.assert_called_once_with(100, "4242-4242-4242-4242")  # ¿Parámetros correctos?
```

#### Comentarios Detallados:
- **Configuración de Comportamientos**: El mock simula una pasarela activa (`esta_activa.return_value = True`) y un cobro exitoso.
- **Verificación de Llamadas**: Usamos `assert_called_once()` y `assert_called_once_with(...)` para asegurar que las dependencias se usaron correctamente.
- **Ventaja Clave**: Si el método `realizar_pago` deja de llamar a `cobrar`, esta prueba fallará inmediatamente.

---

## Capítulo 4: Técnicas Avanzadas con `unittest.mock` (Ampliado)
### 1. `side_effect`: Dinamismo en Respuestas
- **Uso**: Ejecuta una función o lanza una excepción cuando se llama al método.
```python
mock = Mock()

# Ejemplo 1: Lanzar una excepción en la tercera llamada
def side_effect():
    if mock.llamadas < 2:
        mock.llamadas += 1
        return 42
    else:
        raise ConnectionError("Timeout")
mock.llamadas = 0
mock.metodo.side_effect = side_effect

# Ejemplo 2: Devolver valores secuenciales
mock.metodo.side_effect = [10, 20, 30]
mock.metodo()  # 10
mock.metodo()  # 20
```

### 2. `patch`: Mocks a Nivel de Módulo
- **Contexto**: Cuando no puedes inyectar dependencias (ej: módulos globales).
```python
from unittest.mock import patch
import requests

def obtener_cantidad_usuarios():
    respuesta = requests.get("https://api.midominio.com/usuarios")
    return respuesta.json()["count"]

# Test usando patch para simular 'requests.get'
@patch('requests.get')
def test_obtener_cantidad_usuarios(mock_get):
    # Configurar el mock
    mock_respuesta = Mock()
    mock_respuesta.json.return_value = {"count": 1000}
    mock_get.return_value = mock_respuesta
    
    # Ejecutar
    resultado = obtener_cantidad_usuarios()
    
    # Verificar
    assert resultado == 1000
    mock_get.assert_called_once_with("https://api.midominio.com/usuarios")
```

#### Análisis:
- **`@patch('requests.get')`**: Parchea la función `get` del módulo `requests`.
- **Mock Anidado**: `mock_respuesta` simula el objeto `Response` de `requests`.

---

## Capítulo 5: Comparativa Stubs vs Mocks (Ampliado)
| Aspecto                | Stubs                                  | Mocks                                  |
|------------------------|----------------------------------------|----------------------------------------|
| **Responsabilidad**    | Proveer datos de entrada.              | Verificar interacciones.               |
| **Uso en Pruebas**     | "Si X devuelve Y, entonces Z".         | "Asegurar que X llamó a Y con Z".      |
| **Ejemplo Real**       | Simular una DB que devuelve un usuario.| Verificar que se envió un email tras registrarse. |
| **Flexibilidad**       | Ideal para estados simples.            | Útil para comportamientos complejos.   |
| **Ventaja Principal**  | Simplifican el entorno de prueba.      | Detectan errores de integración.       |
| **Riesgo**             | Pueden ocultar errores en dependencias.| Pruebas frágiles (ej: cambios en nombres de métodos). |

### Caso de Uso Combinado:
```python
def test_sistema_complejo():
    # Stub: Simula respuesta de base de datos
    stub_db = Mock()
    stub_db.buscar_usuario.return_value = {"id": 1, "nombre": "Alice"}
    
    # Mock: Verifica que se envió un email
    mock_email = Mock()
    
    # Sistema bajo prueba
    servicio = ServicioUsuarios(stub_db, mock_email)
    servicio.registrar_usuario(1)
    
    # Verificaciones
    mock_email.enviar.assert_called_once_with("Alice", "Bienvenido!")
```

---

## Capítulo 6: Aplicación en Proyectos Reales (Ampliado)
### Escenario 1: Microservicios
- **Contexto**: Un microservicio A llama al B via HTTP.
- **Pruebas**:
  - Usa **stubs** para simular respuestas de B (ej: éxito, error 404).
  - Usa **mocks** para asegurar que A envía los headers correctos a B.

### Escenario 2: Bases de Datos
- **Problema**: Las pruebas de integración con DBs reales son lentas.
- **Solución**:
  - **Fakes**: Usar SQLite en memoria como substituto de PostgreSQL.
  - **Mocks**: Verificar que se ejecutaron las consultas SQL esperadas.

### Escenario 3: CI/CD (Integración Continua)
- **Flujo**:
  1. Las pruebas unitarias con mocks/stubs se ejecutan en cada commit.
  2. Si pasan, se despliegan pruebas de integración con servicios reales.

---

## Conclusión Final
**Mocks y Stubs son herramientas esenciales** para crear pruebas:
- **Rápidas**: Al evitar I/O (red, DB).
- **Confiables**: Al aislar fallos al componente bajo prueba.
- **Mantenibles**: Al reducir el acoplamiento entre componentes.

**En proyectos Python**:
- Usa `unittest.mock` para la mayoría de casos.
- Considera `pytest-mock` para integración más limpia con pytest.
- **Nunca** subestimes el valor de pruebas de integración reales tras las unitarias.