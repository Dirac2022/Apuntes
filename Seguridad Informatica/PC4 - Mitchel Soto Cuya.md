	Preguntas 5 puntos



### Parte 1

#### Pregunta 1
Juan es responsable de gestionar las llaves criptográficas utilizadas por su organización. ¿Cuál de las siguientes afirmaciones es correcta acerca de cómo debe seleccionar y gestionar esas llaves? (Elija todas las que correspondan)

- A.     Las llaves deben ser lo suficientemente largas para protegerse contra futuros ataques si se espera que los datos sigan siendo confidenciales.
- B.     Las llaves deben elegirse utilizando un algoritmo que los genere a partir de un patrón predecible.
- C.    Las llaves deben mantenerse indefinidamente.
- D.    Las llaves más largas proporcionan mayores niveles de seguridad.


---

**Respuesta : A, D**
- Las opciones correctas son la A y la D ya que llaves con una longitud larga proporcionan una mayor seguridad. Además las llaves **no** deben seguirse usando un algoritmo predecible (B) y las llaves no deben ser indefinidas (C). Deben tener un ciclo de vida definido.

---

#### Pregunta 2
Juan recibió recientemente un correo electrónico de Bob. ¿Qué objetivo criptográfico debería cumplirse para convencer a Juan de que Bob era realmente el remitente del mensaje?

- A.     No repudio
- B.     Confidencialidad
- C.    Disponibilidad
- D.    Integridad


---

**Respuesta: A**

En este caso el **No repudio** es un principio que garantiza que una entidad no pueda negar la realización de una acción una vez que ha ocurrido (como lo vimos en clase). Entonces este sería el objetivo que debe cumplirse para asegurar que efectivamente Bob era el remitente.

---

#### Pregunta 3

Si usted está implementando AES para el cifrado de los archivos de su organización que planea almacenar en un servicio de almacenamiento en la nube, deseando tener el cifrado más fuerte posible. ¿Qué longitud de llave debe elegir?
    

- A. 192 bits
- B. 256 bits
- C. 512 bits
- D. 1.024 bits
    

---

**Solución: B**  
Aunque el cifrado AES soporta 3 longitudes: 128, 192 y 256 bits. Lo recomendable para obtener el cifrado más fuere posible sería el de 256 bits.

---

#### Pregunta 4
Si usted desea crear un producto de seguridad, para facilitar el intercambio de llaves del cifrado simétrico entre dos partes que no tienen forma de intercambiar llaves de manera segura. ¿Qué algoritmo podría utilizar para facilitar el intercambio?
    

- A. Rijndael
- B. Blowfish
- C. Vernam
- D. Diffie-Hellman
    

---

**Solución: D** 

Tal como lo vimos en clase, el algoritmo específico para facilitar el intercambio de llaves es Diffie-Hellman.

---

#### Pregunta 5
¿Qué ocurre cuando la relación entre el texto plano y la llave es lo suficientemente complicada como para desalentar al atacante a seguir alterando el texto plano y analizar el texto cifrado resultante con el objetivo de determinar la llave?  (Elija todas las opciones que correspondan).
    

- A. Confusión
- B. Transposición
- C. Polimorfismo
- D. Difusión
    

---

**Solución: A y D** 
- La **confusión** buscahacer que la relación entre la llave y el texto cifrado sea lo más compleja y enrevesada posible. Y la **Difusión** busa que un pequeño cambio en el texto plano se propague a muchos bits del texto cifrado

---

#### Pregunta 6
Alice está implementando un criptosistema basado en AES para utilizarlo dentro de su organización. ¿Cuáles de los siguientes objetivos se pueden alcanzar con AES?  (Elija todas las que correspondan).
    

- A. No repudio
- B. Confidencialidad
- C. Autenticación
- D. Integridad
    

---

**Solución:** B. Confidencialidad, C. Autenticación, D. Integridad  
**Justificación:** AES proporciona confidencialidad. Con modos como GCM también ofrece autenticación e integridad. El no repudio requiere firmas digitales, no cifrado simétrico.

