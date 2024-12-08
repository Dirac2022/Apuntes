
Docker es un contenedor que encapsula software en un sistema de ficheros que contiene todo lo necesario para su ejecución.

Garantiza estabilidad y portabilidad a todos los sistemas. Docker es
- **Ligero** a la hora de consumir recursos
- **Abierto** y compatible (Docker es software libre)
- **Seguro** permitiendo el aislamiento entre contenedores.

<div style="text-align:center">
<figure>
<img src="https://media.licdn.com/dms/image/v2/D4D12AQGqjSqEGElq1w/article-inline_image-shrink_1500_2232/article-inline_image-shrink_1500_2232/0/1688608296456?e=1738800000&v=beta&t=XK9rbBpUbeiJiC2ehxLyhwGHA_tGcbAuhzKaKkKVc98" alt="">
<figcaption>
Docker - Contenedores vs Maquinas Virtuales
</figcaption>
</figure>
</div>


# Docker Engine CLI
- Docker dispone de una API remota para su gestión y uso.
- Tambien dispone de una CLI.
- El demonio de Docker se ejecuta en segundo plano y gestiona la ejecución de los contenedores.


# Docker CLI

Muestra el estado del servicio
```bash
docker info
```

Contenedor de test
```bash
docker run hello-world
```

Contenedor real e interactivo
```bash
docker run -ti ubuntu /bin/bash
```

Lista de contenedores en ejecución (`-a` contenedores parados)
```bash
docker ps
```

```bash
docker ps -a
```

```bash
docker run -rm -t -i <image> <command>
```

Alterar el estado de contenedores
```bash
docker stop <container>
```

```bash
docker kill <container>
```

```bash
docker rm <container>
```

	
# Imagenes
Una imagen es un binario ejecutable que incluye todo lo necesario para ejecutar una aplicación: código, tiempo de ejecución, librerías y configuraciones.

- Las utilizaremos como punto de inicio de nuestros contenedores.
- Definen una serie de capas que añaden funcionalidad a partir de una **imagen base** (SO)
- Podemos gestionar imágenes:
	- Definidas por nosotros (Dockerfile)
	- Descargadas desde un **registro**

![[images base docker.png]]


# Contenedores
Un contenedor es una unidad de software estándar que empaqueta el código y todas sus dependencias para que la aplicación se ejecute de una manera rápida y confiable en cualquier entorno.


<div style="text-align:center">
<figure>
<img src="https://miro.medium.com/v2/resize:fit:828/format:webp/0*CP98BIIBgMG2K3u5.png" alt="">
<figcaption>
Dockerfile, Image and Container
</figcaption>
</figure>
</div>

- Los contenedores se inician a partir de una imagen, creando su propia estructura de archivos.
- Pueden estar en ejecución o detenidos en cualquier momento.
- Los cambios realizados dentro del contendedor son persistentes, **pero solo dentro del contenedor mismo**.
- Aunque generalmente se ejecutan como servicios, es posible acceder a ellos de manera interactiva,
- Docker permite la configuración de redes y volúmenes compartidos entre contenedores y el host.

```bash
docker run --rm -ti python:3.6-slim
```

```bash
docker run --rm -ti node:8-slim
```

```bash
docker run --rm nginx
```


Listar imágenes en nuestro sistema local
```bash
docker images ls
```

Borrar imágenes en nuestro sistema local
```bash
docker rmi <nombre>/<id>
```

Limpiar el sistema de Docker eliminando recursos que no estén en uso
```bash
docker system prune
```




# Registro

<div style="text-align:center">
<figure>
<img src="https://i.ytimg.com/vi/JVrx3aF3FPo/maxresdefault.jpg" alt="">
<figcaption>
</figcaption>
</figure>
</div>


- **Repositorios** a los que podemos subir imágenes para más tarde utilizarlas nosotros, colaboradores o terceros.
```bash
docker push
```

```bash
docker pull
```

- Las imágenes están **disponibles** a través del cliente Docker.
- Permite el control de versiones, etiquetado, etc.
```bash
<image-name>:<tag>
```

```bash
ubuntu:latest
```

