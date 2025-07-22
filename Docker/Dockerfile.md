
<img src="https://miro.medium.com/v2/resize:fit:1100/format:webp/0*CP98BIIBgMG2K3u5.png" >

Dockerfile is a text file that contains a list of commands (instructions), which describes how a Docker image is built based on them. The command `docker build` tells Docker to build the image by following the content (instructions) inside the Dockerfile.

## Structure and Format

Dockerfile starts with a `FROM` command which indicates the base image. The subsequent commands in the Docker file are executed on the base image which must be a valid image.

Here is the format:

```dockerfile
# Comments
COMMAND arguments
```

A comment line starts with `#` and describes the purpose or whatever you want.

> [!tip] The `COMMAND` is not required to be uppercase but it is a convention here to distinguish them from arguments.

**An example**

```Dockerfile
# The latest version of Ubuntu is used as the base image for this Dockerfile.
FROM ubuntu:latest

# Set the author field for the generated image.
MAINTAINER tony.montana@example.com

# Run some commands.  
RUN apt-get update && apt-get install -yq curl
RUN apt-get clean

# Commands to run when the generated image gets launched
CMD ["top"]
CMD ["ls", "-l"]

# Set working directory and environment variables.  
WORKDIR /root
ENV VAR1 version1

# Add a shell script to the generated iamge.
ADD run.sh /root/run.sh
RUN chmod +x run.sh

# Set entry point and argments for the generated image.
ENTRYPOINT ["./run.sh"]
CMD ["arg1"]
```


---

## `ENTRYPOINT`
En un **Dockerfile**, `ENTRYPOINT` es una instrucción que define el **comando principal** que se ejecutará cuando el contenedor inicie. Determina la aplicación o proceso que mantendrá el contenedor en ejecución.  


🔹 **¿Qué hace `ENTRYPOINT`?**  
- Define el **ejecutable por defecto** del contenedor.  
- Los argumentos pasados con `docker run` se añaden al comando del `ENTRYPOINT`.  
- Si no se especifica, el `ENTRYPOINT` por defecto es `/bin/sh -c` (en imágenes basadas en Linux).  


📌 **Diferencia entre `ENTRYPOINT` y `CMD`**  

| `ENTRYPOINT`                                                           | `CMD`                                                                                      |
| ---------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| Define el **comando base** (siempre se ejecuta).                       | Define **argumentos por defecto** (se pueden sobrescribir).                                |
| Si se usa, `CMD` actúa como parámetro adicional.                       | Si no hay `ENTRYPOINT`, `CMD` es el comando ejecutado.                                     |
| Ejemplo: `ENTRYPOINT ["python"]` + `CMD ["app.py"]` → `python app.py`. | Ejemplo: `CMD ["python", "app.py"]` → Se puede reemplazar con `docker run mi-imagen bash`. |


📂 **Sintaxis**  
Hay dos formas de definir `ENTRYPOINT`:  

**1. Forma exec (recomendada)**  
```dockerfile
ENTRYPOINT ["ejecutable", "param1", "param2"]
```  
Ejemplo:  
```dockerfile
ENTRYPOINT ["python", "app.py"]
```  

**2. Forma shell**  
```dockerfile
ENTRYPOINT comando param1 param2
```  
Ejemplo:  
```dockerfile
ENTRYPOINT python app.py
```  
*(Esta forma ejecuta el comando en un shell, lo que puede afectar señales como `SIGTERM`).*  


**🔥 Ejemplos prácticos**  

Ejemplo 1: `ENTRYPOINT` + `CMD`  
```dockerfile
# Dockerfile
FROM alpine
ENTRYPOINT ["echo", "Mensaje:"]
CMD ["Hola Docker"]
```  
- Si ejecutas:  
  ```bash
  docker run mi-imagen
  ```  
  → Salida: `Mensaje: Hola Docker`.  

- Si pasas argumentos:  
  ```bash
  docker run mi-imagen "¡Hola Mundo!"
  ```  
  → Salida: `Mensaje: ¡Hola Mundo!`.  


Ejemplo 2: Sobrescribir `ENTRYPOINT`  
- Para cambiarlo temporalmente, usa `--entrypoint`:  
  ```bash
  docker run --entrypoint bash mi-imagen
  ```  


📌 **¿Cuándo usar `ENTRYPOINT`?**  
1. **Contenedores como comandos**: Si quieres que el contenedor actúe como un ejecutable (ejemplo: `docker run mi-cli --help`).  
2. **Procesos persistentes**: Servicios como `nginx`, `postgres`, etc.  
3. **Scripts de inicialización**: Si necesitas ejecutar un script al iniciar (ejemplo: `ENTRYPOINT ["/app/start.sh"]`).  


🚀 **Conclusión**  
- `ENTRYPOINT` = **Comando principal** (difícil de sobrescribir).  
- `CMD` = **Argumentos por defecto** (fácil de modificar en `docker run`).  
- Usa `ENTRYPOINT` para aplicaciones que deben ejecutarse siempre de una forma específica.  

---

## Build Context