---

#### Pregunta 7

7. ¿Cuál es el único criptosistema conocido como totalmente seguro?
    

- A. Cifrado por transposición
    
- B. Cifrado de sustitución
    
- C. Estándar de cifrado avanzado
    
- D. One-time pad
    

---

**Solución:** D. One-time pad  
**Justificación:** El OTP es teóricamente irrompible si se usa correctamente: clave verdaderamente aleatoria, del mismo tamaño que el mensaje y usada una única vez.

---

#### Pregunta 8

8. ¿Cuáles de los siguientes son requisitos que debe cumplir para el uso de One-time pad?  
    (Elija todos los que correspondan).
    

- A. La llave de cifrado debe tener al menos la mitad de la longitud del mensaje.
    
- B. La llave de cifrado debe generarse aleatoriamente.
    
- C. Cada one-time pad debe ser utilizado una sola vez.
    
- D. El One-time pad debe estar físicamente protegido contra su divulgación.
    

---

**Solución:** B, C, D  
**Justificación:** La clave debe ser verdaderamente aleatoria (B), única por mensaje (C) y protegida (D). A es incorrecta, debe ser del mismo tamaño que el mensaje, no la mitad.

---

#### Pregunta 9

9. Juan administra un criptosistema simétrico con 20 usuarios. Si un usuario fue comprometido, ¿cuántas claves debe cambiar?
    

- A. 1
    
- B. 2
    
- C. 19
    
- D. 190
    

---

**Solución:** C. 19  
**Justificación:** En cifrado simétrico, cada par de usuarios necesita una clave. Si un usuario fue comprometido, se deben reemplazar sus claves con los otros 19 usuarios.

---

#### Pregunta 10

10. ¿Qué tipo de cifrado opera sobre grandes fragmentos de un mensaje?
    

- A. Cifrado de flujo
    
- B. Cifrado César
    
- C. Cifrado por bloques
    
- D. Cifrado ROT3
    

---

**Solución:** C. Cifrado por bloques  
**Justificación:** El cifrado por bloques procesa bloques completos (e.g., 128 bits en AES), a diferencia del cifrado de flujo que lo hace bit a bit o carácter a carácter.

---

(continúo en el siguiente mensaje desde la **Pregunta 11** hasta la **Pregunta 40**)


#### Pregunta 11

11. ¿Cuántas claves debe generar James si María y Eva desean intercambiar archivos cifrados de forma segura?
    

- A. Una
    
- B. Dos
    
- C. Tres
    
- D. Cuatro
    

---

**Solución:** A. Una  
**Justificación:** En un sistema de cifrado simétrico, se necesita una clave única por par de comunicación. Solo se requiere una clave compartida entre María y Eva.

---

#### Pregunta 12

12. ¿Qué técnica permite que varias personas recuperen una llave sin requerir la presencia de todos?
    

- A. Split knowledge
    
- B. M of N Control
    
- C. Work function
    
- D. Zero-knowledge proof
    

---

**Solución:** B. M of N Control  
**Justificación:** Este método permite que cualquier subconjunto de M personas de un grupo de N puedan reconstruir una clave, sin necesidad de que estén todos presentes.

---

#### Pregunta 13

13. ¿Qué se utiliza para crear un texto cifrado único cada vez que se cifra el mismo mensaje con la misma clave?
    

- A. Vector de inicialización
    
- B. Cifrado de Vigenère
    
- C. Esteganografía
    
- D. Cifrado de flujo
    

---

**Solución:** A. Vector de inicialización  
**Justificación:** El IV (Initialization Vector) garantiza que el mismo mensaje cifrado con la misma clave resulte diferente cada vez.

---

#### Pregunta 14

14. ¿Qué modo de funcionamiento proporciona confidencialidad y autenticidad?
    

- A. BCE
    
- B. GCM
    
- C. OFB
    
