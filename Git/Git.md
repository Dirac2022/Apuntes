
Tipos de jerarquía en git
- Sistema: para la computadora
- Global: para el mismo usuario
- Local: para repositorios

- git merge
- git branch
- git fetch
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
```sh
git add archivo.txt
```


>[!info] Propósito de del comando `add`
>**Añadir archivos al área de preparación (staging area):** `git add` mueve los cambios que has hecho en tus archivos desde el árbol de trabajo (working directory) al área de preparación (staging area). Solo los archivos que están en el área de preparación se incluirán en el próximo commit.

> [!tip]
> Si solo se coloca `git add .` se agregan todos los archivos del directorio de trabajo.
> Si se tiene otro archivo, por ejemplo ``archivo2.txt`` se pueden agregar ambos archivos dejando un espacio entre ellos  `git add archivo.txt archivo2.txt`

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


# 🧩`git diff`

El comando `git diff` te permite **ver línea por línea las diferencias** entre:

- tus archivos modificados y los últimos commits,
- el área de preparación (staging),
- diferentes ramas o commits.

Es una herramienta fundamental para **inspeccionar qué ha cambiado antes de hacer un commit** o para comparar ramas durante el desarrollo.

---

```bash
git diff                         # Cambios entre el working directory y el staging
git diff --staged                # Cambios entre staging y el último commit (HEAD)
git diff HEAD                    # Cambios entre working directory y el último commit
git diff <commit1> <commit2>     # Diferencias entre dos commits
git diff <rama1> <rama2>         # Diferencias entre ramas
git diff <archivo>               # Cambios en un archivo específico
```

---

## 🔍 Casos comunes explicados

**1. Cambios NO añadidos al staging**
```bash
git diff
```

Compara los archivos modificados que **aún no están en staging** (`git add`), con el último commit (`HEAD`).

---

**2. Cambios añadidos al staging (pero no commiteados)**
```bash
git diff --staged
```

Muestra lo que se ha preparado para commit. Útil antes de ejecutar `git commit`.

---

**3. Ver cambios respecto al último commit**
```bash
git diff HEAD
```
Muestra todos los cambios hechos desde el último commit: **modificados + staged**.

---

**4. Comparar dos commits**
```bash
git diff abc123 def456
```
Compara dos commits específicos usando sus hashes. Usa `git log --oneline` para obtenerlos.

---

**5. Comparar ramas**
```bash
git diff rama-base rama-objetivo
```
Ejemplo:

```bash
git diff main feature
```

Significa: "¿Qué ha cambiado en `feature` que no está en `main`?"  
💡 Es equivalente a:

```bash
git diff main..feature
```


## `git diff --quiet`

Verifica si hay diferencias entre el área de stagin y el directorio de trabajo, o entre commits, **sin mostrar las diferencias en pantalla**.

Retorna un código de salida:
- `0`: No hay diferencias
- `1`: Si hay diferencias.
- `>1`: Se produjo un error.

Ejemplo:

```sh
git diff --quiet
if [ $? -eq 1 ]; then
	echo "Hay cambios no guardados"
fi
```

**Uso entre commits**

```sh
git diff --quiet HEAD~1 HEAD
```


**Verificar si uno o varios archivos ha cambiado**

```sh
git diff --quiet -- archivo1.txt archivo2.txt
```

`--`: es un separador que indica que lo que sigue son rutas.

**Verificar si una carpeta (y su contenido ha cambiado)**

```sh
git diff --quiet -- src/
```

**Verificar si hay cambios entre el último commit y el archivo actual**

```sh
git diff --quiet HEAD -- archivo.txt
```

---

## ⚠️ Sobre el uso de `A..B`

### Explicación de `git diff A..B`

```bash
git diff A..B
```

Muestra **los cambios necesarios para transformar `A` en `B`**.  
Es decir: qué hay en `B` que no está en `A`.

🧠 **Orden importante**: el primero es la base, el segundo el objetivo.

---

### Comparación visual

|Comando|¿Qué compara?|Qué muestra|
|---|---|---|
|`git diff`|Working directory vs Staging|Cambios no añadidos|
|`git diff --staged`|Staging vs Último commit (HEAD)|Cambios ya añadidos|
|`git diff HEAD`|Working directory vs HEAD|Todos los cambios sin commitear|
|`git diff main`|HEAD vs `main` (si estás en otra rama)|Cambios actuales respecto a main|
|`git diff main..feature`|main vs feature|Cambios en feature|
|`git diff feature..main`|feature vs main|Cambios en main respecto a feature|
|`git diff abc123 def456`|Dos commits específicos|Diferencias entre versiones|

---

## 📄 Ejemplo paso a paso

```bash
# Crear archivo y primer commit
echo "Hola" > saludo.txt
git add saludo.txt
git commit -m "Saludo inicial"

# Editamos archivo
echo "¿Cómo estás?" >> saludo.txt

# 1. Ver cambios no añadidos
git diff

# 2. Agregar al staging
git add saludo.txt

# 3. Ver cambios en staging
git diff --staged
```

---

## 🔧 Otras opciones útiles

| Opción        | ¿Qué hace?                                   |
| ------------- | -------------------------------------------- |
| `--color`     | Forzar color en la salida                    |
| `--name-only` | Solo mostrar nombres de archivos modificados |
| `--stat`      | Mostrar resumen por archivo                  |
| `--word-diff` | Mostrar diferencias por palabra              |
| `--cached`    | Alias de `--staged`                          |
|               |                                              |

Ejemplo:

```bash
git diff --stat
```

Salida:

```
 saludo.txt | 2 ++
 1 file changed, 2 insertions(+)
```

---

## 🎯 Comparación específica entre ramas

### Estando en `feature-branch`:

```bash
git diff main
```

→ Cambios de `feature-branch` con respecto a `main`.

---

### Lo inverso:

```bash
git diff feature-branch..main
```

→ Qué hay en `main` que no está en `feature-branch`.


#### 🧠 `git diff --quiet`: 

El comando `git diff --quiet` se utiliza para **verificar si hay diferencias** entre archivos versionados en Git sin mostrar el contenido de esas diferencias. Es útil cuando se quiere actuar **en función de si hubo o no cambios**, especialmente en scripts, hooks o integraciones automáticas.

**🧪 ¿Qué hace?**

- **No imprime nada en consola.**
    
- Solo retorna un **código de salida**:
    
    - `0`: ✅ No hay diferencias.
    - `1`: ⚠️ Sí hay diferencias.
    - `>1`: ❌ Error al ejecutar el comando.

**🛠️ Sintaxis**

```bash
git diff --quiet [<opciones>] [--] [<archivo(s) o carpeta(s)>]
```

- `--quiet`: Modo silencioso (sin salida).
- `--`: Separador para distinguir rutas.
- `<archivo(s)>` o `<carpeta(s)>`: Opcional. Puedes indicar rutas específicas a comparar.


**✅ Ejemplos de uso**

1. Verificar si todo el proyecto tiene cambios sin mostrar detalles

```bash
git diff --quiet
```

2. Verificar si un archivo específico ha cambiado

