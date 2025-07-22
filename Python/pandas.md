

# Modificar nombres de columnas `in-place`

```python
df.renama(colums={'old_name':'new_name'}, inplace=True)
```


# Cambiar el orden de las columnas 

Existen varias formas de reordenar las columnas en un DataFrame. Aquí te muestro los métodos más útiles:

**1. Selección directa del orden deseado**

```python
import pandas as pd

# DataFrame de ejemplo
df = pd.DataFrame({
    'Nombre': ['Ana', 'Juan', 'María'],
    'Edad': [25, 30, 28],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia'],
    'Salario': [30000, 45000, 38000]
})

# Reordenar columnas especificando el nuevo orden
df = df[['Ciudad', 'Nombre', 'Salario', 'Edad']]

print(df)
```

**Usar `reindex()`**

```python
# Especificar el nuevo orden de columnas
nuevo_orden = ['Edad', 'Ciudad', 'Salario', 'Nombre']
df = df.reindex(columns=nuevo_orden)

print(df)
```

**3. Mover columnas específicas al principio o final**

```python
# Mover 'Salario' al principio
columnas = ['Salario'] + [col for col in df if col != 'Salario']
df = df[columnas]

print("\nCon 'Salario' al principio:")
print(df)

# Mover 'Edad' al final
columnas = [col for col in df if col != 'Edad'] + ['Edad']
df = df[columnas]

print("\nCon 'Edad' al final:")
print(df)
```

**4. Usar `iloc` para reordenar por posición**

```python
# Reordenar por índices de columnas (0-based)
# Orden: columna 2, luego 0, luego 3, luego 1
df = df.iloc[:, [2, 0, 3, 1]]

print("\nReordenado por posición:")
print(df)
```

**5. Función para mover columnas**

```python
def mover_columna(df, col_name, new_position):
    columnas = df.columns.tolist()
    columnas.remove(col_name)
    columnas.insert(new_position, col_name)
    return df[columnas]

# Mover 'Nombre' a la posición 2 (tercera columna)
df = mover_columna(df, 'Nombre', 2)

print("\nCon 'Nombre' en tercera posición:")
print(df)
```

**6. Usar `loc` con el nuevo orden**

```python
# Otra forma de especificar el orden
nuevo_orden = ['Salario', 'Edad', 'Ciudad', 'Nombre']
df = df.loc[:, nuevo_orden]

print("\nCon nuevo orden específico:")
print(df)
```

## Consejos importantes:
1. Estos métodos **no modifican** el DataFrame original (a menos que uses `inplace=True` donde esté disponible)
2. Puedes guardar el orden de columnas en una lista y reutilizarla
3. Para DataFrames grandes, el método de selección directa (`df[['col1', 'col2']]`) suele ser el más eficiente
4. Verifica siempre el resultado con `df.columns` después del reordenamiento