- D. CTR
    

---

**Solución:** B. GCM  
**Justificación:** El modo Galois/Counter Mode (GCM) proporciona tanto cifrado como autenticación (integridad).

---

#### Pregunta 15

15. ¿Qué caso de uso considera Julia si le preocupa el almacenamiento de datos sin cifrar en la RAM?
    

- A. Datos en movimiento
    
- B. Datos en reposo
    
- C. Datos en destrucción
    
- D. Datos en uso
    

---

**Solución:** D. Datos en uso  
**Justificación:** Los datos en uso son aquellos que están siendo procesados, por ejemplo, cargados en memoria RAM, y pueden estar temporalmente sin cifrar.

---

#### Pregunta 16

16. ¿Qué algoritmos deben dejar de usarse por estar obsoletos? (Elija todos los que correspondan)
    

- A. AES
    
- B. DES
    
- C. 3DES
    
- D. RC5
    

---

**Solución:** B. DES y C. 3DES  
**Justificación:** DES está completamente obsoleto, y 3DES ha sido desaprobado por NIST debido a vulnerabilidades conocidas y bajo rendimiento.

---

#### Pregunta 17

17. ¿Qué modo propaga errores entre bloques?
    

- A. Electronic Code Book
    
- B. Cipher Block Chaining
    
- C. Output Feedback
    
- D. Counter
    

---

**Solución:** B. Cipher Block Chaining (CBC)  
**Justificación:** En CBC, un error en un bloque afecta también al siguiente bloque descifrado, propagando errores.

---

#### Pregunta 18

18. ¿Qué método de distribución de claves es más engorroso en ubicaciones geográficas diferentes?
    

- A. Diffie-Hellman
    
- B. Cifrado de clave pública
    
- C. Offline
    
- D. Escrow
    

---

**Solución:** C. Offline  
**Justificación:** El intercambio de claves fuera de línea (por ejemplo, físicamente) es difícil y poco práctico a distancia.

---

#### Pregunta 19

19. ¿Cuál es el algoritmo simétrico más seguro de la lista?
    

- A. AES-256
    
- B. 3DES
    
- C. RC4
    
- D. Skipjack
    

---

**Solución:** A. AES-256  
**Justificación:** AES-256 es actualmente el estándar más seguro y ampliamente recomendado para cifrado simétrico.

---

#### Pregunta 20

20. Si 6 empleados deben comunicarse entre ellos de forma privada usando clave simétrica, ¿cuántas claves se necesitan?
    

- A. 1
    
- B. 6
    
- C. 15
    
- D. 30
    

---

**Solución:** C. 15  
**Justificación:** En un sistema simétrico, cada par único necesita una clave. Para n usuarios: n(n-1)/2 → 6(5)/2 = 15 claves.

---

#### Pregunta 21

21. ¿Qué pasa si Juan cambia un carácter del texto y vuelve a calcular SHA-2?
    

- A. Cambia un carácter del hash
    
- B. Comparte el 50% del hash
    
- C. No cambia
    
- D. Es completamente diferente
    

---

**Solución:** D. Es completamente diferente  
**Justificación:** Debido al efecto avalancha, un cambio mínimo en el input produce un hash completamente diferente.

---

#### Pregunta 22

22. ¿Qué tipo de ataque analiza el consumo de electricidad?
    

- A. Fuerza bruta
    
- B. Canal lateral
    
- C. Texto plano conocido
    
- D. Análisis de frecuencia
    

---

**Solución:** B. Canal lateral  
**Justificación:** Los ataques por canal lateral se basan en información como consumo de energía, tiempo de ejecución o radiación electromagnética.

---

#### Pregunta 23

23. ¿Qué clave debe usar Mario para cifrar un mensaje para Margarita?
    

- A. Clave pública de Mario
    
- B. Clave privada de Mario
    
- C. Clave pública de Margarita
    
- D. Clave privada de Margarita
    

---

