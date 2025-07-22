
## **Variables en Bash**

Las variables en Bash son contenedores para almacenar datos. No requieren declaración de tipo (son *dinámicamente tipadas*).

---

 **Tipos de Variables:**

### Variables locales
Solo disponibles en el shell actual.  
   ```bash
   nombre="Juan"
   edad=25
   ```

### Variables de entorno
Accesibles por procesos hijos. Se declaran con `export`.  
   ```bash
   export PATH="$PATH:/usr/local/bin"
   ```

**Ejemplo**

```sh
NOMBRE="Cesar"
readonly PI=3.14159
export ENV="producción"
```


1. **`NOMBRE="Cesar"`**  
   - **Variable local** (solo disponible en el script/shell actual).  
   - Su valor puede modificarse más adelante.  

2. **`readonly PI=3.14159`**  
   - **Variable de solo lectura** (constante).  
   - No puede ser modificada ni eliminada después de su declaración.  

3. **`export ENV="producción"`**  
   - **Variable de entorno** (disponible para procesos hijos/subshells).  
   - Accesible con `echo $ENV` o en scripts ejecutados desde este shell.  
 

**Clave**:
- **`NOMBRE`**: Volátil y mutable (solo en el shell actual).  
- **`PI`**: Inmutable (constante).  
- **`ENV`**: Persiste en procesos hijos (como variables globales).  

### Variables Especiales
Predefinidas por Bash:   
- `$0`: Nombre del script.  
- `$1`, `$2`, ... `$n`: Argumentos pasados al script.  
- `$#`: Número de argumentos.   
- `$?`: Estado de salida del último comando (0 = éxito).  
- `$$`: PID del proceso actual.  
- `$!`: PID del último proceso en segundo plano.  



> [!note] `set -u`
> Activa el modo **"strict mode"** para variables no definidas:  
>
> - **Qué hace**: Si el script intenta usar una variable **no declarada**, Bash **falla inmediatamente** (en lugar de tratarla como vacía `""`).  
> - **Objetivo**: Evitar errores silenciosos por variables mal escritas o no inicializadas.  
> 
>  ```sh
> #!/bin/bash
>  set -u  # ¡Activa el modo estricto!
> 
>  echo "$variable_inexistente"  # ❌ Error: "variable_inexistente: unbound variable"
>  echo "Esto no se ejecutará."
>  ```
> Para desactivarlo
> 
>  ```sh
>  set +u
>  ``` 


### Arrays

Colecciones indexadas o asociativas (Bash ≥4.0).  

   ```bash
   # Array indexado
   frutas=("manzana" "banana" "naranja")
   echo "${frutas[1]}"  # Imprime "banana" (índice 1)

   # Array asociativo
   declare -A usuario
   usuario=([nombre]="Ana" [edad]=30)
   echo "${usuario[nombre]}"  # Imprime "Ana"
   ```
  
#### Array Indexado (lista ordenada)
**Sintaxis**:  
  ```bash
  frutas=("manzana" "banana" "cereza")  
  ```  
- **Características**:  
  - Acceso por posición numérica: `${frutas[0]}` → `"manzana"`.  
  - Ideal para listas simples.  
  - Operaciones comunes:  
    ```bash
    frutas+=("durazno")  # Añadir elemento  
    echo "${#frutas[@]}" # Contar elementos  
    ```

#### Array Asociativo** (diccionario clave-valor)
- **Sintaxis**:  
  ```bash
  declare -A edades=(["Alice"]=28 ["Bob"]=35)  
  ```  
- **Características**:  
  - Acceso por clave: `${edades["Alice"]}` → `28`.  
  - Perfecto para configuraciones o propiedades.  
  - Requiere `declare -A`.  

#### **Regla de Oro**:  
- **Usa comillas siempre** para evitar errores con espacios o caracteres especiales.  

---

### **Acceso a Variables:**
- **Sintaxis Básica:** `$nombre_variable` o `${nombre_variable}`.  
- **Uso de Llaves `{}`:** Obligatorias para evitar ambigüedades.  
  ```bash
   idioma="español"
   echo "Hola en ${idioma}es"  # Sin llaves: "Hola en español"
  ```

---

## **Sintaxis y Operadores Clave**

### Operadores Aritméticos

