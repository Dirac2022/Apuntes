
### **Capítulo 1: Fundamentos de Testing Unitario**
#### **1.1 Definición de Test Unitario**
Un test unitario es un **fragmento de código diseñado para verificar el comportamiento de una unidad lógica** (función, método, clase) en condiciones controladas. Su objetivo principal es **aislar cada parte del programa y demostrar que funciona correctamente** en escenarios específicos.

**Ejemplo Práctico:**
```python
def test_suma_numeros_positivos():
    # Arrange (Preparación): Definir entradas
    a = 5
    b = 3
    
    # Act (Ejecución): Invocar al código bajo prueba
    resultado = a + b
    
    # Assert (Verificación): Confirmar el resultado esperado
    assert resultado == 8, "La suma de 5 y 3 debe ser 8"
```
- **Línea 1**: Declaración del test usando el prefijo `test_` (requerido por pytest para detección automática).
- **Línea 3-4**: Fase de _Arrange_ donde se establecen las condiciones iniciales.
- **Línea 7**: Fase de _Act_ donde se ejecuta la operación bajo prueba.
- **Línea 10**: Fase de _Assert_ con mensaje descriptivo en caso de fallo.

#### **1.2 Problemas del Enfoque Tradicional (sin Fixtures)**
Cuando los tests requieren **configuración compleja o recurrente**, el código se vuelve repetitivo y difícil de mantener. Ejemplo clásico:

```python
class TestBaseDeDatos:
    def test_insercion(self):
        # Configuración manual en cada test
        self.conexion = ConexionBD("localhost", "usuario", "contraseña")
        self.conexion.conectar()
        
        # Ejecución
        resultado = self.conexion.insertar("INSERT INTO tabla VALUES...")
        
        # Verificación
        assert resultado.es_valido()
        
        # Limpieza manual
        self.conexion.cerrar()

    def test_consulta(self):
        # Repetición de la misma configuración
        self.conexion = ConexionBD("localhost", "usuario", "contraseña")
        self.conexion.conectar()
        
        # ...
```
- **Problemas Detectados**:
  - **Duplicación de código**: Configuración repetida en múltiples tests.
  - **Fragilidad**: Cambios en la configuración requieren modificar todos los tests.
  - **Poca legibilidad**: El código de configuración ensucia la lógica del test.

---

### **Capítulo 2: Introducción a Fixtures - Conceptos Nucleares**
#### **2.1 Definición Técnica de Fixture**
Un fixture es una **función decorada** en pytest que:
1. **Prepara recursos** necesarios para la ejecución de tests.
2. **Permite reutilización** de dichos recursos entre múltiples tests.
3. **Gestiona automáticamente** el ciclo de vida (creación/destrucción) de los recursos.

**Anatomía de un Fixture Básico:**
```python
import pytest

@pytest.fixture  # Decorador que define la función como fixture
def recurso_compartido():
    # Fase de Setup (Creación del recurso)
    recurso = crear_recurso_complejo()
    
    # Entrega el control al test
    yield recurso  
    
    # Fase de Teardown (Limpieza post-test)
    destruir_recurso(recurso)
```
- **Línea 3**: `@pytest.fixture` convierte una función normal en un fixture.
- **Línea 5-6**: Código de inicialización que se ejecuta antes del test.
- **Línea 9**: `yield` marca el punto donde el test recibe el recurso.
- **Línea 12**: Código que se ejecuta después que el test finaliza, incluso si falla.

#### **2.2 Flujo de Ejecución Detallado**
Cuando un test utiliza un fixture:
1. pytest **detecta** los fixtures requeridos en los parámetros del test.
2. Ejecuta el **código previo al yield** del fixture (setup).
3. **Pasa el recurso** al test y ejecuta el código del test.
4. **Ejecuta el código posterior al yield** (teardown), independientemente del resultado.

**Visualización Temporal**:
```
[Test Execution Timeline]
|------------------ Test ------------------|
|--- Fixture Setup ---|                    |--- Fixture Teardown ---|
                      |--- Test Code ---|
```

---

### **Capítulo 3: Decoradores y Configuración de Fixtures**
#### **3.1 El Decorador `@pytest.fixture`**
Este decorador acepta múltiples parámetros para controlar el comportamiento del fixture:

```python
@pytest.fixture(
    scope="function",  # Alcance del fixture
    autouse=False,     # Ejecución automática sin inyección
    params=None,       # Parametrización del fixture
    name=None          # Nombre alternativo para el fixture
)
def mi_fixture():
    # ...
```

**Parámetros Clave**:
1. **`scope`** (Alcance):
   - **Valores Posibles**: "function" (default), "class", "module", "session"
   - **Ejemplo Práctico**:
     ```python
     @pytest.fixture(scope="module")
     def conexion_db():
         # Se ejecuta una vez por módulo de tests
         conn = DB.connect()
         yield conn
         conn.close()
     ```