**Solución:** C. Clave pública de Margarita  
**Justificación:** En criptografía asimétrica, se cifra con la clave pública del receptor para que solo su clave privada lo descifre.

---

#### Pregunta 24

24. Si cifras 2048 bits con ElGamal, ¿cuánto mide el texto cifrado?
    

- A. 1024 bits
    
- B. 2048 bits
    
- C. 4096 bits
    
- D. 8192 bits
    

---

**Solución:** C. 4096 bits  
**Justificación:** ElGamal genera un texto cifrado que es aproximadamente el doble del tamaño del texto original.

---

#### Pregunta 25

25. Si se usa RSA de 3072 bits y se quiere un equivalente ECC, ¿qué longitud se debe usar?
    

- A. 256 bits
    
- B. 512 bits
    
- C. 1024 bits
    
- D. 2048 bits
    

---

**Solución:** A. 256 bits  
**Justificación:** ECC ofrece una seguridad comparable a RSA con claves mucho más pequeñas. ECC de 256 bits ≈ RSA de 3072 bits.

---

#### Pregunta 26

26. ¿Qué tamaño puede tener el digest SHA-2 de un mensaje de 2048 bytes?
    

- A. 160 bits
    
- B. 512 bits
    
- C. 1024 bits
    
- D. 2048 bits
    

---

**Solución:** B. 512 bits  
**Justificación:** SHA-2 tiene variantes, pero SHA-512 genera un hash de 512 bits independientemente del tamaño del mensaje.

---

#### Pregunta 27

27. ¿Qué tecnología está obsoleta y no debe usarse?
    

- A. SHA-3
- B. TLS 1.2
- C. IPsec
- D. SSL 3.0

---

**Solución:** D. SSL 3.0  
**Justificación:** SSL 3.0 es inseguro y ha sido reemplazado por TLS. Es vulnerable a ataques como POODLE.

---

#### Pregunta 28

28. ¿Qué puede haberse añadido a los hashes para que no coincidan con los calculados?
    

- A. Sal
- B. Doble hash
- C. Cifrado añadido
- D. One-time pad

---

**Solución:** A. Sal  
**Justificación:** La sal es un valor aleatorio añadido antes del hash para evitar ataques con tablas precomputadas (como rainbow tables).

---

#### Pregunta 29

29. ¿Qué clave usa Richard para descifrar un mensaje cifrado con RSA por Sue?


- A. Clave pública de Richard
- B. Clave privada de Richard
- C. Clave pública de Sue
- D. Clave privada de Sue


---

**Solución:** B. Clave privada de Richard  
**Justificación:** En criptografía asimétrica, quien recibe el mensaje usa su propia clave privada para descifrar.

---

#### Pregunta 30

30. ¿Qué clave usa Richard para firmar digitalmente?

- A. Clave pública de Richard
- B. Clave privada de Richard
- C. Clave pública de Sue
- D. Clave privada de Sue


---

**Solución:** B. Clave privada de Richard  
**Justificación:** Las firmas digitales se generan con la clave privada del firmante para que puedan ser verificadas con su clave pública.

---

#### Pregunta 31

31. ¿Cuál no está soportado por FIPS 186-4?

- A. Algoritmo de firma digital
- B. RSA
- C. ElGamal DSA
- D. Curva elíptica DSA
    

---

**Solución:** C. ElGamal DSA  
**Justificación:** FIPS 186-4 no incluye ElGamal como algoritmo de firma digital aprobado.

---

#### Pregunta 32

32. ¿Qué norma regula certificados digitales en comunicaciones seguras?
    

- A. X.500
- B. X.509
- C. X.900
- D. X.905


---

**Solución:** B. X.509  
**Justificación:** X.509 es el estándar para la infraestructura de clave pública (PKI) y el formato de certificados digitales.

---

#### Pregunta 33

33. ¿Qué tipo de ataque se sospecha si un atacante aplica electricidad a un dispositivo?
    