```bash
git diff --quiet -- archivo.txt
```

3. Verificar si una carpeta ha cambiado (recursivamente)

```bash
git diff --quiet -- src/
```

4. Verificar cambios entre dos commits

```bash
git diff --quiet HEAD~1 HEAD -- src/
```

5. Verificar solo lo que está en staging

```bash
git diff --cached --quiet -- archivo.txt
```



**🧩 Aplicaciones comunes**

- **Scripts de CI/CD**: para evitar ejecutar tareas innecesarias si no hay cambios.
- **Hooks de Git**: para cancelar un commit si no hay cambios relevantes.
- **Automatización**: en despliegues, linters, pruebas, etc.


---

### 💡 Ejemplo en un script Bash

```bash
#!/bin/bash

if ! git diff --quiet -- src/; then
    echo "Hay cambios en src/. Ejecutando pruebas..."
    ./run_tests.sh
else
    echo "Sin cambios en src/. Saltando pruebas."
fi
```

---

### 📋 Resumen visual

|Comando|Significado|
|---|---|
|`git diff --quiet`|Verifica si hay cambios en todo el proyecto|
|`git diff --quiet -- archivo`|Verifica si ese archivo cambió|
|`git diff --cached --quiet`|Verifica cambios ya indexados (staged)|
|Código de salida `0`|Sin diferencias|
|Código de salida `1`|Hay diferencias|
|Código de salida `>1`|Error al ejecutar el comando|

---

¿Deseas ahora que te genere un **hook `pre-commit` funcional** que use `git diff --quiet` para permitir commits solo si se modificaron archivos en una carpeta específica, como `src/`?



---


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

---

> [!tip ] **Ejemplo con `edit`**
>
   En un archivo agregue una clase pero por error la llamé `Graph` en vez de `Tree`
>
> ```python
> # other line codes
>
> class Graph:
>
>    def __init__(self, root: Node=None):
>        self.root = Node
>
># other line codes
> ```
>
>
> ```sh
> dirac@ubuntu:~/Documents/DS/git-bisect$ git logall
> * 81a97ae (HEAD -> main) feat: add Graph class
> * 27778f9 feat: add set_value method in Node class
> * 8c044d7 feat: add app.py
> dirac@ubuntu:~/Documents/DS/git-bisect$ code .
> dirac@ubuntu:~/Documents/DS/git-bisect$ git rebase -i HEAD~1
> Stopped at 81a97ae...  feat: add Graph class
> You can amend the commit now, with
> 
>   git commit --amend 
> 
> Once you are satisfied with your changes, run
> 
>   git rebase --continue
> ```
> 
> Y en 
> 
> ```text
> pick 81a97ae feat: add Graph class
> ```
> 
> - Se cambia `pick` por `edit` (o reword en el caso de solo querer cambiar el mensaje).
> - Se corrige el código `Graph` → `Tree`. Se guardan los cambios
> 
> ```sh
> dirac@ubuntu:~/Documents/DS/git-bisect$ git commit --amend -m "feat: add Tree class"
> [detached HEAD 42ea7be] feat: add Tree class
>  Date: Sat May 24 12:02:07 2025 -0500
>  1 file changed, 7 insertions(+)
>  
> dirac@ubuntu:~/Documents/DS/git-bisect$ git rebase --continue
> You must edit all merge conflicts and then
> mark them as resolved using git add
> 
> dirac@ubuntu:~/Documents/DS/git-bisect$ git logall
> * 42ea7be (HEAD) feat: add Tree class
> | * 81a97ae (main) feat: add Graph class
> |/  
> * 27778f9 feat: add set_value method in Node class
> * 8c044d7 feat: add app.py
> dirac@ubuntu:~/Documents/DS/git-bisect$ git branch
> * (no branch, rebasing main)
>   main
> 
> ```
> 
> Si embargo después de hacer `git rebase -i` creamos una rama divergente. Vemos que al hacer `git branch` `HEAD` apunta a `(no branch, rebasing main)`. Para resolverlo:
> 
> 
> ```sh
> dirac@ubuntu:~/Documents/DS/git-bisect$ git checkout main
> M	app.py
> Warning: you are leaving 1 commit behind, not connected to
> any of your branches:
> 
>   42ea7be feat: add Tree class
> 
> If you want to keep it by creating a new branch, this may be a good time
> to do so with:
> git branch <new-branch-name\> 42ea7be
>  Switched to branch 'main'
> dirac@ubuntu:~/Documents/DS/git-bisect$ git reset --hard 42ea7be
> HEAD is now at 42ea7be feat: add Tree class
> dirac@ubuntu:~/Documents/DS/git-bisect$ git logall
> * 42ea7be (HEAD -> main) feat: add Tree class
> * 27778f9 feat: add set_value method in Node class
> * 8c044d7 feat: add app.py
> dirac@ubuntu:~/Documents/DS/git-bisect$ 
> 
> ```


---

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

| Tipo       | Uso                                                              |
| ---------- | ---------------------------------------------------------------- |
| `feat`     | Para agregar una nueva característica (por ejemplo, una clase).  |
| `fix`      | Para corregir un error en el código.                             |
| `refactor` | Para mejorar el código sin cambiar su funcionalidad.             |
| `docs`     | Para actualizar la documentación.                                |
| `style`    | Cambios de formato o estilo que no afectan la lógica del código. |
| `test`     | Para agregar o modificar pruebas.                                |
| `chore`    | Cambios menores que no afectan la lógica del proyecto.           |

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


# 🕵️‍♀️ `git blame`


Saber **quién modificó una línea de un archivo**, **en qué commit**, y **cuándo lo hizo**.

Esto te ayuda a:

- Rastrear errores ("¿quién escribió esto y por qué?")
- Entender el contexto histórico de un cambio
- Saber a quién preguntarle si no entendés una parte del código
- Ver la evolución de una función o sección

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

**✅ Ver con menos info (solo autor y línea)**
```bash
git blame -e archivo.py
```

Incluye email del autor.

---


**✅ Ver desde una línea específica**
```bash
git blame -L 10,20 archivo.py
```

Muestra únicamente las líneas de la 10 a la 20 (inclusive) del archivo.
También puedes usar esta forma equivalente:
```bash
git blame -L 5,+5 archivo.py
```
Esto muestra **5 líneas a partir de la línea 5**, es decir, de la línea 5 a la 9.

---

**✅ Ver blame de un commit pasado**
```bash
git blame archivo.py  # último estado (HEAD)

git blame HEAD~3 -- archivo.py
```
Para ver cómo estaba el archivo **hace 3 commits**.

---

**✅ Saber qué línea cambió en qué commit, y ver el commit**
```bash
git blame archivo.py
# copia el hash, por ejemplo: a1b2c3d4

git show a1b2c3d4
```

Así ves **todo el cambio que hizo esa persona** en ese commit.

---

## 🧼 Tip visual (si usás VS Code)

En Visual Studio Code:

- Click derecho en el archivo → `Blame`
- O instala la extensión: **GitLens** → súper visual, te dice autores, cambios, tiempo, todo.