Uso: `$((expresión))` o `let` para asignaciones.  
```bash
a=5
b=3
suma=$((a + b))  # 8
let "resta = a - b"  # 2
```


| Operador | Descripción         |
| -------- | ------------------- |
| `+`      | Suma                |
| `-`      | Resta               |
| `*`      | Multiplicación      |
| `/`      | División entera     |
| `%`      | Módulo              |
| `**`     | Exponente (Bash ≥4) |


---

### Operadores de Comparación

**Para Números:**  
- `-eq`: Igual (`==`).  
- `-ne`: No igual (`!=`).  
- `-gt`: Mayor que (`>`).  
- `-lt`: Menor que (`<`).  
- `-ge`: Mayor o igual (`>=`).  
- `-le`: Menor o igual (`<=`).  

**Para Cadenas:**  
- `=`, `==`: Igualdad (no usan `$` dentro de `[[ ]]`).  
- `!=`: Desigualdad.  
- `>`: Mayor (orden lexicográfico).  
- `<`: Menor (orden lexicográfico).  
- `-z`: Cadena vacía.  
- `-n`: Cadena no vacía.  

```bash
if [[ $edad -gt 18 ]]; then
   echo "Mayor de edad"
fi

if [[ "$nombre" == "Ana" ]]; then
   echo "Hola Ana"
fi
```

---

### Operadores Lógicos

- `&&`: AND (en condiciones: `-a` en `[ ]`, `&&` en `[[ ]]`).  
- `||`: OR (en condiciones: `-o` en `[ ]`, `||` en `[[ ]]`).  
- `!`: NOT.  
```bash
# Ejemplo con [[ ]]
if [[ $edad -gt 18 && "$nombre" == "Ana" ]]; then
   echo "Ana es mayor de edad"
fi
```

---

## Estructuras de Control

### Condicionales: `if`, `elif`, `else`
```bash
if [[ -f "$archivo" ]]; then  # -f: verifica si es archivo regular
   echo "$archivo existe."
elif [[ -d "$archivo" ]]; then  # -d: verifica si es directorio
   echo "$archivo es un directorio."
else
   echo "No existe."
fi
```

---

### Ciclos: `for`, `while`, `until`

**`for` (estilo lista o C):**  
```bash
# Estilo lista
for fruta in "manzana" "banana" "naranja"; do
   echo "Fruta: $fruta"
done

# Estilo C
for ((i=0; i<5; i++)); do
   echo "Número: $i"
done
```

---


```bash
# Sintaxis básica
mi_array=("elemento1" "elemento2" "elemento3")

# También puedes declararlo así
mi_array=(
    "elemento1"
    "elemento2"
    "elemento3"
)

# O asignar valores por índice
mi_array[0]="primero"
mi_array[1]="segundo"
mi_array[2]="tercero"
```



#### 1. Iterar sobre todos los elementos:


```bash
for elemento in "${mi_array[@]}"
do
    echo "$elemento"
done
```

#### 2. Iterar con índice:

```bash
for i in "${!mi_array[@]}"
do
    echo "Índice: $i, Valor: ${mi_array[$i]}"
done
```

#### 3. Usando un for al estilo C:

```bash
for ((i=0; i<${#mi_array[@]}; i++))
do
    echo "${mi_array[$i]}"
done
```

#### Ejemplo completo

```bash
#!/bin/bash

# Definir un array
frutas=("manzana" "banana" "naranja" "uva")

# Iterar sobre los elementos
echo "Lista de frutas:"
for fruta in "${frutas[@]}"
do
    echo "- $fruta"
done

# Iterar con índices
echo "\nFrutas con sus índices:"
for i in "${!frutas[@]}"
do
    echo "Fruta $i: ${frutas[$i]}"
done
```

#### Notas importantes:
- `${array[@]}` expande a todos los elementos del array
- `"${array[@]}"` maneja correctamente elementos con espacios
- `${!array[@]}` devuelve los índices del array
- `${#array[@]}` devuelve el número de elementos en el array



---



**`while`:**  
```bash
contador=0
while [[ $contador -lt 5 ]]; do
   echo "Contador: $contador"
   ((contador++))
done
```

**`until`:**  
```bash
contador=5
until [[ $contador -eq 0 ]]; do
   echo "Contador: $contador"
   ((contador--))
done
```

