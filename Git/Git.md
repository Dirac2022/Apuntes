
Tipos de jerarquía en git
- Sistema: para la computadora
- Global: para el mismo usuario
- Local: para repositorios


# Configuraciones básicas
Configuraciones a nivel global

```git
git config --global user.name
```

```git
git config --global user.email "daronmitchel@gmail.com"
```

Lista de configuraciones 
```
git config --list
```

Lista de configuraciones globales
```git
git config --global --list
```

Agregar editor de texto
```git
git config --global core.editor "core --wait"
```


>[!tip] comando --wait
> Espera a que se cierre la ventana para realizar los cambios, por ejemplo si se esta trabajando en un editor


Para configurar el salto de línea y retorno de carro automático
```git
git config --global core.autocrlf true
```


## Areas
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



# Crear repositorio

```git
mkdir repo
```

```git
cd repo
```


Inicializar git dentro de la carpeta `repo`
```git
git init
```
Este comando convierte un directorio existente en un nuevo repositorio de Git, listo para el control de versiones.
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
```git
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
> - `git status -s` Nos muestra una salida más compacta y fácil de leer
> 	-  M archivo modificado
> 		-  Si esta en verde, esta agregado al *Staging* y esta listo para commit
> 		- Si esta en rojo, no esta agregado al *Staging*
> 	- A archivo agregado al área de preparación o *Staging*
> 	- ?? Archivo no rastreado
> - `git status -b` Muestra información adicional sobre la rama actual y su relación con la rama remota.
> Si esta en verde, esta agregado al *Staging* y esta listo para commit
> Si esta en rojo, no esta agregado al *Staging*


Remover el archivo del *Staging Area*
```git
git rm --cached archivo.txt
```

Para subir un archivo al repositorio 
- Agregando un mensaje en el commit
```git
git commit -m "Agregando los dos primeros archivos de texto"
```

- Agregando un mensaje con el editor de texto
Si tenemos un archivo adicional `archivob.txt`
```git
git add archivob.txt
```

```git
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
