
# ``if __name__ == '__main__'``
En Python, la estructura `if __name__ == '__main__':` se utiliza para determinar si un script se está ejecutando directamente o si está siendo importado como un módulo en otro script. Esta condición permite ejecutar un bloque de código solo cuando el script es ejecutado directamente, y no cuando se importa en otro archivo.

### Explicación:

- **`__name__`**: Es una variable especial de Python que se asigna dependiendo de cómo se ejecuta el script. Si el script se ejecuta directamente, `__name__` se establece como `'__main__'`.
- **`if __name__ == '__main__':`**: Verifica si el valor de `__name__` es `'__main__'`, lo cual significa que el script está siendo ejecutado directamente.

### ¿Por qué es útil?

Este constructo permite que un archivo de Python pueda actuar como un script ejecutable y como un módulo reutilizable. Así, cuando un script contiene funciones o clases que también pueden usarse en otros scripts, el código que debe ejecutarse solo al correr el script directamente se coloca dentro de `if __name__ == '__main__':`.

### Ejemplo práctico:

```python
def saludar():
    print("¡Hola, mundo!")

# Este bloque solo se ejecutará si el archivo se ejecuta directamente.
if __name__ == '__main__':
    saludar()  # Se llamará a la función saludar solo si este script se ejecuta directamente.
```

#### ¿Qué sucede si el script se importa?

Si este script se importa en otro archivo, el bloque dentro de `if __name__ == '__main__':` no se ejecutará automáticamente. Solo se importarán las funciones y clases definidas fuera de ese bloque.

**Uso común**: Esta estructura es especialmente útil para escribir scripts de prueba o para garantizar que ciertas secciones de código se ejecuten solo cuando se quiere ejecutar el archivo como programa principal y no como módulo de una biblioteca.