---

## ⚠️ Consejo:

No uses `git blame` para "culpar" a alguien. 🙅‍♂️ Usalo para **entender el contexto**, mejorar el código, y colaborar mejor.

---



# 🏷️  `git tag` 

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


# 🧼`git clean`

`git clean` se usa para **eliminar archivos no rastreados (*untracked*)** del directorio de trabajo en un repositorio Git. Es útil cuando quieres limpiar archivos temporales, binarios compilados, o cualquier archivo que no esté siendo seguido por Git y que no esté en `.gitignore`.

> ⚠️ ¡Cuidado! `git clean` puede eliminar archivos permanentemente. Siempre es recomendable usar la opción `-n` o `--dry-run` primero para ver qué se eliminará.


```bash
git clean [opciones]
```

---
**📦 Archivos *untracked***
Son archivos que:

- No han sido añadidos con `git add`.
- No forman parte del seguimiento de Git.
- Aparecen al ejecutar `git status` como "Untracked files".

---

## 🎛️ Opciones / Banderas comunes

| Opción             | Descripción                                                                                        |
| ------------------ | -------------------------------------------------------------------------------------------------- |
| `-n` / `--dry-run` | Muestra qué archivos se eliminarían **sin eliminarlos**. Muy útil para revisar antes de borrar.    |
| `-f` / `--force`   | Fuerza la eliminación. Requerido para ejecutar el comando.                                         |
| `-d`               | También elimina directorios no rastreados (por defecto solo borra archivos).                       |
| `-x`               | También elimina archivos ignorados (los que están en `.gitignore`).                                |
| `-X`               | Elimina solo los archivos ignorados, **pero deja los no rastreados que no estén en `.gitignore`**. |

---

## 🧪 Ejemplos

**1. Ver qué se eliminaría sin borrar nada**
```bash
git clean -n
```

Salida esperada:
```
Would remove archivo_temporal.txt
Would remove carpeta_cache/
```

---

**2. Eliminar archivos no rastreados**
```bash
git clean -f
```
---

**3. Eliminar archivos y **directorios** no rastreados**
```bash
git clean -fd
```

---

**4. Eliminar archivos ignorados y no rastreados**
```bash
git clean -fxd
```

> ⚠️ Esto puede ser muy destructivo. Úsalo con cuidado.

---

**5. Eliminar solo los archivos ignorados**
```bash
git clean -fX
```

---

## 🧯 Consejo de seguridad

Antes de usar `git clean` con `-f`, prueba primero con:
```bash
git clean -nx
```

Eso te dirá qué se eliminaría si usaras `-fx`. Siempre revisar primero puede salvarte de perder archivos importantes.

---

## 🧾 Resumen visual

```
git clean -n        # Simula la limpieza, no borra nada
git clean -f        # Elimina archivos no rastreados
git clean -fd       # También borra carpetas no rastreadas
git clean -fx       # Borra TODO, incluso lo ignorado
git clean -fX       # Borra SOLO lo ignorado
```

---


# 🔁 `git revert`

El comando `git revert` **no borra el historial**.  
En cambio, **crea un nuevo commit** que **revierte los cambios** de un commit anterior.

> Es como un "anti-commit" que deshace otro commit, pero de forma segura y transparente.

---

## 🔄 Diferencias con `git reset`

|Característica|`git reset`|`git revert`|
|---|---|---|
|Modifica historial|✅ (si es `--hard` o `--mixed`)|❌ (no modifica historial)|
|Crea nuevo commit|❌|✅|
|Seguro en equipos|❌|✅|
|Elimina commits|Sí|No (los revierte)|

```bash
git revert <commit>
```

1. Analiza los cambios introducidos por ese commit.
2. Aplica un commit inverso.
3. Abre el editor para que pongas un mensaje de commit (puedes aceptarlo tal cual o modificarlo).

---

## 🔁 Ejemplo paso a paso

Supón este historial:
```
A -- B -- C -- D (HEAD)
```

Quieres revertir el commit `C`:
```bash
git revert C
```

Resultado:
```
A -- B -- C -- D -- C' (HEAD)
```

Donde `C'` es un nuevo commit que **deshace** lo que hizo `C`.

---

## ⚙️ Variantes útiles

### ✅ Revertir múltiples commits

```bash
git revert A^..C
```

Esto revierte todos los commits **desde `A^` hasta `C`** (inclusive).

> ⚠️ Esto crea **un commit de reversión por cada uno** (a menos que uses `--no-commit` y los combines tú).

---

### ✅ Revertir sin hacer commit automáticamente

```bash
git revert --no-commit <commit>
```

Aplica los cambios en el directorio de trabajo **sin hacer commit aún**.  
Te permite revisar, editar o combinar con otros cambios antes de confirmar.

---

### ✅ Revertir múltiples commits y combinar

```bash
git revert --no-commit C B A
git commit -m "Revertí varios commits"
```

Esto aplica las 3 reversiones y **las fusiona en un solo commit**.

---

### ✅ Silenciar conflictos (si no quieres editar mensajes)

```bash
git revert --no-edit <commit>
```

No te abrirá el editor de texto. Usa el mensaje por defecto.

---

### ✅ Revertir un merge commit

Por defecto, **Git no te deja revertir un merge commit directamente**, porque puede causar ambigüedad.  Pero puedes hacerlo así:
```bash
git revert -m 1 <merge_commit_hash>
```

Aquí `-m 1` indica **qué padre del merge conservar**:

- `1` → la primera rama (generalmente la base)
- `2` → la rama fusionada

Por ejemplo:
```sh
git revert -m 1 HEAD
```
Este comando está diciendo:

"Quiero revertir el último commit (HEAD), que es un commit de tipo merge, y conservar los cambios de su primer padre (main)".

---

## 🧪 Ejemplo práctico

```bash
echo "línea 1" > archivo.txt
git add archivo.txt
git commit -m "Primer commit"

echo "línea 2" >> archivo.txt
git commit -am "Segundo commit"

git log --oneline
# Verás dos commits

git revert HEAD
# Esto revierte el segundo commit
```

---

## 🧠 Tip: revertir un commit ya revertido (¡cuidado!)

Git se quejará si intentas revertir un commit que **ya fue revertido antes**, para evitar que deshagas el anti-commit. Puedes forzar con:

```bash
git revert --no-commit <commit>
```

...y manejarlo tú manualmente.

---

## ✅ Resumen visual

```bash
git revert <commit>            # Revertir un solo commit
git revert A^..C               # Revertir varios commits
git revert --no-commit C B A   # Revertir múltiples sin hacer commit
git revert -m 1 <merge_hash>   # Revertir un merge commit
```

---


# `git rebase`

`git rebase` es un comando que **mueve o reescribe** la base de una rama para que "parta" desde otro punto en la historia. Es útil para:

- Mantener un historial limpio y lineal.
- Aplicar tus commits como si hubieran sido creados encima de una rama más actualizada.

---

## 🧾 Sintaxis

```bash
git rebase <branch>
```

> Esto aplica los commits de tu rama actual sobre la rama `<branch>` como si los hubieras creado desde allí.

