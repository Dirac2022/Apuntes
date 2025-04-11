
Tipos de jerarquía en git
- Sistema: para la computadora
- Global: para el mismo usuario
- Local: para repositorios


# Configuraciones básicas
Configuraciones a nivel global

```shell
git config --global user.name "nombre"
```

```shell
git config --global user.email "daronmitchel@gmail.com"
```

Lista de configuraciones 
```shell
git config --list
```

Lista de configuraciones globales
```shell
git config --global --list
```

Agregar editor de texto
```shell
git config --global core.editor "code --wait"
```


>[!tip] comando --wait
> Espera a que se cierre la ventana para realizar los cambios, por ejemplo si se esta trabajando en un editor

Activar el coloreado en la salida de la terminal, para que la información sea más legible
```shell
git config --global color.ui true
```


Para configurar el salto de línea y retorno de carro automático (Windows)
```shell
git config --global core.autocrlf true
```

Para Linux/Mac
```shell
git config --global core.autocrlf input
```

# Areas
### Repositorio
- **Definición:** Es el lugar donde Git almacena toda la información relacionada con tu proyecto, incluyendo el historial de cambios, configuraciones, y los commits.
- **Características:**
  - Contiene la carpeta `.git`, que guarda toda la metadata y el historial.
  - Puede ser **local** (en tu máquina) o **remoto** (en un servidor como GitHub).
  - Es el lugar donde se manejan las ramas, los tags, y todos los objetos de Git.

### Directorio de Trabajo (Working Directory)
- **Definición:** Es el directorio en tu sistema de archivos donde trabajas directamente con los archivos de tu proyecto. Aquí es donde creas, editas y eliminas archivos.
- **Características:**
  - Contiene la versión más reciente del proyecto desde el último checkout.
  - Los archivos aquí pueden estar en tres estados:
    - **Modificados:** Cambios realizados pero no aún añadidos al área de preparación (staging area).
    - **Preparados:** Cambios añadidos al área de preparación.
    - **Confirmados:** Cambios guardados en el repositorio con un commit.

### Área de Preparación (Staging Area)
- **Definición:** Es una especie de "área intermedia" donde se guardan los cambios antes de confirmarlos (hacer commit).
- **Características:**
  - Permite que prepares varios cambios juntos antes de guardarlos en el repositorio.
  - Los cambios en el área de preparación no afectan al repositorio hasta que se hace un commit.

| Área                                          | Definición                                                    | Función Principal                                              |
| --------------------------------------------- | ------------------------------------------------------------- | -------------------------------------------------------------- |
| **Repositorio**                               | Almacén central de todo el historial del proyecto             | Guarda la historia de cambios, gestiona ramas y objetos de Git |
| **Directorio de Trabajo (Working Directory)** | Carpeta en el sistema de archivos donde trabajas directamente | Donde se crean, modifican y eliminan archivos                  |
| **Área de Preparación (Staging Area)**        | Zona intermedia antes de confirmar cambios                    | Permite agrupar y preparar cambios para el commit              |

### Repositorio Remoto
- **Definición:** Es una copia del repositorio que se encuentra en un servidor externo.
- **Características:**
  - Se utiliza para compartir el proyecto con otros colaboradores.
  - Ejemplos incluyen GitHub, GitLab, Bitbucket.
  - Se sincroniza con el repositorio local mediante comandos como `git push` y `git pull`.

# Estados
En Git, los archivos pasan por diferentes **estados** antes de ser guardados en el historial. Los 3 estados principales son

#### Modified
- Significa que has editado un archivo, pero Git aún no lo está rastreando para un commit.
- Se muestra en `git status` como `modified`
- No está listo para ser guardado en el historia
 
#### Staged
Preparado para un **commit** o "Indexado"
- Significa que el archivo modificado ya está listo para ser guardado en el próximo commit.
- Se logra con `git add <archivo>`
- Se muestra en `git status` como `staged`

