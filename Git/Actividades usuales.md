
# Descargar info de main trabajando en una rama diferente

1. Vemos si nuestro repo tiene los últimos cambios
```bash
git status
```

2. Nos cambiamos a la rama `main` localmente
```bash
git checkout main
```

3. Actualizamos la rama `main` desde el remoto
```bash
git pull origin main
```

4. Volvemos a nuestra rama
```bash
git checkout mitchel
```

5. Actualizamos la rama con los cambios en la rama `main`

**Opción A**
```bash
git merge main
```

**Opción B**
```bash
git rebase main
```


6. Subir cambios al repositorio remoto
```bash
git push origin mitchel
```



# Merge

Para realizar un push a la rama remota `deploy` desde tu rama local `mitchel`, puedes seguir los pasos detallados a continuación en Git Bash. Aquí asumimos que no te importa el contenido actual de la rama `deploy` y deseas que tu trabajo en `mitchel` sobrescriba lo que esté en `deploy`.

### Pasos detallados:

1. **Asegúrate de estar en la rama local `mitchel`:**
    
    Para confirmar que estás trabajando en la rama correcta, ejecuta:
    
    ```bash
    git branch
    ```
    
    Esto te mostrará una lista de todas las ramas locales, y deberías ver un asterisco (*) al lado de `mitchel`, indicando que estás en esa rama.
    
    Si no estás en la rama `mitchel`, cámbiate a ella con:
    
    ```bash
    git checkout mitchel
    ```
    
2. **Actualizar tu rama local `mitchel` (opcional):**
    
    Si no has hecho un `git pull` recientemente en tu rama `mitchel`, es recomendable hacerlo para asegurarte de que tu rama local está actualizada con los cambios más recientes de la rama remota `mitchel`. Ejecuta:
    
    ```bash
    git pull origin mitchel
    ```
    
    Esto trae los cambios más recientes de la rama `mitchel` remota a tu rama local `mitchel`.
    
3. **Cambiar a la rama remota `deploy`:**
    
    Ahora, necesitas asegurarte de que puedes hacer push a la rama `deploy` del repositorio remoto. Primero, debes cambiar a la rama remota `deploy` en tu repositorio local (sin necesidad de hacer un cambio en tu rama local actual `mitchel`):
    
    ```bash
    git fetch origin
    ```
    
    Esto obtiene todas las ramas remotas y las actualiza en tu repositorio local.
    
    Luego, cambia a la rama remota `deploy`:
    
    ```bash
    git checkout deploy
    ```
    
    Si no tienes una rama local `deploy`, Git la creará automáticamente y la rastreará con la rama remota correspondiente.
    
4. **Sobrescribir el contenido de la rama `deploy` con tu trabajo en `mitchel`:**
    
    Para hacer que el contenido de la rama `mitchel` sobrescriba el contenido de la rama `deploy`, puedes hacer un **hard reset** de la rama `deploy` para que apunte al estado actual de `mitchel`:
    
    ```bash
    git reset --hard mitchel
    ```
    
    Esto hará que tu rama `deploy` local sea exactamente igual a la rama `mitchel` local.
    
5. **Subir la rama `deploy` actualizada a la rama remota `deploy`:**
    
    Ahora que tienes tu rama `deploy` local completamente actualizada con el contenido de `mitchel`, el siguiente paso es hacer el push a la rama remota `deploy`. Como ya has realizado un reset, puedes sobrescribir el contenido remoto sin ningún problema:
    
    ```bash
    git push origin deploy --force
    ```
    
    El flag `--force` es necesario porque estás sobrescribiendo el historial de la rama `deploy` remota con tu contenido de `mitchel`. Ten en cuenta que esto puede afectar a otras personas si están trabajando en esa rama, pero como mencionaste, no te importa lo que esté en la rama `deploy`.
    

### Resumen de los comandos:

1. `git checkout mitchel` – Asegúrate de estar en la rama `mitchel` local.
2. `git pull origin mitchel` – Actualiza tu rama `mitchel` local (opcional).
3. `git fetch origin` – Actualiza las referencias remotas.
4. `git checkout deploy` – Cambia a la rama `deploy`.
5. `git reset --hard mitchel` – Sincroniza `deploy` con `mitchel`.
6. `git push origin deploy --force` – Realiza el push de `deploy` a la rama remota.

Con estos pasos, habrás sobrescrito la rama remota `deploy` con el contenido más actualizado de la rama `mitchel`.


**Sale mensaje de error**
~/Documents/Sigepat-Frontend (mitchel) $ git checkout deploy Unlink of file 'node_modules/@esbuild/win32-x64/esbuild.exe' failed. Should I try again? (y/n) y


El mensaje que estás viendo indica que Git está teniendo problemas para borrar un archivo específico (`esbuild.exe`), probablemente porque está siendo utilizado por otro proceso (como un servidor en ejecución o un editor de código). Esto puede ocurrir cuando tienes archivos bloqueados por otros programas y Git no puede hacer la operación de cambio de rama.