To build your Docker image, you could call `docker image build` command by specifying building directory with the Dockerfile in the terminal and some arguments can be provided as well. For example:

```sh
docker image build .
```

It tells Docker to build an image according to the Docker file in the current directory, called the **`context`** of the build.

An important note here is the build is run by the Docker daemon instead of the CLI, so the entire context is transferred to the daemon. A warning from Docker document is

>[!warning] Do not use your root directory, `/`, as the `PATH` as it causes the build to transfer the entire contents of your hard drive to the Docker daemon.

A `.dockerignore` file is useful sometimes when you want to ignore some files in the Docker image context directory.


## Layers

When the Docker daemon builds your image, it executes the steps defined in the Dockerfile. A container is generated in each step and the instruction is run inside of the generated container. Once the instruction succeeds, the container is stored as a new image, as a new layer is added. The next instruction will build another new one on top of the previous one.

The fully output of the example Dockerfile: 

```sh
Sending build context to Docker daemon  3.584kB
Step 1/12 : FROM ubuntu:latest
 ---> d70eaf7277ea
Step 2/12 : MAINTAINER rocky.chen@example.com
 ---> Running in 5d1f44d64602
Removing intermediate container 5d1f44d64602
 ---> 82eb396b28ec
Step 3/12 : RUN apt-get update && apt-get install -yq curl
 ---> Running in cc6adb835c4d
...
Removing intermediate container cc6adb835c4d
 ---> bbd0dc87c576
Step 4/12 : RUN apt-get clean
 ---> Running in 7664a4778017
Removing intermediate container 7664a4778017
 ---> a9ed19e6119d
Step 5/12 : CMD ["top"]
 ---> Running in 7e37bb170506
Removing intermediate container 7e37bb170506
 ---> d6c8736f0e9f
Step 6/12 : CMD ["ls", "-l"]
 ---> Running in cbd1a7512232
Removing intermediate container cbd1a7512232
 ---> 0c087c832e7f
Step 7/12 : WORKDIR /root
 ---> Running in 3068d7075458
Removing intermediate container 3068d7075458
 ---> d80343d04808
Step 8/12 : ENV VAR1 version1
 ---> Running in ae6480ddac50
Removing intermediate container ae6480ddac50
 ---> 3c649e8e249c
Step 9/12 : ADD run.sh /root/run.sh
 ---> b0419c4d6864
Step 10/12 : RUN chmod +x run.sh
 ---> Running in 12520302b333
Removing intermediate container 12520302b333
 ---> f52955a93631
Step 11/12 : ENTRYPOINT ["./run.sh"]
 ---> Running in 22bc5cc335b1
Removing intermediate container 22bc5cc335b1
 ---> 409dee822026
Step 12/12 : CMD ["arg1"]
 ---> Running in 44cf42bcd050
Removing intermediate container 44cf42bcd050
 ---> 8c2b84201d65
Successfully built 8c2b84201d65
Successfully tagged myimage:latest
```

There are 12 steps per the output texts because there are 12 lines of instructions in the Dockerfile.

After all steps complete, the image could be shown in the output of the command `docker image ls`:

```sh
$ docker image ls 
REPOSITORY  TAG    IMAGE ID      CREATED         SIZE 
my_image    latest 6c284ed9fe68  17 minutes ago  115MB
```


## Cache

Let's run the build command again with the same Dockerfile:

```sh
$ docker build -t my_image .  
Sending build context to Docker daemon 3.584kB  
Step 1/12 : FROM ubuntu:latest  
---> d70eaf7277ea  
Step 2/12 : MAINTAINER rocky.chen@example.com  
---> **Using cache**  
---> 82eb396b28ec  
Step 3/12 : RUN apt-get update && apt-get install -yq curl  
---> Using cache  
---> bbd0dc87c576  
Step 4/12 : RUN apt-get clean  
---> Using cache  
---> 738becba91a0  
Step 5/12 : CMD ["top"]  
---> Using cache  
---> 58e31420c1dd  
Step 6/12 : CMD ["ls", "-l"]  
---> Using cache  
---> ec643d75f7ee  
Step 7/12 : WORKDIR /root  
---> Using cache  
---> 4c79437f5c37  
Step 8/12 : ENV VAR1 version1  
---> Using cache  
---> 8ce59472dc52  
Step 9/12 : ADD run.sh /root/run.sh  
---> Using cache  
---> ab7f0e31b020  
Step 10/12 : RUN chmod +x run.sh  
---> Using cache  
---> 769075a61ee3  
Step 11/12 : ENTRYPOINT ["./run.sh"]  
---> Using cache  
---> 26b434f12885  
Step 12/12 : CMD ["arg1"]  
---> Using cache  
---> 6c284ed9fe68  
Successfully built 6c284ed9fe68  
Successfully tagged my_image:latest
```

The **`Using cache`** in each step indicates that the Docker daemon used cache directly to generate the intermedium image instead of building again.

The cache is used when the instructions in the Dockerfile are same or unchanged with the previous version.


## Image Launch