```bash
ubuntu:xenial
```


# Comunicacion entre contenedores: Redes

- Los contenedores pueden conectarse entre ellos o a otros sistemas (por ejemplo host) mediante redes.
- Podemos crear múltiples adaptadores y controlar los puertos accesibles a cada contenedor para crear diversas arquitecturas.

```bash
docker network create MyNetwork
docker run --rm --network MyNetwork -p 80:80
```


# Persistencia de datos: Volumenes

- Docker puede crear **volúmenes de datos persistentes** que se montan sobre el sistema de ficheros de un contenedor.
- Los volúmenes pueden **compartirse** entre contenedores para establecer **comunicación**.
- Podemos montar un directorio local como un volumen de datos.

```bash
docker run --rm -v /home/folder:/root/app /bin/bash
```

# Dockerfiles

- Define la construcción (**build**) de una imagen de docker.
- Cada **comando** crea una **capa**, almacenada en una cache.
- Las imágenes y contenedores pueden **compartir capas**.

```dockerfile
FROM ubuntu:14.04

RUN apt-get update && apt-get install -y apache2
COPY index.html /var/www/

EXPOSE 80

CMD ["/usr/sbin/apache2", "-D", "FOREGROUND"]
```

- `FROM` : inicia la creación del contenedor a partir de una imagen base.
- `ubuntu:14.04`: indica que la imagen base será Ubuntu en su versión 14.04
- `RUN`: ejecuta un comando en el contenedor durante el proceso de construcción.
- `apt-get update`: actualiza la lista de paquetes disponibles en los repositorios de Ubuntu-
- `apt-get install -y apache2`: instala el servidor web Apache2 en el contenedor. La opción `-y` se usa para aceptar automáticamente todas las preguntas o advertencias que puedan surgir durante la instalación.
- `COPY` copia archivos o directorios desde el contexto de construcción (máquina local) al contenedor.
- `EXPOSE 80`: indica que el contenedor se escuchará en el puerto 80.
- `CMD`: define el comando que se ejecutará cuando se inicie un contenedor desde esta imagen.
- `"/usr/sbin/apache2"`: especifica la ruta del binario de Apache dentro del contenedor.
- `"-D", "FOREGROUND"`: sirve para que Apache se ejecute en primer plano. En caso contrario, el contenedor terminará inmediatamente después de iniciarse.

## Dockerfiles: Buenas practicas

- Diseña cada contenedor para una **función específica**.
	-  Este principio se basa en el concepto de *microservicios*. Un contenedor debe estar diseñado para hacer **una única tarea** o función de manera eficiente.
- Los contenedores deben ser **efímeros**.
	- No se debe guardar el estado de manera permanente en el contenedor. Si se elimina o reinicia, debe poder ser recreado sin perder funcionalidad.
- Minimiza el número de capas y su **tamaño** (cache).
- Cuidado con la **seguridad**, evita usar root y vigila los puertos.
- Cuidado con la **privacidad**, todas las capas están disponibles.


# Docker Cheat Sheet

## Build
Build an image from the Dockerfile in the current directory and tag the image
```bash
docker build -t myimage:1.0
```

List all images that are locally stored with the Docker Engine
```bash
docker image ls
```

Delete an image from the local image store
```bash
docker image rm alpine:3.4
```


## Share
Pull an image from a registry
```shell
docker pull myimage:1.0
```

Retag a local image with a new image name and tag
```bash
docker tag myimage:1.0 myrepo/myimage:2.0
```

Push an image to a registry
```bash
docker push myrepo/myimage:2.0
```

## Run
Run a container from the Alpine version 3.9 image, name the running container “web” and expose port 5000 externally, mapped to port 80 inside the container
```bash
docker container run --name web -p 5000:80 alpine:3.9
```

Stop a running container through SIGTERM
```bash
docker container kill web
```

List the networks
```bash
docker network ls
```

List the running containers (add ``--all`` to include stopped containers) 
```bash
docker container ls
```

Delete all running and stopped containers
```bash
docker container rm -f $(docker ps -aq)
```

Print the last 100 lines of a container's log
```bash
docker container logs --tail 100 web
```