Para resolver este problema, puedes probar los siguientes pasos:

### 1. **Cerrar procesos que puedan estar usando el archivo**

Si tienes algún servidor, editor de código (como VSCode) o terminal que esté utilizando archivos dentro de `node_modules`, ciérralos. Asegúrate de que no haya procesos en segundo plano utilizando archivos en esa carpeta.

### 2. **Eliminar el archivo manualmente**

Si el archivo en cuestión sigue bloqueado, intenta eliminarlo manualmente. Ve a la carpeta `node_modules` y elimina el archivo `esbuild.exe` manualmente desde el explorador de archivos o usando la terminal:

```bash
rm node_modules/@esbuild/win32-x64/esbuild.exe
```

Luego, vuelve a intentar el comando `git checkout deploy`.

### 3. **Reintentar el cambio de rama**

Después de cerrar cualquier proceso que pueda estar usando el archivo o eliminarlo manualmente, intenta nuevamente cambiar a la rama `deploy`:

```bash
git checkout deploy
```

### 4. **Ignorar el archivo si no es necesario**

Si el archivo sigue dando problemas y no es esencial para tu trabajo, puedes intentar excluir la carpeta `node_modules` de Git utilizando `.gitignore`. Si no has hecho esto antes, agrega las siguientes líneas al archivo `.gitignore` en el directorio raíz de tu proyecto:

```
node_modules/
```

Luego, puedes intentar eliminar la carpeta `node_modules` de Git con el siguiente comando, lo que podría resolver el problema de bloqueo de archivos:

```bash
git rm -r --cached node_modules
```

Después de esto, intenta cambiar de rama de nuevo.

### 5. **Forzar el checkout con el flag `-f`**

Si aún no puedes cambiar de rama y estás seguro de que deseas forzar el cambio, puedes usar el flag `-f` para forzar el checkout, ignorando los posibles conflictos:

```bash
git checkout -f deploy
```

Este comando forzará el cambio de rama y descartará cualquier cambio no confirmado que pueda estar causando conflictos. Sin embargo, asegúrate de que no tengas cambios importantes sin confirmar antes de usarlo.

### 6. **Si todo falla, reiniciar la terminal o el sistema**

Si el problema persiste, intenta cerrar la terminal de Git Bash, reiniciar tu computadora o intentar en otra terminal (como Git CMD o Terminal en VSCode) para asegurarte de que no haya ningún proceso bloqueando el archivo.

Una vez que hayas resuelto el problema con el archivo bloqueado, podrás cambiar a la rama `deploy` y continuar con los pasos de `git reset --hard mitchel` para sobrescribir el contenido de esa rama con lo que tienes en `mitchel`.


# Cambiar remote origin

Si ya tienes configurado un remoto (`origin`) apuntando a otro repositorio y deseas cambiarlo para que apunte a `https://github.com/Dirac2022/sigepat-frontend.git`, sigue estos pasos:

### **1. Verifica el remoto actual**

Ya lo hiciste con:

```bash
git remote -v
```

Esto confirma que `origin` actualmente apunta a:

```
https://github.com/Zdm17y4/Sigepat-Frontend.git
```

---

### **2. Elimina el remoto actual**

Primero, elimina el remoto `origin` existente:

```bash
git remote remove origin
```

Puedes verificar que se eliminó correctamente ejecutando nuevamente:

```bash
git remote -v
```

No debería aparecer nada relacionado con `origin`.

---

### **3. Añade el nuevo remoto**

Agrega el nuevo remoto apuntando a `https://github.com/Dirac2022/sigepat-frontend.git`:

```bash
git remote add origin https://github.com/Dirac2022/sigepat-frontend.git
```

Verifica que ahora apunta al repositorio correcto:

```bash
git remote -v
```

Deberías ver algo como esto:

```
origin  https://github.com/Dirac2022/sigepat-frontend.git (fetch)
origin  https://github.com/Dirac2022/sigepat-frontend.git (push)
```

---

### **4. Sube tus cambios al nuevo remoto**

Si ya tienes _commits_ en tu repositorio local y deseas enviarlos al nuevo remoto, usa:

```bash
git push -u origin main
```

Esto configura `origin` y la rama `main` para futuras sincronizaciones.

---

### **Resumen de comandos**

|Paso|Comando|
|---|---|
|Verificar remoto actual|`git remote -v`|
|Eliminar remoto actual|`git remote remove origin`|
|Agregar nuevo remoto|`git remote add origin https://github.com/Dirac2022/sigepat-frontend.git`|
|Verificar nuevo remoto|`git remote -v`|
|Subir cambios al nuevo remoto|`git push -u origin main`|


# Primer commit