Once the image is built successfully, it is stored in the local registry by default. To list all images, use following command:

```sh
$ docker image ls -a
```

Next, we could start to launch the image with a Docker container. First, let’s get started with a simple version of Dockerfile:

```sh
# The latest version of Ubuntu is used as the base image for this Dockerfile.
FROM ubuntu:latest
# Set the author field for the generated image.
MAINTAINER rocky.chen@example.com
# Run some commands.
RUN apt-get update && apt-get install -yq curl
RUN apt-get clean
```

Then, build it with:

```sh
$ docker build -t my_image .
```

Now, we have an image in the Docker local registry and launch it:

```sh
$ docker run -it --rm my_image /bin/bash
root@8f4991177fe8:/# curl
curl: try 'curl --help' or 'curl --manual' for more information
```

The `-it` instructs Docker to allocate a pseudo-TTY connected to the container's stdin

---
>[!tip] `-it`
>El flag `-it` es una combinación de dos opciones
>- `-i (--interative)`: Mantiene STDIN (entrada standard) abierto, permitiendo interactuar con el contenedor.
>- `-t (--tty)`: Asigna una terminal virtual (TTY) al contenedor, lo que permite una interfaz interactiva similar a un shell normal.
>- Si solo se usa `-i` , puedes enviar entrada al contenedor, pero no tendrás un prompt de terminal (formato de shell amigable).
>- Si solo usas `-t`, el contenedor tendrá una terminal, pero no podrás interactuar con ella.
>
> **TTY** es una terminal virtual que permite la comunicación entre el usuario y un programa en modo texto. Es importante en Docker ya que
> - Sin TTY, los comandos interactivos no funcionarían correctamente.
> - Cuando usas `-t`, Docker crea un pseudo-TTY para que el contenedor se comporte como una terminal normal.

---

The `-rm` means deleting the container after it exists.


## Instruction - `CMD`

`CMD` command is to provide defaults when a container is being launched, including an executable or arguments for `ENTRYPOINT`.

The `CMD` instruction has three forms:

1. `CMD ["executable", "param1", "param2"]` (exec form, this is the preferred form)
2. `CMD ["param1", "param2"]` (as default parameters to `ENTRYPOINT`)
3. `CMD command param1 param2` (shell form)

**Notes**

- Only the last one `CMD` instruction takes effect in a Dockerfile
- If `CMD` provides the default arguments for `ENTRYPOINT`, both `CMD` and `ENTRYPOINT` must be **JSON** array formatted.
- In **JSON** array format, double-quote `"` must be used.
- Exec format does not invoke a command shell.
- For example, `CMD ["echo", "$HOME"]` outputs `$HOME` exactly instead of the environment value of `$HOME`. To echo the value, do this:

```dockerfile
CMD echo $HOME
# or
CMD ["sh", "-c", "echo $HOME"]
```


---
>[!tip] `sh -c`
>- `sh` es el interprete de comandos (shell) más básico en sistemas  Unix/Linux. Es equivalente a `bash` en muchos casos, pero más minimalista. Docker lo usa por defecto cuando necesitas ejecutar comandos en una shell.
>
>- `-c` le indica al shell `sh` que ejecute el siguiente texto como un comando, en lugar de leer comandos desde la entrada estándar.
>
> Se usa `["sh", "-c", "comando"]` cuando se necesite
> 	- Variables (`$VAR`).
> 	- Operadores (`&&`, `||`, `>`, `*`).
> 	- Comandos múltiples.
> 

---

## Instruction - `ENTRYPOINT`

The `ENTRYPOINT` specifies an executable as an entry point of a container. When the container is launched, the command specified by `ENTRYPOINT` will be run first.

For `ENTRYPOINT` instruction, there are two forms:

- `ENTRYPOINT ["executable", "param1", "param2"]` (exec form, the preferred form)
- `ENTRYPOINT command param1 param2` (shell form)

**Notes**

1. Any command arguments passed to  `docker run` will be appended to the `ENTRYPOINT` command.
2. The command arguments passed to `docker run` will override the ones provided by `CMD`.
3. `ENTRYPOINT` could be overridden by running `docker run --entrypoint <command and arguments>`.

## Docker example

Now, let’s go back the our first Dockerfile example. Before building the image, here is the content of `run.sh` file in the same directory with Dockerfile:



```sh
#!/bin/shecho "The current directory : $(pwd)"  
echo "The VAR1 variable : $VAR1"  
echo "There are $# arguments: $@"
```

Then, build it and run:

```sh
$ docker build -t myimage .  
$ docker run -it --rm myimage  
The current directory : /root  
The VAR1 variable : version1  
There are 1 arguments: arg1
```

We can see the output reflects `ENTRYPOINT` and `CMD` instructions in the last two line of the Dockerfile.

Now, let’s try to push some arguments to `docker run`:

```sh
$ docker run -it --rm myimage arg2 arg3  
The current directory : /root  
The VAR1 variable : version1  
There are 2 arguments: arg2 arg3
```

As expected, the input arguments (`arg2` and `arg3`) override the `CMD` at the last line.
