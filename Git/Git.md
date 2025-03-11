
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
git config --global core.editor "core --wait"
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

## Comando `git status`
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
```

```shell
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
```
rm archivob.txt
```

Luego, tenemos dos opciones, usar `git add` para actualizar los cambios o `git restore` para descartar los cambios en el directorio de trabajo

Agregamos la eliminación
```git
git add archivob.txt
```

```git
	git commit -m "eliminando archivo" -a
```

## Restaurar un archivo modificado o borrado
Si se ha eliminado un archivo `archivo.txt` (por ejemplo manualmente) del directorio de trabajo
```git
git restore archivo.txt
```

Con esto restauras el archivo del área de preparación. También sirve para restaurar el archivo a la ultima versión en la que se hizo commit

Si hemos hecho un cambio en un determinado archivo `archivo.txt` y hemos guardado el archivo en cuestión, usando `checkout` podemos restaurar el archivo a la ultima versión en la que se le hizo commit
```git
git checkout archivo.txt
```

Para restaurar un archivo modificado y que se ha subido al area de *Staging* con `git add`
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
```git
git mv dirac.txt archivo2.txt
```
Al usar el comando `status` saldrá un archivo al que se le ha renombrado y esta listo para el `commit`
```git
git commit -m "Cambio de nombre de dirac a archivo2" -a
```

> [!tip]
> Si cambiamos el nombre de un archivo y hacemos `checkout` con el nombre anterior, el comando `checkout` reestablece este archivo anterior, mientras que el el archivo con el nuevo nombre permanece inalterado.


### Uso de `git show`
Se utiliza para mostrar información detallada sobre objetos en Git como commits, árboles o blobs.


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
```git
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

### Resumen del flujo típico

1. Realizas varios _commits_ localmente para registrar cambios pequeños y lógicos.
2. Revisas los _commits_ pendientes con `git log`.
3. Cuando los cambios están listos, haces un solo _push_ para enviarlos al remoto.

¿Te gustaría practicar algún comando o explorar un caso particular?