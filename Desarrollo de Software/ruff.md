
## 🧠 1. ¿Qué es `ruff`?

`ruff` es un **linter ultrarrápido** y **formateador** para código Python, escrito en Rust. Su propósito es ayudarte a mantener un código limpio, legible y consistente, detectando errores, problemas de estilo y redundancias automáticamente.

### ✅ ¿Qué hace `ruff`?

- Verifica errores de estilo y convenciones (como `flake8`, `pylint`).
- Elimina imports no usados (`autoflake`, `isort`).
- Puede formatear automáticamente (como `black`).
- Corre rápido incluso en proyectos grandes.

---

## ⚙️ 2. Instalación

Puedes instalar `ruff` con `pip` o `pipx`.

```bash
# Opción rápida
pip install ruff

# Opción recomendada (ambiente aislado)
pipx install ruff
```

---

## 🛠️ 3. Uso básico

```bash
# Analiza un archivo
ruff archivo.py

# Analiza todo el proyecto
ruff .

# Corrige automáticamente los errores que puede
ruff . --fix
```

---

## 📁 4. Configuración del archivo `pyproject.toml`

Para personalizar `ruff`, se recomienda usar el archivo estándar `pyproject.toml`:

```toml
[tool.ruff]
line-length = 100
target-version = "py311"

[tool.ruff.lint]
select = ["E", "F", "I", "B", "UP", "C4"]
ignore = ["E501"]  # Ignora la longitud de línea

[tool.ruff.format]
quote-style = "single"
indent-style = "space"
```

### Explicación:

- `select`: Reglas a habilitar.
- `ignore`: Reglas a ignorar.
- `line-length`: Longitud máxima de línea.
- `target-version`: Versión de Python objetivo.

---

## 📋 5. Categorías de reglas más comunes

|Código|Nombre|Descripción|
|---|---|---|
|`E`|pycodestyle|Estilo de código (espacios, indentación, etc.)|
|`F`|pyflakes|Variables sin usar, imports sin usar|
|`I`|isort|Orden de imports|
|`B`|bugbear|Errores potenciales y malas prácticas|
|`UP`|pyupgrade|Reescribe código obsoleto|
|`C4`|comprehensions|Mejora listas, sets, dicts|

---

## 🧪 6. Ejemplos prácticos

### 🧹 Código original:

```python
import os, sys
import math
from collections import deque

def foo(x): return x+  1
```

### ⚙️ Corrección automática:

```bash
ruff . --fix
```

### ✅ Resultado limpio:

```python
import math
from collections import deque

def foo(x):
    return x + 1
```

---

## 🧠 7. Integración con editores

### Visual Studio Code (VSCode)

1. Instala la extensión: **Ruff** (oficial).
2. Configura en `settings.json`:

```json
"python.linting.enabled": true,
"python.linting.ruffEnabled": true,
"python.linting.ruffPath": "ruff",
"editor.formatOnSave": true,
"[python]": {
    "editor.defaultFormatter": "charliermarsh.ruff"
}
```

---

## 🧩 8. Comparación con otras herramientas

|Herramienta|Rol principal|¿Ruff puede reemplazarla?|
|---|---|---|
|`flake8`|Linting|✅ Sí|
|`pylint`|Linting pesado|⚠️ Parcialmente|
|`isort`|Imports|✅ Sí|
|`black`|Formateador|⚠️ En algunos casos sí|
|`autoflake`|Limpieza|✅ Sí|
|`pyupgrade`|Modernización|✅ Sí|

---

## 📈 9. Comandos avanzados

```bash
# Solo linting, sin formateo
ruff check .

# Solo formateo, sin reglas
ruff format .

# Ignora una carpeta
ruff . --exclude tests/

# Muestra reglas activas
ruff linter

# Mostrar código y descripción de errores
ruff check . --show-source
```

---

## 🧪 10. Integración con CI/CD (GitHub Actions)

```yaml
name: Ruff Lint
on: [push, pull_request]

jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: chartboost/ruff-action@v1
```

---

## 🧠 11. Buenas prácticas

- Usa `ruff . --fix` antes de cada `commit`.
- Agrega `ruff` al pre-commit hook para integrarlo automáticamente.
- Documenta tu configuración en `pyproject.toml`.
- Revisa qué reglas quieres activar: no necesitas todas.
- Si trabajas con `black`, configura `ruff format` para ser compatible.

---

## ✅ 12. Resumen visual

```plaintext
          +----------------------+
          |       Código         |
          +----------------------+
                     ↓
              ┌─────────────┐
              │ ruff check  │ ← Linter (estilo, errores)
              └─────────────┘
                     ↓
              ┌─────────────┐
              │ ruff format │ ← Formateador (autoajuste)
              └─────────────┘
                     ↓
             Código limpio ✔️
```

---

## 📦 13. Recursos oficiales

- Página oficial: [https://docs.astral.sh/ruff/](https://docs.astral.sh/ruff/)
- Repositorio GitHub: [https://github.com/astral-sh/ruff](https://github.com/astral-sh/ruff)

---