- A. Ataque de implementación
- B. Inyección de fallos
- C. Temporización
- D. Texto cifrado elegido


---

**Solución:** B. Inyección de fallos  
**Justificación:** Es un ataque físico que altera el comportamiento del sistema para intentar extraer información secreta.

---

#### Pregunta 34

34. ¿Qué puerto TCP se usa normalmente para tráfico TLS?
    
- A. 22
- B. 80
- C. 443
- D. 1443
    
---

**Solución:** C. 443  
**Justificación:** El puerto 443 es el puerto predeterminado para HTTPS, que usa TLS para comunicaciones seguras.

---

#### Pregunta 35

35. ¿Qué ataque es posible para un atacante externo sin acceso físico?


- A. Solo texto cifrado
- B. Texto plano conocido
- C. Texto plano elegido
- D. Inyección de fallos

---

**Solución:** A. Solo texto cifrado  
**Justificación:** Este es el ataque más básico y realista desde fuera de un sistema sin acceso físico ni información adicional.

---

#### Pregunta 36

36. ¿Qué herramienta mejora un ataque por fuerza bruta?


- A. Tablas Rainbow
- B. Filtrado jerárquico
- C. TKIP
- D. Mejora aleatoria

---

**Solución:** A. Tablas Rainbow  
**Justificación:** Las rainbow tables almacenan hashes precalculados para acelerar la búsqueda inversa de contraseñas.

---

#### Pregunta 37

37. ¿Cuál es el formato relacionado con certificados binarios de Windows?

- A. CCM
- B. PEM
- C. PFX
- D. P7B
    

---