2. **`autouse`** (Auto-uso):
   - **`True`**: El fixture se ejecuta automáticamente para todos los tests en su alcance.
   - **Ejemplo**:
     ```python
     @pytest.fixture(autouse=True, scope="session")
     def configurar_logs():
         # Configura logs para toda la sesión de tests
         logging.basicConfig(level=logging.DEBUG)
     ```

3. **`params`** (Parametrización):
   - Permite ejecutar el test múltiples veces con diferentes valores del fixture.
   - **Ejemplo Avanzado**:
     ```python
     @pytest.fixture(params=["utf-8", "iso-8859-1"])
     def codificacion(request):
         return request.param  # 'request' da acceso a los parámetros

     def test_decodificacion(codificacion):
         # Se ejecutará dos veces: una por cada codificación
         dato = "ñ".encode(codificacion)
         assert dato.decode(codificacion) == "ñ"
     ```

#### **3.2 El Objeto `request` en Fixtures**
Cuando un fixture necesita acceder a información contextual (como parámetros), pytest provee el objeto `request`:

```python
@pytest.fixture
def recurso_parametrizado(request):
    # request.param contiene el valor actual de parametrización
    valor = request.param * 2
    yield valor
    # Limpieza opcional basada en el parámetro
```

---

### **Capítulo 4: Tipología de Fixtures y Patrones Avanzados**
#### **4.1 Fixtures de Tipo Factory**
Patrón donde el fixture retorna una **función generadora** en lugar de un objeto directo, permitiendo crear múltiples instancias con diferentes parámetros.

**Implementación Detallada**:
```python
@pytest.fixture
def producto_factory():
    # Función interna que actúa como factory
    def _factory(nombre: str, precio: float) -> Producto:
        return Producto(
            nombre=nombre,
            precio=precio,
            sku=generar_sku_aleatorio()  # Función hipotética
        )
    
    # Retorna la factory para uso en tests
    return _factory

def test_precio_producto(producto_factory):
    # Uso de la factory para crear instancia específica
    producto = producto_factory(nombre="Laptop", precio=1500.0)
    assert producto.precio == 1500.0
```

**Ventajas**:
- **Flexibilidad**: Permite personalizar parámetros en cada test.
- **Encapsulamiento**: Mantiene la lógica de creación en un solo lugar.

#### **4.2 Fixtures con Dependencias**
Los fixtures pueden **depender de otros fixtures**, creando una jerarquía de inicialización.

**Ejemplo Complejo**:
```python
@pytest.fixture
def configuracion():
    return {"timeout": 30, "intentos": 3}

@pytest.fixture
def api_client(configuracion):
    # Usa valores del fixture 'configuracion'
    client = APIClient(
        timeout=configuracion["timeout"],
        max_retries=configuracion["intentos"]
    )
    client.autenticar()
    yield client
    client.cerrar()

def test_api_llamada(api_client):
    respuesta = api_client.get("/usuarios")
    assert respuesta.status_code == 200
```

**Flujo de Dependencias**:
1. pytest ejecuta `configuracion`.
2. Usa el resultado en `api_client`.
3. Finalmente inyecta `api_client` en el test.

---

### **Capítulo 5: Manejo de Estado y Alcances (Scopes)**
#### **5.1 Jerarquía de Scopes**
pytest organiza los fixtures en una jerarquía de alcances, donde **los scopes más amplios tienen prioridad**:

```
session > module > class > function
```

**Ejemplo de Fixture con Scope de Módulo**:
```python
@pytest.fixture(scope="module")
def modelo_entrenado():
    # Entrenamiento costoso en tiempo
    datos = cargar_dataset_grande()
    modelo = ModeloML()
    modelo.entrenar(datos)
    yield modelo
    # Liberar memoria post-tests del módulo
    del modelo
```

**Comportamiento**:
- Se ejecuta **una vez por archivo de tests** (módulo).
- Todos los tests en el módulo comparten la misma instancia.
- Reduce tiempo de ejecución para recursos costosos.

#### **5.2 Combinación de Scopes**
Cuando múltiples fixtures con diferentes scopes interactúan, pytest administra su ciclo de vida automáticamente:

```python
@pytest.fixture(scope="session")
def servidor():
    serv = iniciar_servidor()
    yield serv
    serv.detener()

@pytest.fixture(scope="function")
def cliente(servidor):  # Depende de un fixture de sesión
    return servidor.crear_cliente()

def test_conexion(cliente):
    assert cliente.ping()
```

**Gestión de Recursos**:
- `servidor` se inicia una vez al principio de la sesión.
- `cliente` se crea y destruye para cada test.

---

