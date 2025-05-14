
Completar hasta lab 25

HackMyVM
-> HMVLabs -> Chapter 1 Go Venus -> Flags -> 

--- 
Investigacion (PC 05)
buscar 5 un papers sobre vulnerabilidades de los LLM de esos 5 profundizar sobre uno , podemos guiarnos con owasp2025 

---
Descargar kalilinux para VMBox
[Kali Linux 2024.3 VM Images | Kali Linux 2024.3 VirtualBox Image | Kali Linux 2024.3 VMware Image](https://www.linuxvmimages.com/images/kalilinux/)

[**https://www.linuxvmimages.com/**](https://www.linuxvmimages.com/)

---

- Descargar de HackMyVM

![[Pasted image 20250329180434.png]]


-   **Kalilinux**
-   **Centos**
-   **Ubuntu**

[**https://hackmyvm.eu**](https://hackmyvm.eu)

**Descargar la máquina virtual de canto**

**Conectarse al servicio ssh**

- ssh nombredeusuario@servidor --p puerto
- Host: venus.hackmyvm.eu
- Port: 5000
- User: hacker
- Pass: havefun!


```sh
ssh hacker@venus.hackmyvm.eu -p 5000
```

> [!Note]
> Se esta intentado conectarse al servidor `venus.hackvm.eu` usando el usuario `hacker` a través del puerto `5000`.



Acceder a usuario sophia

```sh
su sophia
# Ingresar password
```


ls no sale, usar luego cd ~

```sh
cd ~
```

Con eso accedemos al home de sophia



**Laboratorio 1**

**User sophia has saved her password in a hidden file in this folder. Find it and log in as sophia.**

La primera misión es encontrar el archivo oculto en el directorio

Comando

![[Comandos#`ls`]]

ls (list) lista los archivos de un directorio

**opciones:**

-   -d --- Lista los nombres del directorio
-   -a --- Lista todos los archivos (inclusive los ocultos) de un directorio.
-   -h --- Muestra el tamaño de los archivos en Kbytes, Mbytes, Gbytes.
-   -r --- Invierte el orden de clasificación.
-   -t --- Clasifica por la hora de modificación, los más nuevos primero
-   -R --- Lista subdirectorios de manera recursiva

**Comodines utilizados:**

-  `*` El comodín asterisco representa cualquier carácter de cualquier longitud
-   `?` El comodín interrogación representa un solo carácter
-   `[]` El comodín corchete es utilizado para un intervalo de caracteres
-   `{}` El comodín llaves es utilizado para representar una lista de opciones

``touch`` --- Puede ser utilizado para crear archivos vacíos
``cat`` --- Muestra el contenido de un archivo binario o texto.

**Solución:**

ls

Los archivos que inician con un punto son los archivos ocultos, no se muestra con la orden ls, necesita utilizar la opción -a

ls --a

El resultado muestra el archivo '.myhiddenpazz' usaremos el comando cat

cat .myhiddenpazz

su sophia

Password:
Nos trasladamos a su directorio home cd \~ para encontrar el flag,

>[!tip] sophia
> Y1o645M3mR84ejc

**Laboratorio 2**

**The user angela has saved her password in a file but she does not remember where \... she only remembers that the file was called whereismypazz.txt**

Encontrar el archivo "whereismypazz.txt"

Comando
![[Comandos#`find`]]

find --- Busca por archivos/directorios en el disco.

opciones:

-   -name busca con el nombre del archivo y del directorio
-   -exec aplica un comando al resultado de find. Donde {} representa el archivo encontrado e \\; finaliza el comando.
-   -type -l busca los enlaces simbolicos
-   -type -f busca los enlaces archivos
-   -type -d busca los enlaces directorios

-   -maxdepth \[num\] --- Realiza una busqueda \[num\] subdirectorios dentro del directorio que está buscando.

-   -size \[num\] --- Busca el archivo que tiene el tamaño \[num\]. La opción -size puede especificarse con b para especificar el tamaño en bloques de 512 bytes, c especifica el tamaño en bytes y k especifica el tamaño en Kbytes.

wc --- cuenta el número de palabras, bytes y líneas de un archivo. La opción -l muestra la cantidad de líneas de un archivo.

**Flujo de datos**

-   stdin (Standard Input) 0--- Permite la comunicación del usuario con el computador. Son dispositivos que envian datos al computador para el procesamiento. Ejemplos: Teclado, mouse, canal óptica, scanner. los dispositivos de entrada standard (stdin) en los sistemas GNU/Linux es el teclado.

-   stdout (Standard Output) 1--- Permite la comunicación del computador con el usuario. Son dispositivos que permiten al usuario visualizar los resultados del procesamiento enviado al computador. Ejemplos: Monitor, Impresora, Plotter. El dispositivo de salida standar (stdout) en el sistema GNU/Linux es el Monitor.

-   stderr (Standard Error) 2--- Permite a un comando enviar mensajes de error para el usuário via erro standard, abreviado como stderr. Como es el caso de la salida standard, su destino es el monitor y también pode ser redirecionado (por ejemplo, para un archivo o impresora).

Trabajando con operadores de redirección

-   Para redireccionar la salida del comando ls a un archivo, sobrescribiendo datos.

ls /etc/\*.conf \> /tmp/lista.txt

-   Para redireccionar la salida del comando ls a un archivo, incrementando los datos al final del archivo.

ls /var/log/\*.log \>\> /tmp/lista.txt

cat /tmp/lista.txt

-   Utiliza el PIPE para transformar la salida de un comando en la entrada de otro comando:

cat /etc/passwd \| wc --l

2\>/dev/null los errores encontrados en el descriptor del archivo se envían al /dev/null,

find / -name \"whereismypazz.txt\" -type f

La primera '/' especifica donde buscar, en este caso en el denominado directorio root. La opción -name especifica el nombre del archivo, -type especifica que se busca un archivo, como hay algunos archivos a los que no se tienen acceso genera un error, no se necesita mostrar.

```sh
find / -name "whereismypazz.txt" -type f 2>/dev/null
```

> [!tip] `2\>/dev/null` suprime los mensajes de error.


>[!tip] angela
> oh5p9gAABugHBje


**Laboratorio 3**

**The password of the user emma is in line 4069 of the file findme.txt**

Comando

help
Sed

El comando sed de Linux te permite buscar, sustituir, insertar y eliminar líneas en un archivo sin abrirlo con un editor de texto.

opciones:

-   -n --- muestra solamente la línea específica de un archivo.
-   -i --- Afecta y substituye directamente en el archivo.


cat -n findme.txt \| grep 4069

head

-   Función: Muestra las primeras líneas de un archivo.
-   Sintaxis básica: head \[opciones\] \[archivo
-   Uso común:
    -   Sin opciones: Muestra las primeras 10 líneas del archivo. Ejemplo: head archivo.txt
    -   Con opción -n o \--lines: Permite especificar el número de líneas a mostrar. Ejemplo: head -n 5 archivo.txt muestra las primeras 5 líneas.

tail

-   Función: Muestra las últimas líneas de un archivo.

-   Sintaxis básica: tail \[opciones\] \[archivo\]

-   Uso común:

    -   Sin opciones: Muestra las últimas 10 líneas del archivo. Ejemplo: tail archivo.txt

    -   Con opción -n o \--lines: Permite especificar el número de líneas a mostrar. Ejemplo: tail -n 5 archivo.txt muestra las últimas 5 líneas.

cat findme.txt \|head -n 4069 \| tail -n 1

cat findme.txt \| awk \'NR==4069\'


>[!tip] emma
> fIvltaGaq0OUH8O



**Laboratorio 4**

**User mia has left her password in the file -.**

ls -al

El archivo tiene como nombre "-" pero no podemos pasarlo como nombre del archivo en el comando cat por lo tanto tenemos que especificar donde se encuentra el archivo, en el directorio actual ./

find . -type f 2\>/dev/null

`.` : Para buscar desde el directorio actual en el que nos encontramos
`-type f` : Para buscar un tipo de elemento. En este caso archivos regulares. Los archivos regulares son simplemente archivos de datos común. Es decir, archivos de cualquier tipo, como imagenes, texto, ejecutables, etc.

cat ./-

>[!tip] mia
> iKXIYg0pyEH2Hos


**Laboratorio 5**

**It seems that the user camila has left her password inside a folder called hereiam**

find / -name hereiam -type d 2\>/dev/null

ls -la /opt/hereiam

cat /opt/hereiam/.here

>[!tip] camila
> F67aDmCAAgOOaOc


**Laboratorio 6**

**The user luna has left her password in a file inside the muack folder.**

find muack/ -type f -exec cat {} \\;

Busca en todos los archivos del directorio muack y realiza una operación "cat" en cada uno de ellos.

- `{}` Es un marcador de posición para el resultado encontrado por find

-  `\;` Indica por cada resultado encontrado, el comando cat se ejecuta una vez en el resultado encontrado.

xargs es un comando que construye y ejecuta comandos utilizando la salida de otro comando como argumento.

find . -type f \| xargs cat

>[!tip] luna
> j3vkuoKQwvbhkMc


**Laboratorio 7**

**The user eleanor has left her password in a file that occupies 6969 bytes**

find / -size 6969c -type f 2\>/dev/null

Asumiremos que el password no se encuentra en un archivo comprimido, primero veamos el contenido del archivo '.txt'

La c al final del número indica que el tamaño se mide en **bytes** (caracteres, de ahí la c).

>[!tip] eleanor
> UNDchvln6Bmtu7b

**Laboratorio 8**

**The user victoria has left her password in a file in which the owner is the user violin.**

find / -user violin -type f 2\>/dev/null

cat /usr/local/games/yo

>[!tip] victoria
> pz8OqvJBFxH0cSj


**Laboratorio 9**

**The user isla has left her password in a zip file.**

unzip passw0rd.zip

Para descomprimir un archivo zip, necesitamos el permiso en la carpeta destino. Como no tenemos permisos en el actual directorio nosotros crearemos un folder temporal en '/tmp'

unzip passw0rd.zip -d /tmp/pass

cat /tmp/pass/pwned/victoria/passw0rd.txt

Otra forma

mkdir /tmp/alumno

cp passw0rd.zip /tmp/alumno

cd /tmp/alumno

unzip passw0rd.zip

cat passw0rd.txt


>[!tip] isla
> D3XTob0FUImsoBb


**Laboratorio 10**

**The password of the user violet is in the line that begins with a9HFX (these 5 characters are not part of her password).**

Notas:

-   "grep": Se utiliza para buscar patrones de texto con lo que recibe. En este caso "a9HFX"

-   "\^": Representa el inicio de una línea. Por ejemplo, si tuvieras otra palabra como "holaquetal", podrías usar este símbolo "\^" para poner "hola" y te buscaría específicamente las líneas que comiencen con esas letras al inicio. Es decir, no en el medio, ni al final, sino al inicio.

cat passy \| grep \^a9HFX

grep \^a9HFX passy

> [!tip] violet
> WKINVzNQLKLDVAc


**Laboratorio 11**

**The password of the user lucy is in the line that ends with 0JuAZ (these last 5 characters are not part of her password).**

El password de Lucy se encuentra en el archivo 'end' y en una línea con el final de '0JuAZ'. Para obtener el password, usaremos el comando cat en este resultado buscaremos utilizando expresiones regulares '0JuAZ'.

cat end \| grep 0JuAZ\$

grep 0JuAZ\$ end

> [!tip] lucy
> OCmMUjebG53giud

**Laboratorio 12**

**The password of the user elena is between the characters fu and ck**

Construyamos la expresión regular:

1.  La cadena inicia con 'fu' utilizaremos \^fu

2.  En seguida viene un conjunto arbitrario de caracteres \*

3.  La cadena termina con 'ck' utilizaremos ck\$

cat file.yo \| grep \^fu.\*ck\$

grep \^fu.\*ck\$ file.yo

grep -oP \'(?\<=fu).\*?(?=ck)\' file.yo

**-o**: Hace que grep solo muestre la parte del texto que coincide con el patrón, en lugar de la línea completa.

**-P**: Habilita el uso de expresiones regulares Perl, que son más potentes y flexibles.

> [!tip] elena
> 4xZ5lIKYmfPLg9t


**Laboratorio 13**

**The user alice has her password is in an environment variable.**

printenv

printenv \| grep -i PASS

env \| grep PASS

> [!tip] alice
> Cgecy2MY2MWbaqt


**Laboratorio 14**

**The admin has left the password of the user anna as a comment in the file passwd.**

cat /etc/passwd \| grep alice

> [!tip] anna
> w8NvY27qkpdePox


**Laboratorio 15**

**Maybe sudo can help you to be natalia.**

sudo -u natalia /bin/bash

whoami

cd \~

**NOPASSWD:**: Esta opción indica que anna no necesita proporcionar su contraseña para ejecutar el comando especificado. Normalmente, al usar sudo, se le pide al usuario que ingrese su contraseña, pero con NOPASSWD, esta verificación se omite.

El usuario anna puede ejecutar el comando /bin/bash como el usuario natalia en la máquina venus, y no se le pedirá la contraseña para hacerlo. Esto le da a anna un nivel elevado de acceso, ya que puede obtener una sesión de Bash con los privilegios de natalia sin necesidad de autenticar cada vez

> [!tip] user
> -


**Laboratorio 16**

**The password of user eva is encoded in the base64.txt file**

cat base64.txt \| base64 -d

base64 -d base64.txt


> [!tip] eva
> upsCA3UFu10fDAO

**Laboratorio 17**

**The password of the clara user is found in a file modified on May 1, 1968.**

find / -type f -mtime +18615 2\>/dev/null

find / -type f ! -newermt 1970-01-02 -ls 2\>/dev/null

cat /usr/lib/cmdo

**-mtime +18615**: Este flag filtra los archivos según su última modificación. Específicamente, busca archivos que fueron modificados hace más de 18,615 días. El valor +18615 significa \"más de 18,615 días\". Este es un número muy grande, equivalente a más de 50 años, por lo que este comando buscará archivos que no han sido modificados en un periodo muy largo de tiempo.

> [!tip] clara
> 39YziWp5gSvgQN9


**Laboratorio 18**

**The password of user frida is in the password-protected zip (rockyou.txt can help you)**

Comando

opciones:

Now, we have a bruteforcing task for the zip file. Firstly, we have to copy the file to our local machine. Then, we can crack this using john the ripper.

scp -P 5000 clara@venus.hackmyvm.eu:\~/protected.zip .

zip2john protected.zip \> fridahash

john fridahash \--wordlist=/home/kali/rockyou.txt

unzip protected.zip

cat pwned/clara/protected.txt

> [!tip] user
> -


**Laboratorio 19**

The password of eliza is the only string that is repeated (unsorted) in repeated.txt.

uniq -d repeated.txt


> [!tip] eliza
> Fg6b6aoksceQqB9

**Laboratorio 20**

The user iris has left me her key.

ssh iris@localhost -i .iris_key

**ssh**: Es el comando para conectarse a un servidor remoto usando el protocolo SSH (Secure Shell). SSH es una herramienta para acceso remoto seguro y transferencia de archivos.

**iris@localhost**: Especifica el usuario y el servidor al que te estás conectando. En este caso, iris es el nombre de usuario y localhost indica que te estás conectando al servidor local (es decir, el propio ordenador en el que estás trabajando).

**-i .iris_key**: La opción -i especifica un archivo de clave privada que SSH utilizará para la autenticación en lugar de una contraseña. Aquí, .iris_key es el archivo de clave privada que se encuentra en el directorio actual.

> [!tip] iris
> kYjyoLcnBZ9EJdz
> kYjyoLcnBZ9EJdz


**Laboratorio 21**

User eloise has saved her password in a particular way.

base64 -d eloise \| file --

base64 -d eloise \> eloise.jpg

> [!tip] eloise
> yOUJlV0SHOnbSPm



**Laboratorio 22**

User lucia has been creative in saving her password.

xxd -r hi

**xxd**: Es un comando de Unix que normalmente convierte datos binarios a una representación hexadecimal. Sin embargo, con la opción -r, invierte ese proceso, es decir, convierte de hexadecimal a binario.

**-r**: Esta opción le dice a xxd que debe realizar la conversión inversa, de hexadecimal a binario (o texto legible).

**hi**: Es el nombre del archivo que contiene los datos en formato hexadecimal.


> [!tip] lucia
> uvMwFDQrQWPMeGP


errEWQWOPNMEeGOP

**Laboratorio 23**

The user isabel has left her password in a file in the /etc/xdg folder but she does not remember the name, however she has dict.txt that can help her to remember.

```sh
while IFS= read -r line; do readlink -e /etc/xdg/$line ; done < dict.txt
```

```sh
for i in $(cat dict.txt); do ls /etc/xdg/$i 2>/dev/null ; done
```

> [!tip] isabel
> H5ol8Z2mrRsorC0

**Laboratorio 24**

The password of the user freya is the only string that is not repeated in repeated.txt

```sh
uniq -u different.txt
```

> [!tip] freya
> EEDyYFDwYsmYawj

**Laboratorio 25**

User alexa puts her password in a .txt file in /free every minute and then deletes it.

```sh
false; while [ $? -ne 0 ]; do cat /free/* ; done 2>/dev/null
```

watch cat /free/\*

El comando watch en sistemas Unix/Linux se utiliza para ejecutar un comando repetidamente a intervalos regulares, y mostrar los resultados en la terminal. Por defecto, watch ejecuta el comando especificado cada 2 segundos y actualiza la pantalla con la salida del comando. Es especialmente útil para monitorear el cambio en la salida de un comando en tiempo real.

> [!tip] user
> mxq9O3MSxxX9Q3S

**Laboratorio 26**

The password of the user ariel is online! (HTTP)

curl <http://localhost>

Definir una function curl sino se tiene el programa

```sh
function __curl() {
  read -r proto server path <<< "$(printf '%s' "${1//// }")"
  if [ "$proto" != "http:" ]; then
    printf >&2 "sorry, %s supports only http\n" "${FUNCNAME[0]}"
    return 1
  fi
  DOC=/${path// //}
  HOST=${server//:*}
  PORT=${server//*:}
  [ "${HOST}" = "${PORT}" ] && PORT=80
  exec 3<>/dev/tcp/${HOST}/${PORT}
  printf 'GET %s HTTP/1.0\r\nHost: %s\r\n\r\n' "${DOC}" "${HOST}" >&3
  (while read -r line; do
    [ "$line" = $'\r' ] && break
  done && cat) <&3
  exec 3>&-
}
```

```sh
__curl http://localho
```

>[!tip] ariel
>33EtHoz9a0w2Yqo


**Laboratorio 27**

Seems that ariel dont save the password for lola, but there is a temporal file.

vim -r .goas.swp

:w /tmp/dict.txt

:q!

1era opción

```sh
vim -r .goas.swp
```
Dentro de `vim`, guarda el contenido usando: `:w /tmp/dict.txt`, y luego sal de `vim` usando `:q!`
Luego ejecuta en el terminal:
```sh
while IFS= read -r line; do echo $line | timeout 2 su lola 2>/dev/null; if [ $? -eq 0 ]; then echo $line; break; fi; done < /tmp/dict.txt
```
---
- `while IFS= read -r line; do ... done < /tmp/dict.txt`: Este es un bucle que lee cada línea del archivo `/tmp/dict.txt` y la guarda en la variable `line`.
    - `IFS=`: Evita que `read` divida la línea en palabras basándose en espacios, tabulaciones o nuevas líneas.
    - `read -r line`: Lee la línea sin interpretar las barras invertidas.
- `echo $line | timeout 2 su lola 2>/dev/null`: Para cada línea leída del archivo, este comando intenta cambiar al usuario "lola" usando `su`.
    - `echo $line |`: Envía la línea actual (potencial contraseña) como entrada al comando `su`.
    - `timeout 2`: Limita el tiempo de ejecución del comando `su` a 2 segundos. Esto es útil para evitar que el script se quede colgado si una contraseña incorrecta requiere mucho tiempo para fallar.
    - `su lola`: Intenta cambiar al usuario "lola". Se espera que la contraseña se solicite desde la entrada estándar (que estamos proporcionando con el `echo`).
    - `2>/dev/null`: Redirige la salida de error estándar del comando `su` a `/dev/null`, para que no veas mensajes de error en la pantalla.
- `if [ $? -eq 0 ]; then echo $line; break; fi`: Después de intentar el `su`, este comando verifica el código de salida (`$?`) del último comando ejecutado (en este caso, `su`).
    - Si el código de salida es 0, significa que el comando `su` tuvo éxito (es decir, la contraseña era correcta). En este caso, se imprime la contraseña (`echo $line`) y el bucle se detiene (`break`).
---

2da opción: (tiene que estar instalado)
```sh
hydra -l lola -P /tmp/dict.txt ssh://venus.hackmyvm.eu:5000
```

---
**Análisis del Comando Hydra:**
- `hydra`: Es una herramienta de fuerza bruta de contraseñas muy popular.
- `-l lola`: Especifica el nombre de usuario que se va a atacar, en este caso, "lola".
- `-P dict.txt`: Especifica el archivo que contiene la lista de posibles contraseñas, que es `/tmp/dict.txt` (el archivo que creaste en el Paso 2).
- `ssh://venus.hackmyvm.eu:5000`: Especifica el servicio y la ubicación del servidor SSH al que se intentará acceder. En este caso, es un servidor llamado `venus.hackmyvm.eu` en el puerto 5000, utilizando el protocolo SSH.
----

>[!tip] lola
>d3LieOzRGX5wud6



**Laboratorio 28**

The user celeste has left a list of names of possible .html pages where to find her password.

ssh -L 9001:127.0.0.1:80 lola@venus.hackmyvm.eu -p 5000

gobuster dir -w pages.txt -u http://127.0.0.1:9001 -x html

find / -name \"\*.html\" -path \'/var/www\*\' 2\>/dev/null

for i in \$(cat pages.txt); do response=\$(curl -s -o /dev/null -w \"%{http_code}\" \"http://localhost/\$i.html\");echo \"Path: \$i \| Response Code: \$response\" \| grep -v 404; done


Paso 1:
```sh
ssh -L 9001:127.0.0.1:80 lola@venus.hackmyvm.eu -p 5000
```
---
Este comando establece un túnel SSH. Vamos a analizar sus partes:

- `ssh`: Es el comando para iniciar una conexión SSH.
- `-L 9001:127.0.0.1:80`: Esto especifica el reenvío de puertos local. Significa que cualquier conexión que hagas a tu máquina local en el puerto 9001 será redirigida al puerto 80 del host `127.0.0.1` (localhost) en el servidor `venus.hackmyvm.eu` al que te conectas a través de SSH. En otras palabras, el puerto 80 del servidor remoto se "mapeará" a tu puerto local 9001.
- `lola@venus.hackmyvm.eu`: Es el usuario (`lola`) y la dirección del servidor remoto (`venus.hackmyvm.eu`) al que te vas a conectar.
- `-p 5000`: Especifica el puerto SSH en el servidor remoto, que es 5000 en lugar del puerto estándar 22.

**Acción:** Ejecuta este comando en tu terminal. Se te pedirá la contraseña del usuario `lola` en `venus.hackmyvm.eu`. Si el Laboratorio 27 tuvo éxito, deberías tener esta contraseña. Una vez que te autentiques, la conexión SSH se mantendrá abierta en segundo plano, y el túnel de puertos estará activo. **No cierres esta conexión SSH mientras trabajas en este laboratorio.**

---



Paso 2:
```sh
for i in $(cat pages.txt); do response=$(curl -s -o /dev/null -w "%{http_code}" "http://localhost:9001/$i.html"); echo "Path: $i.html | Response Code: $response" | grep -v 404; done
```
---
Este script intenta acceder a cada nombre de página listado en el archivo `pages.txt` a través del túnel SSH y verifica el código de respuesta HTTP. Vamos a desglosarlo:

- `for i in $(cat pages.txt); do ... done`: Este bucle lee cada línea del archivo `pages.txt` y la asigna a la variable `i`. Se asume que `pages.txt` contiene una lista de nombres de página (sin la extensión `.html`).
- `response=$(curl -s -o /dev/null -w "%{http_code}" "http://localhost/$i.html")`: Para cada nombre de página `$i`, este comando utiliza `curl` para hacer una petición HTTP al servidor web remoto (a través del túnel en `http://localhost:9001`, pero aquí se omite el puerto, por lo que podría haber un error, lo corregiremos más adelante).
    - `-s`: Modo silencioso, no muestra la barra de progreso ni mensajes de error.
    - `-o /dev/null`: Descarga el contenido de la respuesta a la nada. No nos interesa el cuerpo de la página en este momento, solo el código de respuesta.
    - `-w "%{http_code}"`: Muestra solo el código de respuesta HTTP (ej: 200, 404, etc.).
- `echo "Path: $i | Response Code: $response"`: Imprime el nombre de la página (`$i`) y el código de respuesta HTTP obtenido.
- `| grep -v 404`: Filtra la salida para mostrar solo las líneas que _no_ contienen el código de respuesta 404 (que indica que la página no fue encontrada). Esto nos mostrará las páginas que existen.

---

Paso 3: la salida del paso 2 son archivos html validos
```sh
curl http://localhost:9001/nombre_de_pagina.html
```

>[!tip] celeste
>VLSNMTKwSV2o8Tn




**Laboratorio 29**

The user celeste has access to mysql but for what?

```sh
mysql -u celeste -p
```
Este comando se utiliza para establecer una conexión a un servidor MySQL como el usuario `celeste`. Necesitarás conocer la contraseña de este usuario (`-p`) para que la conexión sea exitosa.

```mysql
show databases;
use venus;
show tables;
select * from people;
```

Versión corta:
```sh
mysql -u celeste -p -e "SELECT * FROM people;" venus 
```
Muestra directamente la tabla.

**Pasos a seguir:**
1. Copia el contenido de la tabla mostrada.
2. Guarda el contenido en un archivo, digamos data.txt
3. Agrega este script en el mismo nivel de tu archivo `data.txt`
```python
# Empezo el prime

content = []

with open('data.txt', 'r') as file:
    for line in file:
        content.append(line.split('|'))

# Quito los encabezados y pie de pagina (Cambiar si es necesario)
content[:] = content[4:-1]

for i, line in enumerate(content):
    line[:] = line[2:4] # Obtengo las columnas donde esta el usuario y contraseña (Cambiar si es necesario)
    line[0] = line[0].strip() # Quito espacios al inicio y al final
    line[1] = line[1].strip()
    content[i] = ':'.join(line) # Formato user:password para usar hydra


with open('credentials.txt', 'w') as file:
    for line in content:
        file.write(line + '\n')

for line in content: # Muestra en consola el resultado
    print(line)
```

4. Ahora que tienes el archivo `credentials.txt`
```sh
hydra -C dict_nina.txt venus.hackmyvm.eu -s 5000 ssh -Vv
```
Puedes quitar el `Vv` si no quieres ver los detalles de la ejecución.


>[!tip] nina
>- ixpeqdWuvC5N9kG



**Laboratorio 30**

**The user kira is hidding something in http://localhost/method.php**

```sh
curl -XPUT <http://localhost/method.php>
```

**GET**: Solicita un recurso sin modificar el servidor.
**POST**: Envía datos para crear o actualizar un recurso.
**PUT**: Reemplaza o crea un recurso específico.
**DELETE**: Elimina un recurso.
**PATCH**: Modifica parcialmente un recurso existente.
**HEAD**: Obtiene solo los encabezados de un recurso.
**OPTIONS**: Informa sobre los métodos soportados para un recurso.
**CONNECT**: Establece un túnel de conexión, usado en proxying.
**TRACE**: Muestra lo que llega al servidor para depuración.

>[!tip] user
> tPlqxSKuT4eP3yr


**Laboratorio 31**

**The user veronica visits a lot http://localhost/waiting.php**

curl http://localhost/waiting.php

El servidor nos dice que espera un agente usuario, especificando con la cadena «PARADISE». user agent string "PARADISE"

```sh
curl -A PARADISE http://localhost/waiting.php
```

>[!tip] veronica
>- QTOel6BodTx2cwX



**Laboratorio 32**

**The user veronica uses a lot the password from lana, so she created an alias.**

Los alias son creados en el archivo escondido `.bashrc` , vamos a ver si existe.

ls -la

El archivo existe, ahora busquemos la cadena 'lana' en este archivo usando grep.

```sh
cat .bashrc | grep lana
```

alias

>[!tip] lana
>- UWbc0zNEVVops1v


**Laboratorio 33**

**The user noa loves to compress her things.**

Primero veamos si existe en el home directory un archivo comprimido.

```sh
ls --al
```

Encontramos un archivo 'zip.gz' con el comando file podemos determinar qué tipo de archivo es.

file zip.gz

Es un archivo tar, como no tenemos permisos en este directorio crearemos en el directorio /tmp/zip y descomprimiremos el archivo.

```sh
mkdir /tmp/zip
tar -xvf zip.gz -C /tmp/zip
```

Veamos el contenido del directorio creado.

```sh
ls -la /tmp/zip
```

Encontramos un directorio 'pwned'  que habrá ahí?

```sh
ls -la /tmp/zip/pwned
```

¿Que hay en el archivo zip?

```sh
cat /tmp/zip/pwned/lana/zip
```


>[!tip] noa
>- 9WWOPoeJrq6ncvJ



**Laboratorio 34**

**The password of maia is surrounded by trash**

Primero veamos que hay en el home directory.

```sh
ls --al
```
Vemos un archivo trash, este archivo de que tipo será?
```sh
file trash
```
Este es una llave secreta PGP.
```sh
strings trash
```

>[!warning] No consideres los caracteres `\n`

>[!tip] maia
>- h1hnDPHpydEjoEN



**Laboratorio 35**

**The user gloria has forgotten the last 2 characters of her password \... They only remember that they were 2 lowercase letters.**

El objetivo es generar los dos últimos dígitos de la contraseña. Además, recibimos una útil pista, las dos siguientes letras son minúsculas. Así pues, tenemos 26×26 combinaciones posibles.

Primero veamos cual es la parte conocida del password

```sh
ls --al

cat forget
```

Creamos un script

```python
incomplete_passwd = "v7xUVE2e5bjUc"

lower = 'abcdefghijklmnopqrstuvwxyz'


with open('passwd.txt', 'w') as file:
    for char1 in lower:
        for char2 in lower:
            file.write(incomplete_passwd + char1 + char2 + '\n')
```

Con el archivo resultante podemos realizar un ataque de fuerza bruta utilizando hydra.

```sh
hydra -l gloria -P paswd.txt ssh://venus.hackmyvm.eu:5000
```


>[!tip] gloria
> v7xUVE2e5bjUcxw


**Laboratorio 36**

**User alora likes drawings, that\'s why she saved her password as \...**

Veamos en que archivo podemos encontrar:

```sh
ls --la
```

Hay un archivo llamado image, veamos ¿Qué tipo de archivo es?

```sh
file image
```

Encontramos que es un archivo de texto, entonces lo abrimos con cat.

```sh
cat image
```

Evidentemente es un código QR, tratemos de leer con un Smartphone, pero no se puede, entonces nos creamos un script.

```python
with open(\'image\', \'r\') as img:
	lines = img.readlines()

for l in lines:
	print(l.replace(\'#\', chr(0x2588)), end=\'\')
```

Este código si es leído por un Smartphone

sed -e \'s/#/\\xe2\\x96\\x88/g\' image

>[!tip] alora
>mhrTFCoxGoqUxtw



**Laboratorio 37**

**User Julie has created an iso with her password.**

El password se encuentra en un iso.

```sh
ls -al
```

Podríamos descargar el iso mediante scp en nuestro directorio.

```sh
scp -P 5000 alora@venus.hackmyvm.eu:/pwned/alora/music.iso ./
```

Creamos un nuevo directorio llamado 'iso' en el folder '/media' donde montamos el archivo ISO:

```sh
$ sudo mkdir /media/iso
$ sudo mount -o loop ./music.iso /media/iso
```

Mostrando el contenido del directorio:

```sh
ls -la /media/iso
```

Encontramos un archivo 'music.zip'. desempaquetamos este archivo. Como tenemos los permisos correspondientes, desempaquetaremos el archivo en este directorio:

```sh
$ unzip /media/iso/music.zip -d ./
```

Veamos el contenido de 'pwned/alora/music.txt' y obtenemos el password.

```sh
$ cat pwned/alora/music.txt
```

Desmontamos el archivo ISO y eliminamos el directorio de montaje

```sh
$ sudo umount /media/iso
$ sudo rm -r /media/iso
```


-----

>[!tip] Resumen
>En el Laboratorio 37, descargamos un archivo ISO (`music.iso`) desde un servidor remoto. Un ISO es una imagen de disco, como un CD o DVD, que contiene un sistema de archivos completo. Montamos este ISO en nuestro sistema como si fuera un disco real para acceder a su contenido. Dentro, encontramos un archivo ZIP (`music.zip`) que desempaquetamos. Finalmente, leímos un archivo de texto (`music.txt`) que contenía la contraseña. Desmontamos el ISO al final para liberar recursos del sistema y mantener la organización. 

---


>[!tip] julia
>sjDf4i2MSNgSvOv


---


**Laboratorio 38**

**The user irene believes that the beauty is in the difference.**

Comparemos dos archivos para encontrar sus diferencias, veamos que archivos podemos comparar

```sh
$ ls --al
```

La obvia comparación que podríamos realizar, es utilizando los archivos 1.txt 2.txt

```sh
$ diff 1.txt 2.txt
```

>[!tip] irene
>8VeRLEFkBpe2DSD



----



**Laboratorio 39**

**The user adela has lent her password to irene.**

```sh
$ openssl rsautl -decrypt -inkey id_rsa.pem -in pass.enc
```


----

**Análisis del Comando:**

Bash

```
openssl rsautl -decrypt -inkey id_rsa.pem -in pass.enc
```

Vamos a desglosar cada parte de este comando:

- **`openssl`**: Este es el comando principal que invoca la herramienta de línea de comandos OpenSSL. OpenSSL es una biblioteca de software robusta para aplicaciones que aseguran las comunicaciones a través de redes contra escuchas o necesidades de identificación del otro extremo, en ambos extremos. También proporciona utilidades de línea de comandos para trabajar con diversas tareas de criptografía.
    
- **`rsautl`**: Este es un subcomando de `openssl` que se utiliza para realizar operaciones RSA (Rivest–Shamir–Adleman). RSA es un algoritmo de criptografía asimétrica ampliamente utilizado. La criptografía asimétrica utiliza un par de claves: una clave pública para cifrar datos y una clave privada correspondiente para descifrarlos.
    
- **`-decrypt`**: Esta opción le dice a `openssl rsautl` que la operación que queremos realizar es el descifrado. Esto significa que vamos a tomar datos cifrados y, utilizando la clave adecuada, los convertiremos de nuevo a su forma original (texto plano).
    
- **`-inkey id_rsa.pem`**: Esta opción especifica el archivo que contiene la clave que se utilizará para la operación. En este caso, el archivo se llama `id_rsa.pem`. Por la convención de nombres (`id_rsa`), es muy probable que este archivo contenga una clave privada RSA. Para poder descifrar los datos cifrados con una clave pública RSA, necesitamos la clave privada correspondiente. La extensión `.pem` es un formato común para almacenar claves criptográficas (públicas o privadas) en texto ASCII, codificadas en Base64 y delimitadas por encabezados y pies de página (`-----BEGIN RSA PRIVATE KEY-----`, `-----END RSA PRIVATE KEY-----`, por ejemplo).
    
- **`-in pass.enc`**: Esta opción especifica el archivo que contiene los datos de entrada para la operación. En este caso, el archivo se llama `pass.enc`. Por la extensión `.enc`, es muy probable que este archivo contenga los datos cifrados que queremos descifrar.

----


>[!tip] adela
> nbhlQyKuaXGojHx



----



**Laboratorio 40**

**User sky has saved her password to something that can be listened to.**

On the directory, we have a "wtf" file that has a morse code. We can decode that using CyberChef. Also, please copy this morse code to your local machine.

Cambiar la contraseña a minuscula

>[!tip] sky
> papaparadise


---



**Laboratorio 41**

**User sarah uses header in http://localhost/key.php**

```sh
$ curl http://localhost/key.php
```

Key header is true?

El servidor pregunta si el campo "Key" es verdadero true. Nosotros asignamos al header "Key: true"

```sh
$ curl -H \'key: true\' http://localhost/key.php
```

>[!tip] sarah
>LWOHeRgmIxg7fuS


-----


**Laboratorio 42**

**The password of mercy is hidden in this directory.**

ls --la

Como puede ver en el resultado, fácilmente podemos encontrar el archivo oculto '...'

```sh
$ cat ...
```

>[!tip] mercy
> ym5yyXZ163uIS8L

---



**Laboratorio 43**

**User mercy is always wrong with the password of paula.**

Si nosotros vemos el archivo ".bash_history", de donde obtendremos el usuario paula utilizando el comando history.

ls -la


```sh
cat .bash_history
```

history

>[!tip] paula
>dlHZ6cvX6cLuL8p


-----


**Laboratorio 44**

**The user karla trusts me, she is part of my group of friends.**

Karla está en el grupo Friends, veamos que grupos hay

```sh
$ groups
```

El grupo 'hidden' puede ser el punto inicial, Busquemos los archivos asignados al grupo hidden:

```sh
find / -group hidden -type f 2>/dev/null
```

Hay un solo archivo asignado al grupo. Veamos el contenido del archivo oculto.

```sh
$ cat /usr/src/.karl-a
```

>[!tip] karla
>gYAmvWY3I7yDKRf


-----


**Laboratorio 45**

**User denise has saved her password in the image.**

Veamos que contienen el home directory del usuario

ls -la

En efecto podemos encontrar la imagen llamada, 'yuju.jpg' verifiquemos el formato

file yuju.jpg

Confirmado el archivo como jpeg, asumimos que el password esta escondido con alguna técnica de steganografia.

```sh
$ exiftool yuyu.jpg
```

>[!tip] denise
>pFg92DpGucMWccA



----

**Laboratorio 46**

**The user zora is screaming doas!**

If Zora is screaming doas, let's just use it:

Si ejecutamos
```sh
$ doas
```

Obtenemos
``usage: doas \[-Lns\] \[-C config\] \[-u user\] command \[args\]``

The command expects another command to be executed. Also, you can specify a user under which the command will be executed. So if we can execute the bash with the user 'zora', we would be in the next level:

Ejecutamos:
```ah
doas -u zora /bin/bash
```

Now we just have to enter our own password (that of 'denise'), and we are in the next level!

----

El laboratorio nos introduce al comando `doas`, que es similar a `sudo` pero más simple y a menudo encontrado en sistemas OpenBSD y algunos otros Unix-like. La descripción nos muestra el uso básico de `doas`, que permite ejecutar comandos como otro usuario. La clave para este laboratorio es usar `doas` para ejecutar una shell (bash) como el usuario `zora`. Una vez que podamos ejecutar comandos como `zora`, habremos avanzado al siguiente nivel (implícitamente, obteniendo acceso a la cuenta de `zora`).

**Análisis del Comando `doas` y su Uso:**

El laboratorio nos proporciona la sintaxis básica de `doas`:

```
usage: doas [-Lns] [-C config] [-u user] command [args]
```

Vamos a desglosar las partes relevantes para este laboratorio:

- **`doas`**: Este es el comando que invocamos para ejecutar otro comando con los privilegios de otro usuario, similar a `sudo`.
- **`-u user`**: Esta opción nos permite especificar bajo qué usuario queremos ejecutar el comando que sigue. En este caso, el laboratorio sugiere usar `-u zora` para intentar ejecutar un comando como el usuario `zora`.
- **`command [args]`**: Después de las opciones, especificamos el comando que queremos ejecutar y cualquier argumento que pueda tener ese comando. En el laboratorio, el comando que se sugiere ejecutar es `/bin/bash`.

**Explicación de `/bin/bash`:**

- `/bin/bash` es la ruta completa al ejecutable de la shell Bash (Bourne-Again SHell), que es una de las shells más comunes en sistemas Linux y Unix. Ejecutar `/bin/bash` inicia una nueva sesión de shell interactiva. Si se ejecuta con los privilegios de otro usuario, esta nueva shell se ejecutará con la identidad de ese usuario.

**El Proceso de Solución:**

El laboratorio nos guía directamente hacia la solución. El proceso es el siguiente:

1. **Intentar ejecutar `bash` como el usuario `zora` usando `doas`:**
    
    Según la guía, el comando que debemos usar es:
    
    Bash
    
    ```
    doas -u zora /bin/bash
    ```
    
    **Acción:** Ejecuta este comando en tu terminal.
    
2. **Proporcionar la contraseña:**
    
    La guía nos dice: "Now we just have to enter our own password (that of 'denise'), and we are in the next level!"
    
    Esto implica que `doas` está configurado de tal manera que permite al usuario actual (que presumiblemente es `denise` en el contexto del laboratorio, ya que acabamos de resolver el Laboratorio 45 donde interactuamos con la cuenta de Denise) ejecutar comandos como `zora` proporcionando _su propia contraseña_ (la de `denise`).
    
    **Acción:** Cuando ejecutes el comando `doas -u zora /bin/bash`, es probable que se te solicite una contraseña. **Ingresa la contraseña del usuario `denise`** (la contraseña que obtuviste en el Laboratorio 45).

----



>[!tip] zora
>BWm1R3jCcb53riO


------


**Laboratorio 47**

**The user belen has left her password in venus.hmv**

Veamos que contienen el home directory del usuario

```sh
$ ls -la
```

No encontramos el archivo 'venus.hmv', entonces buscaremos el archivo.

```sh
$ find / -name venus.hmv 2\>/dev/null
```

como no encontramos el archivo, quizás no sea un archivo sino un URL

```sh
$ curl venus.hmv
```

>[!tip] belen
>2jA0E8bQ4WrGwWZ 


---



**Laboratorio 48**

**It seems that belen has stolen the password of the user leona...**

Veamos que podríamos encontrar en los archivos del home directory de Belen's

ls -la

En la lista podemos encontrar un archivo extraño 'stolen.txt' veamos el contenido

cat stolen.txt

La cadena inicia con \$1\$ esta cadena podría tener el formato de md5crypt, utilizaremos JohnTheRipper para encontrar el texto plano del hash.

Manual de crypt te lo dirá:

  -----------------------------------------------------------------------
  **ID**     **Método**
  ---------- ------------------------------------------------------------
  1          MD5

  2a         Blowfish

  5          SHA-256 (since glibc 2.7)

  6          SHA-512 (since glibc 2.7) 
  -----------------------------------------------------------------------

john \--format=md5crypt \--wordlist=/usr/share/wordlists/rockyou.txt stolen.txt

>[!tip] user
>- 


**Laboratorio 49**

**User ava plays a lot with the DNS of venus.hmv lately...**

Veamos la carpeta 'bind' donde estan almacenados los registros locales de DNS:

ls -la /etc/bind

En el resultado resalta inmediatamente el archivo 'db.venus.hmv' si vemos el contenido podremos encontrar el password.

>[!tip] user
>- 


**Laboratorio 50**

**The password of maria is somewhere...**