```bash
# 1. Inicializar el repositorio Git local
git init

# 2. Agregar el repositorio remoto
git remote add origin https://github.com/DesarrolloDeAplicacion/Beta-App.git

# 3. Verificar que se agregó correctamente
git remote -v

# 4. Agregar todos los archivos al staging
git add .

# 5. Realizar el primer commit
git commit -m "Primer commit: Inicialización del proyecto Android"

# 6. Cambiar a la rama principal (desde 2020 GitHub usa 'main' por defecto)
# 1. Renombra la rama actual (tradicionalmente 'master') a 'main'
# 2. Fuerza el cambio incluso si existe otra rama con ese nombre
git branch -M main

# 7. Subir los cambios al repositorio remoto
git push -u origin main
```

```bash
git branch -M main
```

| Comando | Significado                                                |
| ------- | ---------------------------------------------------------- |
| branch  | Comando para gestionar ramas                               |
| -M      | Flag de "move/rename" forzado (mayúscula significa forzar) |
| main    | Nuevo nombre de la rama                                    |

```bash
git push -u origin main
```

| Comando | Significado                         |
| ------- | ----------------------------------- |
| -u      | Flag de "upstream" (--set-upstream) |
| origin  | Nombre del repositorio remoto       |
| main    | Nombre de la rama a subir           |

El flag `-u` es especialmente importante porque:

1. Establece una relación de seguimiento entre tu rama local y la rama remota
2. En futuros push, solo necesitarás escribir `git push` sin especificar origin main
3. Te permite ver la relación entre ramas locales y remotas con `git branch -vv`

# Cambiar nombre de una rama

Nombre antiguo `master`, nuevo nombre `main`
```sh
git branch -m master main
```


# Eliminar ramas
## 🧹 Eliminar ramas **locales**

### ✅ 1. Comando básico

```bash
git branch -d nombre_rama
```

Esto elimina la rama **localmente**, pero **solo si ya está mergeada** con otra (como `main` o `develop`).

#### Ejemplo:

```bash
git branch -d feature/login
```

---

### ⚠️ Forzar eliminación (aunque no esté mergeada)

```bash
git branch -D nombre_rama
```

Úsalo con cuidado. Esto borra la rama sin importar si tiene cambios pendientes o no.

```bash
git branch -D feature/experimental-bugfix
```

---

## 🚀 Eliminar ramas **remotas**

### ✅ 2. Comando clásico con `push`

```bash
git push origin --delete nombre_rama
```

#### Ejemplo:

```bash
git push origin --delete feature/login
```

Esto borra la rama del **repositorio remoto (GitHub, GitLab, etc.)**.

---

## 🕵️‍♂️ Ver todas tus ramas

### Ramas locales:

```bash
git branch
```

### Ramas remotas:

```bash
git branch -r
```

---

## 🧽 Limpiar referencias a ramas remotas eliminadas

Cuando alguien borra una rama remota y vos seguís viendo `origin/feature/vieja`, podés limpiar eso con:

```bash
git fetch -p
```

(`-p` es de _prune_, podar)

---

## 🎯 Recap rápido

|Acción|Comando|
|---|---|
|Borrar rama local|`git branch -d nombre_rama`|
|Forzar borrado local|`git branch -D nombre_rama`|
|Borrar rama remota|`git push origin --delete nombre_rama`|
|Limpiar ramas remotas viejas|`git fetch -p`|

---


# Eliminar archivos ya rastreados por Git para agregarlos al .gitignore

Cuando tienes archivos que ya están siendo rastreados por Git pero quieres ignorarlos moviéndolos al `.gitignore`, necesitas seguir estos pasos:

## Pasos para ignorar archivos rastreados:

1. **Primero, agrega los archivos/rutas a tu `.gitignore`**:
   ```bash
   echo "nombre-del-archivo-o-carpeta/" >> .gitignore
   ```

2. **Luego, elimina estos archivos del caché de Git** (esto no borra los archivos físicamente):
   ```bash
   git rm --cached nombre-del-archivo-o-carpeta
   ```
   Para eliminar un directorio completo y su contenido:
   ```bash
   git rm -r --cached nombre-del-directorio/
   ```

3. **Si quieres eliminar todos los archivos rastreados que coincidan con el .gitignore**:
   ```bash
   git rm -r --cached .
   git add .
   ```

4. **Finalmente, confirma los cambios**:
   ```bash
   git commit -m "Eliminar archivos rastreados que ahora están en .gitignore"
   ```

## Notas importantes:
- El comando `--cached` es crucial porque elimina los archivos solo del índice de Git, no de tu sistema de archivos.
- Después de esto, los archivos no serán rastreados por Git pero seguirán existiendo en tu directorio de trabajo.
- Si los archivos ya fueron confirmados en el historial de Git, necesitarás este proceso para dejar de rastrearlos en futuros commits.