---

### Selección: `case`

```bash
case "$fruta" in
   "manzana")
      echo "Es roja"
      ;;
   "banana")
      echo "Es amarilla"
      ;;
   *)  # Default
      echo "Fruta desconocida"
      ;;
esac
```


**Sintaxis Básica**

```bash
case "$variable" in
  patrón1)
    comando1
    ;;
  patrón2)
    comando2
    ;;
  *)
    comando_default
    ;;
esac
```

**Componentes:**
1. **`case "$variable" in`**: Inicia la estructura, comparando `$variable` con los patrones.
2. **Patrones**:
   - Pueden ser **texto literal** (`txt`), **comodines** (`*.sh`) o **regex** (con `extglob` activado).
   - `*)`: Patrón comodín para el caso default.
3. **`;;`**: Termina cada bloque de comandos (similar a `break` en otros lenguajes).
4. **`esac`**: Cierra la estructura (`case` al revés).

**Ejemplo 1: Validar opciones**

```bash
read -p "Elige (s/n): " opcion
case "$opcion" in
  s|S) echo "Sí" ;;
  n|N) echo "No" ;;
  *)   echo "Opción inválida" ;;
esac
```

**Ejemplo 2: Comparar con comodines**

```bash
case "$archivo" in
  *.txt) echo "Archivo de texto" ;;
  *.sh|*.bash) echo "Script Bash" ;;
  *) echo "Otro formato" ;;
esac
```




---

## Funciones

**Definición y Parámetros:**  
```bash
saludar() {
   local nombre=$1  # Variable local
   echo "Hola, $nombre"
}
saludar "Carlos"  # Llama a la función
```
- `$1`, `$2`, ...: Argumentos posicionales.  
- `$@`: Todos los argumentos como lista.  
- `$#`: Número de argumentos.  

---

## Manejo de Archivos y Redirección

**Operadores de Redirección:**  
- `>`: Sobrescribe archivo.  
- `>>`: Anexa a archivo.  
- `<`: Lee entrada desde archivo.  
- `2>`: Redirige stderr.  
- `&>`: Redirige stdout y stderr.  

**Ejemplos:**  
```bash
grep "error" /var/log/syslog > errores.txt  # Guarda salida en archivo
wc -l < errores.txt  # Cuenta líneas desde archivo
```

---

## Expansión y Comodines (Globbing)

- `*`: Cualquier cadena de caracteres.  
- `?`: Un solo carácter.  
- `[...]`: Cualquier carácter dentro de los corchetes.  
- `{a,b}`: Expansión de llaves (ej: `file.{txt,log}`).  

```bash
cp /var/log/*.log ./backup/  # Copia todos los .log
echo file{1..3}.txt  # Imprime file1.txt file2.txt file3.txt
```

---

## **7. Buenas Prácticas y Consejos**
1. **Comillas:**  
   - Usa `"` para evitar problemas con espacios: `echo "$nombre"`.  
   - Usa `'` para literales: `echo '$PATH'`.  

2. **Pruebas:**  
   - Usa `[[ ]]` en lugar de `[ ]`: Soporta más operadores y evita errores.  

3. **Variables no Definidas:**  
   - Usa `set -u` para detener el script si se usa una variable no definida.  

4. **Manejo de Errores:**  
   ```bash
   comando_riesgoso || { echo "Falló"; exit 1; }
   ```

---

## **Ejemplo Integrado: Script de Monitoreo**
```bash
#!/bin/bash
# Monitorea uso de disco y alerta si > 90%

set -u  # Detiene si hay variables no definidas

limite=90
disco="/dev/sda1"
uso=$(df -h | grep "$disco" | awk '{print $5}' | tr -d '%')

if [[ $uso -gt $limite ]]; then
   echo "ALERTA: Uso de disco $disco = ${uso}%" >&2  # >&2: stderr
   exit 1
else
   echo "OK: Uso de disco $disco = ${uso}%"
   exit 0
fi
```

---

#### **Resumen Final**
- **Variables:** Locales, de entorno, arrays.  
- **Operadores:** Aritméticos (`$(( ))`), comparación (`-eq`, `==`), lógicos (`&&`, `||`).  
- **Estructuras:** `if`, `for`, `while`, `case`, funciones.  
- **Manejo de Archivos:** Redirección (`>`, `<`), globbing (`*`, `?`).  
- **Buenas Prácticas:** Comillas, `[[ ]]`, manejo de errores.  