---

## 🎯 Ejemplo básico: Reescribiendo historia para limpiar

Supón esta estructura:

```
A---B---C  main
         \
          D---E  feature
```

### 1. Te mueves a la rama `feature`:

```bash
git checkout feature
```

### 2. Haces `rebase` sobre `main`:

```bash
git rebase main
```

Esto reescribe los commits D y E como si hubieran sido creados **después de C**:

```
A---B---C---D'---E'  feature
```

> ⚠️ D y E se convierten en **D' y E'**, nuevos commits con el mismo contenido, pero diferente hash.

---

## ✅ Ventajas del Rebase

- Historia más **limpia y lineal**.
- Facilita entender qué cambió cada persona.
- Menos commits de tipo "merge".

---

## 🔁 Comparación: `merge` vs `rebase`

|Aspecto|`merge`|`rebase`|
|---|---|---|
|Historia|Preserva estructura original|Linealiza la historia|
|Conflictos|Puede haber|También puede haber|
|Commits extra|Sí, crea commit de tipo merge|No, reescribe commits existentes|
|Historia clara|No siempre|Más fácil de leer|
|Seguro en `main`|✅ Sí|⚠️ No recomendado|

---

## ⚠️ Precauciones con `rebase`

- **Nunca hagas rebase de ramas públicas compartidas** (si otros ya basan trabajo en tus commits).
    
- Al reescribir historia pública, puedes causar conflictos al hacer push:
    

```bash
git push --force
```

> Forzar el push puede sobrescribir cambios de otros. ¡Cuidado!

---

## 📦 Rebase interactivo (`git rebase -i`)

Permite **editar, reordenar, combinar, borrar** commits. Ejemplo:

```bash
git rebase -i HEAD~3
```

Te muestra los últimos 3 commits para que edites algo como:

```
pick a1b2c3 primer commit
pick d4e5f6 segundo commit
pick 789abc tercer commit
```

Puedes cambiar `pick` por:

- `reword`: cambiar mensaje
- `edit`: modificar contenido
- `squash`: combinar commits
- `drop`: eliminar commit

---

## 🧪 Ejemplo práctico real

```bash
# Clonas un repo y haces una rama
git checkout -b fix-bug

# Haces 2 commits
git commit -am "Fix error 1"
git commit -am "Fix error 2"

# Luego, en main hacen avances:
git checkout main
git pull origin main  # Nuevos commits D, E

# Vuelves a tu rama:
git checkout fix-bug

# Rebasas tus cambios sobre lo nuevo de main
git rebase main
```

---

## 🧩 ¿Cuándo usar `git rebase`?

|Situación|¿Rebase o Merge?|
|---|---|
|Antes de hacer merge a main (privado)|✅ Rebase|
|Para mantener historia clara en tu rama|✅ Rebase|
|Para colaborar en equipo|⚠️ Merge (más seguro)|
|Cuando compartes tu rama públicamente|❌ No rebase (usa merge)|

---


# 🍒 `git cherry-pick`

`git cherry-pick` es un comando que te permite **aplicar un commit específico de otra rama (o del historial)** directamente a tu rama actual, **sin hacer una fusión completa ni un rebase**.

🔧 Es como decir:
> "Quiero _este_ cambio (este commit en particular), y nada más."

```bash
git cherry-pick <commit>
```

---

## 📌 ¿Cuándo usar `git cherry-pick`?

- Cuando quieres **traer un commit puntual** de una rama a otra sin mezclar todo.
- Para **reutilizar un bugfix** que ya hiciste en una rama (`hotfix`, por ejemplo) en otra (`main`).
- En casos donde **una fusión o rebase traería demasiados cambios innecesarios**.

---
### Variantes útiles:

|Comando|¿Qué hace?|
|---|---|
|`git cherry-pick <commit>`|Aplica un commit específico|
|`git cherry-pick A B C`|Aplica varios commits|
|`git cherry-pick A..B`|Aplica una secuencia de commits excluyendo A, incluyendo B|
|`git cherry-pick --no-commit <commit>`|Aplica el cambio pero **no hace el commit**|
|`git cherry-pick --abort`|Cancela un cherry-pick si hubo conflictos|
|`git cherry-pick --continue`|Continúa luego de resolver conflictos|

---

## 🔁 Ejemplo práctico paso a paso

### 🎯 Escenario

Estás en la rama `main`, y en la rama `featureX` hiciste un commit que te gustaría traer a `main`.

1. Crear entorno de ejemplo:

```bash
git init cherry-pick-ejemplo
cd cherry-pick-ejemplo
echo "Hola mundo" > archivo.txt
git add .
git commit -m "Inicial"
```

2. Crear una rama y un commit allí:

```bash
git checkout -b featureX
echo "Nueva funcionalidad" >> archivo.txt
git commit -am "Agrega funcionalidad X"
```

3. Volver a `main`:

```bash
git checkout main
```

4. Ver el hash del commit que quieres copiar:

```bash
git log --oneline
```

Supongamos que el commit es `abc1234`.

5. Hacer cherry-pick:

```bash
git cherry-pick abc1234
```

✅ Ahora, el contenido de ese commit estará en `main`, como si lo hubieras hecho ahí directamente.

---

## ❗ Conflictos

Si el contenido que quieres traer **entra en conflicto con lo que ya tienes**, Git te pedirá resolverlo manualmente y luego ejecutar:

```bash
git add .
git cherry-pick --continue
```

O si quieres abortar:

```bash
git cherry-pick --abort
```

---

## 🧃 Diferencia con otras operaciones

|Comando|Qué trae|Combina cambios completos|Crea merge commit|
|---|---|---|---|
|`merge`|Todo el historial desde el punto común|✅ Sí|✅ Sí|
|`rebase`|Cambia la base de commits|✅ Sí|❌ No|
|`cherry-pick`|Solo un commit específico|❌ No|❌ No|

---

## 📌 Tip adicional

Puedes usar `git cherry-pick -x <commit>` para que en el mensaje del nuevo commit se agregue una nota tipo:
```bash
(cherry picked from commit abc1234)
```
Esto es útil para seguimiento.

---

# 🧠 `git checkout`

`git checkout` es un comando que sirve principalmente para:

1. **Cambiar de rama**
2. **Restaurar archivos desde otro commit**
3. **Resolver conflictos usando `--ours` y `--theirs`**

---

## 📌 Sintaxis general

```bash
git checkout <rama>               # Cambiar de rama
git checkout <commit> -- <archivo> # Restaurar un archivo desde un commit
git checkout --ours <archivo>      # Resolver conflictos usando nuestra versión
git checkout --theirs <archivo>    # Resolver conflictos usando la versión del otro
```

---

## ✅ 1. Cambiar de rama

```bash
git checkout main
```
Esto te mueve a la rama `main`.

---
## ✅ 2. Restaurar un archivo desde otro commit o rama

```bash
git checkout develop -- archivo.txt
```

Esto toma `archivo.txt` desde la rama `develop` y lo coloca en tu rama actual (no cambia de rama).

---