#### Committed
Archivo guardado en el historial
- Significa que los cambios en el área de [[#Área de Preparación (Staging Area)|staging]] fueron guardados en el historial del repositorio
- Se logra con `git commit -m "Mensaje del commit"`
- Después de un commit, los cambios quedan seguros en el repositorio local



# Crear repositorio

```shell
mkdir repo
```

```shell
cd repo
```

Inicializar git dentro de la carpeta `repo`
```shell
git init
```
1. Crea un subdirectorio oculto llamada `.git`, don de se almacenan todos los archivos y configuraciones del repositorio
2. Convierte la carpeta en un repositorio Git, lo que permite rastrear cambios en los archivos
3. Si ya es un repositorio Git, `git init` lo reinicializa sin perder historial.

### Agregando un archivo al Staging Area

Agregar el archivo creado `archivo.txt` al *Staging Area* 
```git
git add archivo.txt
```


>[!info] Propósito de del comando `add`
>**Añadir archivos al área de preparación (staging area):** `git add` mueve los cambios que has hecho en tus archivos desde el árbol de trabajo (working directory) al área de preparación (staging area). Solo los archivos que están en el área de preparación se incluirán en el próximo commit.

> [!tip]
> Si solo se coloca `git add .` se agregan todos los archivos de la 
> Si se tiene otro archivo, por ejemplo archivo2.txt se pueden agregar ambos archivos dejando un espacio entre ellos  `git add archivo.txt archivo2.txt`

##  `git status`
Se utiliza para obtener información sobre el estado actual del repositorio, mostrando los cambios que se han hecho, pero que aún no han sido confirmados, y cualquier archivo que no esté bajo control de versiones.

Nos muestra información sobre nuestro directorio de trabajos y el area de preparación
```shell
git status
```

### Salidas del comando `git status`
- **En la rama actual:** Indica en qué rama estás trabajando.
- **Sin cambios para confirmar:** Indica que no hay cambios que puedan ser confirmados.
- **Cambios que no han sido confirmados:** Muestra los archivos que han sido modificados pero no se han agregado al área de preparación.
- **Archivos listos para ser confirmados:** Muestra los archivos en el área de preparación listos para ser confirmados.
- **Archivos no rastreados:** Lista los archivos que no están bajo control de versiones.
- **Indicaciones adicionales:** Puede mostrar mensajes sobre cómo sincronizar con el repositorio remoto, conflictos de fusión, etc.


>[!info] Variaciones
> - `git status -s` : Nos muestra una salida más compacta y fácil de leer. -  Si esta en verde, esta agregado al *Staging* y esta listo para commit. Si esta en rojo, no esta agregado al *Staging*
> 	-  `M`   : archivo modificado
> 	- `A` : archivo agregado al área de preparación o *Staging*
> 	- `??` : Archivo no rastreado
> - `git status -b` : Muestra información adicional sobre la rama actual y su relación con la rama remota.
> Si esta en verde, esta agregado al *Staging* y esta listo para commit
> Si esta en rojo, no esta agregado al *Staging*


Remover el archivo del *Staging Area*
```shell
git rm --cached archivo.txt
```
Se usa para eliminar un archivo del área de **[[#Área de Preparación (Staging Area)|staging]]**, pero sin borrarlo físicamente del sistema de archivos.


## `git commit`
Este comando se usa para guardar los cambios en el historial del repositorio.

Guarda solo los archivos que fueron agregaron a **[[#Área de Preparación (Staging Area)|staging]]** con `git add`
```shell
git commit -m "Mensaje"
```

Hace un commit de todos los archivos modificados y rastreados (tracked). No necesita `git add` pero no incluirá archivos nuevos (untracked).
```shell
git commit -m "mensaje" -a
```

### Ejemplo

Para subir un archivo al repositorio 
- Agregando un mensaje en el commit
```shell
git commit -m "Agregando los dos primeros archivos de texto"
```

- Agregando un mensaje con el editor de texto
Si tenemos un archivo adicional `archivob.txt`
```shell
git add archivob.txt
git commit
```

Luego nos abriría automáticamente vscode por la configuración `git config --global core.editor "core --wait"` Agregamos un mensaje y cerramos el editor. Con esto se completara el commit.

Pasar archivos del Working Directory al Repositorio
```git
git commit -a 
```

# Restore, checkout

## Eliminando un archivo del repositorio
Eliminar archivo `archivob.txt` del repo
```shell
rm archivob.txt
```

Luego, tenemos dos opciones, usar `git add` para actualizar los cambios o `git restore` para descartar los cambios en el directorio de trabajo

Agregamos la eliminación
```shell
git add archivob.txt
git commit -m "eliminando archivo" -a
```

## Restaurar un archivo modificado o borrado
Si se ha eliminado un archivo `archivo.txt` (por ejemplo manualmente) del directorio de trabajo
```shell
git restore archivo.txt
```

Con esto restauras el archivo del área de preparación. También sirve para restaurar el archivo a la ultima versión en la que se hizo commit

>[!warning] `git restore` no restaura el archivo si este no ha sido rastreado por git, es decir, si no se hizo un `git add` con el archivo en cuestión, si se llega a borrar, el comando `git restore` no lo podrá recuperar.

Si hemos hecho un cambio en un determinado archivo `archivo.txt` y hemos guardado el archivo en cuestión, usando `checkout` podemos restaurar el archivo a la ultima versión en la que se le hizo commit
```shell
git checkout archivo.txt
```

Para restaurar un archivo modificado y que **se ha subido al area de *Staging* con `git add`**
```git
git reset --hard
```
Esto realiza una restauración extrema donde se descartan los archivos agregados al area de *Staging*. Ya que con `git checkout` no funcionaría la restauración.

>[!info] Efectos de `git reset --hard`
>- **Área de Trabajo:** El área de trabajo se restablece para que coincida exactamente con el commit objetivo, lo que significa que todos los archivos en tu directorio de trabajo se revertirán a ese estado. Cualquier cambio no confirmado se perderá.
>    
>- **Área de Preparación:** El área de preparación también se restablece para que coincida con el commit objetivo. Cualquier cambio que estaba en staging pero no fue confirmado se perderá.


## Cambiar nombre a un archivo

Si queremos cambiar el archivo `dirac.txt` a `archivo2.txt`
```shell
git mv dirac.txt archivo2.txt
```
Al usar el comando `status` saldrá un archivo al que se le ha renombrado y esta listo para el `commit`
```shell
git commit -m "Cambio de nombre de dirac a archivo2" -a
```

> [!tip]
> Si cambiamos el nombre de un archivo y hacemos `checkout` con el nombre anterior, el comando `checkout` reestablece este archivo anterior, mientras que el el archivo con el nuevo nombre permanece inalterado.

# `git show`
Se utiliza para mostrar información detallada sobre objetos en Git como commits, árboles o blobs.

Se puede usar para mostrar la información del archivo dado su ultimo commit
```shell
git show archivo.txt
```

# `git diff`
Muestra las diferencias entre archivos en distintas etapas del repositorio
- Archivos modificados pero no agregados al staging (`git diff`)
- Archivos en staging comparados con el último commit (`git diff --staged`)
- Diferencias entre dos commits específicos (`git diff commit1 commit2`)
- Diferencias entre una rama y otra (`git diff main feature`)

**Ejemplo** Ver diferencias entre commits específicos
Supón que `archivo.txt` ha cambiado en diferentes commits y queremos ver cómo cambió entre dos versiones
```shell
git diff abc1234 def5678 -- archivo.txt
```

Salida esperada
```shell
diff --git a/archivo.txt b/archivo.txt
index e69de29..83c99ab 100644
--- a/archivo.txt
+++ b/archivo.txt
@@ -1 +1 @@
-Hola, este es un archivo de prueba.
+Hola, este es un documento de prueba.
```

Si en vez colocamos `git diff abc1234 def5678` nos muestra las diferencias entre los archivos que se actualizaron con los dos commits
## `git diff --name-only`
Muestra solo los nombres de los archivos que se han modificado que no se han agregado al staging area.

**Ejemplo**
Si modifico el archivo `archivo1.txt` y lo guardo. Al realizar
```shell
git diff --name-only
```
Me mostrara
```shell
archivo1.txt
```


## `git diff --word-diff`
Comparar cambios palabra por palabra. El comando muestra diferencias a nivel de palabras en lugar de líneas completas.


# `git log`
Este comando muestra una lista detallada de los commits en el historial, incluyendo
- Hash del commit
- Autor del commit
- Fecha y hora
- Mensaje del commit

```shell
git log
```

**Ejemplo**
![[git log.png]]


## `git log --oneline`
Ver el historial en una línea por commit

**Ejemplo**

![[git log --oneline.png]]

## `git log -n <N>`
Mostrar solo los últimos N commits

**Ejemplo** Muestra solo los últimos 3 commits
```shell
git log -n 3
```

**Ejemplo** Muestra los últimos 5 commits en una línea
```shell
git log --oneline -n 5
```


## `git log --oneline --graph`
Mostrar commits en forma de árbol
```
git log --oneline --graph
```

>[!tip] Util si hay ramas y fusiones


# Modificar y Deshacer commits

## `git commit --amend`
Se usa para modificar el último commit, ya sea cambiando su mensaje, agregando archivos nuevos o eliminando archivos que no debían ser incluidos-
```shell
git commit --amend
```

**Ejemplo**: Si solo quieres cambiar el mensaje sin modificar los archivos incluidos
```shell
git commit --amend -m "Nuevo mensaje del commit"
```

### Ejemplo
---
Supongamos tenemos 2 archivos `archivo.txt` y `texto.txt` Y modificamos 4 veces `archivo.txt` con sus 4 commits correspondientes. Hacemos un quinto commit con `archivo.txt` y tenemos

![[ejemplo git --amend 1.png]]

Sin embargo, tenemos cambios sin guardar en `texto.txt` y debimos agregarlo al quinto commit. Además hicimos una ultima modificación a `archivo.txt` y no queremos realizar otro commit. 

![[ejemplo git --amend 2.png]]

Hemos preparado los archivos para un nuevo commit, sin embargo, usando `git commit --amend` lo que hacemos es "agregarlos al quinto commit".


![[ejemplo git --amend 4.png]]

Al ejecutar el comando, se abre el editor:
![[ejemplo git --amend 3.png]]

Luego vemos que se ha "modificado" el quinto commit
![[ejemplo git --amend 5.png]]
- Antes: quinto commit ->be5cafb
- Después: ultimo commit -> b0233d5

>[!tip] En realidad es un commit distitnto (por el hash) ya que no se pueden moficar commits.

---

## `git rebase`
Es un comando que reorganiza los commits, permitiendo modificar su historial de una manera más limpia y ordenada.

### `git rebase -i HEAD~N`
La opción `i` (interactiva) permite editar commits antes de moverlos.
```shell
git rebase -i HEAD~N
```
Donde `N` es el número de commits que deseas modificar.

Por ejemplo, si ejecutamos `git rebase -i HEAD~3` nos podría salir
```
pick abc123 Primer commit
pick def456 Segundo commit
pick ghi789 Tercer commit
```

Aqui podemos:
- `pick`: mantener el commit.
- `reword`: editar el mensaje del commit
- `edit`: modificar el contenido del commit
- `squash (s)`: fusionar commits en uno solo
- `drop`: eliminar el commit.


### `git rebase --continue`
Se usa para continuar el proceso de rebase después de resolver conflictos

### `git rebase --abort`
Este comando cancela el `rebase` y devuelve el repositorio al estado antes de iniciarlo.
- Revierte todos los cambios realizados hasta el momento
- Restablece la rama al estado en el que estaba antes de ejecutar `git rebase`


### Ejemplo
---
Continuando con el ejemplo de [[#`git commit --amend`]]
Supongamos que queremos eliminar el tercer commit (81ee28a)

![[Pasted image 20250319115212.png]]

Modificamos `pick` por `edit` en el ``tercer commit``
![[Pasted image 20250319115303.png]]
Guardamos, cerramos y luego usamos el comando
```shell
git commit --amend
```

Esto nos abre un archivo, donde anteriormente estaba el mensaje "tercer commit", lo cambiamos por "commit modificado"

![[Pasted image 20250319115725.png]]


Vemos el historial con `log`
![[Pasted image 20250319115833.png]]
Se han borrado los commit a partir del tercer commit. Para restaurarlos tenemos que usar `git commit --continue`

![[Pasted image 20250319120006.png]]
Los commits posteriores al tercer commit se han "restaurado". Los commits cuarto y ultimo tienen diferente hash. 

---












# Obtener las ramas de un repositorio remoto

```git
git fetch origin
```


# Descargar repo remoto de github

Verificar si git esta configurado
```git
git --version
```

Clonar el repositorio
```git
git clone https://github.com/Dirac2022/sigepat.git
```

Posicionarse en la carpeta del repositorio clonado
```git
cd sigepat
```

Verificar el estado del repositorio
```shell
git status
```

Configurar las credenciales
```git
git config --global user.name "Nombre"
git config --global user.email "email"
```


# Commits

### 1. **Convenciones generales de mensajes de _commit_**

- Usa el idioma del proyecto (por lo general, inglés).
- La primera línea debe ser breve (50 caracteres o menos) y describir el cambio de forma general.
- Si necesitas más detalles, usa una línea en blanco y luego agrega una descripción más larga en el segundo párrafo (72 caracteres por línea como máximo).
- Usa un tono imperativo (ejemplo: "Add", "Fix", "Update").

---

### 2. **Estructura básica de un mensaje de _commit_**

Un mensaje típico sigue este formato:

```
[Tipo]: [Descripción breve]

[Descripción detallada opcional]
```

#### Tipos comunes:

|Tipo|Uso|
|---|---|
|`feat`|Para agregar una nueva característica (por ejemplo, una clase).|
|`fix`|Para corregir un error en el código.|
|`refactor`|Para mejorar el código sin cambiar su funcionalidad.|
|`docs`|Para actualizar la documentación.|
|`style`|Cambios de formato o estilo que no afectan la lógica del código.|
|`test`|Para agregar o modificar pruebas.|
|`chore`|Cambios menores que no afectan la lógica del proyecto.|

---

### 3. **Ejemplos de mensajes para casos comunes**

#### a) **Crear una nueva clase**

```plaintext
feat: Add User class for handling user-related operations

Created a new User class with basic attributes: username, email, and password.
```

#### b) **Modificar una clase (añadir un atributo o método)**

```plaintext
feat: Add 'lastLogin' attribute to User class

Added 'lastLogin' to track the last login date of a user. Updated the constructor and added a method to update this attribute.
```

#### c) **Modificar un método existente**

```plaintext
fix: Update 'validatePassword' method in User class

Improved the password validation logic to enforce stricter password policies.
```

#### d) **Eliminar un atributo o método**

```plaintext
refactor: Remove 'age' attribute from User class

The 'age' attribute was redundant as it can be derived from the 'birthdate' attribute.
```

#### e) **Eliminar una clase completa**

```plaintext
refactor: Remove unused Admin class

The Admin class was removed as it is no longer needed in the current system design.
```

#### f) **Actualizar la documentación**

```plaintext
docs: Update README to include User class details
```

---

### 4. **¿Cuándo hacer _commit_ y _push_?**

#### a) **Frecuencia de _commits_**

- Haz un _commit_ después de completar una tarea lógica pequeña, por ejemplo:
    - Crear una nueva clase.
    - Añadir un método importante.
    - Solucionar un problema específico.

#### b) **Frecuencia de _push_**

- Haz un _push_ al terminar una sección importante de trabajo o al final de tu jornada.
- Mantén tu repositorio remoto sincronizado regularmente para evitar conflictos.

---

### 5. **Flujo de trabajo sugerido**

|Paso|Comando|Ejemplo / Comentario|
|---|---|---|
|**Agregar cambios al _staging_**|`git add [archivo]` o `git add .`|`git add User.java` para añadir solo el archivo modificado.|
|**Hacer un _commit_**|`git commit -m "[mensaje]"`|`git commit -m "feat: Add User class"`|
|**Enviar cambios al remoto**|`git push origin [rama]`|`git push origin main`|

---

### 6. **Errores comunes y cómo evitarlos**

|Error|Solución / Práctica recomendada|
|---|---|
|Mensajes vagos o genéricos|Escribe mensajes descriptivos (por ejemplo, evita "updated code").|
|Mezclar cambios no relacionados|Divide los cambios en _commits_ separados por funcionalidad.|
|No hacer _push_ regularmente|Haz _push_ al menos una vez al día o después de cambios significativos.|
# Frequencia de commits
### 1. **Relación entre _commits_ y _push_**

- Un **commit** guarda cambios en el repositorio **local**. Puedes hacer tantos _commits_ como quieras mientras trabajas localmente.
- Un **push** envía los _commits_ realizados a un repositorio **remoto** (por ejemplo, GitHub).

Esto significa que puedes realizar múltiples _commits_ relacionados a diferentes cambios antes de enviarlos todos juntos con un solo _push_.

---

### 2. **Ventajas de varios _commits_ por _push_**

|Ventaja|Descripción|
|---|---|
|**Historial claro**|Cada _commit_ representa un cambio lógico, lo que facilita entender el historial del proyecto.|
|**Facilidad para revertir**|Si un cambio específico causa problemas, puedes revertir un solo _commit_ sin afectar los demás.|
|**Colaboración eficiente**|Otros desarrolladores pueden ver exactamente qué cambios hiciste y por qué.|

---

### 3. **Ejemplo práctico: Varios _commits_ relacionados a un _push_**

Supongamos que estás trabajando en una clase `User` y realizas estos cambios:

#### a) **Primer cambio: Creas la clase base**

```bash
# Modificas el código
git add User.java
git commit -m "feat: Add base User class with essential attributes"
```

#### b) **Segundo cambio: Añades un método**

```bash
# Añades un nuevo método
git add User.java
git commit -m "feat: Add 'getFullName' method to User class"
```

#### c) **Tercer cambio: Corriges un error**

```bash
# Arreglas un error en el constructor
git add User.java
git commit -m "fix: Correct constructor logic in User class"
```

Finalmente, haces un **push** de todos estos _commits_ al repositorio remoto:

```bash
git push origin main
```

---

### 4. **Cómo ver los _commits_ antes de hacer un _push_**

Puedes revisar los _commits_ pendientes de enviar con el comando:

```bash
git log origin/main..HEAD
```

Esto mostrará los _commits_ en tu rama local que aún no están en el remoto.

---

### 5. **Buenas prácticas para varios _commits_**

|Recomendación|Descripción|
|---|---|
|**Haz _commits_ pequeños y frecuentes**|Cada _commit_ debe ser un cambio lógico y coherente, no un "gran paquete".|
|**Revisa tus mensajes**|Usa mensajes descriptivos y claros para cada _commit_.|
|**Evita _push_ innecesarios**|No hagas _push_ después de cada _commit_ si los cambios aún no están listos.|
|**Agrupa cambios relacionados**|Por ejemplo, todos los cambios en la clase `User` pueden ir en un solo _push_.|

---

### 6. **¿Cuándo hacer un solo _commit_ en lugar de varios?**

En algunos casos, podrías preferir un solo _commit_ si:

- El cambio es muy pequeño (por ejemplo, corregir un error tipográfico).
- Los cambios son inseparables y pertenecen a una única tarea lógica.

En estos casos, puedes agrupar los cambios antes de hacer un _commit_.

```bash
git add .
git commit -m "feat: Complete User class with methods and attributes"
```

---

# Otros comandos

## ✅  `git cat-file`

`git cat-file` es un comando de bajo nivel en Git que te permite **ver información sobre objetos internos de Git**, como commits, blobs, árboles y tags.

---

### 🔍 Sintaxis básica

```bash
git cat-file -p <objeto>
```

- `-p` significa “pretty-print” (muestra el contenido de forma legible).
    
- `<objeto>` puede ser:
    
    - el **hash** de un commit,
    - el hash de un **blob** (archivo),
    - un **tag**,
    - o un **árbol** (estructura de directorios).

---

### 📦 ¿Qué objetos puedo inspeccionar?

1. **Commits**
    ```bash
    git cat-file -p <commit-hash>
    ```
    Muestra el contenido del commit: autor, fecha, mensaje y referencia al árbol de archivos.
    
2. **Blobs**
    ```bash
    git cat-file -p <blob-hash>
    ```
    Muestra el **contenido de un archivo en ese punto**, como si hicieras `cat archivo.txt`.
    
3. **Trees**
    ```bash
    git cat-file -p <tree-hash>
    ```
    Muestra los archivos y carpetas (como un `ls` interno de ese snapshot).


---

# Objetos en Git
En Git, los objetos principales son **commit object**, **tree object**, **blob object** y **tag object**. Estos objetos forman la base del sistema de control de versiones de Git y están diseñados para almacenar y gestionar los datos de manera eficiente. A continuación, se explican en detalle cada uno de ellos, junto con ejemplos para ilustrar su funcionamiento.

## Commit Object
Un objeto *commit* representa un punto en el historial del repositorio. Es una "instantánea" de los cambios realizados en el proyecto y contiene información como:
- El hash único del commit.
- Un mensaje descriptivo sobre los cambios realizados.
- La referencia al árbol (*tree object*) que describe la estructura del proyecto en ese momento.
- Referencias a commits anteriores (padres).
- Información del autor y fecha.

**Ejemplo:**
Cuando ejecutas `git commit -m "Added new feature"`, Git crea un objeto commit que incluye el mensaje "Added new feature", el estado actual del árbol de archivos y las referencias necesarias para conectar este commit con el anterior. Puedes inspeccionar un commit con `git log`, que muestra detalles como:

```
commit 09f4acd3f8836b7f6fc44ad9e012f82faf861803 (HEAD -> master)
Author: John Doe 
Date: Fri Mar 26 09:35:54 2021 +0100
Updated index.html with a new line
```

Este commit apunta a un árbol que contiene la estructura de archivos en ese momento[1][5].

## Tree Object
Un objeto *tree* representa la estructura jerárquica de directorios y archivos en el repositorio. Cada árbol contiene referencias a otros árboles (subdirectorios) o blobs (archivos) junto con permisos y nombres.

**Ejemplo:**
Supongamos que tienes una estructura de directorios como esta:
```
/project
  ├── src/
  │   └── main.c
  └── README.md
```
Cuando haces un commit, Git crea un árbol que describe esta estructura. Puedes inspeccionar un árbol con `git cat-file -p ` para ver algo como:
```
100644 blob a3c6e3 README.md
040000 tree b7d9c2 src
```
Aquí, `README.md` es un archivo (blob) y `src` es un subdirectorio (otro árbol)[3][6].

## Blob Object
Un objeto *blob* almacena el contenido binario de los archivos. No incluye metadatos como nombres o ubicaciones; solo guarda los datos del archivo.

**Ejemplo:**
Si agregas un archivo llamado `example.txt` con `git add`, Git crea un blob para almacenar su contenido. Puedes inspeccionar el blob con `git cat-file -p ` y ver su contenido:
```
An example file
```
Si otro archivo tiene exactamente el mismo contenido, Git reutiliza el blob existente en lugar de crear uno nuevo, optimizando el almacenamiento[2][3][7].

## Tag Object
Un objeto *tag* es una referencia a un commit específico. Se usa para marcar puntos importantes en el historial, como versiones de lanzamiento. Existen dos tipos principales de tags:
- **Ligero:** Solo apunta al hash del commit.
- **Anotado:** Contiene metadatos adicionales como mensajes, autor y fecha.

**Ejemplo:**
Para crear un tag anotado llamado `v1.0.0`, puedes usar:
```
git tag -a v1.0.0 -m "Version 1.0 release"
```
Esto crea un objeto tag que apunta al commit actual y agrega información adicional. Los tags son útiles para identificar versiones específicas del proyecto

---

## Relación entre los objetos
Estos objetos trabajan juntos para representar el estado del repositorio:
1. Un *commit* apunta a un *tree*, que describe la estructura de archivos.
2. Los *trees* contienen referencias a blobs (contenidos de archivos) y otros trees (subdirectorios).
3. Los *tags* apuntan a commits específicos, permitiendo identificar versiones importantes.

**Ejemplo general:**
Imagina que haces cambios en varios archivos, los agregas al área de staging (`git add .`) y luego haces un commit (`git commit -m "Initial setup"`). Git crea:
- Blobs para cada archivo modificado.
- Un tree que organiza esos blobs según la estructura del proyecto.
- Un commit que referencia ese tree.
Más tarde, podrías marcar este commit con un tag (`git tag v1.0`) para señalarlo como la primera versión




# 🔍 ¿Qué hace `git merge --squash otra-rama`?

El comando:

```bash
git merge --squash otra-rama
```

**NO crea un commit de fusión automáticamente**. En lugar de eso, hace esto:

1. **Toma todos los cambios acumulados de la rama `otra-rama`** (desde que divergieron).
2. **Los aplica** _como si fueran un solo gran cambio_ en tu rama actual (por ejemplo `main` o `develop`).
3. Pero **NO hace el commit por ti**.
4. Y **NO conserva el historial de commits individuales** de la rama `otra-rama`.

---

### 🤔 ¿Y por qué necesito hacer `git add` y luego `git commit`?

Después de hacer `git merge --squash`, Git **marca todos los cambios como "modificados"** (staged o unstaged, según el caso), pero **no los confirma** automáticamente.

Entonces tienes que hacer esto manualmente:

```bash
git add .
git commit -m "Merge changes from 'otra-rama' using squash"
```

Esto es necesario porque `--squash` _prepara los cambios pero te deja a ti la responsabilidad de decidir qué se incluye y qué se escribe en el commit final_.

---

### 🆚 ¿Cuál es la diferencia con `git merge` y `git merge --no-ff`?

|Comando|Crea commit automáticamente|Conserva historial de commits de la rama|Requiere `add` y `commit` manual|
|---|---|---|---|
|`git merge`|✅ Sí (si es necesario)|✅ Sí|❌ No|
|`git merge --no-ff`|✅ Sí (fuerza commit)|✅ Sí|❌ No|
|`git merge --squash`|❌ No|❌ No (todo se aplasta en uno)|✅ Sí|

---

### 🧠 ¿Cuándo usar `git merge --squash`?

Es útil cuando:

- Quieres **fusionar cambios** pero sin agregar ruido al historial.
- Quieres que todo aparezca como **un solo commit limpio** (ideal para ramas con muchos commits experimentales).
- Estás trabajando solo y no necesitas conservar el historial detallado de la rama que fusionas.

---

### ✅ Ejemplo completo:

```bash
git checkout main
git merge --squash otra-rama
git add .
git commit -m "Squash merge from 'otra-rama': implement feature XYZ"
```

---


# `git blame`
## 🔍 ¿Para qué sirve `git blame`?

### 🧠 Propósito principal:

Saber **quién modificó una línea de un archivo**, **en qué commit**, y **cuándo lo hizo**.

Esto te ayuda a:

- Rastrear errores ("¿quién escribió esto y por qué?")
    
- Entender el contexto histórico de un cambio
    
- Saber a quién preguntarle si no entendés una parte del código
    
- Ver la evolución de una función o sección
    

---

## 🧪 Ejemplo básico

```bash
git blame archivo.py
```

Ejemplo de salida:

```
a1b2c3d4 (Juan Pérez   2024-11-10 15:42:22 +0100  1) def calcular_total(pedido):
e5f6g7h8 (Ana Martínez 2024-12-01 10:15:10 +0100  2)     return pedido.precio * pedido.cantidad
```

→ Eso te dice:

- Qué commit introdujo cada línea
    
- Quién lo hizo
    
- Cuándo
    
- Qué línea exacta es
    

---

## 🔧 Opciones útiles

### ✅ Ver con menos info (solo autor y línea)

```bash
git blame -e archivo.py
```

Incluye email del autor.

---

### ✅ Ver desde una línea específica

```bash
git blame -L 10,20 archivo.py
```

→ Muestra solo las líneas 10 a 20.

---

### ✅ Ver blame de un commit pasado

```bash
git blame archivo.py  # último estado (HEAD)

git blame HEAD~3 -- archivo.py
```

→ Para ver cómo estaba el archivo **hace 3 commits**.

---

### ✅ Saber qué línea cambió en qué commit, y ver el commit

```bash
git blame archivo.py
# copia el hash, por ejemplo: a1b2c3d4

git show a1b2c3d4
```

→ Así ves **todo el cambio que hizo esa persona** en ese commit.

---

## 🧼 Tip visual (si usás VS Code)

En Visual Studio Code:

- Click derecho en el archivo → `Blame`
    
- O instalá la extensión: **GitLens** → súper visual, te dice autores, cambios, tiempo, todo.
    

---

## ⚠️ Consejo:

No uses `git blame` para "culpar" a alguien. 🙅‍♂️ Usalo para **entender el contexto**, mejorar el código, y colaborar mejor.

---

¡Vamos con una clase completa de `git tag`! 🎯  
Esta herramienta es esencial para marcar **puntos importantes en la historia de tu proyecto**, como versiones (`v1.0.0`, `v2.0`, etc).

---





# 🏷️  `git tag` 

---

## 🔍 ¿Qué es un tag en Git?

Un **tag** (etiqueta) es como un “marcador” que apunta a un **commit específico**, generalmente usado para señalar **versiones estables** (ej: `v1.0.0`).

📦 Muy usado en **deploys, releases, CI/CD, control de versiones, changelogs, etc.**

---

## 🧠 Tipos de tags

 **1. Lightweight tag (etiqueta ligera)**
- Es un puntero simple a un commit.
- No tiene metadatos (ni mensaje, ni autor del tag).
```bash
git tag v1.0.0
```

**2. Annotated tag (etiqueta anotada) ✅ recomendada**
- Se guarda como objeto Git.
- Tiene mensaje, autor, fecha y puede firmarse con GPG.
```bash
git tag -a v1.0.0 -m "Versión 1.0.0 inicial"
```

---

## 🚀 Crear un tag

**Crear tag en el commit actual (HEAD)**
```bash
git tag -a v1.2.0 -m "Release v1.2.0"
```

**Crear tag en un commit específico**
```bash
git tag -a v1.1.0 1a2b3c4d -m "Versión antigua"
```

---

## 📤 Subir tags al repositorio remoto (GitHub, GitLab...)

**Subir un tag individual**
```bash
git push origin v1.2.0
```


**Subir todos los tags de golpe**
```bash
git push --tags
```

---

## ❌ Borrar tags

**Local**
```bash
git tag -d v1.2.0
```

**Remoto**
```bash
git push origin --delete tag v1.2.0
```

---

## 📋 Listar todos los tags

```bash
git tag
```



## 🔎 Ver detalles de un tag

```bash
git show v1.2.0
```

---

## 🔄 Checkout a un tag

```bash
git checkout v1.2.0
```

⚠️ Esto te deja en estado `detached HEAD`, es decir: estás viendo un commit del pasado, **no estás en una rama**.

Si querés trabajar desde ahí:

```bash
git checkout -b hotfix/v1.2.1
```

---

## 🧪 Caso práctico: flujo de versiones

```bash
git checkout main
git pull origin main
git tag -a v1.0.0 -m "Primera versión estable"
git push origin v1.0.0
```

🎉 ¡Ya hiciste tu primer release!

---

## 🛠️ GitHub Release + Tags

En GitHub:

- Si subís un tag, podés crear una **release** desde la interfaz web.
    
- Las acciones (`GitHub Actions`) y muchos pipelines se activan con tags.
    

---

## 🧠 Recap visual

|Acción|Comando|
|---|---|
|Crear tag ligero|`git tag v1.0.0`|
|Crear tag anotado|`git tag -a v1.0.0 -m "mensaje"`|
|Ver tags|`git tag`|
|Subir tag|`git push origin v1.0.0`|
|Subir todos los tags|`git push --tags`|
|Ver detalles|`git show v1.0.0`|
|Eliminar tag local|`git tag -d v1.0.0`|
|Eliminar tag remoto|`git push origin --delete tag v1.0.0`|
|Checkout a un tag|`git checkout v1.0.0`|

---

## 📦 Bonus: Cómo usar tags con SemVer

Tags suelen seguir la convención **SemVer (Semantic Versioning)**:

```
vMAJOR.MINOR.PATCH
```

Ejemplo:

- `v1.0.0`: Primer release
    
- `v1.1.0`: Nuevas features compatibles
    
- `v1.1.1`: Bugfixes
    

---
