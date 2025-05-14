
### 🧠 1. Definición de Bucket Sort

**Bucket Sort**, también conocido como **bin sort**, es un algoritmo de ordenamiento por distribución. Su idea principal es:

> Dividir el rango de los datos en "buckets" o cubetas, distribuir los elementos de entrada en estos buckets y luego ordenar cada bucket individualmente, para finalmente concatenarlos todos en un único arreglo ordenado.

Es especialmente eficiente cuando los datos están distribuidos uniformemente sobre un rango conocido.


### 📌 2. ¿Cuándo usar Bucket Sort?

Bucket Sort **no es universal**. Es útil en:

- Datos **continuos** o **reales**.
- Datos **uniformemente distribuidos** sobre un rango.
- Cuando puedes dividir los datos en buckets con número reducido de elementos por cubeta.
- Cuando se requiere una solución cercana a tiempo lineal O(n)O(n).

---

### ⛔ 3. Restricciones y supuestos

- Conocer o estimar el **rango de los datos**.
- Ideal para datos **reales o flotantes**.
- Mejor si los valores están **uniformemente distribuidos**.
- No es eficiente si todos los elementos caen en un solo bucket (peor caso).



### ⏱️ 4. Complejidad del algoritmo

| Escenario     | Complejidad temporal |
| ------------- | -------------------- |
| Mejor caso    | O(n + k)             |
| Caso promedio | O(n + k)             |
| Peor caso     | O(n^2)               |

- n: número de elementos a ordenar.
- k: número de buckets (suele ser proporcional a nn).

**Espacio adicional:** O(n+k)O(n + k)

---

### 📐 5. Principio matemático detrás

La lógica es distribuir los valores en rangos proporcionales. Suponiendo que el arreglo tiene valores en el rango $[0, 1)$, podemos hacer:

$$\text{bucket\_index}(x) = \lfloor n \cdot x \rfloor \tag{1}$$

Para valores en un rango $[a, b)$, podemos escalar:

$$\text{bucket\_index}(x) = \left\lfloor \frac{(x - a)}{(b - a)} \cdot n \right\rfloor \tag{2}$$

Esto asigna cada número al bucket correspondiente.

---

### ⚙️ 6. Algoritmo paso a paso

#### **Fase 1: Distribución**

- Crear `k` buckets vacíos.
- Insertar cada elemento del arreglo en su bucket correspondiente (usando fórmula 1 o 2).

#### **Fase 2: Ordenamiento**

- Ordenar cada bucket individualmente (usualmente con otro algoritmo como Insertion Sort).

#### **Fase 3: Concatenación**

- Combinar todos los buckets en orden para obtener el arreglo final ordenado.

---

### 🧾 7. Pseudocódigo

```plaintext
BUCKET_SORT(A, k)
1. Crear una lista de k buckets vacíos: B[0..k-1]
2. Para cada elemento x en A:
      - Calcular índice del bucket: index = calcular_bucket(x, k, min, max)
      - Insertar x en B[index]
3. Para cada bucket B[i]:
      - Ordenar B[i] usando Insertion Sort u otro algoritmo eficiente en pequeños tamaños
4. Concatenar todos los buckets en orden para formar el arreglo ordenado
```

---

### 🔁 8. Ejemplo intermedio (paso a paso)

Vamos a ordenar el siguiente arreglo de 12 elementos en el rango [0,1)[0, 1):

A=[0.78,0.17,0.39,0.26,0.72,0.94,0.21,0.12,0.23,0.68,0.34,0.15]A = [0.78, 0.17, 0.39, 0.26, 0.72, 0.94, 0.21, 0.12, 0.23, 0.68, 0.34, 0.15]

**Paso 1:** Crear 12 buckets (mismo número que elementos):

```plaintext
B0, B1, ..., B11 (inicialmente vacíos)
```

**Paso 2:** Insertar en buckets usando la fórmula:

index=⌊n⋅x⌋=⌊12⋅x⌋\text{index} = \lfloor n \cdot x \rfloor = \lfloor 12 \cdot x \rfloor

Resultado:

|Elemento|Índice bucket|Bucket|
|---|---|---|
|0.78|9|B9|
|0.17|2|B2|
|0.39|4|B4|
|0.26|3|B3|
|0.72|8|B8|
|0.94|11|B11|
|0.21|2|B2|
|0.12|1|B1|
|0.23|2|B2|
|0.68|8|B8|
|0.34|4|B4|
|0.15|1|B1|

Buckets después de la distribución:

```plaintext
B0: []
B1: [0.12, 0.15]
B2: [0.17, 0.21, 0.23]
B3: [0.26]
B4: [0.39, 0.34]
B5: []
B6: []
B7: []
B8: [0.72, 0.68]
B9: [0.78]
B10: []
B11: [0.94]
```

**Paso 3:** Ordenar cada bucket (usamos Insertion Sort):

```plaintext
B1: [0.12, 0.15]
B2: [0.17, 0.21, 0.23]
B4: [0.34, 0.39]
B8: [0.68, 0.72]
```

**Paso 4:** Concatenar en orden:

[0.12,0.15,0.17,0.21,0.23,0.26,0.34,0.39,0.68,0.72,0.78,0.94][0.12, 0.15, 0.17, 0.21, 0.23, 0.26, 0.34, 0.39, 0.68, 0.72, 0.78, 0.94]

✅ ¡Arreglo ordenado!

---

### 🧪 9. Segundo ejemplo: valores en otro rango

Supongamos:

A=[5,12,18,22,30,35,40,42,49,50,55,60](en el rango [0, 60])A = [5, 12, 18, 22, 30, 35, 40, 42, 49, 50, 55, 60] \quad \text{(en el rango [0, 60])}

Queremos aplicar bucket sort con 6 buckets. Usamos la fórmula general:

bucket(x)=⌊x−060−0⋅6⌋=⌊x60⋅6⌋\text{bucket}(x) = \left\lfloor \frac{x - 0}{60 - 0} \cdot 6 \right\rfloor = \left\lfloor \frac{x}{60} \cdot 6 \right\rfloor

Distribución:

|x|Bucket|
|---|---|
|5|0|
|12|1|
|18|1|
|22|2|
|30|3|
|35|3|
|40|4|
|42|4|
|49|4|
|50|5|
|55|5|
|60|6 → se ajusta a 5|

Ordenamos cada bucket:

- B0: [5]
    
- B1: [12, 18]
    
- B2: [22]
    
- B3: [30, 35]
    
- B4: [40, 42, 49]
    
- B5: [50, 55, 60]
    

Resultado final ordenado:

[5,12,18,22,30,35,40,42,49,50,55,60][5, 12, 18, 22, 30, 35, 40, 42, 49, 50, 55, 60]

---

### 📘 10. Conclusión

✅ **Ventajas**:

- Muy rápido en el caso ideal.
    
- Simple en concepto.
    
- Puede alcanzar complejidad lineal si los datos están bien distribuidos.
    

⚠️ **Desventajas**:

- No es eficiente si la distribución es mala.
    
- Requiere conocimiento del rango de los datos.
    
- No es "in-place" (usa memoria adicional).
    

---

¿Te gustaría que también prepare una versión visual del proceso (esquema gráfico del flujo de Bucket Sort)?