### **Capítulo 6: Fixtures en Acción - Caso de Estudio Completo**
**Contexto**: Sistema de autenticación con:
- `Usuario`: Modelo con nombre y permisos.
- `SistemaAuth`: Gestiona login y permisos.

**Implementación de Fixtures**:
```python
# tests/conftest.py
import pytest
from src.auth import SistemaAuth, Usuario

@pytest.fixture(scope="module")
def sistema_auth():
    # Inicialización costosa: 1 vez por módulo
    sistema = SistemaAuth()
    sistema.configurar(clave_secreta="test_123")
    yield sistema
    # Limpieza: Borrar datos de prueba
    sistema.limpiar_base()

@pytest.fixture
def usuario_admin(sistema_auth):
    # Crea un usuario administrador
    usuario = Usuario(nombre="admin", es_admin=True)
    sistema_auth.registrar(usuario)
    return usuario

@pytest.fixture
def usuario_normal(sistema_auth):
    # Crea un usuario regular
    usuario = Usuario(nombre="user1", es_admin=False)
    sistema_auth.registrar(usuario)
    return usuario
```

**Tests Utilizando Fixtures**:
```python
# tests/test_auth.py
def test_login_admin(usuario_admin, sistema_auth):
    # Act
    resultado = sistema_auth.login(usuario_admin.nombre)
    
    # Assert
    assert resultado.es_exitoso()
    assert sistema_auth.es_admin(usuario_admin)

def test_login_normal(usuario_normal, sistema_auth):
    resultado = sistema_auth.login(usuario_normal.nombre)
    assert resultado.es_exitoso()
    assert not sistema_auth.es_admin(usuario_normal)
```

**Análisis de Flujo**:
1. `sistema_auth` se crea una vez por módulo (`scope="module"`).
2. `usuario_admin` y `usuario_normal` se recrean para cada test (`scope="function"` default).
3. Ambos tests comparten la misma instancia de `sistema_auth`.

---

### **Capítulo 7: Ejercicio 5 - Refactorización con Fixtures**
**Contexto Original**:
- Clase `Carrito` con métodos para agregar productos y calcular total.
- Tests crean instancias directamente en cada test.

**Objetivo**:
- Centralizar creación de `Carrito` y `Producto` usando fixtures.

#### **Paso 1: Definir Fixtures en `conftest.py`**
```python
# tests/conftest.py
import pytest
from src.carrito import Carrito
from src.factories import ProductoFactory

@pytest.fixture
def carrito():
    """Fixture que provee una instancia nueva y vacía de Carrito para cada test."""
    # Setup: Crear carrito
    nuevo_carrito = Carrito()
    
    # Entregar recurso
    yield nuevo_carrito
    
    # Teardown: Opcional (no necesario aquí, pero se muestra la estructura)
    nuevo_carrito.vaciar()  # Método hipotético

@pytest.fixture
def producto_generico():
    """Fixture que crea un producto con valores predeterminados usando una fábrica."""
    # Utiliza la fábrica con parámetros fijos
    return ProductoFactory(
        nombre="Producto Genérico",
        precio=100.0,
        stock=10
    )
```

**Explicación Detallada**:
- **`carrito` Fixture**:
  - **Línea 6**: Decorador estándar sin parámetros (`scope="function"` por defecto).
  - **Línea 8**: Creación de instancia fresca para cada test.
  - **Línea 11**: `yield` entrega el carrito al test.
  - **Línea 14**: Código de limpieza (ejecutado post-test).

- **`producto_generico` Fixture**:
  - **Línea 18**: Usa `ProductoFactory` para crear instancias consistentes.
  - **Parámetros Fijos**: Garantiza valores conocidos para las pruebas.

#### **Paso 2: Refactorizar Tests Existentes**
**Antes**:
```python
def test_agregar_producto():
    carrito = Carrito()  # Instanciación manual
    producto = Producto("Camisa", 25.0)
    carrito.agregar(producto)
    assert len(carrito.productos) == 1

def test_total_carrito():
    carrito = Carrito()
    carrito.agregar(Producto("Libro", 50.0))
    carrito.agregar(Producto("Lápiz", 5.0))
    assert carrito.total() == 55.0
```

**Después**:
```python
def test_agregar_producto(carrito, producto_generico):
    # Act
    carrito.agregar(producto_generico)
    
    # Assert
    assert len(carrito.productos) == 1, "El carrito debe contener 1 producto tras agregar"
    assert producto_generico in carrito.productos, "El producto agregado debe estar en la lista"

def test_total_carrito(carrito, producto_generico):
    # Arrange: Configurar múltiples productos
    producto_generico.precio = 75.0  # Modificar precio para este test
    
    # Act
    carrito.agregar(producto_generico)
    carrito.agregar(producto_generico)
    
    # Assert
    assert carrito.total() == 150.0, "Total debe ser suma de dos productos a 75 cada uno"
```