**Documentación Oficial:**  
```bash
man bash  # Manual completo en tu terminal
```



---

# Miscelánea

## `shift N`

El comando **`shift N`** se utiliza en scripts de Bash para **eliminar los primeros `N` argumentos posicionales** y **desplazar los restantes hacia la izquierda**, modificando así los valores de `$1`, `$2`, `$@` y `$#`.

---

```bash
shift [N]  # Si no se especifica N, por defecto es 1.
```

**Efectos:**
1. **Elimina los primeros `N` argumentos** (desaparecen de la lista).
2. **Reenumera los argumentos restantes**:
   - `$1` pasa a ser el argumento que originalmente estaba en `$N+1`.
   - `$2` pasa a ser `$N+2`, y así sucesivamente.
3. **Actualiza las variables especiales**:
   - `$@` y `$*`: Ahora contienen solo los argumentos restantes.
   - `$#`: Disminuye en `N` (el nuevo total de argumentos).

---

#### **📌 Ejemplos Prácticos**

**1. `shift 1` (Comportamiento por Defecto)**

```bash
#!/bin/bash
echo "Antes del shift:"
echo "\$1 = $1, \$2 = $2, \$3 = $3"
echo "Todos los argumentos: $@"
echo "Total: $#"

shift 1  # Elimina $1 y desplaza el resto

echo "Después del shift 1:"
echo "\$1 = $1, \$2 = $2"  # $1 ahora es el antiguo $2
echo "Argumentos restantes: $@"
echo "Total restante: $#"
```

**Si se ejecuta:**
```bash
./script.sh A B C
```

**Salida:**
```
Antes del shift:
$1 = A, $2 = B, $3 = C
Todos los argumentos: A B C
Total: 3

Después del shift 1:
$1 = B, $2 = C
Argumentos restantes: B C
Total restante: 2
```

---

**2. `shift 2` (Eliminar Dos Argumentos)**

```bash
#!/bin/bash
echo "Antes del shift:"
echo "\$1 = $1, \$2 = $2, \$3 = $3"

shift 2  # Elimina $1 y $2, $3 pasa a ser $1

echo "Después del shift 2:"
echo "\$1 = $1"  # Ahora es el antiguo $3
echo "Argumentos restantes: $@"
echo "Total restante: $#"
```

**Si se ejecuta:**
```bash
./script.sh X Y Z
```

**Salida:**
```
Antes del shift:
$1 = X, $2 = Y, $3 = Z

Después del shift 2:
$1 = Z
Argumentos restantes: Z
Total restante: 1
```

---

**3. `shift` sin Argumentos (Equivalente a `shift 1`)**

```bash
shift  # Igual que shift 1
```

---

# ## **📌 Casos de Uso Comunes**

**1. Procesamiento de Argumentos en Bucles**  
   Útil para iterar sobre argumentos en un `while`:
   ```bash
   while [ "$#" -gt 0 ]; do
       echo "Argumento actual: $1"
       shift 1  # Avanza al siguiente
   done
   ```

**2. Ignorar Opciones Ya Procesadas**  
   Ejemplo típico en scripts que manejan flags (`-f`, `-v`, etc.):
   ```bash
   if [ "$1" = "-v" ]; then
       VERBOSE=true
       shift 1  # Elimina el flag "-v" para que $1 ahora sea el siguiente argumento
   fi
   ```

**3. Descartar Argumentos Innecesarios**  
   Si solo te interesan los argumentos desde la posición `N+1`:
   ```bash
   shift 3  # Descarta los primeros 3 argumentos
   echo "Argumentos útiles: $@"
   ```

---

**📌 Resumen**

| Comando    | Efecto                                                |
| ---------- | ----------------------------------------------------- |
| `shift`    | Elimina `$1` (equivalente a `shift 1`).               |
| `shift 1`  | Elimina el primer argumento (`$1`).                   |
| `shift N`  | Elimina los primeros `N` argumentos (`$1` a `$N`).    |
| `shift $#` | Elimina **todos** los argumentos (útil para limpiar). |

---