## ✅ 3. Resolver conflictos: `--ours` y `--theirs`

Estas banderas se usan **cuando estás en medio de un conflicto de `merge`**.

- `--ours`: Selecciona **la versión de la rama actual (donde hiciste el merge)**
- `--theirs`: Selecciona **la versión de la rama que estás fusionando**

### 🎯 Queremos ver cómo se usan `--ours` y `--theirs` al resolver conflictos.

**1. Crear un repositorio y ramas**
```bash
mkdir ejemplo-checkout
cd ejemplo-checkout
git init
echo "Linea original" > archivo.txt
git add .
git commit -m "Commit inicial"
```

**2. Crear y modificar en `rama1`**
```bash
git checkout -b rama1
echo "Cambio en rama1" > archivo.txt
git commit -am "Cambio desde rama1"
```

**3. Volver a `main` y hacer otro cambio**
```bash
git checkout main
echo "Cambio en main" > archivo.txt
git commit -am "Cambio desde main"
```

**4. Intentar hacer merge (ocurre conflicto)**
```bash
git merge rama1
```

Git te dirá que hay **conflicto** en `archivo.txt`.


### ⚠️ En este punto, el archivo `archivo.txt` tendrá un contenido como:
```txt
<<<<<<< HEAD
Cambio en main
=======
Cambio en rama1
>>>>>>> rama1
```

### 🛠️ Resolver usando `--ours` o `--theirs`

- Si quieres conservar la versión de **main** (la rama actual):
    ```bash
    git checkout --ours archivo.txt
    ```
    
- Si quieres conservar la versión de **rama1** (la rama que estás fusionando):
    ```bash
    git checkout --theirs archivo.txt
    ```

Después de eso:
```bash
git add archivo.txt
git commit
```

¡Conflicto resuelto y merge completo!

---

### 🧠 Resumen visual

| Opción     | Significa                            | Usa la versión de...         |
| ---------- | ------------------------------------ | ---------------------------- |
| `--ours`   | "Quédate con **nuestro** cambio"     | La rama actual (`HEAD`)      |
| `--theirs` | "Quédate con **el cambio del otro**" | La rama que estás fusionando |


**🚫 Nota importante**

Las opciones `--ours` y `--theirs` **solo funcionan en un conflicto de merge**, no puedes usarlas de forma aislada fuera de ese contexto.



# 🧳 `git stash`

El comando `git stash` guarda **temporalmente** tus cambios en una "pila de cambios" (stash stack), para que puedas volver a un **estado limpio** del repositorio (como el último commit) y continuar trabajando en otra cosa.

Ideal cuando:

- Tienes trabajo en curso pero necesitas cambiar de rama.
- Quieres hacer una prueba limpia sin perder lo que estabas haciendo.
- Quieres aplicar los cambios más tarde en otra rama.


```bash
git stash [opciones]
```

---

## 🔑 Comandos principales

**1. `git stash`**
Guarda cambios **no comprometidos** (tracked, no staged o staged) y revierte el working directory al último commit (HEAD).

```bash
git stash
```

---

**2. `git stash push [-m "mensaje"] [--include-untracked] [--all]`**
Versión más explícita del anterior. Puedes añadir un mensaje y decidir qué incluir.
```bash
git stash push -m "Mi trabajo en progreso"
git stash push --include-untracked      # Incluye archivos nuevos no añadidos
git stash push --all                    # Incluye archivos ignorados también
```

---

**3. `git stash list`**
Muestra todos los elementos guardados en la pila de stash.
```bash
git stash list
```

Salida típica:
```
stash@{0}: On main: Mi trabajo en progreso
stash@{1}: WIP on develop: 34fd1d2 agregando funcion
```

---

**4. `git stash show [stash@{n}]`**
Muestra un resumen de los cambios en un stash específico (por defecto el más reciente).
```bash
git stash show
git stash show stash@{1}
```

Con diferencias detalladas:
```bash
git stash show -p
```

---

**5. `git stash apply [stash@{n}]`**
Aplica los cambios de un stash **a tu working directory**, pero **no lo elimina** de la pila.
```bash
git stash apply               # Aplica stash más reciente
git stash apply stash@{1}     # Aplica uno específico
```

---

**6. `git stash pop`**
Aplica los cambios del stash más reciente **y lo elimina** de la pila.
```bash
git stash pop
```

Es como:
```bash
git stash apply && git stash drop
```

---

**7. `git stash drop [stash@{n}]`**
Elimina un stash específico.
```bash
git stash drop stash@{1}
```

---

**8. `git stash clear`**
Elimina **todos** los elementos del stash.
```bash
git stash clear
```

---

**9. `git stash branch <nombre-rama>`**
Crea una nueva rama con el stash aplicado automáticamente (y lo quita de la pila).
```bash
git stash branch fix-rapido stash@{1}
```

---

## 📦 ¿Qué guarda `git stash`?

Por defecto:

- Cambios en archivos **seguros (tracked)**.
- Cambios **staged (ya añadidos con `git add`)**.

**No incluye**:

- Archivos nuevos (*untracked*).
- Archivos ignorados.

Pero puedes incluirlos con:
```bash
git stash push --include-untracked
git stash push --all
```

---

## 🧠 Trucos y buenas prácticas

|Situación|Comando recomendado|
|---|---|
|Guardar todo, incluyendo untracked|`git stash push --include-untracked`|
|Guardar todo, incluso ignorados|`git stash push --all`|
|Nombrar tu stash|`git stash push -m "mensaje claro"`|
|Revisar diferencias de un stash|`git stash show -p stash@{n}`|
|Recuperar un stash en una nueva rama|`git stash branch nombre stash@{n}`|
|Aplicar y eliminar stash al mismo tiempo|`git stash pop`|
|Solo aplicar sin eliminar stash|`git stash apply`|

---

## 🎯 Ejemplo completo

```bash
# Creamos y modificamos archivos
echo "Hola" > saludo.txt
git add saludo.txt
git commit -m "saludo inicial"

echo "¿Cómo estás?" >> saludo.txt

# Guardamos stash con mensaje
git stash push -m "Agregando saludo extendido"

# Comprobamos que se guardó
git stash list

# Volvemos a aplicar los cambios
git stash apply stash@{0}

# O aplicamos y eliminamos
git stash pop

# Si ya no lo necesitamos
git stash clear
```

---

## 🔬 Profundizando: ¿Dónde se guarda un stash?

Cada `stash` es un **objeto especial** de Git, compuesto de:

- Un commit del estado del working directory.
- Un commit del staging area.
- Un commit padre (el HEAD en el momento del stash).

Puedes verlos usando:

```bash
git log refs/stash
```

---


# 🔍 `git bisect`

`git bisect` es un **algoritmo de búsqueda binaria** automatizado dentro de Git que te ayuda a encontrar **el commit exacto** donde un bug fue introducido.

👉 En lugar de revisar manualmente decenas (o cientos) de commits, `git bisect` va reduciendo la búsqueda a la mitad hasta encontrar el culpable. Es ideal para:

- Bugs que **aparecen en algún punto** de la historia del proyecto.
- Cambios de comportamiento, errores de lógica o regresiones.

