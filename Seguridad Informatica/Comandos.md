


**Gestión de archivos y directorios**
- [[#📁 `ls`]]
- [[#🔍 `find`]]
- [[#📄 `cat`]]
- [[#💬 `echo`]]

**Procesamiento de texto**
- `sed` - Editor de flujo  
- `sed 's/old/new/g'` - Reemplazo global  
- `sed -n '5,10p'` - Muestra líneas 5-10  

- `awk` - Procesamiento avanzado  
- `awk '{print $1}'` - Muestra primera columna  
- `awk 'NR==100'` - Muestra línea 100  

- `sort`/`uniq` - Ordenar y filtrar únicos  
- `uniq -d`: Muestra duplicados  
- `uniq -u`: Muestra únicos  

- [[#🔍 `grep`]]
- [[#🔁 `uniq`]]
- [[#✂️ `sed`]]
- [[#🧑‍💻 `read`]]
- [[#✂️ `cut`]]
- [[#📥`tail`]]

**Redirecciones y tuberías**
- `>` - Sobrescribe archivo  
- `>>` - Añade al final  
- `2>` - Redirige errores  
- `|` - Conecta comandos  
- `cat log.txt | grep "error" | wc -l`  


**Comprensión/Archivos**
- `tar` - Archivos .tar  
- `-xvf`: Extraer  
- `-cvf`: Crear  
- `unzip` - Archivos ZIP  
- `gzip`/`gunzip` - Compresión gzip  

- [[#📦 `tar`]]
- [[#🗜️ `unzip`]]
 


**Permisos y usuarios**
- `chmod` - Cambia permisos  
- `chmod 755 archivo`  
- `chown` - Cambia dueño  
- `sudo` - Ejecutar como root  
- `sudo -u usuario comando`  

**Redes y conexiones**
- `curl` - Transferencia web  
- `curl -H "Header: valor" URL`  
- `curl -X POST -d "data" URL`  
- `wget` - Descargas web  
- `ssh` - Conexión remota  
- `ssh -i clave.pem user@host -p 2222`  
- `scp` - Copia segura  
- `scp -P 2222 archivo user@host:/ruta`  

- [[#🌐 `curl`]]



**Variables y entorno**
- `env` - Muestra variables  
- `export` - Crea variables  
- `printenv` - Lista variables  

**Procesos y sistema**
- `ps` - Procesos activos  
- `ps aux | grep proceso`  
- `top`/`htop` - Monitor sistema  
- `kill` - Terminar procesos  
- `kill -9 PID`  


**Herramientas especiales**
- `base64` - Codificación Base64  
- `base64 -d` para decodificar  
- `xxd` - Hexdump  
- `xxd -r` para revertir hex  
- `file` - Identifica tipo archivo  
- `strings` - Extrae texto de binarios  

- [[#🧵 `strings`]]
- [[#🔧 `xxd`]]
- [[#🔧 `file`]]
- [[#🔧 `base64`]]

**Comandos para pentesting**
- `hydra` - Fuerza bruta  
- `hydra -l user -P dicc.txt ssh://host`  
- `john` - Crackeo hashes  
- `john --format=md5crypt hash.txt`  
- `exiftool` - Metadatos imágenes  
- `binwalk` - Análisis de binarios  


**Otros**

- [[#🛠️ `diff`]]
- [[#🛠️ `exiftool`]]
## Comodines
- `*` : El comodín asterisco representa cualquier carácter de cualquier longitud
- ``?`` : El comodín interrogación representa un solo carácter
- ``[ ]`` : El comodín corchete es utilizado para un intervalo de caracteres
- ``{ }`` : El comodín llaves es utilizado para representar una lista de opciones
- ``touch`` : Puede ser utilizado para crear archivos vacíos
- ``cat`` : Muestra el contenido de un archivo binario o texto.


## 📁 `ls`

Lista los archivos de un directorio

- `-d` : Lista los nombres del directorio
- `-a` : Lista todos los archivos (inclusive los ocultos) de un directorio. 
- `-l` : Formato largo  
- `-h` : Muestra el tamaño de los archivos en KB, MB, GB.
- `-r` : Invierte el orden de clasificación.
- `-t` : Clasifica por la hora de modificación, los más nuevos primero 
- `-R` : Lista subdirectorios de manera recursiva


## 🔍 `find`

`find` es una herramienta de búsqueda muy poderosa en Unix/Linux que permite:

- Buscar archivos o directorios
- Aplicar filtros por nombre, tamaño, tipo, permisos, fechas, etc.
- Ejecutar comandos sobre los resultados

Todo esto puede hacerse de forma recursiva y muy precisa.

```bash
find [ruta] [opciones] [expresión]
```

**Ejemplo:**

```bash
find . -name "*.txt"
```

Esto busca todos los archivos que terminan en `.txt` **en el directorio actual y sus subdirectorios**.

---

### 🔩 Opciones y expresiones más usadas en `find`

#### `-name` — buscar por nombre (sensible a mayúsculas)

```bash
find . -name "archivo.txt"
```

📌 Busca el archivo "archivo.txt" a partir del directorio actual (`.`).
📌 Si queremos buscar desde el directorio raíz usaríamos `/`

---

#### `-iname` — buscar por nombre (ignora mayúsculas)

```bash
find . -iname "archivo.txt"
```

📌 Igual que `-name` pero no distingue entre mayúsculas/minúsculas.

---

#### `-type` — buscar por tipo

```bash
find . -type f      # Solo archivos
find . -type d      # Solo directorios
```

📌 Sirve para filtrar por tipo de archivo. Los más comunes son:

- `f`: archivo normal
- `d`: directorio
- `l`: enlace simbólico

---

#### `-size` — buscar por tamaño

```bash
find . -size +1M       # Archivos de más de 1 MB
find . -size -500k     # Archivos de menos de 500 KB
```

📌 Sufijos:

- `c` bytes
- `k`: kilobytes
- `M`: megabytes
- `G`: gigabytes

Usa `+` para “mayor que” y `-` para “menor que”.
Para búsquedas exactas no se pone prefijos.

---

#### `-perm` — buscar por permisos

```bash
find . -perm 644
find . -perm -111       # Archivos ejecutables por todos
```

📌 Puedes usar permisos exactos (ej. 644) o con guiones:

- `-` antes del número: cualquier combinación que contenga esos permisos.

---

#### `-user` y `-group` — buscar por propietario

```bash
find /home -user juan
find . -group desarrolladores
```

📌 Filtra archivos por su dueño o grupo.

---

#### `-mtime`, `-atime`, `-ctime` — por fechas

```bash
find . -mtime -7        # Modificados hace menos de 7 días
find . -atime +30       # Accedidos hace más de 30 días
```

📌 Sufijos:

- `-mtime`: por fecha de modificación
- `-atime`: por fecha de último acceso
- `-ctime`: por cambio en metadatos

---

#### `-exec` — ejecutar comandos sobre los resultados

```bash
find . -name "*.log" -exec rm {} \;
```

📌 Explicación:

- `-exec`: permite ejecutar un comando sobre cada archivo encontrado
- `{}`: representa el archivo encontrado
- `\;`: termina el comando (¡importante!)

---

### 💾 Redirigir salida a archivo o usar con `xargs`

```bash
find . -name "*.log" > lista.txt        # Guarda la lista en un archivo
find . -name "*.log" | xargs rm         # Elimina todos los archivos listados
```

📌 `xargs` ejecuta `rm` sobre cada línea de la salida del `find`.

---

### 🧪 Ejemplo completo

Supón que quieres borrar todos los archivos `.tmp` modificados hace más de 10 días en tu carpeta `Documentos`:

```bash
find ~/Documentos -name "*.tmp" -mtime +10 -exec rm {} \;
```

Resultado: elimina todos los archivos temporales viejos.

---

### 🧠 Trucos y combinaciones

#### ✅ 1. **Buscar archivos modificados en la última hora**

```bash
find . -mmin -60
```

#### 🔍 Explicación:

- `-mmin`: como `-mtime`, pero en minutos.
- `-60`: menos de 60 minutos desde la última modificación.

💡 Útil para scripts que detectan cambios recientes.

---

#### ✅ 2. **Buscar archivos vacíos**

```bash
find . -type f -empty
```

#### 🔍 Explicación:

- `-type f`: solo archivos
- `-empty`: tamaño 0 (vacíos)

💡 Sirve para limpiar archivos sin contenido.

---

#### ✅ 3. **Buscar y mover archivos grandes**

```bash
find . -type f -size +100M -exec mv {} /ruta/de/respaldo/ \;
```

#### 🔍 Explicación:

- Busca archivos de más de 100 MB
- Los mueve a otra carpeta para liberar espacio

💡 Ideal para administración de discos.




## 📄 `cat`

`cat` significa **concatenate** (concatenar). Es una herramienta básica y poderosa que se usa en Unix/Linux para:

- Mostrar el contenido de archivos
- Unir varios archivos en uno solo
- Redirigir contenido hacia otros archivos

```bash
cat [opciones] archivo(s)
```

---

### 📂 Ejemplo básico

```bash
cat archivo.txt
```

📌 Muestra en pantalla (stdout) el contenido completo de `archivo.txt`.

---

### 🔩 Opciones más comunes

#### `-n` — numerar las líneas

```bash
cat -n archivo.txt
```

📌 Muestra el contenido del archivo **con números de línea** al inicio de cada una.

---

#### `-b` — numerar solo las líneas **no vacías**

```bash
cat -b archivo.txt
```

📌 Similar a `-n`, pero **omite la numeración** en las líneas vacías.

---

#### `-s` — suprimir líneas vacías repetidas

```bash
cat -s archivo.txt
```

📌 Si hay **varias líneas vacías seguidas**, solo deja **una**.

---

#### `-E` — mostrar el carácter de fin de línea (`$`)

```bash
cat -E archivo.txt
```

📌 Útil para ver **saltos de línea**. Agrega un `$` al final de cada línea.

---

### 📦 Concatenar archivos

```bash
cat archivo1.txt archivo2.txt
```

📌 Muestra el contenido de ambos archivos, uno tras otro.

---

### 💾 Redirigir el contenido a otro archivo

```bash
cat archivo1.txt archivo2.txt > combinado.txt
```

📌 Une los contenidos de `archivo1.txt` y `archivo2.txt`, y **guarda** el resultado en `combinado.txt`.

---

### 🧪 Ejemplo completo

Supón que tienes dos archivos:

**saludo.txt**
```
Hola
```

**nombre.txt**
```
Camila
```

Y ejecutas:
```bash
cat saludo.txt nombre.txt > mensaje.txt
```

El archivo `mensaje.txt` quedará así:

```
Hola
Camila
```

---

### 🧠 Trucos y combinaciones

#### ✅ 1. **Ver el contenido de múltiples archivos rápidamente**

```bash
cat *.log
```

🔍 Muestra todos los archivos `.log` juntos.

---

#### ✅ 2. **Combinar con `grep` para filtrar contenido**

```bash
cat archivo.txt | grep 'clave'
```

🔍 Muestra solo las líneas de `archivo.txt` que contienen `"clave"`.

🧠 Aunque no siempre es necesario usar `cat` con `grep`, puede ayudarte en combinaciones más complejas.

---

#### ✅ 3. **Crear un archivo desde la terminal**

```bash
cat > nuevo.txt
```

🔍 Empiezas a escribir directamente desde la terminal. Cuando termines, presiona `Ctrl + D` para guardar.

---







## 💬 `echo`

`echo` es un **comando simple pero muy útil en Unix/Linux** que sirve para:

- Mostrar texto o variables en la terminal
- Escribir contenido en archivos
- Mostrar el resultado de comandos en scripts

Se usa todo el tiempo para depurar, imprimir resultados o simplemente dar formato a la salida en la terminal.

```bash
echo [opciones] [texto o variable]
```

---

### ✏️ Ejemplo básico

```bash
echo "Hola mundo"
```

📌 Imprime en pantalla: `Hola mundo`

---

### 🔩 Usos comunes de `echo`

#### ✅ 1. **Mostrar variables**

```bash
nombre="Alice"
echo $nombre
```

📌 Imprime: `Alice`

> 💡 Ojo: sin el `$` solo muestra el nombre de la variable, no su contenido.

---

#### ✅ 2. **Concatenar texto con variables**

```bash
usuario="bob"
echo "Hola, $usuario"
```

📌 Salida: `Hola, bob`

---

#### ✅ 3. **Escribir en un archivo**

```bash
echo "clave123" > secreto.txt
```

📌 Crea el archivo `secreto.txt` con el contenido `clave123`.

> ⚠️ Esto **sobrescribe** el archivo si ya existe.

---

#### ✅ 4. **Agregar texto al final de un archivo**

```bash
echo "otra línea" >> secreto.txt
```

📌 Añade `otra línea` al final de `secreto.txt`, sin borrar lo anterior.

---

#### ✅ 5. **Mostrar cadenas con caracteres especiales**

```bash
echo -e "Hola\nMundo"
```

📌 Salida:

```
Hola
Mundo
```

> 🔹 La opción `-e` **activa caracteres especiales** como:

|Secuencia|Significado|
|---|---|
|`\n`|Nueva línea|
|`\t`|Tabulación (tab)|
|`\\`|Barra invertida (`\`)|
|`\"`|Comillas dobles|

---

#### ✅ 6. **Imprimir sin salto de línea final**

```bash
echo -n "Sin salto"
```

📌 No agrega una nueva línea al final de la salida.

---

### 💡 Trucos útiles

#### 📁 Mostrar el contenido de una variable con texto formateado

```bash
archivo="documento.txt"
echo "El archivo es: $archivo"
```

#### 💻 Mostrar el resultado de un comando

```bash
echo "Hoy es: $(date)"
```

📌 Imprime: `Hoy es: Lun Abr 7 14:32:01 UTC 2025`

---

### 🧠 Resumen

|Opción|Función|
|---|---|
|`-e`|Habilita caracteres especiales|
|`-n`|No imprime el salto de línea|
|`>`|Escribe en archivo (sobrescribe)|
|`>>`|Agrega al final de archivo|

---

Si necesitas que te lo adapte a un caso de uso real (por ejemplo, dentro de un CTF o script), dime y te doy un ejemplo concreto 💻





## 🔍 `grep`

`grep` es un comando de Linux que sirve para **buscar texto dentro de archivos**. Su nombre viene de _“Global Regular Expression Print”_. Es muy poderoso porque permite encontrar líneas que coincidan con una **cadena de texto** o una **expresión regular**.

```bash
grep [opciones] "patrón" [archivo...]
```

---

### 🔩 Opciones y expresiones más usadas en `grep`

#### `-i` — ignorar mayúsculas y minúsculas

```bash
grep -i "error" archivo.txt
```

📌 Encuentra todas las líneas que contengan "error", "Error", "ERROR", etc.

---

#### `-r` o `-R` — búsqueda recursiva en carpetas

```bash
grep -r "clave" ./carpeta
```

📌 Busca el texto en todos los archivos dentro de la carpeta y subcarpetas.

---

#### `-n` — mostrar el número de línea

```bash
grep -n "clave" archivo.txt
```

📌 Muestra el número de la línea donde se encuentra la coincidencia.

---

#### `-v` — invertir la coincidencia

```bash
grep -v "clave" archivo.txt
```

📌 Muestra las líneas que **no** contienen el patrón.

---

#### `-c` — contar coincidencias

```bash
grep -c "clave" archivo.txt
```

📌 Solo muestra el número de líneas que coinciden con el patrón.

---

#### `-l` — mostrar solo nombres de archivos con coincidencias

```bash
grep -l "clave" *.txt
```

📌 Útil para saber en qué archivos aparece un patrón.

---

#### `-o` — mostrar solo la parte que coincide

```bash
grep -o "error" archivo.txt
```

📌 Muestra únicamente las palabras que coinciden, no la línea completa.

---

#### `-E` — usar expresiones regulares extendidas

```bash
grep -E "error|fail" archivo.txt
```

📌 Permite usar `|`, `+`, `{}`, etc., sin necesidad de escaparlos con `\`.

---

### 💾 Usos comunes

#### ✅ 1. **Buscar una palabra específica en un archivo**

```bash
grep "error" archivo.txt
```

🔍 **Explicación**:

- Busca todas las líneas que contengan la palabra “error”.
---

#### ✅ 2. **Buscar sin importar mayúsculas/minúsculas**

```bash
grep -i "warning" archivo.txt
```

🔍 **Explicación**:

- Coincide con “warning”, “Warning”, “WARNING”, etc.

---

#### ✅ 3. **Buscar en múltiples archivos a la vez**

```bash
grep "main" *.c
```

🔍 **Explicación**:

- Muestra las líneas donde aparece “main” en todos los archivos `.c`.

---

#### ✅ 4. **Buscar en todo un directorio (recursivo)**

```bash
grep -r "password" /etc
```

🔍 **Explicación**:

- Busca la palabra "password" dentro de todos los archivos en `/etc` y sus subdirectorios.

---

### 🧠 Trucos y combinaciones

#### ✅ 1. **Combinar con `ps` para buscar procesos**

```bash
ps aux | grep firefox
```

🔍 **Explicación**:

- Muestra solo los procesos relacionados con "firefox".

💡 Súper útil para ver si un proceso está corriendo.

---

#### ✅ 2. **Filtrar resultados que no contienen algo**

```bash
grep -v "DEBUG" log.txt
```

🔍 **Explicación**:

- Muestra todas las líneas del log que **no** contienen la palabra "DEBUG".

---

#### ✅ 3. **Buscar múltiples palabras (usando regex extendida)**

```bash
grep -E "error|fail|warning" archivo.log
```

🔍 **Explicación**:

- Encuentra líneas que contengan **cualquiera** de las palabras.

---

### 🧠 Tip extra: combinar con `--color=auto`

```bash
grep --color=auto "palabra" archivo.txt
```

📌 Resalta en color las coincidencias, ¡más fácil de ver!

---



## 🔁 `uniq`

`uniq` es un comando en Unix/Linux que se utiliza para **eliminar duplicados de una lista** o **mostrar solo los valores que aparecen una vez**. Funciona generalmente con la entrada ordenada, ya que solo detecta duplicados consecutivos.

```bash
uniq [opciones] [archivo]
```

---

### 🔩 Opciones y expresiones más usadas en `uniq`

#### `-d` — mostrar solo las líneas duplicadas

```bash
uniq -d archivo.txt
```

📌 Muestra solo las líneas que se repiten consecutivamente en el archivo.

#### `-u` — mostrar solo las líneas únicas (sin duplicados)

```bash
uniq -u archivo.txt
```

📌 Muestra solo las líneas que **no** están duplicadas consecutivamente.

#### `-c` — mostrar el conteo de repeticiones

```bash
uniq -c archivo.txt
```

📌 Muestra cuántas veces aparece cada línea en el archivo.

Ejemplo de salida:

```
  3 line1
  2 line2
  1 line3
```

📌 El número al principio de cada línea indica cuántas veces se repite esa línea.

#### `-i` — ignorar mayúsculas y minúsculas

```bash
uniq -i archivo.txt
```

📌 Hace que el comando ignore las diferencias entre mayúsculas y minúsculas al comparar las líneas.

#### `-f N` — omitir las primeras N columnas

```bash
uniq -f 2 archivo.txt
```

📌 Omitirá las primeras N palabras o columnas en cada línea al comparar, útil cuando solo te interesa comparar parte de la línea.

#### `-s N` — omitir los primeros N caracteres

```bash
uniq -s 2 archivo.txt
```

📌 Omite los primeros N caracteres de cada línea al comparar.

#### `-w N` — comparar solo los primeros N caracteres

```bash
uniq -w 5 archivo.txt
```

📌 Solo compara los primeros N caracteres de cada línea. Esto es útil cuando solo te interesa una parte de la línea para verificar duplicados.

---

### 💾 Usos comunes

#### ✅ 1. **Eliminar líneas duplicadas consecutivas**

```bash
sort archivo.txt | uniq
```

🔍 **Explicación**:

- `sort`: ordena el archivo.
- `uniq`: elimina las líneas duplicadas consecutivas.

💡 Esto es útil cuando necesitas eliminar duplicados de un archivo sin importar el orden original.

#### ✅ 2. **Contar el número de veces que aparece cada línea**

```bash
sort archivo.txt | uniq -c
```

🔍 **Explicación**:sort

- `sort`: ordena el archivo.
- `uniq -c`: cuenta las repeticiones de cada línea.

💡 Es útil cuando quieres ver la frecuencia de las líneas en un archivo.

#### ✅ 3. **Ver solo las líneas duplicadas**

```bash
sort archivo.txt | uniq -d
```

🔍 **Explicación**:

- `sort`: ordena el archivo.
- `uniq -d`: muestra solo las líneas duplicadas.

💡 Esto te ayuda a identificar qué elementos están repetidos en un archivo.

---

### 🧠 Trucos y combinaciones

#### ✅ 1. **Eliminar líneas duplicadas en un archivo y guardarlo en otro archivo**

```bash
sort archivo.txt | uniq > archivo_sin_duplicados.txt
```

🔍 **Explicación**:

- `sort`: ordena el archivo.
- `uniq`: elimina duplicados.
- `>`: redirige la salida a un nuevo archivo.

💡 Ideal para crear una versión limpia de un archivo sin duplicados.

#### ✅ 2. **Usar `uniq` con entradas estándar**

```bash
echo -e "line1\nline1\nline2\nline3\nline3" | uniq
```

🔍 **Explicación**:

- `echo`: genera una entrada con saltos de línea.
- `uniq`: elimina duplicados consecutivos de la entrada.

💡 Útil cuando se trata de datos generados dinámicamente o desde una tubería.




## ✂️  `sed`

`sed` significa **Stream Editor**. Es una herramienta muy poderosa en Unix/Linux que sirve para:

- Buscar texto
- Reemplazar texto
- Insertar o borrar líneas
- Filtrar contenido

Todo esto se hace **sin abrir el archivo en un editor**, procesando el texto línea por línea (streaming).


```bash
sed [opciones] 'comando' archivo
```

**Ejemplo**:
```bash
sed 's/hola/HOLA/' archivo.txt
```

Esto busca la palabra "hola" y la reemplaza por "HOLA", pero **solo en la primera coincidencia de cada línea**, y **no modifica el archivo original**, solo lo muestra en pantalla.

---

### 🔩 Comandos más usados en `sed`

####  `s` — sustitución (substitute)

```bash
sed 's/patron/nuevo/' archivo
```

Reemplaza el **primer patrón** encontrado en cada línea.
**Opciones comunes para `s`:**

- `g`: reemplaza **todas** las coincidencias de la línea
- `i`: ignora mayúsculas y minúsculas

📌 Ejemplos:

```bash
sed 's/hola/adiós/' archivo.txt         # Reemplaza la primera ocurrencia por línea
sed 's/hola/adiós/g' archivo.txt        # Reemplaza todas las ocurrencias por línea
sed 's/hola/adiós/gi' archivo.txt       # Reemplaza sin importar mayúsculas y todas las ocurrencias
```

---
####  `-n` — no imprimir automáticamente

```bash
sed -n 'p' archivo.txt
```

El flag `-n` le dice a `sed` que **no imprima nada a menos que se lo ordenes con `p` (print)**.

📌 Ejemplo útil:

```bash
sed -n '3p' archivo.txt     # Imprime solo la línea 3
```

---

#### `d` — eliminar (delete)

```bash
sed '2d' archivo.txt        # Borra la línea 2
sed '1,3d' archivo.txt      # Borra desde la línea 1 a la 3
sed '/error/d' archivo.txt  # Borra todas las líneas que contengan "error"
```

---

#### `i` — insertar antes de una línea

```bash
sed '3i\Línea nueva' archivo.txt
```

📌 Inserta una nueva línea antes de la línea 3.

---

#### `a` — añadir después de una línea

```bash
sed '3a\Línea añadida' archivo.txt
```

📌 Inserta una nueva línea después de la línea 3.

---

#### `c` — cambiar línea

```bash
sed '3c\Texto nuevo' archivo.txt
```

📌 Cambia el contenido **completo** de la línea 3 por "Texto nuevo".

---

#### `r archivo2` — leer contenido de otro archivo e insertarlo

```bash
sed '/aquí/r otroarchivo.txt' archivo.txt
```

📌 Inserta el contenido de `otroarchivo.txt` después de cada línea que contenga "aquí".

---

#### `w archivo_salida.txt` — escribir coincidencias en otro archivo

```bash
sed -n '/error/w errores.txt' archivo.txt
```

📌 Guarda en `errores.txt` todas las líneas que contienen "error".

---

### 💾 Cómo modificar directamente un archivo

Usa la opción `-i` (**in-place**):

```bash
sed -i 's/hola/adiós/g' archivo.txt
```

Esto sí **modifica directamente el archivo**.

⚠️ Usa con cuidado. Para hacer copia de seguridad:

```bash
sed -i.bak 's/hola/adiós/g' archivo.txt
# Crea una copia llamada archivo.txt.bak
```

---

### 🧪 Ejemplo completo

Supón que tienes este archivo `frutas.txt`:

```
manzana
banana
cereza
manzana
```

Y ejecutas:

```bash
sed 's/manzana/kiwi/g' frutas.txt
```

Resultado:

```
kiwi
banana
cereza
kiwi
```

---

### 🧠 Trucos y combinaciones


#### ✅ 1. **Reemplazar varias cosas a la vez**

```bash
sed -e 's/hola/adiós/' -e 's/mundo/planeta/' archivo.txt
```

#### 🔍 Explicación:

- `-e` permite usar **varias expresiones de `sed` en una sola línea**.
- `'s/hola/adiós/'` reemplaza la **primera ocurrencia** de "hola" por "adiós" en cada línea.
- `'s/mundo/planeta/'` reemplaza la **primera ocurrencia** de "mundo" por "planeta" en cada línea.

💡 **Resultado esperado**: Si tienes una línea como:

```
hola mundo
```

Se transforma en:

```
adiós planeta
```

---

#### ✅ 2. **Eliminar líneas vacías**

```bash
sed '/^$/d' archivo.txt
```

#### 🔍 Explicación:

- `/^$/`: esto es una **expresión regular** que significa "línea vacía".
    
    - `^` = inicio de línea.
    - `$` = fin de línea.
    - Si no hay nada entre ellos, es una línea vacía.
- `d`: elimina la línea si coincide con el patrón.


💡 **Resultado esperado**: Si tienes:

```
hola

mundo
```

Después del comando:

```
hola
mundo
```

Se eliminó la línea vacía.

---

#### ✅ 3. **Mostrar solo líneas que **NO** contienen un patrón**

```bash
sed -n '/error/!p' archivo.txt
```

#### 🔍 Explicación:

- `-n`: suprime la impresión automática.
- `/error/`: busca líneas que contienen "error"
- `!p`: el **signo de exclamación** `!` significa **"no coinciden"**, y `p` imprime.
    - Entonces: “**Imprime las líneas que NO contienen la palabra 'error'**”.

💡 **Ejemplo**: Archivo:

```
todo bien
error en la línea 2
continúa
```

Resultado:

```
todo bien
continúa
```

---



## 🧑‍💻 `read`

`read` es un **comando interno de Bash** que se utiliza para **leer una línea de entrada desde el teclado (stdin)** o desde un archivo línea por línea. Se usa frecuentemente en scripts para capturar datos ingresados por el usuario o para recorrer archivos línea a línea.

```bash
read [opciones] variable
```

**Ejemplo simple:**

```bash
read nombre
```

📌 Espera que el usuario escriba algo y presione ENTER.  
📌 El valor se guarda en la variable `nombre`.

---

### 🔩 Opciones más usadas con `read`

#### `-p` — mostrar un mensaje antes de leer

```bash
read -p "¿Cuál es tu nombre? " nombre
```

📌 Muestra un mensaje al usuario antes de recibir el input.

---

#### `-s` — modo silencioso (oculta lo que se escribe)

```bash
read -s -p "Introduce tu contraseña: " clave
```

📌 Útil para contraseñas. Lo que escribes **no se ve** en pantalla.

---

#### `-t` — tiempo límite para esperar input (en segundos)

```bash
read -t 5 -p "Responde rápido: " respuesta
```

📌 Espera solo 5 segundos. Si no se escribe nada, `read` termina.

---

#### `-n` — número de caracteres a leer

```bash
read -n 1 -p "Presiona una tecla para continuar..."
```

📌 Captura solo 1 carácter y no espera ENTER.

---

#### `-a` — guardar en un array

```bash
read -a palabras
```

📌 Divide la entrada en palabras separadas por espacios y las guarda en un array llamado `palabras`.

---

#### `-r` — no interpreta backslashes como caracteres especiales

```bash
read -r linea
```

📌 Evita que `\n`, `\t`, `\\`, etc. sean interpretados.  
💡 Muy útil al leer archivos línea por línea.

---

### 🧪 Ejemplo completo de uso con archivo

Supón que tienes un archivo `nombres.txt`:

```txt
Juan
Ana
Luis
```

Puedes recorrerlo así:

```bash
while IFS= read -r nombre; do
  echo "Hola $nombre"
done < nombres.txt
```

📌 `IFS=` evita que se recorten espacios al inicio/final.  
📌 `-r` evita que las barras invertidas se interpreten.  
📌 `< nombres.txt` indica que lea desde ese archivo.

---

### 🧠 Trucos y buenas prácticas

#### ✅ Leer múltiples variables

```bash
read nombre edad ciudad
```

📌 Si escribes: `Lucía 23 Lima`, se asigna:

- `nombre=Lucía`
    
- `edad=23`
    
- `ciudad=Lima`
    

---

#### ✅ Leer línea con espacios

```bash
read -r linea
```

📌 Así puedes leer frases completas o líneas de texto tal cual están.

---

### 🧾 Resumen

|Opción|Función|
|---|---|
|`-p`|Muestra mensaje antes de leer|
|`-s`|Oculta el input (modo silencioso)|
|`-t`|Tiempo límite para ingresar datos|
|`-n`|Leer solo cierta cantidad de caracteres|
|`-a`|Guarda entrada en un array|
|`-r`|No interpreta caracteres especiales|

---

	



## ✂️ `cut`

`cut` es un comando de línea de comandos en Linux/Unix que se utiliza para **extraer secciones específicas de cada línea de un archivo o entrada estándar (stdin)**, como por ejemplo **campos delimitados por un carácter** o **ciertos rangos de caracteres o bytes**.

🧰 **Sintaxis básica**

```bash
cut [opciones] [archivo]
```

También puede leer de `stdin`:

```bash
echo "texto" | cut [opciones]
```

---

**🔑 Opciones más comunes**

|Opción|Significado|
|---|---|
|`-b` N|Selecciona el byte número N (o rango de bytes)|
|`-c` N|Selecciona el carácter número N (o rango de caracteres)|
|`-f` N|Selecciona el campo número N (usado con `-d`)|
|`-d` DELIM|Define el delimitador de campos (por defecto es tabulador `\t`)|
|`--complement`|Muestra lo que **no** fue seleccionado|
|`--output-delimiter=DELIM`|Cambia el delimitador de salida entre campos seleccionados|

---

### 📌 Ejemplos detallados

**1. 🔤 Extraer ciertos *caracteres***

```bash
echo "abcdef" | cut -c 1-3
```

📤 **Salida:** `abc`

✅ Extrae del carácter 1 al 3.

---

**2. 🔢 Extraer ciertos *bytes***

```bash
echo "áéíóú" | cut -b 1-3
```

⚠️ Los caracteres con tilde ocupan más de un byte. Esto puede generar cortes incorrectos.

---

**3. 📊 Extraer *campos* de un archivo delimitado por comas**

Supongamos que `datos.csv` contiene:

```
Juan,25,Perú
Ana,30,Chile
Luis,28,Argentina
```

```bash
cut -d ',' -f 1 datos.csv
```

📤 **Salida:**

```
Juan
Ana
Luis
```

✅ Extrae el **primer campo** usando coma como delimitador.

---

**4. 🧩 Extraer *múltiples campos**

```bash
cut -d ',' -f 1,3 datos.csv
```

📤 **Salida:**

```
Juan,Perú
Ana,Chile
Luis,Argentina
```

---

**5. 👇 Usar entrada estándar**

```bash
echo "uno:dos:tres" | cut -d ':' -f 2
```

📤 **Salida:** `dos`

---

**6. 🧪 Complemento (inverso)**

```bash
echo "123456789" | cut -c 1-3 --complement
```

📤 **Salida:** `456789`

✅ Excluye los caracteres 1 al 3.


### 📚 Tips adicionales

- No puedes combinar `-b`, `-c` y `-f` al mismo tiempo.
    
- Si el archivo no tiene el delimitador que defines con `-d`, la línea entera se muestra tal cual.
    
- Si estás trabajando con archivos CSV complejos (con campos entrecomillados o con comas dentro del campo), `cut` **no es suficiente**. Es mejor usar `awk` o `csvkit`.
    


### 📌 Resumen visual

| ¿Qué quieres extraer? | Opción que usas |
| --------------------- | --------------- |
| Bytes                 | `-b`            |
| Caracteres            | `-c`            |
| Campos delimitados    | `-f -d`         |

---






¡Claro! Aquí tienes una **explicación completa, clara y práctica del comando `tail`** en Linux/Ubuntu, siguiendo el mismo estilo estructurado:

---

## 📥`tail`

`tail` es un comando en Linux que se utiliza para **mostrar las últimas líneas de un archivo de texto o entrada estándar**. Es muy útil para monitorear **logs en tiempo real**, ver el final de archivos grandes o depurar salidas.

---

**Sintaxis básica**

```bash
tail [opciones] [archivo]
```

O con `stdin`:

```bash
comando | tail [opciones]
```



**🔑 Opciones más comunes**

|Opción|Descripción|
|---|---|
|`-n N`|Muestra las últimas **N líneas** (por defecto son 10 líneas)|
|`-f`|**Sigue** el archivo en tiempo real (útil para logs)|
|`-F`|Igual que `-f`, pero **reabre** el archivo si se renombra o reemplaza|
|`-c N`|Muestra los últimos **N bytes** del archivo|
|`--pid=PID`|Termina `-f` cuando finalice el proceso con ese PID|
|`--retry`|Vuelve a intentar abrir archivos que no existen inicialmente|

---

### 📌 Ejemplos prácticos

**1. 📄 Ver las últimas 10 líneas de un archivo (por defecto)**

```bash
tail archivo.txt
```

---

**2. 🔢 Ver las últimas 20 líneas**

```bash
tail -n 20 archivo.txt
```

✅ Útil si solo te interesa el final de un archivo de logs.

---

**3. 🧪 Ver los últimos 100 *bytes***

```bash
tail -c 100 archivo.txt
```

---

**4. 🧵 Seguir un archivo en *tiempo real***

```bash
tail -f /var/log/syslog
```

📤 Esto imprimirá las nuevas líneas que se agreguen al final del archivo.

---

**5. 🧠 Seguir un archivo que podría ser reemplazado (como logs de rotación)**

```bash
tail -F /var/log/nginx/access.log
```

✅ A diferencia de `-f`, `-F` **reabre** el archivo si es reemplazado.

---

**6. 📡 Leer salida de otro comando**

```bash
dmesg | tail -n 5
```

✅ Muestra las últimas 5 líneas del buffer del kernel.

---

**🚀 Tip útil: Combinación con otros comandos**

Ver logs de un servicio en vivo

```bash
journalctl -u nginx.service -f
```

_(Aunque este no es `tail`, hace algo similar usando `-f`)_

---

### 📚 Resumen visual

|Quieres...|Comando|
|---|---|
|Ver últimas 10 líneas|`tail archivo.txt`|
|Ver últimas N líneas|`tail -n N archivo.txt`|
|Ver últimos N bytes|`tail -c N archivo.txt`|
|Ver en tiempo real|`tail -f archivo.txt`|
|Seguir y reabrir archivo|`tail -F archivo.txt`|

---



¡Claro! Aquí tienes la explicación del comando `head` en Linux/Ubuntu:

---

## 🔼 `head`

`head` es un comando que se usa para **mostrar las primeras líneas de un archivo o entrada estándar (stdin)**. Por defecto, muestra las primeras 10 líneas.


**🧰 Sintaxis básica**

```bash
head [opciones] [archivo]
```

También se puede usar con tuberías:

```bash
comando | head [opciones]
```



**🔑 Opciones más comunes**

|Opción|Descripción|
|---|---|
|`-n N`|Muestra las **primeras N líneas** del archivo|
|`-c N`|Muestra los **primeros N bytes** del archivo|
|`-q`|No imprime los nombres de archivo (en múltiples)|
|`-v`|Siempre imprime los nombres de archivo|

---

### 📌 Ejemplos prácticos

**1. 📄 Mostrar las primeras 10 líneas de un archivo (por defecto)**

```bash
head archivo.txt
```

---

**2. 🔢 Mostrar las primeras 5 líneas**

```bash
head -n 5 archivo.txt
```

---

**3. 📦 Mostrar los primeros 50 bytes**

```bash
head -c 50 archivo.txt
```

---

**4. 📂 Usar con varios archivos**

```bash
head archivo1.txt archivo2.txt
```

✅ Muestra el encabezado de cada archivo por separado.

---

**5. 📡 Leer salida de otro comando**

```bash
ls -l | head -n 3
```

✅ Muestra las primeras 3 líneas de la salida del comando `ls -l`.

---

**📚 Resumen visual**

|Quieres...|Comando|
|---|---|
|Ver primeras 10 líneas|`head archivo.txt`|
|Ver primeras N líneas|`head -n N archivo.txt`|
|Ver primeros N bytes|`head -c N archivo.txt`|

---





## 📦 `tar`

`tar` (Tape ARchiver) es un comando de Unix/Linux utilizado para **empaquetar múltiples archivos en un solo archivo**. Muy útil para **crear backups, comprimir archivos** o **extraer contenido**. No siempre comprime por sí solo, pero puede combinarse con `gzip`, `bzip2`, `xz`, etc.

```bash
tar [opciones] [archivo.tar] [archivos/directorios]
```

---

### 🔩 Opciones y expresiones más usadas en `tar`

#### `-c` — crear un archivo `.tar`

```bash
tar -cf archivo.tar carpeta/
```

📌 Crea un nuevo archivo `.tar` con el contenido de la carpeta.

---

#### `-x` — extraer (descomprimir) un archivo `.tar`

```bash
tar -xf archivo.tar
```

📌 Extrae el contenido del archivo `.tar` en el directorio actual.

---

#### `-t` — listar el contenido de un archivo `.tar`

```bash
tar -tf archivo.tar
```

📌 Muestra los archivos que contiene el archivo `.tar` sin extraerlos.

---

#### `-v` — modo detallado (verbose)

```bash
tar -cvf archivo.tar carpeta/
```

📌 Muestra los archivos que se están añadiendo o extrayendo. Útil para ver el progreso.

---

#### `-f` — especificar el archivo tar (obligatorio en casi todos los usos)

```bash
tar -cf backup.tar archivo.txt
```

📌 Define el nombre del archivo resultante `.tar`. Siempre debe ir al final de las opciones.

---

#### `-z` — comprimir o descomprimir con `gzip` (`.tar.gz` o `.tgz`)

```bash
tar -czf archivo.tar.gz carpeta/
```

📌 Crea un archivo `.tar.gz` (comprimido con gzip).

---

#### `-j` — comprimir o descomprimir con `bzip2` (`.tar.bz2`)

```bash
tar -cjf archivo.tar.bz2 carpeta/
```

📌 Crea un archivo `.tar.bz2` (comprimido con bzip2).

---

#### `-J` — comprimir o descomprimir con `xz` (`.tar.xz`)

```bash
tar -cJf archivo.tar.xz carpeta/
```

📌 Crea un archivo `.tar.xz` (comprimido con xz).

---

### 💾 Usos comunes

#### ✅ 1. **Crear un archivo `.tar.gz` con una carpeta**

```bash
tar -czvf backup.tar.gz carpeta/
```

🔍 **Explicación**:

- `-c`: crear
    
- `-z`: comprimir con gzip
    
- `-v`: mostrar lo que hace
    
- `-f`: nombre del archivo
    

💡 Muy útil para respaldos.

---

#### ✅ 2. **Extraer un archivo `.tar.gz`**

```bash
tar -xzvf backup.tar.gz
```

🔍 Extrae el contenido del archivo comprimido `.tar.gz`.

---

#### ✅ 3. **Listar el contenido de un `.tar` sin extraerlo**

```bash
tar -tvf archivo.tar
```

🔍 Muestra qué archivos contiene el archivo `.tar`.

---

#### ✅ 4. **Extraer solo un archivo específico dentro de un `.tar`**

```bash
tar -xvf archivo.tar ruta/dentro/del/tar.txt
```

🔍 Extrae solo el archivo o carpeta que indiques.

---

#### ✅ 5. **Extraer en una carpeta específica**

```bash
tar -xvf archivo.tar -C /ruta/de/destino/
```

🔍 Extrae el contenido en la carpeta indicada.

---

### 🧠 Trucos y combinaciones

#### ✅ 1. **Crear y comprimir un archivo al vuelo**

```bash
tar -czf - carpeta/ | ssh user@host "cat > backup.tar.gz"
```

📌 Comprime una carpeta local y la guarda directamente en otra máquina por SSH.

---

#### ✅ 2. **Ver el contenido de un `.tar.gz` remoto sin descargarlo**

```bash
curl -s http://sitio.com/archivo.tar.gz | tar -tzf -
```

📌 Lista el contenido de un archivo comprimido sin necesidad de descargarlo primero.

---

### 📝 Resumen Visual

|Acción|Comando|
|---|---|
|Crear `.tar`|`tar -cf archivo.tar carpeta/`|
|Extraer `.tar`|`tar -xf archivo.tar`|
|Crear `.tar.gz`|`tar -czf archivo.tar.gz carpeta/`|
|Extraer `.tar.gz`|`tar -xzf archivo.tar.gz`|
|Ver contenido `.tar.gz`|`tar -tzf archivo.tar.gz`|
|Extraer en otro directorio|`tar -xf archivo.tar -C /ruta/`|

---



## 🗜️ `unzip`

`unzip` es un comando en Linux que se usa para **extraer archivos de un archivo `.zip`**.

Es compatible con archivos comprimidos en formato `.zip` y permite ver, listar, y descomprimir su contenido fácilmente desde la terminal.

```bash
unzip [opciones] archivo.zip
```

---

### 📂 Ejemplo básico

```bash
unzip archivo.zip
```

Descomprime todo el contenido de `archivo.zip` en el directorio actual.

---

### 🔩 Opciones más comunes

#### `-l` — listar el contenido del archivo zip

```bash
unzip -l archivo.zip
```

📌 Muestra una lista de archivos contenidos en `archivo.zip` sin descomprimirlos.

---

#### `-d` — especificar el directorio de destino

```bash
unzip archivo.zip -d carpeta_destino/
```

📌 Extrae los archivos dentro de `carpeta_destino/`.  Si la carpeta no existe, la crea.

---

#### `-o` — sobrescribir archivos sin preguntar

```bash
unzip -o archivo.zip
```

📌 Sobrescribe archivos existentes **automáticamente**, sin pedir confirmación.

---

#### `-n` — nunca sobrescribir archivos existentes

```bash
unzip -n archivo.zip
```

📌 No sobrescribe los archivos que ya existen. Los ignora.

---

#### `-q` — modo silencioso (quiet)

```bash
unzip -q archivo.zip
```

📌 Extrae sin mostrar mensajes en la terminal.

---

#### `-v` — modo detallado (verbose)

```bash
unzip -v archivo.zip
```

📌 Muestra información detallada de los archivos comprimidos (tamaños, fecha, etc.).

---

### 🧪 Ejemplo completo

Supón que tienes un archivo `proyecto.zip` con esta estructura:

```
main.py
readme.md
carpeta/datos.txt
```

Y ejecutas:

```bash
unzip proyecto.zip -d proyecto/
```

Resultado:

```
proyecto/main.py
proyecto/readme.md
proyecto/carpeta/datos.txt
```

---

### 🧠 Trucos y combinaciones

#### ✅ 1. **Extraer un solo archivo específico**

```bash
unzip archivo.zip nombre.txt
```

🔍 Extrae **solo `nombre.txt`** del `.zip`.

---

#### ✅ 2. **Extraer varios archivos usando patrones**

```bash
unzip archivo.zip '*.txt' '*.md'
```

🔍 Extrae solo los archivos `.txt` y `.md`.

⚠️ Para que funcione el comodín `*`, debes **poner las comillas**.

---

#### ✅ 3. **Extraer y sobrescribir silenciosamente en un directorio específico**

```bash
unzip -oq archivo.zip -d destino/
```

🔍 Extrae **sin mostrar nada** (`-q`) y **sobrescribiendo automáticamente** (`-o`).

---

### 🧨 Error común

```bash
bash: unzip: command not found
```

📌 Solución: instalar `unzip` con tu gestor de paquetes.

- En Debian/Ubuntu:
    

```bash
sudo apt install unzip
```

- En Red Hat/Fedora:
    

```bash
sudo dnf install unzip
```

---


## 🌐 `curl`

`curl` es un comando de línea en Unix/Linux usado para **transferir datos desde o hacia un servidor**, soportando múltiples protocolos como HTTP, HTTPS, FTP, etc. Es muy utilizado para **probar APIs**, **descargar archivos**, o **simular peticiones web** desde la terminal.

```bash
curl [opciones] [URL]
```

---

### 🔩 Opciones y expresiones más usadas en `curl`

#### `-X` — definir el método HTTP

```bash
curl -X POST http://localhost/api
```

📌 Define el método HTTP a usar (`GET`, `POST`, `PUT`, `DELETE`, etc.).

---

#### `-d` — enviar datos en el cuerpo de la solicitud

```bash
curl -X POST -d "nombre=Ana&edad=20" http://localhost/registro
```

📌 Envía datos tipo formulario. Se usa con `POST`, `PUT`, etc.

---

#### `-H` — agregar cabeceras HTTP

```bash
curl -H "Content-Type: application/json" http://localhost
```

📌 Añade cabeceras personalizadas como tipo de contenido, autenticación, etc.

---

#### `-A` — definir el User-Agent

```bash
curl -A "Mozilla/5.0" http://localhost
```

📌 Cambia la cabecera `User-Agent`, que identifica qué cliente está haciendo la solicitud.

💡 Por ejemplo:

```bash
curl -A "PARADISE" http://localhost/waiting.php
```

🔍 En este caso, `curl` le está diciendo al servidor que el cliente se llama `"PARADISE"`. Esto puede ser útil si el servidor **responde solo a ciertos User-Agents**, como en retos CTF o filtros web.

---

#### `-o` — guardar la salida en un archivo

```bash
curl -o salida.html http://localhost
```

📌 Guarda el contenido de la respuesta en un archivo.

---

#### `-s` — modo silencioso

```bash
curl -s http://localhost
```

📌 No muestra la barra de progreso ni mensajes innecesarios.

---

#### `-v` — modo verbose (detallado)

```bash
curl -v http://localhost
```

📌 Muestra todos los detalles de la solicitud y respuesta (cabeceras, conexión...).

---

#### `-L` — seguir redirecciones

```bash
curl -L http://acortador.com/x123
```

📌 Sigue automáticamente las redirecciones HTTP.

---

#### `-u` — autenticación básica

```bash
curl -u usuario:clave http://localhost/privado
```

📌 Autenticación HTTP básica (Basic Auth).

---

### 💾 Usos comunes

#### ✅ 1. **Hacer una solicitud GET simple**

```bash
curl http://localhost/index.html
```

🔍 Por defecto, `curl` usa `GET`.

---

#### ✅ 2. **Enviar datos con POST**

```bash
curl -X POST -d "usuario=juan" http://localhost/login
```

🔍 Envia datos al servidor como si fuera un formulario web.

---

#### ✅ 3. **Consumir una API con JSON**

```bash
curl -X POST -H "Content-Type: application/json" \
-d '{"nombre":"Luis"}' http://localhost/api
```

🔍 Envía un objeto JSON a una API REST.

---

#### ✅ 4. **Simular otro navegador con `-A`**

```bash
curl -A "Mozilla/5.0" http://localhost
```

🔍 Simula ser un navegador web real para evitar bloqueos.

---

#### ✅ 5. **Usar un User-Agent personalizado (por ejemplo, en CTFs)**

```bash
curl -A "PARADISE" http://localhost/waiting.php
```

🔍 A veces el servidor **solo responde si usas ese User-Agent exacto**.

---

#### ✅ 6. **Descargar un archivo con su nombre original**

```bash
curl -O http://localhost/archivo.zip
```

🔍 Guarda el archivo con el mismo nombre que tiene en el servidor.

---

### 🧠 Trucos y combinaciones

#### ✅ 1. **Ver solo el código de estado HTTP**

```bash
curl -s -o /dev/null -w "%{http_code}\n" http://localhost
```

📌 Útil para ver si el servidor responde `200 OK`, `404 Not Found`, etc.

---

#### ✅ 2. **Enviar cabeceras y datos con POST**

```bash
curl -X POST -H "Content-Type: application/json" \
-d '{"mensaje":"Hola"}' http://localhost/chat
```

📌 Interacción completa con una API REST.

---

#### ✅ 3. **Descargar y guardar el resultado directamente**

```bash
curl -o respuesta.json http://localhost/api/info
```

📌 Guarda la respuesta JSON en un archivo.

---

¿Te gustaría ahora ver ejemplos para cada método HTTP (`GET`, `POST`, `PUT`, `DELETE`) usando `curl`?




## 🧵 `strings`

El comando `strings` se utiliza para **extraer y mostrar las cadenas de texto legibles** de archivos binarios, ejecutables o cualquier archivo que contenga datos binarios mezclados con texto.

> 💡 Es especialmente útil en ingeniería inversa, análisis forense o CTFs (Capture The Flag).

```bash
strings [opciones] archivo
```

---

### 🔩 Opciones más usadas en `strings`

#### `-n <N>` — definir la longitud mínima de las cadenas

```bash
strings -n 6 archivo.bin
```

📌 Solo muestra cadenas de **al menos 6 caracteres**. Por defecto, el mínimo es 4.

---

#### `-t x` — mostrar la **posición en hexadecimal** donde se encuentra la cadena

```bash
strings -t x archivo.bin
```

📌 Muestra en qué **posición hexadecimal** del archivo comienza cada cadena encontrada.

---

#### `-e <enc>` — cambiar la codificación del archivo

```bash
strings -e l archivo.bin
```

📌 Cambia la codificación usada. Por ejemplo:

- `s` = single 7-bit (default)
- `S` = single 8-bit
- `b` = 16-bit big-endian
- `l` = 16-bit little-endian
    

---

#### `-f` — muestra el nombre del archivo antes de cada línea (útil con múltiples archivos)

```bash
strings -f *.bin
```

📌 Muestra el nombre del archivo antes de cada cadena encontrada.

---

### 💾 Usos comunes

#### ✅ 1. **Ver texto dentro de un ejecutable o binario**

```bash
strings programa.exe
```

🔍 Extrae las cadenas de texto que pueden dar pistas como comandos, rutas, mensajes de error, contraseñas embebidas, etc.

---

#### ✅ 2. **Buscar cadenas dentro de una imagen o archivo sospechoso**

```bash
strings imagen.jpg | grep flag
```

🔍 Se usa mucho en CTFs o análisis de malware para buscar palabras clave ocultas.

---

#### ✅ 3. **Filtrar cadenas por longitud**

```bash
strings -n 8 archivo.dat
```

🔍 Solo muestra cadenas de mínimo 8 caracteres. Útil para evitar “ruido” en la salida.

---

#### ✅ 4. **Buscar ubicaciones de cadenas en hexadecimal**

```bash
strings -t x archivo.so
```

🔍 Muestra en qué offset hexadecimal aparecen las cadenas, útil en análisis binario.

---

### 🧠 Trucos y combinaciones

#### ✅ 1. **Extraer texto de un ejecutable y guardarlo**

```bash
strings malware.exe > texto_extraido.txt
```

📌 Ideal para análisis posterior o para buscar patrones específicos con `grep`.

---

#### ✅ 2. **Buscar texto oculto en imágenes (esteganografía básica)**

```bash
strings foto.png | grep "CTF{"
```

📌 Algunos CTFs esconden banderas dentro de archivos PNG, JPG o incluso ZIP.

---

#### ✅ 3. **Buscar múltiples palabras clave en binarios**

```bash
strings archivo | grep -Ei "user|password|flag"
```

📌 Muy útil para encontrar credenciales o banderas ocultas.

---

### 📝 Resumen Visual

|Acción|Comando|
|---|---|
|Extraer texto de un archivo|`strings archivo`|
|Cadenas de mínimo 10 caracteres|`strings -n 10 archivo`|
|Mostrar offsets hexadecimales|`strings -t x archivo`|
|Buscar texto específico|`strings archivo|
|Extraer de varios archivos|`strings -f *.bin`|

---



## 🔬 `xxd`

El comando `xxd` en Linux es una herramienta para crear una **representación hexadecimal** de un archivo binario, o bien para convertir de hexadecimal a binario. Es muy útil para inspeccionar archivos en formato binario y para depuración o análisis de datos.

```bash
xxd [opciones] [archivo]
```

**Ejemplo:**

```bash
xxd archivo.bin
```

Esto generará una salida en formato hexadecimal del archivo `archivo.bin`.

---

### 🔩 Opciones más comunes en `xxd`

#### `-p` — formato "plain" (sin direcciones de memoria ni ASCII)

```bash
xxd -p archivo.bin
```

📌 Esta opción imprime el archivo en un formato más "limpio", sin la información adicional como las direcciones de memoria o la representación ASCII. Solo muestra los datos en formato hexadecimal.

---

#### `-r` — convertir de hexadecimal a binario

```bash
xxd -r archivo.hex
```

📌 Convierte un archivo en formato hexadecimal (como el generado por `xxd`) de nuevo a su forma binaria original.

---

#### `-c` — especificar cuántas columnas de bytes se muestran por línea

```bash
xxd -c 8 archivo.bin
```

📌 Controla cuántos bytes se muestran por línea. En este ejemplo, se mostrarán 8 bytes por línea en lugar de la configuración predeterminada.

---

#### `-g` — agrupar los bytes en unidades más grandes

```bash
xxd -g 2 archivo.bin
```

📌 Agrupa los bytes en unidades de mayor tamaño. En este caso, agrupará los bytes en pares de 2.

---

#### `-s` — empezar desde un desplazamiento específico

```bash
xxd -s 16 archivo.bin
```

📌 Comienza a mostrar el contenido desde un desplazamiento en bytes específico. En este ejemplo, comenzará desde el byte 16 (el primer byte es el 0).

---

### 💾 Ejemplo básico

Para ver el contenido de un archivo binario en formato hexadecimal:

```bash
xxd archivo.bin
```

Salida típica:

```text
0000000: 89 50 4e 47 0d 0a 1a 0a  00 00 00 0d 49 48 44 52  .PNG........IHDR
0000010: 00 00 00 02 00 00 00 02  08 02 00 00 00 d3 88 fd  ..............
```

Aquí, el comando muestra la **dirección de memoria** (`0000000`, `0000010`, ...) y la **representación hexadecimal** de los datos del archivo, además de la representación **ASCII** a la derecha (si es visible).

---

### 🧪 Ejemplo completo

Supón que tienes un archivo binario llamado `imagen.bin`, y quieres inspeccionar sus primeros 64 bytes en formato hexadecimal:

```bash
xxd -c 16 -s 0 imagen.bin
```

Esto mostrará los primeros 64 bytes del archivo (`-c 16` muestra 16 bytes por línea, y `-s 0` empieza desde el primer byte).

---

### 🧠 Trucos y combinaciones

#### ✅ 1. **Convertir de hexadecimal a binario**

Si tienes un archivo hexadecimal (`archivo.hex`) y quieres devolverlo a su formato binario:

```bash
xxd -r archivo.hex > archivo.bin
```

#### ✅ 2. **Inspeccionar una sección específica del archivo**

Si solo deseas ver una sección del archivo en formato hexadecimal (por ejemplo, a partir del byte 100):

```bash
xxd -s 100 archivo.bin
```

---


## 📄 `file`

**`file`** permite identificar el tipo de un archivo basándose en el contenido de dicho archivo, no solo en su extensión. Es útil porque a veces los archivos pueden tener extensiones incorrectas o no tenerlas, y aún así el comando puede decirte qué tipo de datos contienen.

```bash
file [archivo]
```

**Ejemplo:**

```bash
file eloise.jpg
```

Este comando examina el archivo `eloise.jpg` y te dice si realmente es una imagen JPEG, o si está corrupto o es de otro tipo.

---

### 🔩 Opciones comunes de `file`

#### `-i` — Mostrar el tipo MIME

```bash
file -i eloise.jpg
```

📌 Esto muestra el tipo MIME del archivo, que es una forma estándar de describir el tipo de archivo en internet (como `image/jpeg` o `text/plain`).

#### `-b` — Eliminar la ruta y solo mostrar el tipo de archivo

```bash
file -b eloise.jpg
```

📌 Esto solo muestra el tipo de archivo sin mostrar el nombre completo del archivo o la ruta.

#### `-f` — Leer una lista de archivos desde un archivo

```bash
file -f lista_de_archivos.txt
```

📌 Permite leer los nombres de los archivos desde un archivo de texto y mostrar el tipo de cada archivo en la lista.

---

### 🧪 Ejemplo completo

Imagina que tienes un archivo llamado `archivo.zip` y quieres saber qué tipo de archivo es. Usarías el siguiente comando:

```bash
file archivo.zip
```

Esto podría devolver algo como:

```
archivo.zip: Zip archive data, version 2.0, extracted by pkunzip
```

Si el archivo realmente es un archivo comprimido en formato ZIP, el comando te lo confirmará.

---

## 🔐 `base64`

El comando `base64` es una herramienta en sistemas Unix/Linux que se utiliza para **codificar y decodificar datos en formato Base64**. Este formato es comúnmente utilizado para representar datos binarios (como imágenes o archivos) en un formato textual que puede ser fácilmente transmitido a través de medios que solo aceptan texto, como correos electrónicos o algunas APIs.

```bash
base64 [opciones] [archivo]
```

---

### 🔩 Opciones y expresiones más usadas en `base64`

#### `-d` o `--decode` — decodificar en lugar de codificar

```bash
base64 -d archivo.txt
```

📌 Convierte datos que están codificados en Base64 de vuelta a su formato original.

---

#### `-i` — especificar el archivo de entrada

```bash
base64 -i archivo.txt
```

📌 Permite especificar el archivo que contiene los datos a codificar. Si no se utiliza esta opción, `base64` leerá desde la entrada estándar.

---

#### `-o` — especificar el archivo de salida

```bash
base64 -i archivo.txt -o archivo_codificado.txt
```

📌 Permite especificar un archivo donde guardar la salida del comando. Si no se usa esta opción, la salida será mostrada en la terminal.

---

#### `-w N` — especificar el número de caracteres por línea (para la codificación)

```bash
base64 -w 80 archivo.txt
```

📌 La opción `-w` permite definir el número de caracteres por línea en la salida codificada. El valor predeterminado es 76, pero se puede cambiar según sea necesario.

---

#### `-b` — limitar la codificación a un bloque de tamaño N

```bash
base64 -b 1024 archivo.txt
```

📌 Codifica los datos en bloques de tamaño específico, por ejemplo, 1024 bytes. Esto puede ser útil cuando se trabaja con grandes cantidades de datos.

---

### 💾 Usos comunes

#### ✅ 1. **Codificar un archivo en Base64**

```bash
base64 archivo.txt
```

🔍 **Explicación**:
- Codifica el archivo `archivo.txt` en Base64 y lo muestra en la terminal.


💡 Esto es útil cuando necesitas convertir datos binarios a un formato de texto para su transmisión.

#### ✅ 2. **Decodificar un archivo Base64 a su formato original**

```bash
base64 -d archivo_base64.txt > archivo_original.txt
```

🔍 **Explicación**:

- `-d`: decodifica el archivo codificado en Base64.
- La salida se guarda en `archivo_original.txt`.


💡 Esto es útil cuando recibes datos en Base64 y quieres restaurarlos a su formato original.

#### ✅ 3. **Codificar la salida de un comando**

```bash
echo "Texto a codificar" | base64
```

🔍 **Explicación**:

- `echo "Texto a codificar"`: genera la cadena de texto.
- `base64`: codifica esa cadena a formato Base64.

💡 Esto puede ser útil si necesitas codificar un texto rápidamente en la terminal.

---

### 🧠 Trucos y combinaciones

#### ✅ 1. **Codificar un archivo y guardarlo en un nuevo archivo**

```bash
base64 archivo.txt > archivo_codificado.txt
```

🔍 **Explicación**:

- Codifica el archivo y redirige la salida a `archivo_codificado.txt`.
    

💡 Esto es útil para almacenar los datos codificados sin mostrarlo en la terminal.

#### ✅ 2. **Decodificar un archivo Base64 y guardar la salida en un archivo binario**

```bash
base64 -d archivo_base64.txt > archivo_original.bin
```

🔍 **Explicación**:

- `-d`: decodifica el archivo Base64.
    
- `> archivo_original.bin`: redirige la salida decodificada a un archivo binario.
    

💡 Esto es útil cuando necesitas restaurar un archivo binario (como una imagen o archivo comprimido) que fue codificado en Base64.

#### ✅ 3. **Codificar una cadena larga con saltos de línea**

```bash
echo -e "Texto largo\ncon saltos de línea" | base64 -w 0
```

🔍 **Explicación**:

- `-w 0`: elimina los saltos de línea en la salida, manteniendo todo en una sola línea.
    

💡 Esto puede ser útil si necesitas un Base64 que sea de una sola línea sin interrupciones.

---

### 🧪 Ejemplo completo

Si tienes un archivo binario (por ejemplo, una imagen) y quieres enviarlo como texto (por ejemplo, por correo electrónico), puedes usar `base64` para codificarlo:

```bash
base64 imagen.png > imagen_base64.txt
```

Esto convierte la imagen en un archivo de texto que puedes enviar. La persona que reciba el archivo puede luego usar el comando `base64 -d` para restaurar la imagen a su formato original.

---

`base64` es muy útil para la transmisión de datos binarios en entornos que solo admiten texto, como correos electrónicos o servicios que no permiten adjuntos binarios.



## Ejemplos clave

```bash
# Buscar archivos modificados hace +1 año
find / -type f -mtime +365 -exec ls -lh {} \; 2>/dev/null

# Extraer línea específica (ej. línea 4069)
sed -n '4069p' archivo.txt
awk 'NR==4069' archivo.txt

# Monitorizar cambios en directorio
watch -n 1 "ls -lht /ruta"

# Descifrar contraseña en Base64
echo "U2VjcmV0QDEyMw==" | base64 -d

# Conexión SSH con forwarding
ssh -L 9001:localhost:80 user@host -p 2222
```

## Consejos adicionales
1. Usar `man comando` para ver manuales  
2. `command --help` muestra ayuda rápida  
3. `history` muestra últimos comandos  
4. `!!` repite último comando  
5. `Ctrl+R` busca en historial  
6. Usar `tab` para autocompletar 

```

Este bloque unificado contiene todos los comandos organizados por categorías, con sus opciones más útiles y ejemplos prácticos. ¿Necesitas que profundice en alguna sección en particular?
```



## 📊 `diff`

`diff` es un comando en Unix/Linux que se utiliza para **comparar línea por línea dos archivos** (o directorios) y mostrar sus diferencias.

> 💡 Es muy útil en programación, control de versiones y análisis de cambios entre archivos de texto.

```bash
diff [opciones] archivo1 archivo2
```

---

### 🔩 Opciones más usadas en `diff`

#### `-u` — formato unificado (unified diff)

```bash
diff -u original.txt modificado.txt
```

📌 Muestra las diferencias en un **formato más legible**, utilizado en `git` y parches.

Ejemplo:

```diff
--- original.txt
+++ modificado.txt
@@ -1,3 +1,3 @@
-Hola mundo
+Hola Linux
```

---

#### `-c` — formato contexto (context diff)

```bash
diff -c archivo1 archivo2
```

📌 Muestra diferencias con **líneas de contexto** antes y después del cambio. Ideal para leer manualmente.

---

#### `--side-by-side` — comparación lado a lado

```bash
diff --side-by-side archivo1 archivo2
```

📌 Muestra los archivos en **columnas paralelas**, útil para comparación visual.

---

#### `-i` — ignorar diferencias de mayúsculas

```bash
diff -i archivo1 archivo2
```

📌 Ignora diferencias entre mayúsculas y minúsculas.

---

#### `-w` — ignorar espacios en blanco

```bash
diff -w archivo1 archivo2
```

📌 Ignora **espacios y tabulaciones** al comparar líneas.

---

#### `-r` — comparar recursivamente directorios

```bash
diff -r dir1/ dir2/
```

📌 Compara todos los archivos dentro de dos directorios de forma recursiva.

---

### 💾 Usos comunes

✅ 1. **Comparar dos archivos de texto línea por línea**

```bash
diff archivo1.txt archivo2.txt
```

🔍 Muestra qué líneas están cambiadas, eliminadas o añadidas.

---

✅ 2. **Ver diferencias en estilo Git (unified)**

```bash
diff -u archivo1.txt archivo2.txt
```

🔍 Muy usado para crear parches o revisar cambios entre versiones de código.

---

✅ 3. **Ver cambios lado a lado**

```bash
diff --side-by-side archivo1.txt archivo2.txt
```

🔍 Ideal para comparar manualmente contenido similar.

---

✅ 4. **Ignorar cambios estéticos (espacios o mayúsculas)**

```bash
diff -iw archivo1.txt archivo2.txt
```

🔍 Útil para evitar falsos positivos en comparaciones de texto.

---

✅ 5. **Comparar dos carpetas completas**

```bash
diff -r carpeta_original/ carpeta_nueva/
```

🔍 Muestra qué archivos se modificaron, agregaron o eliminaron entre dos estructuras de directorio.

---

### 🧠 Trucos y combinaciones

✅ 1. **Crear un parche (patch) de cambios**

```bash
diff -u original.txt modificado.txt > cambios.patch
```

📌 Puedes aplicar ese parche con el comando `patch` después.

---

✅ 2. **Usar `diff` con archivos HTML o código fuente**

```bash
diff -u index_v1.html index_v2.html
```

📌 Detecta modificaciones precisas en líneas de código.

---

✅ 3. **Comparar múltiples archivos con un bucle**

```bash
for file in *.txt; do diff -q carpeta1/$file carpeta2/$file; done
```

📌 Compara archivos con el mismo nombre en dos carpetas distintas.

---

### 📝 Resumen Visual

|Acción|Comando|
|---|---|
|Comparar archivos|`diff archivo1 archivo2`|
|Formato Git / parche|`diff -u archivo1 archivo2`|
|Comparación lado a lado|`diff --side-by-side archivo1 archivo2`|
|Ignorar mayúsculas y espacios|`diff -iw archivo1 archivo2`|
|Comparar carpetas|`diff -r carpeta1/ carpeta2/`|

---

## 🧰 `exiftool`

`exiftool` es una poderosa herramienta de línea de comandos usada para **leer, escribir y editar metadatos** en archivos multimedia, especialmente imágenes. Es compatible con muchos formatos como JPG, PNG, MP4, PDF, entre otros.

```bash
exiftool [opciones] archivo
```

> 📌 **Metadatos**: Son datos incrustados dentro de un archivo que describen su contenido. Por ejemplo, una foto puede contener información como la cámara usada, la fecha de captura o la ubicación GPS.

---

### 🔩 Opciones más usadas en `exiftool`

#### 📖 Leer metadatos de un archivo

```bash
exiftool imagen.jpg
```

📌 Muestra todos los metadatos disponibles de la imagen.

---

#### `-a` — mostrar todos los metadatos, incluso los duplicados

```bash
exiftool -a imagen.jpg
```

📌 Muestra **todos los metadatos posibles**, incluso si están repetidos bajo diferentes nombres.

---

#### `-s` — salida en formato compacto (solo etiquetas y valores)

```bash
exiftool -s imagen.jpg
```

📌 Muestra los nombres técnicos de las etiquetas sin descripciones largas.

---

#### `-G` — agrupar etiquetas por sistema (EXIF, IPTC, XMP, etc.)

```bash
exiftool -G imagen.jpg
```

📌 Muestra de qué grupo de metadatos proviene cada campo.

---

#### `-DateTimeOriginal` — mostrar solo una etiqueta específica

```bash
exiftool -DateTimeOriginal imagen.jpg
```

📌 Muestra solo la **fecha de captura original** de la imagen.

---

#### `-overwrite_original` — sobrescribir archivo original al editar

```bash
exiftool -overwrite_original -Comment="Nueva descripción" imagen.jpg
```

📌 Evita que se cree una copia de respaldo `.jpg_original`.

---

#### `-GPSLatitude`, `-GPSLongitude` — extraer ubicación GPS

```bash
exiftool -GPSLatitude -GPSLongitude imagen.jpg
```

📌 Muestra la ubicación donde se tomó la foto (si está disponible).

---

### 💾 Usos comunes

✅ 1. **Ver toda la información de una imagen**

```bash
exiftool selfie.jpg
```

🔍 Muestra desde tipo de lente, ISO, hora, hasta la app con la que fue tomada.

---

✅ 2. **Editar metadatos de una imagen**

```bash
exiftool -Artist="Nombre del autor" imagen.jpg
```

🔍 Inserta el nombre del fotógrafo o autor en los metadatos.

---

✅ 3. **Eliminar metadatos sensibles**

```bash
exiftool -all= imagen.jpg
```

🔍 Borra todos los metadatos (incluidos los GPS), dejando solo la imagen en sí.

---

✅ 4. **Extraer ubicación GPS**

```bash
exiftool -n -GPSLatitude -GPSLongitude imagen.jpg
```

🔍 Te da las coordenadas numéricas exactas para usar en mapas.

---

✅ 5. **Renombrar archivos por fecha de captura**

```bash
exiftool '-FileName<DateTimeOriginal' -d "%Y-%m-%d_%H-%M-%S.%%e" *.jpg
```

🔍 Cambia el nombre de los archivos a algo como `2025-05-03_14-21-00.jpg`.

---

### 🧠 Trucos y combinaciones

✅ 1. **Ver solo etiquetas importantes**

```bash
exiftool -Model -Make -ExposureTime -FNumber imagen.jpg
```

📌 Extrae solo datos técnicos relevantes de fotografía.

---

✅ 2. **Editar varios archivos a la vez**

```bash
exiftool -Copyright="Mi nombre" *.jpg
```

📌 Cambia o añade metadatos en todos los archivos JPG del directorio.

---

✅ 3. **Guardar salida en un archivo de texto**

```bash
exiftool imagen.jpg > metadatos.txt
```

📌 Muy útil para analizar los datos con calma o compartirlos.

---

### 📝 Resumen Visual

|Acción|Comando|
|---|---|
|Ver todos los metadatos|`exiftool archivo.jpg`|
|Borrar todos los metadatos|`exiftool -all= archivo.jpg`|
|Extraer coordenadas GPS|`exiftool -GPSLatitude -GPSLongitude archivo.jpg`|
|Añadir autor|`exiftool -Artist="Tu nombre" archivo.jpg`|
|Editar sin backup|`-overwrite_original`|

	
---

