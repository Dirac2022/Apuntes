
El módulo `json` en Python permite trabajar con datos en formato JSON (JavaScript Object Notation), que es un formato ligero de intercambio de datos.

### Funciones principales:

```python
import json

# Convertir de Python a JSON (serialización)
json_string = json.dumps(python_obj, indent=2)  # indent para formato bonito

# Convertir de JSON a Python (deserialización)
python_obj = json.loads(json_string)

# Leer/Escribir archivos JSON
with open('datos.json', 'w') as f:
    json.dump(python_obj, f)  # Escribir en archivo

with open('datos.json', 'r') as f:
    data = json.load(f)  # Leer archivo
```

### Ejemplo completo:

```python
import json

# Datos de ejemplo
datos_python = {
    "nombre": "Juan",
    "edad": 30,
    "ciudad": "Madrid",
    "hobbies": ["fútbol", "lectura"]
}

# Convertir a JSON
json_str = json.dumps(datos_python, indent=2)
print("JSON string:")
print(json_str)

# Convertir de vuelta a Python
datos_recuperados = json.loads(json_str)
print("\nObjeto Python recuperado:")
print(datos_recuperados)
```