---

## 🧠 ¿Cómo funciona?

Supón que:

- Tienes un commit donde **todo funcionaba bien**.
- Y un commit más reciente donde **algo se rompió**.

`git bisect` va probando commits intermedios y, según tu respuesta (**bueno** o **malo**), Git reduce el rango de commits hasta hallar el culpable.

---

## 🛠️ Sintaxis básica

```bash
git bisect start
git bisect bad <commit_malo>
git bisect good <commit_bueno>
# Git escoge un commit intermedio automáticamente.
# Tú pruebas y le dices:
git bisect good  # si ese commit funciona
git bisect bad   # si ese commit también falla
# Repite hasta encontrar el commit exacto
```

---

## ✅ Flujo paso a paso con ejemplo

Imagina que tienes un bug que no estaba antes, pero ahora sí:

**1. Inicia `git bisect`**
```bash
git bisect start
```

**2. Marca el commit actual (donde el bug está) como malo:**
```bash
git bisect bad
```

O especifica el hash:
```bash
git bisect bad abc1234
```

**3. Marca un commit anterior conocido como bueno:**
```bash
git bisect good 4f6d3e1
```

> Git ahora hace **checkout automático** a un commit intermedio.

**4. Prueba ese commit manualmente. Si el bug está presente:**
```bash
git bisect bad
```

Si el bug no está:
```bash
git bisect good
```

Git repetirá este proceso y te llevará a otro commit intermedio. Este ciclo se repite unas pocas veces ($log_₂(N)$) hasta encontrar **el commit culpable exacto**.

**5. Una vez encontrado el commit, Git lo imprime:**
```bash
<hash> is the first bad commit
```

**6. Sal del modo bisect:**
```bash
git bisect reset
```

---

## 🧪 Automatización: `git bisect run`

Puedes automatizar el proceso con un script de prueba.
### Ejemplo:

```bash
git bisect start
git bisect bad
git bisect good 1234abcd

git bisect run ./test_script.sh
```

Donde `test_script.sh` retorna:

- `0` si todo está bien.
- Cualquier otro valor si hay error (ej. bug).

Git ejecutará el script en cada commit intermedio **automáticamente** y hará la búsqueda sin intervención manual.

---

## 📌 ¿Qué necesitas para usar `git bisect` efectivamente?

- Saber **dónde el bug ya existía** (mal commit).
- Saber **dónde no existía** (buen commit).
- Poder verificar **si el bug está o no en un commit** (prueba manual o script).

---

## 🧠 ¿Qué busca realmente `git bisect`?

Internamente, utiliza una **búsqueda binaria en el grafo de commits** para minimizar la cantidad de pasos. Por cada respuesta que das (`good` o `bad`), elimina la mitad de los commits posibles.

Si hay 1000 commits entre el bueno y el malo, con `log₂(1000) ≈ 10`, lo encuentra en unos **10 pasos o menos**.

---

## 📋 Ejemplo completo

```bash
# Iniciar el modo bisect
git bisect start

# Marcar el commit actual como malo
git bisect bad

# Marcar un commit donde todo funcionaba
git bisect good abc1234

# Git te lleva a un commit intermedio
# Compilas, pruebas manualmente y respondes:
git bisect good  # si no hay bug
git bisect bad   # si el bug existe

# Cuando lo encuentra
# => abc7890 is the first bad commit

# Salir
git bisect reset
```

---

## 🧠 Tips adicionales

|Consejo|Explicación|
|---|---|
|Puedes usar etiquetas o ramas como argumentos|`git bisect good v1.0.0`|
|Puedes hacer checkout entre pruebas si necesitas|Solo asegúrate de no modificar nada|
|Puedes usar `git bisect log` para guardar tu progreso|y `git bisect replay` para repetir|
|Automatiza todo con scripts|para bugs que pueden ser verificados automáticamente|

---