**Solución:** C. PFX  
**Justificación:** PFX (o PKCS #12) es un formato binario usado comúnmente en sistemas Windows para almacenar certificados con su clave privada.

---

#### Pregunta 38

38. ¿Cuál es la principal desventaja de las listas de revocación de certificados?


- A. Manejo de claves
- B. Latencia
- C. Mantenimiento de registros
- D. Vulnerabilidad a fuerza bruta
    

---

**Solución:** B. Latencia  
**Justificación:** Las CRL pueden ser grandes y tardar en descargarse, afectando el rendimiento y la validación en tiempo real.

---

#### Pregunta 39

39. ¿Qué algoritmo se considera actualmente inseguro?

- A. ElGamal
- B. RSA
- C. Criptografía de Curva Elíptica
- D. Merkle-Hellman Knapsack
    

---

**Solución:** D. Merkle-Hellman Knapsack  
**Justificación:** Fue uno de los primeros sistemas de clave pública, pero ya no se considera seguro debido a ataques exitosos conocidos.

---

#### Pregunta 40

40. ¿Qué ventaja ofrece SSH2 sobre SSH1?
    

- A. Autenticación multifactor
- B. Sesiones simultáneas
- C. Encriptación 3DES
- D. Encriptación IDEA

---

**Solución:** B. Sesiones simultáneas  
**Justificación:** SSH2 soporta múltiples canales sobre una sola conexión, permitiendo sesiones simultáneas. Además, corrige vulnerabilidades del SSH1.

### Parte 2

Demostrar paso a paso cómo una firma digital combina la criptografía asimétrica con funciones hash para proporcionar autenticidad e integridad de manera eficiente (puede utilizar OpenSSL). 5 puntos

---

Voy a demostrarlo con una aplicación directa y personal. Yo tengo una máquina Windows (Laptop HP). Pero tengo instalado VirtualBox y una maquina virtual Ubuntu. Dentro de esa máquina virtual Ubuntu yo usualmente hago mis proyectos y trabajos y actualmente estoy trabajando con Docker. Ahora **¿qué pasa si quiero gestionar mi docker host mediante conexión remota?**. Una solución es justamente hacer uso de TLS con firmas digitales y OpenSSL. A continuación expondré con detalle los pasos que seguí.


#### Dentro de mi maquina virtual Ubuntu

Aquí presento los contenedores que he trabajado dentro de mi maquina virtual Ubuntu: 

![[Pasted image 20250704160358.png]]

Luego voy a detener el docker en esta máquina virtual y hacer las gestiones mediante una conexión remota. Esto se vera al final. 

Crear el directorio de trabajo

```sh
$ mkdir -p ~/docker-tls
$ ~/docker-tls
```

##### Crear la CA 
Creamos la Autoridad certificadora, aquí vamos a generar una clave privada RSA de 4096 bits cifrada mediante AES-256 longitud de 256

```sh
$ openssl genrsa -aes256 -out ca-key.pem 4096
```

Creamos un certificado auto firmado valido para un año. Este certificado será usado para firmar certificados del servidor y del cliente.

```sh
$ openssl req -new -x509 -days 365 -key ca-key.pem -sha256 -out ca.pem
```

##### Generar certificado para el servidor

Generamos una clave privada ara el servidor Docker.
```sh
$ openssl genrsa -out server-key.pem 4096
```
  
Creamos una CSR (Solicitud de firma de Certificado) he indico la IP de mi máquina virtual Ubuntu. Esta IP es la que será accedida por mi maquina host que hará de cliente remoto. En este caso, la IP de mi maquina virtual Ubuntu es `192.168.81.9`.

```sh
$ openssl req -subj "/CN=192.168.81.9" -sha256 -new -key server-key.pem -out server.csr
```


Aquí especificamos para qué IP es válido el certificado. Y declaramos que el certificado será usado por el servidor.

```sh
$ echo subjectAltName = IP:192.168.81.9 > extfile.cnf
$ echo extendedKeyUsage = serverAuth >> extfile.cnf
```

  
**Firmar el certificado**
Aquí se firma la solicitud `server.csr` usando la CA para emitir el certificado final del servidor.
  
```sh
$ openssl x509 -req -days 365 -sha256 -in server.csr -CA ca.pem -CAkey ca-key.pem \
-CAcreateserial -out server-cert.pem -extfile extfile.cnf
```
  
##### Generar el certificado para el cliente
Algo similar para el certificado para el cliente. **En nuestro caso será mi maquina host Windows.** Sin embargo podría ser otra máquina.

- Genero una clave privada de 4096 bit para el cliente usando RSA
- Creamos una CSR para el cliente
- Indicamos que este certificado se usará para la autenticación del cliente.

```sh
$ openssl genrsa -out key.pem 4096
$ openssl req -subj '/CN=client' -new -key key.pem -out client.csr
$ echo extendedKeyUsage = clientAuth > extfile-client.cnf

```

  Se firma la CSR del cliente

```sh
$ openssl x509 -req -days 365 -sha256 -in client.csr -CA ca.pem -CAkey ca-key.pem \
-CAcreateserial -out cert.pem -extfile extfile-client.cnf
```

##### Proteger los archivos

- Solo lectura para el propietario
- Solo lectura para todos

```sh
$ chmod 0400 ca-key.pem key.pem server-key.pem
$ chmod 0444 ca.pem server-cert.pem cert.pem
```

  
#### Iniciar Docker con TLS
Una vez que realicé todas las configuraciones en mi máquina virtual Ubuntu paso primero detener el servicio de Docker si es que se esta ejecutando.

Detenemos el servicio docker

```sh
sudo systemctl stop docker
```

  Iniciamos el daemon Docker de forma manual:
```sh
sudo dockerd \
--tlsverify \
--tlscacert=ca.pem \
--tlscert=server-cert.pem \
--tlskey=server-key.pem \
-H=0.0.0.0:2376
```

![[Pasted image 20250704160624.png]]
Con esta imagen demuestro que ya he detenido el docker.

Lo que estoy haciendo aquí es
- Activar la verificación TLS.
- Definir el CA que el cliente debe confiar
- Definir el certificado del servidor.
- La clave privada
- **Exponer mi Docker por TCP en el puerto 2376 para cualquier IP**

#### En la maquina cliente remota (En este caso mi Maquina host Windows)

Debo tener una carpeta con los archivos 
- `ca.pem`
- `cert.pem`
- `key.pem`

Dentro de esa carpeta ejecutaré los siguientes comandos con *Git bash*.
Con estos comandos me conectare al servidor remoto con TLS. Y usaré los certificados y validación con CA.

```sh
$ docker --tlsverify \
--tlscacert=ca.pem \
--tlscert=cert.pem \
--tlskey=key.pem \
-H=tcp://192.168.81.9:2376 version
```

  
Aquí configuramos las variables de entorno.  La ruta ``C:\Users\mitch\Documents\docker-tls`` es mi ruta donde se encuentran los certificados para este cliente. 

```sh
$ export DOCKER_HOST=tcp://192.168.81.9:2376
$ export DOCKER_TLS_VERIFY=1 

# En mi Windows:
$ export DOCKER_CERT_PATH="C:\Users\mitch\Documents\docker-tls"
```

Ejecución de los comandos en mi máquina Windows (es la cliente en este caso)

![[Pasted image 20250704160834.png]]


##### Prueba en maquina cliente Windows

Una simple prueba para comprobar la conexión remota 

```sh
$ docker ps
$ docker ps -a
```

Aquí puede ver que efectivamente la conexión fue exitosa:

![[Pasted image 20250704160913.png]]

Y he usado OpenSSL, TLS, RSA, sha256 etc.

>[!tip] Con ello culmino esta parte, profesor

---

### Parte 3
Demostrar el modo EBC pueden provocar la exposición de información confidencial.       5 puntos

Utilizar la imagen de TUX cifrando con AES y modo ECB (Electronic CodeBook).

![Tux.png](data:image/png;base64,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) ![https://raw.githubusercontent.com/robertdavidgraham/ecb-penguin/master/Tux.ecb.png](data:image/png;base64,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)

Vigenere Cipher: 5 puntos

---

Primero hare una explicación teórica:



El modo ECB es el modo de operación más simple para los cifrados de bloque 

1. **División en Bloques:** El mensaje original (texto plano) se divide en bloques de datos del mismo tamaño que el bloque del cifrado (por ejemplo, si usas AES, el tamaño del bloque es de 128 bits o 16 bytes).
2. **Cifrado Independiente:** Cada uno de estos bloques de texto plano se cifra de forma **independiente** utilizando la misma clave de cifrado.
3. **Concatenación:** Los bloques de texto cifrado resultantes se concatenan para formar el texto cifrado final.
    

**Problemas de Seguridad con ECB:**

La simplicidad de ECB es su mayor debilidad. Debido a que cada bloque de texto plano idéntico se cifra con la misma clave y produce el mismo bloque de texto cifrado, **ECB no oculta patrones en el texto plano**.

- **Patrones Repetitivos**
- **Fuga de Información**
- **Vulnerabilidad a Ataques de Reproducción** 

En ECB cada bloque de texto plano tiene una entrada correspondiente de texto cifrado. Si ves el mismo código cifrado, sabes que el texto plano original era el mismo. Esto es inaceptable para la seguridad criptográfica en la mayoría de los casos.


Para la demostración implemente un script en colab. A continuación muestro mis resultados:

![[Pasted image 20250704175548.png]]

**El codigo**:

```python
# Instalo las librerias necesarias}
!pip install pycryptodome opencv-python matplotlib
```

```python
import cv2
import numpy as np
from Crypto.Cipher import AES
from Crypto.Util.Padding import pad
import matplotlib.pyplot as plt

input_image_name = "TUX.png"

encryption_key = b'SixteenByteKey!!' 

original_img_bgr = cv2.imread(input_image_name)

if original_img_bgr is None:
    print(f"Error: No se pudo cargar la imagen '{input_image_name}'.")
    print("Asegúrate de que 'TUX.png' haya sido subida a la carpeta '/content/' de Colab.")
else:
    
    height, width, channels = original_img_bgr.shape
    image_bytes = original_img_bgr.tobytes()

    # Inicializo el cifrador AES en modo ECB
    cipher = AES.new(encryption_key, AES.MODE_ECB)


    padded_image_bytes = pad(image_bytes, AES.block_size)

    print(f"Tamaño original de la imagen en bytes: {len(image_bytes)}")
    print(f"Tamaño de la imagen con padding: {len(padded_image_bytes)}")
    print(f"Tamaño del bloque AES: {AES.block_size} bytes")

    # Cifro los bytes de la imagen
    encrypted_bytes = cipher.encrypt(padded_image_bytes)

    # Reconstruccion de la imagen para visualizacion
    num_bytes_for_display = height * width * channels
    if len(encrypted_bytes) < num_bytes_for_display:
        display_bytes = encrypted_bytes + b'\x00' * (num_bytes_for_display - len(encrypted_bytes))
    else:
        display_bytes = encrypted_bytes[:num_bytes_for_display]


    encrypted_img_np = np.frombuffer(display_bytes, dtype=np.uint8).reshape((height, width, channels))

    print("\nComparación Visual: Original vs. Cifrada en ECB")


    original_img_rgb = cv2.cvtColor(original_img_bgr, cv2.COLOR_BGR2RGB)
    encrypted_img_rgb = cv2.cvtColor(encrypted_img_np, cv2.COLOR_BGR2RGB)

    plt.figure(figsize=(10, 5))

    plt.subplot(1, 2, 1) 
    plt.imshow(original_img_rgb)
    plt.title("Imagen Original")
    plt.axis('off')

    plt.subplot(1, 2, 2) 
    plt.imshow(encrypted_img_rgb)
    plt.title("Imagen Cifrada (Modo ECB)")
    plt.axis('off') # Ocultar ejes

    plt.suptitle("Fuga de Información en el Cifrado ECB", fontsize=18, y=1.02)
    plt.tight_layout(rect=[0, 0.03, 1, 0.95])
    plt.show()
```

---

### Parte 4
Cuál es la llave y el texto (Utilizar el método de Kasiski)

GAXRUQMMNIGEQKOFUQWGGMNMPIWRTQEVGMNRTKIUKWWQQVDWUMWVOCLSWVGVDMRSVIUHGMNMPMRGQZNGEWRGTWLSFWEPCLAWPBMQCLPSTBMPKXAFVMCFGWBKGZZNNISSEKMBPMSVGAYRSCIHQLIEGAPMGAXNUINLGQRPKLEFVMWQGAEYWZMQCLDAIQXNNMLGDRIGKDOWUUIQKZYXQZXNNMCWTTEPCXAUKLEQFMRWCKGVQVDWNIWRPBIVCLIFRCBDKKEFAXRAXIHNUINLGXSFKJLWUKMOGZALCYYRUISAEWQBEWNKQTMQCZLSUIGPKWNWULIFGOUJKLEQFQGAVIPCCZADCXVBVMCUKWRQGTAUKCHNFINACNVRPBESNWWEKMSYQACNOMNSBIWRPMLWPBSEPWDAIQXNNMLKKUYYCKRGGAHVTQGAFWTBTTAKGKVRVIRACLITQJIWTVSLVZAFUNSEOICAQVHVIQTSNLIYCXCECBVNXMSVGTGRPBRGPIGVQVADFMWRICRAFIHQKOILCTIAGTMSTKSQGTQMKVXBQJJWVQZBRZIGTQXNTQOVGTECQTILKKEACKIGPIPQGBRSPAJBTUAUKWRQKOILCTKNTINLKHEENISWICVVFIDQEWRSKINRCLMTKBADGVIYRIIK

- GAX: 2
- GMN: 3
- GA: 2
- GT: 7
- GV: 4
- IG: 5
- IWR: 3
- IHQ:2
- IN: 5
- INL: 3
- IQ: 4
- IQX: 2

--- 