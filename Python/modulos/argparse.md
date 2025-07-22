
`argparse` es un módulo de Python que permite crear **interfaces de línea de comandos (CLI)** de manera profesional. Facilita:

- **Definir argumentos** (obligatorios y opcionales).
- **Validar datos de entrada** (números, opciones fijas, rangos, etc.).
- **Generar mensajes de ayuda automáticos** (con `--help`).
- **Manejar sub-comandos** (como `git commit`, `docker run`).

**¿Por qué usar `argparse` y no `sys.argv`?**
- `sys.argv` solo te da una lista de argumentos sin estructura.
- `argparse` **organiza y valida** los argumentos automáticamente.
- Proporciona **ayuda integrada** y manejo de errores.

---

**Estructura Básica de un Script con `argparse`**

```python
import argparse

# 1. Crear el "parser" (analizador de argumentos)
#    - `description` aparece en la ayuda (`--help`).
parser = argparse.ArgumentParser(description='Un script que saluda al usuario.')

# 2. Añadir un argumento POSICIONAL (obligatorio)
#    - `help`: Descripción que aparece en la ayuda.
parser.add_argument('nombre', help='El nombre de la persona a saludar.')

# 3. Parsear los argumentos (convertirlos a un objeto Python)
args = parser.parse_args()

# 4. Usar los argumentos
print(f"¡Hola, {args.nombre}!")
```

 **📌 ¿Cómo se ejecuta en la terminal?**
```bash
python3 saludo.py Juan
```

**Salida:**

```
¡Hola, Juan!
```

**📌 ¿Qué pasa si no paso el argumento?**

```bash
python3 saludo.py
```

**Error:**

```
usage: saludo.py [-h] nombre
saludo.py: error: the following arguments are required: nombre
```

→ `argparse` **obliga** a pasar el argumento y muestra un mensaje de error claro.

---

## Tipos de Argumentos

### 📌 Argumentos Posicionales (Obligatorios)

Son argumentos que **deben** pasarse en un orden específico.

  ```python
  parser.add_argument('archivo', help='Ruta del archivo a procesar.')
  ```

  ```bash
  python3 script.py datos.txt
  ```

  - Guarda `datos.txt` en `args.archivo`.
  - Si no se pasa, muestra un error.

---

### 📌 Argumentos Opcionales (Flags)

Argumentos que **no son obligatorios** y se usan con `-` o `--`.

  ```python
  parser.add_argument('-v', '--verbose', help='Activar modo detallado.', action='store_true')
  ```

  ```bash
  python3 script.py -v
  # o
  python3 script.py --verbose
  ```


  - Si se usa `-v`, `args.verbose` será `True`.
  - Si no se usa, será `False`.

---

### 📌 Argumentos con Valores

Argumentos opcionales que requieren un valor adicional.

  ```python
  parser.add_argument('-l', '--limite', type=int, default=10, help='Límite de registros a mostrar.')
  ```

  ```bash
  python3 script.py --limite 20
  # o
  python3 script.py -l 20
  ```

  - Guarda `20` en `args.limite`.
  - Si no se pasa, usa el valor por defecto (`10`).

---

## Acciones Especiales (`action=`)
### **📌 `store_true` / `store_false` (Booleanos)**
- **¿Para qué sirve?** Para activar/desactivar un modo (como `--verbose`).
- **Ejemplo:**
  ```python
  parser.add_argument('--debug', action='store_true', help='Activar modo debug.')
  ```
- **¿Cómo funciona?**
  - Si se usa `--debug`, `args.debug = True`.
  - Si no se usa, `args.debug = False`.

---

### **📌 `count` (Contar repeticiones)**
- **¿Para qué sirve?** Para contar cuántas veces se usa un flag (como `-vvv` para nivel de verbosidad).
- **Ejemplo:**
  ```python
  parser.add_argument('-v', '--verbose', action='count', default=0, help='Nivel de verbosidad.')
  ```
- **Uso en terminal:**
  ```bash
  python3 script.py -v    # args.verbose = 1
  python3 script.py -vv   # args.verbose = 2
  ```
- **¿Cómo se usa en el código?**
  ```python
  if args.verbose >= 2:
      print("Modo super detallado activado.")
  ```

---

### **📌 `append` (Lista de valores)**

Permite múltiples valores en un argumento (como `--color rojo --color azul`).

  ```python
  parser.add_argument('--color', action='append', help='Colores preferidos.')
  ```

  ```bash
  python3 script.py --color rojo --color azul
  ```

**Resultado:**

  ```python
  args.color = ['rojo', 'azul']
  ```

---

## Validación y Tipos de Datos
### 📌 `type=` (Forzar tipo de dato)

