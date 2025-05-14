
## 🧠 1. Fundamentos que a veces se pasan por alto

### 🔍 Git **solo ignora archivos no trackeados**

El `.gitignore` **no tiene efecto sobre archivos que ya están bajo control de versiones**. Si algo ya fue trackeado (agregado con `git add`), aunque lo pongas luego en `.gitignore`, **Git lo seguirá versionando**.

✅ Solución:

```bash
git rm --cached archivo
```

---

## 🧾 2. Sintaxis avanzada de `.gitignore`

|Regla|Explicación|Ejemplo|
|---|---|---|
|`folder/`|Ignora todo dentro de `folder/`|`logs/`|
|`folder/**`|Ignora todos los subdirectorios y archivos recursivamente|`src/**`|
|`*.ext`|Ignora todos los archivos con esa extensión|`*.log`|
|`/archivo`|Solo ignora si está en la raíz del repo|`/config.yml`|
|`**/nombre/`|Ignora todas las carpetas llamadas `nombre`, en cualquier parte|`**/__pycache__/`|
|`!archivo`|Excepción: incluye este archivo, aunque coincida con reglas anteriores|`!README.md`|
|`!carpeta/**`|Incluye carpeta y su contenido|`!src/**`|
|`!*.txt`|No ignores archivos `.txt` aunque `*` esté ignorando todo||

---

## 🗂️ 3. Casos prácticos útiles

### ✅ Ignorar todos los entornos virtuales de Python, sin importar nombre

```bash
**/env/
**/venv/
**/.venv/
```

### ✅ Ignorar toda caché de Python (lo mejor para `__pycache__`)

```bash
**/__pycache__/
*.py[cod]
```

### ✅ Ignorar todo menos una carpeta

```bash
# Ignorar todo
*

# Salvar la carpeta `src` y todo dentro de ella
!src/
!src/**
```

### ✅ Ignorar todos los archivos de una extensión **excepto uno**

```bash
*.log
!important.log
```

---

## ⚙️ 4. Uso práctico de `git rm -r --cached`

### Explicación:

|Opción|Significado|
|---|---|
|`-r`|Elimina recursivamente (carpetas + contenido)|
|`--cached`|Elimina **solo del tracking de Git**, **no borra del disco**|

### Ejemplo real:

```bash
git rm -r --cached tests/__pycache__/
```

> Así eliminás todos los archivos dentro de esa carpeta del control de Git, **pero no los borrás de tu proyecto local**.

---

## 🔍 5. Verificación de ignorados: `git check-ignore`

```bash
git check-ignore -v ruta/al/archivo
```

Devuelve:

- La **regla exacta** del `.gitignore` que está ignorando el archivo.
- La **ubicación del `.gitignore`** que contiene la regla.

📌 Ejemplo:

```bash
git check-ignore -v tests/__pycache__/mod_test.cpython-311.pyc
```

---

## 🛑 6. Casos conflictivos y soluciones

### ❌ Tenés múltiples `.gitignore` en subcarpetas y no sabés cuál aplica

Usá:

```bash
git check-ignore -v archivo
```

Te dirá qué `.gitignore` está aplicando la regla.

---

### ❌ Ignorás una carpeta con `*` pero querés conservar una

```bash
# Ignora todo
*

# Salva carpeta src
!src/
!src/**
```

---

### ❌ Querés ignorar archivos generados por pytest, coverage, VSCode, etc.

```bash
# pytest
.pytest_cache/

# coverage
.coverage
htmlcov/

# VSCode settings
.vscode/

# Logs
*.log
```

---

## 🧪 7. Plantillas `.gitignore` para Python moderno

```bash
# Byte-compiled / optimized / DLL files
__pycache__/
*.py[cod]
*$py.class

# Virtual environment
venv/
env/
.venv/
.act9/

# VSCode
.vscode/

# Test outputs
coverage.xml
htmlcov/
.tox/
noxfile.py
.pytest_cache/

# Logs
*.log

# Env vars
.env
```

---

## 🧠 8. Tips Avanzados

- 💡 Podés tener `.gitignore` **por carpeta** si querés ignorar cosas específicas solo ahí.
    
- ⚙️ Podés configurar un `.gitignore` **global** para tu máquina:
    

```bash
git config --global core.excludesfile ~/.gitignore_global
```

---

## 🎓 9. Mini Ejercicio Realista

### Proyecto:

```
mi-proyecto/
├── .gitignore
├── .env
├── src/
│   ├── __pycache__/
│   └── main.py
├── tests/
│   ├── __pycache__/
│   └── test_app.py
└── venv/
```

### Objetivo:

- Ignorar virtualenv
    
- Ignorar `__pycache__` en todos lados
    
- Ignorar `.env`
    
- Ignorar cualquier archivo `.log`
    
- **Mantener** todo el código de `src/` y `tests/`
    

### `.gitignore` final:

```bash
# Entornos virtuales
venv/
.venv/
env/

# Archivos de entorno
.env

# Cachés de Python
**/__pycache__/
*.py[cod]

# Logs
*.log

# VSCode
.vscode/
```

---

## 📌 ¿Querés más?

Puedo prepararte:

- 💾 Plantilla lista para copiar según tu proyecto
    
- 📊 Hoja visual tipo cheat sheet
    
- 🧪 Validación automática de tu `.gitignore` con un script
    
- 🤖 Un script de limpieza para borrar cosas innecesarias del repo
    

¿Querés que te lo arme?