**Mejoras Obtenidas**:
1. **Centralización**: La creación de `Carrito` y `Producto` está en `conftest.py`.
2. **Consistencia**: Todos los tests parten de un estado conocido.
3. **Reusabilidad**: Fixtures pueden usarse en múltiples archivos de test.
4. **Mantenibilidad**: Cambios en la estructura de `Carrito` solo afectan a los fixtures.

#### **Paso 3: Beneficios Adicionales**
- **Aislamiento**: Cada test recibe su propia instancia de `carrito` (scope function), evitando interferencias.
- **Parametrización Flexible**:
  ```python
  @pytest.mark.parametrize("cantidad, total_esperado", [(1, 100), (3, 300)])
  def test_multiples_productos(carrito, producto_generico, cantidad, total_esperado):
      for _ in range(cantidad):
          carrito.agregar(producto_generico)
      assert carrito.total() == total_esperado
  ```

---

### **Capítulo 8: Buenas Prácticas y Antipatrones**
#### **8.1 Recomendaciones Clave**
1. **Nomenclatura Clara**:
   - Nombres de fixtures como `db_connection`, `admin_user`.
   - Evitar nombres genéricos como `data` o `obj`.

2. **Scope Mínimo Necesario**:
   - Usar `scope="function"` a menos que se necesite optimización.
   - Ejemplo de scope amplio:
     ```python
     @pytest.fixture(scope="session")
     def modelo_machine_learning_entrenado():
         # Entrenamiento que toma 10 minutos
         return Modelo.entrenar(datos_grandes)
     ```

3. **Documentación de Fixtures**:
   ```python
   @pytest.fixture
   def usuario_premium():
       """Retorna un usuario con suscripción premium activa y créditos iniciales."""
       usuario = Usuario(suscripcion="premium")
       usuario.agregar_creditos(1000)
       return usuario
   ```

#### **8.2 Antipatrones Comunes**
1. **Fixtures con Lógica Compleja**:
   - ❌ Incorrecto:
     ```python
     @pytest.fixture
     def sistema_complejo():
         # 50 líneas de inicialización
         # ...
     ```
   - ✅ Correcto:
     ```python
     @pytest.fixture
     def subsistema_a():
         return SubsistemaA()

     @pytest.fixture
     def subsistema_b(subsistema_a):
         return SubsistemaB(subsistema_a)

     @pytest.fixture
     def sistema_complejo(subsistema_a, subsistema_b):
         return Sistema(subsistema_a, subsistema_b)
     ```

2. **Abuso de `autouse=True`**:
   - Peligro: Fixtures que modifican estado global sin necesidad.
   - Uso adecuado: Configuración ambiental (ej: logging, conexiones a servicios externos).

---

### **Capítulo 9: Integración con Otras Herramientas**
#### **9.1 `pytest-mock` para Mocking**
Combine fixtures con objetos mock para pruebas aisladas:
```python
import pytest

@pytest.fixture
def mock_servicio_externo(mocker):
    mock = mocker.patch("mi_modulo.ServicioExterno")
    mock.descargar_datos.return_value = {"fake": "data"}
    return mock

def test_integracion_con_mock(carrito, mock_servicio_externo):
    carrito.sincronizar_con_servicio()
    mock_servicio_externo.enviar_carrito.assert_called_once_with(carrito)
```

#### **9.2 `pytest-cov` para Cobertura**
Ejecutar tests con medición de cobertura:
```bash
pytest --cov=src --cov-report=html tests/
```

#### **9.3 Plugins Avanzados**
- **`pytest-django`**: Fixtures para proyectos Django (client, admin_client).
- **`pytest-asyncio`**: Soporte para corrutinas y async/await.
- **`pytest-html`**: Generación de reportes HTML detallados.

---

### **Capítulo 10: Depuración de Fixtures**
Cuando un fixture falla, pytest proporciona información detallada:
```bash
pytest --setup-show tests/test_carrito.py
```
**Salida Ejemplo**:
```
SETUP    F carrito
SETUP    F producto_generico
tests/test_carrito.py::test_agregar_producto (fixtures used: carrito, producto_generico).
TEARDOWN F producto_generico
TEARDOWN F carrito
```

**Técnicas de Depuración**:
1. **Imprimir Estados**:
   ```python
   @pytest.fixture
   def carrito():
       c = Carrito()
       print(f"\nCarrito creado en {hex(id(c))}")  # Debug de instancia
       yield c
       print(f"Carrito destruido en {hex(id(c))}")
   ```

2. **Usar `pdb`**:
   ```python
   @pytest.fixture
   def producto_generico():
       p = ProductoFactory()
       import pdb; pdb.set_trace()  # Breakpoint interactivo
       yield p
   ```

---