> [!tip] Ejemplo
>  El commit conflictivo es el commit `9982e29` (`eleventh commit`)
>  
>  ```sh
>  dirac@ubuntu:~/Documents/DS/bisect-project$ git logall
>  * b8c1f7a (HEAD -> main) sixteenth commit
>  * a4769b7 fifteenth commit
>  * d0ce844 fourteenth commit
>  * 22e7c72 thirteenth commit
>  * a2c60d0 twelfth commit
>  * 9982e29 eleventh commit
>  * 41ca501 tenth commit
>  * e073c3b ninth commit
>  * cfe4371 eight commit
>  * 5db8496 seventh commit
>  * a929e9f sixth commit
>  * 866865e fifth commit
>  * 5726c0d fourth commit
>  * 7cec269 third commit
>  * 1b3c9ce second commit
>  * 415e7ab first commit
>  
>  ```
>  
>  Proceso
>  
>  ```sh
>  # Iniciar git bisect
>  dirac@ubuntu:~/Documents/DS/bisect-project$ git bisect start
>  status: waiting for both good and bad commits
>  dirac@ubuntu:~/Documents/DS/bisect-project$ git branch
>  * main
>  ```
>  
>  - Asignamos el ultimo commit como bad
>  - Asignamos el primer commit como good
>  - Saltamos al commit `eight commit
>  - Ejecutamos las validaciones (pruebas necesarias)
>  
>  ```sh
>  dirac@ubuntu:~/Documents/DS/bisect-project$ git bisect bad main
>  status: waiting for good commit(s), bad commit known
>  dirac@ubuntu:~/Documents/DS/bisect-project$ git bisect good 415e7ab
>  Bisecting: 7 revisions left to test after this (roughly 3 steps)
>  [cfe4371133b776dbce748ddaec5b3db452d3b99d] eight commit
>  ```
>  
>  - Ejecutamos las validaciones (pruebas necesarias) para el `eighth commit`
>  - El commit `eighth commit` no es conflictivo
>  ```sh
>  dirac@ubuntu:~/Documents/DS/bisect-project$ code .
>  dirac@ubuntu:~/Documents/DS/bisect-project$ git bisect good
>  Bisecting: 3 revisions left to test after this (roughly 2 steps)
>  [a2c60d03ef1a375110ebb00d7f1af015de7a2fae] twelfth commit
>  dirac@ubuntu:~/Documents/DS/bisect-project$ 
>  
>  ```
>  
>  - Ejecutamos las validaciones (pruebas necesarias) para el `eighth commit`
>  - El commit `twelfth commit` es conflictivo
>  
>  ```sh
>  dirac@ubuntu:~/Documents/DS/bisect-project$ git bisect bad
>  Bisecting: 1 revision left to test after this (roughly 1 step)
>  \[41ca50179e462cd9e927d737ddfa409360a9b14d\] tenth commit
>  ```
>  
>  - Ejecutamos las validaciones (pruebas necesarias) para el `tenth commit`
>  - El commit `tenth commit` no es conflictivo
>  
>  ```sh
>  dirac@ubuntu:~/Documents/DS/bisect-project$ git bisect good
>  Bisecting: 0 revisions left to test after this (roughly 0 steps)
>  [9982e2965d8cd583f1a9178221ad2595d269a576] eleventh commit
>  dirac@ubuntu:~/Documents/DS/bisect-project$ 
>  dirac@ubuntu:~/Documents/DS/bisect-project$ 
>  dirac@ubuntu:~/Documents/DS/bisect-project$ code .
>  ```
>  
>  - El ultimo commit por revisar es el commit conflictivo
>  - Realizamos los cambios necesarios para resolver el error
>  
>  ```sh
>  dirac@ubuntu:~/Documents/DS/bisect-project$ git bisect reset
>  Previous HEAD position was 9982e29 eleventh commit
>  Switched to branch 'main'
>  dirac@ubuntu:~/Documents/DS/bisect-project$ 
>  ```
>  
>  - Aplicamos `git bisect reset` para salir del modo `bisect`


---



# 🧹 `git reset` 

Internamente, Git maneja tres áreas distintas:

|Área|Descripción breve|
|---|---|
|`HEAD`|Puntero al último commit en la rama actual|
|**Índice (staging)**|Área donde se preparan los archivos para commit|
|Working Directory|Tu carpeta actual con archivos editables|

`git reset` controla **hasta qué punto de esas tres áreas** quieres retroceder.


```bash
git reset [<modo>] <commit>
```

Donde `<commit>` puede ser:

- `HEAD` (el commit actual),
- `HEAD~1` (uno antes del actual),
- `abc1234` (hash corto),
- o incluso una etiqueta o rama (`main`, `develop`, etc).

---

## 🛠️ Modos de `git reset`

|Modo|HEAD se mueve|Índice (staging) cambia|Working Directory cambia|Uso común|
|---|---|---|---|---|
|`--soft`|✅ Sí|❌ No|❌ No|Rehacer commits|
|`--mixed`|✅ Sí|✅ Sí|❌ No|Deshacer staging|
|`--hard`|✅ Sí|✅ Sí|✅ Sí|Borrar todo|

---

## 🧪 Ejemplos didácticos y visuales

**🧼 1. `--soft`: Solo rebobinar HEAD**

```bash
git reset --soft HEAD~1
```

🔎 Qué ocurre:

- El commit más reciente se "deshace".
- Los cambios siguen **preparados para commit** (staging).
- Ideal si solo quieres cambiar el mensaje o modificar algo más.

🎯 Uso típico:

```bash
git commit -m "Commit con error"
git reset --soft HEAD~1
# editas algo más o cambias el mensaje
git commit -m "Commit corregido"
```

---

**🧼 2. `--mixed`: HEAD y staging se resetean**

```bash
git reset --mixed HEAD~1
```

🔎 Qué ocurre:

- Se borra el commit actual.
- Los cambios **siguen en los archivos**, pero **ya no están en staging**.
- Ideal para sacar archivos del staging (`git add`) sin perderlos.

🎯 Atajo común:

```bash
git reset  # equivalente a --mixed
```

---

**🧼 3. `--hard`: Todo se borra**

```bash
git reset --hard HEAD~1
```

🔎 Qué ocurre:

- Se elimina el commit.
- El staging y tus archivos **vuelven al estado del commit anterior**.
- ⚠️ Los cambios que no estaban commiteados se **pierden para siempre** (a menos que uses `reflog`).

🎯 Recomendado solo si estás absolutamente seguro.

---

## 🛡️ Mecanismo Interno

Veamos cómo afecta cada área:

```text
HEAD        → apunta al commit dado
ÍNDICE      → se actualiza si --mixed o --hard
WORKING DIR → se actualiza solo con --hard
```

---

## 🔍 Visual: antes y después

Supón que estás así:

```text
HEAD → C3 ← staging ← working dir (con cambios nuevos)
```

Con `git reset --soft C2`:

```text
HEAD → C2 ← staging (cambios siguen listos)
working dir igual
```

Con `git reset --mixed C2`:

```text
HEAD → C2
staging limpio
working dir con cambios
```

Con `git reset --hard C2`:

```text
HEAD → C2
staging limpio
working dir limpio
```

---

## 💥 Recuperar si te equivocaste

### Usando `git reflog`

```bash
git reflog
```

Te muestra todos los movimientos de `HEAD`, incluso si hiciste un `--hard`. Luego puedes recuperar:

```bash
git reset --hard <hash_anterior>
```

---

## 💡 Casos de uso comunes

|Caso|Comando recomendado|
|---|---|
|Rehacer último commit (mensaje o contenido)|`git reset --soft HEAD~1`|
|Sacar un archivo del staging sin perderlo|`git reset <archivo>`|
|Limpiar staging completamente|`git reset` (o `git reset --mixed`)|
|Borrar cambios y commit localmente|`git reset --hard HEAD~1`|
|Volver a un punto anterior exacto|`git reset --hard abc1234`|

---

## 🧠 Tips avanzados

**Deshacer un archivo del staging (sin tocar los demás)**
```bash
git reset archivo.txt
```

Solo ese archivo vuelve al working directory sin perder cambios.

**No tocar staging ni archivos, solo HEAD**
```bash
git reset --soft HEAD~2
```





# 🚀 `git push` 

---

## 🧾 ¿Qué es `git push`?

El comando `git push` se usa para **enviar tus commits desde el repositorio local hacia un repositorio remoto**. Es el paso que realmente _publica_ tu trabajo para que otros lo vean, accedan o colaboren.

```bash
git push <remoto> <rama>
```

---

## 📦 Ejemplo básico

```bash
# Subir la rama actual al remoto llamado 'origin'
git push origin main
```

Esto toma los commits de tu rama `main` y los envía al servidor remoto (`origin`) para sincronizar el trabajo con el repositorio compartido.

---

## 🌿 ¿Qué se puede "empujar"?

- Ramas (`branches`)
- Etiquetas (`tags`)
- Referencias (`refs`)
- Todo el repositorio (`--mirror`)

---

## 🧠 Concepto clave: _Tracking Branch_

Cuando haces `git push origin main`, Git crea una relación de seguimiento (tracking branch) entre tu rama local `main` y la rama remota `origin/main`.

Esto permite luego hacer simplemente:

```bash
git push
```

... y Git sabrá qué subir.

---

## 🔧 Variaciones y opciones comunes

|Comando|Descripción|
|---|---|
|`git push`|Empuja la rama actual a su rama remota configurada (tracking).|
|`git push origin main`|Empuja la rama `main` al remoto `origin`.|
|`git push origin HEAD`|Empuja la rama actual sin escribir su nombre.|
|`git push --set-upstream origin <rama>`|Asocia una rama local con una remota y la empuja.|
|`git push --all`|Empuja **todas** las ramas locales.|
|`git push --tags`|Empuja **todas** las etiquetas (`tags`).|
|`git push origin <tag>`|Empuja una etiqueta específica.|
|`git push --dry-run`|Muestra qué se empujaría sin hacerlo (modo simulación).|
|`git push origin :rama`|Elimina la rama remota `rama`.|
|`git push origin --delete rama`|Otra forma de eliminar una rama remota.|
|`git push origin local:remota`|Empuja la rama `local` a la rama remota `remota`.|
|`git push --mirror`|Empuja absolutamente todo: ramas, tags, refs.|
|`git push --force`|Fuerza el push incluso si reescribirá el historial. ⚠️ Peligroso.|
|`git push --force-with-lease`|Fuerza el push **solo si el remoto no ha cambiado**. 🔒 Recomendado en vez de `--force`.|

---

## 🛡️ `--force` vs `--force-with-lease`

|Opción|Explicación|
|---|---|
|`--force`|Fuerza el push sin preguntar. Riesgo alto de sobrescribir trabajo ajeno.|
|`--force-with-lease`|Solo sobrescribe si nadie más ha empujado después de ti. Más seguro.|

### ✅ Recomendado:

```bash
git push --force-with-lease origin mi-rama
```

---

## 🔥 Eliminar ramas remotas

```bash
# Método moderno
git push origin --delete nombre-rama

