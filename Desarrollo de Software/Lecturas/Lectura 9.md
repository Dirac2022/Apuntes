### Terminología de Git
#### Rama  

Una **rama** representa una línea de desarrollo independiente. Las ramas sirven como una abstracción del proceso de editar, preparar y confirmar (commit) cambios. Se pueden considerar como una forma de obtener un directorio de trabajo, área de preparación e historial de proyecto completamente nuevos. Los nuevos commits se registran en el historial de la rama actual, lo que crea una bifurcación en la historia del proyecto.

```
      commit A
         |
      commit B
       / 
commit C (rama secundaria)
```
#### Flujo de trabajo centralizado  
  
Si tus desarrolladores ya están acostumbrados a Subversion, el **flujo de trabajo centralizado** te permite disfrutar de los beneficios de Git sin tener que adaptarte a un proceso completamente nuevo. Además, funciona como una transición amigable hacia flujos de trabajo más orientados a Git.

```
 [Dev1]      [Dev2]
    \          /
     \        /
    [Servidor Central]
```
#### Flujo de trabajo con ramas de funcionalidades  

El **flujo de trabajo con ramas de funcionalidades** se basa en el flujo centralizado, encapsulando nuevas funcionalidades en ramas dedicadas. Esto permite el uso de solicitudes de extracción (pull requests) para discutir los cambios antes de integrarlos al proyecto oficial.

```
        main
         |
         +----> feature (nueva funcionalidad)
```

#### Bifurcación (Forking)  

En lugar de usar un único repositorio en el servidor como la base de código “central”, el **forking** otorga a cada desarrollador su propio repositorio en el servidor. Esto significa que cada colaborador posee dos repositorios Git: uno local (privado) y otro público en el servidor.

```
   [Repositorio local]  <---->  [Repositorio público en servidor]
```

#### Flujo de trabajo Gitflow  

El **flujo de trabajo Gitflow** agiliza el ciclo de lanzamiento utilizando ramas aisladas para el desarrollo de características, la preparación de lanzamientos y el mantenimiento. Su modelo de ramificación estricto aporta una estructura muy necesaria para proyectos de mayor envergadura.

```
           feature
              \
           develop --- release --- main/master
              /
         hotfix (mantenimiento)
```
#### HEAD  

**HEAD** es la forma que tiene Git de referirse a la instantánea actual. Internamente, el comando `git checkout` simplemente actualiza el HEAD para que apunte a la rama o commit especificado. Cuando apunta a una rama, Git opera normalmente; pero si se hace checkout a un commit, se entra en un estado de "HEAD separado" (detached HEAD).

```
HEAD --> commit actual
```

---
 **🔁 ¿Qué pasa cuando haces `git checkout <commit>`?**
Cuando haces:
```sh
git checkout abc1234
```
(donde `abc1234` es el hash de un commit), **ya no estás en ninguna rama**. Estás viendo el estado del proyecto en ese commit en particular, **pero sin rama asociada**.

Eso se llama **"estado de HEAD separado"** (en inglés: _detached HEAD_), porque ahora `HEAD` **apunta directamente a un commit**, no a una rama.


**⚠️ ¿Por qué tener cuidado con el detached HEAD?**

Porque si haces cambios y commits en este estado, como por ejemplo:

```sh
git commit -am "Cambios sobre commit viejo"`
```

Esos commits **no estarán en ninguna rama**. Y si cambias de rama después, **los podés perder fácilmente**, a menos que:

1. Crees una nueva rama para guardarlos: `git checkout -b nueva-rama`
2. O los mezcles manualmente a otra rama.

---

#### Hook  
 
Un **hook** es un script que se ejecuta automáticamente cada vez que ocurre un evento específico en un repositorio Git. Los hooks permiten personalizar el comportamiento interno de Git y desencadenar acciones personalizadas en puntos clave del ciclo de desarrollo.


```
[Evento Git] --> [Script Hook] --> [Acción personalizada]
```

#### Main (principal)  

**Main** es la rama de desarrollo por defecto. Cada vez que se crea un repositorio Git, se genera una rama llamada "main" que se establece como la rama activa.

```
main: commit1 --> commit2 --> commit3
```

#### Solicitud de extracción (Pull request)  

Las **solicitudes de extracción** son una característica que facilita la colaboración entre desarrolladores (por ejemplo, en Bitbucket). Proporcionan una interfaz web amigable para discutir los cambios propuestos antes de integrarlos al proyecto oficial.

```
(feature branch) ---> [Pull Request] ---> (main branch)
```
#### Repositorio  

Un **repositorio** es una colección de commits, ramas y etiquetas que identifican los cambios y puntos en el historial del proyecto.

```
[Repositorio]
 |-- Commit A
 |-- Commit B
 |-- Ramas: main, feature, etc.
 |-- Etiquetas: v1.0, v2.0, etc.
```

#### Etiqueta (Tag)  

Una **etiqueta** es una referencia que se utiliza normalmente para marcar un punto particular en la cadena de commits. A diferencia de HEAD, una etiqueta no se actualiza con cada commit.

```
commit ---[Tag v1.0]
```
#### Control de versiones  
  
El **control de versiones** es un sistema que registra los cambios realizados en un archivo o conjunto de archivos a lo largo del tiempo, permitiéndote recuperar versiones específicas en el futuro.

```
[Versión 1] --> [Versión 2] --> [Versión 3]
```
#### Árbol de trabajo (Working tree)  

El **árbol de trabajo** es el conjunto real de archivos que se han extraído (``checkout``) y que normalmente contiene el contenido del árbol del commit al que apunta ``HEAD``, junto con cualquier cambio local que aún no se ha confirmado (``commit``).
```
Working Tree:
 ├── file1.txt (modificado)
 ├── file2.txt
 └── carpeta/
      └── file3.txt
```