Sirve para convertir automáticamente el argumento a un tipo específico (`int`, `float`, etc.).

  ```python
  parser.add_argument('--edad', type=int, help='Edad del usuario.')
  ```
  
  ```bash
  python3 script.py --edad 25
  ```

  ```python
  args.edad = 25  # (como entero, no como string)
  ```

---

### 📌 `choices=` (Opciones fijas)

Sirve para restringir un argumento a ciertos valores.

  ```python
  parser.add_argument('--tamaño', choices=['S', 'M', 'L'], help='Tamaño de la camiseta.')
  ```

  ```bash
  python3 script.py --tamaño M   # ✔️ Válido
  python3 script.py --tamaño XL  # ❌ Error (no está en choices)
  ```

---

### 📌 Validación personalizada

Sirve para definir reglas propias (ejemplo: que un número esté entre 0 y 100).

  ```python
  def porcentaje(valor):
      valor = int(valor)
      if valor < 0 or valor > 100:
          raise argparse.ArgumentTypeError("El porcentaje debe estar entre 0 y 100")
      return valor

  parser.add_argument('--descuento', type=porcentaje, help='Descuento (0-100%).')
  ```

  ```bash
  python3 script.py --descuento 50   # ✔️ Válido
  python3 script.py --descuento 150  # ❌ Error (fuera de rango)
  ```

---

## Grupos Mutuamente Excluyentes

**¿Para qué sirve?** Para que el usuario **no pueda usar dos argumentos al mismo tiempo** (ejemplo: `--rojo` y `--azul` no pueden usarse juntos).

  ```python
  grupo = parser.add_mutually_exclusive_group()
  grupo.add_argument('--rojo', action='store_true', help='Usar color rojo.')
  grupo.add_argument('--azul', action='store_true', help='Usar color azul.')
  ```

  ```bash
  python3 script.py --rojo   # ✔️ Válido
  python3 script.py --azul   # ✔️ Válido
  python3 script.py --rojo --azul  # ❌ Error (no se permiten ambos)
  ```

---

## Sub-comandos (Como `git commit`, `docker run`)

Sirve para crear comandos anidados (ejemplo: `git commit -m "mensaje"`).

  ```python
  # Crear sub-comandos
  subparsers = parser.add_subparsers(dest='comando', help='Sub-comandos disponibles')

  # Subcomando "instalar"
  parser_instalar = subparsers.add_parser('instalar', help='Instalar un paquete')
  parser_instalar.add_argument('paquete', help='Nombre del paquete')

  # Subcomando "eliminar"
  parser_eliminar = subparsers.add_parser('eliminar', help='Eliminar un paquete')
  parser_eliminar.add_argument('paquete', help='Nombre del paquete')
  ```

  ```bash
  python3 script.py instalar numpy
  python3 script.py eliminar pandas
  ```

**Resultado:**

  ```python
  args.comando = "instalar"  # o "eliminar"
  args.paquete = "numpy"     # o "pandas"
  ```

---

## Ejemplo Completo

```python
import argparse

def main():
    # Configuración del parser
    parser = argparse.ArgumentParser(
        description='Gestor de archivos con argparse',
        epilog='Ejemplos de uso:\n'
               '  python script.py archivo.txt --limite 10\n'
               '  python script.py --help'
    )

    # Argumento posicional (obligatorio)
    parser.add_argument('archivo', help='Archivo a procesar')

    # Argumento opcional con valor por defecto
    parser.add_argument('-l', '--limite', type=int, default=10, help='Límite de líneas (default: 10)')

    # Argumento booleano (flag)
    parser.add_argument('-v', '--verbose', action='store_true', help='Mostrar detalles')

    # Grupo de argumentos excluyentes
    grupo = parser.add_mutually_exclusive_group()
    grupo.add_argument('--csv', action='store_true', help='Exportar a CSV')
    grupo.add_argument('--json', action='store_true', help='Exportar a JSON')

    # Parsear argumentos
    args = parser.parse_args()

    # Lógica del script
    print(f"Procesando archivo: {args.archivo}")
    print(f"Límite de líneas: {args.limite}")
    if args.verbose:
        print("Modo detallado activado.")
    if args.csv:
        print("Exportando a CSV...")
    elif args.json:
        print("Exportando a JSON...")

if __name__ == '__main__':
    main()
```

**📌 Posibles usos en terminal:**

```bash
# Ayuda automática
python3 script.py --help

# Procesar un archivo con límite 20
python3 script.py datos.txt --limite 20

# Procesar en modo detallado y exportar a CSV
python3 script.py datos.txt -v --csv
```

---

## Consejos Finales
✅ **Usa `--help` siempre**: Genera documentación automática.  
✅ **Prueba los argumentos**: Verifica que funcionen como esperas.  
✅ **Evita abreviaturas ambiguas**: `-f` puede ser "force" o "file".  
✅ **Documenta bien los argumentos**: Usa `help=` para explicar su función.  

---