# Método antiguo
git push origin :nombre-rama
```

---

## 🧪 Simulación

```bash
git push --dry-run
```

Muestra lo que se empujaría, pero **no realiza ninguna acción**. Ideal para validar antes de ejecutar scripts.

---

## 🧭 Empujar a nombre distinto

```bash
# Subir la rama local "fix-bug" al remoto como "hotfix-login"
git push origin fix-bug:hotfix-login
```

---

## 🧾 Empujar etiquetas

```bash
# Subir una etiqueta específica
git push origin v1.0.0

# Subir todas las etiquetas locales
git push --tags
```

---

## 🧪 Empujar todo el repositorio (peligroso)

```bash
git push --mirror origin
```

Esto empuja todas las ramas, etiquetas y referencias locales al remoto, incluso si hay sobrescritura. Se usa solo para clonar repositorios de forma exacta.

---

## 💡 Mejores prácticas

- Usa `--force-with-lease` en vez de `--force` para proteger el trabajo de otros.
- Usa `--dry-run` en automatizaciones para prevenir errores.
- Borra ramas remotas cuando ya no se usen para mantener limpio el repositorio.
- Empuja etiquetas para versionar software (como `v1.0.0`, `v2.1.3-beta`, etc.).

---

## 🧩 Casos de uso típicos

|Escenario|Comando|
|---|---|
|Empujar nueva rama al remoto y vincularla|`git push --set-upstream origin nueva-rama`|
|Forzar un rebase reescrito|`git push --force-with-lease origin mi-rama`|
|Subir etiquetas de una versión|`git push --tags`|
|Borrar rama remota obsoleta|`git push origin --delete antigua-rama`|

---

¡Perfecto! Vamos a hacer una clase **aún más completa y avanzada** sobre el comando `git log`, incluyendo **funciones menos conocidas** como `-L` y otras opciones avanzadas. Esta es una guía de nivel experto para sacarle el máximo provecho a `git log`.

---

# 🔍 `git log` 


Es el comando que muestra el historial de commits. Pero con las opciones adecuadas, puede ser una **herramienta de análisis poderosa** para inspeccionar:

- Cambios de un archivo o línea específica
- Autoría y fechas
- Historial visual
- Filtros avanzados por contenido, fecha y autor

---

```bash
git log [opciones] [rango_de_commits] [--] [archivo]
```

---

## 📌 Opciones básicas

| Opción       | Descripción                                               |
| ------------ | --------------------------------------------------------- |
| `--oneline`  | Muestra los commits en una sola línea                     |
| `--graph`    | Muestra la estructura del historial en forma de árbol     |
| `--decorate` | Añade nombres de ramas y etiquetas                        |
| `--all`      | Incluye todas las ramas                                   |
| `-n <N>`     | Muestra los últimos N commits                             |
| `--stat`     | Muestra archivos modificados y líneas añadidas/eliminadas |
| `-p`         | Muestra los cambios línea por línea                       |
| `--patch`    | Igual que `-p`                                            |

---

## 📂 Filtro por archivos

```bash
git log archivo.py
```

Muestra los commits que modificaron `archivo.py`.

```bash
git log --follow archivo_renombrado.py
```

Sigue el historial incluso si el archivo cambió de nombre.

---

## 🧠 Filtro por autor, fecha y contenido

```bash
git log --author="estalin"
git log --since="2024-01-01"
git log --until="2024-12-31"
git log --grep="arreglado"
```

Se pueden combinar:

```bash
git log --author="estalin" --since="2024-01-01" --grep="fix"
```

---

## 🧩 Formato personalizado con `--pretty`

```bash
git log --pretty=format:"%h - %an, %ar : %s"
```

Formatos útiles:

|Código|Significado|
|---|---|
|`%h`|Hash corto del commit|
|`%an`|Nombre del autor|
|`%ar`|Tiempo relativo|
|`%s`|Mensaje del commit|

---

## 🔁 Rangos de commits

```bash
git log main..develop
```

→ Muestra commits que están en `develop` pero no en `main`.

```bash
git log HEAD~5..HEAD
```

→ Últimos 5 commits.

---

## 🧠 `git log -L`: _Historial de una función o rango de líneas_

Esta opción rastrea la **historia de un fragmento de código**, incluso si cambia de contenido, nombre o posición.

### 📌 Sintaxis:

```bash
git log -L <inicio>,<fin>:<archivo>
git log -L :<función>:<archivo>
```

---

### 🧪 Ejemplos:

#### 🔢 Por líneas específicas

```bash
git log -L 10,20:main.py
```

→ Muestra cómo evolucionaron las líneas 10 a 20 de `main.py`.

#### 🧩 Por función (nombre)

```bash
git log -L :procesar_datos:main.py
```

→ Muestra la historia completa de la función `procesar_datos`.

> **Nota**: `-L` requiere que Git pueda analizar la sintaxis del archivo. Funciona mejor en lenguajes como C, Java, Python, etc.

---

## 🔬 Otras opciones menos conocidas

|Opción|Qué hace|
|---|---|
|`--name-only`|Muestra solo los nombres de archivos modificados|
|`--name-status`|Muestra archivos con estado (A/M/D)|
|`--abbrev-commit`|Muestra hashes más cortos|
|`--relative-date`|Muestra fechas relativas (ej: "2 weeks ago")|
|`--reverse`|Muestra los commits desde el más antiguo|
|`--first-parent`|Muestra solo el historial de la rama principal al hacer merge|
|`--no-merges`|Oculta commits de merge|
|`--merges`|Muestra solo commits de merge|

---

## 💡 Trucos útiles

|Comando|Qué hace|
|---|---|
|`git log -S 'texto'`|Muestra commits que **añadieron o eliminaron** una cadena específica|
|`git log -G 'regex'`|Muestra commits con **cambios que coincidan con una expresión regular**|
|`git log -p -S 'config'`|Muestra los parches donde aparece el texto "config"|
|`git log --all --grep='fix'`|Encuentra todos los commits que contienen la palabra "fix"|
|`git log -L :main:main.cpp`|Rastrear la historia de una función `main` en `main.cpp`|

---

## 📜 Salida en archivo

```bash
git log --oneline --graph > historial.txt
```

---
