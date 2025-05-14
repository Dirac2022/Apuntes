- Se define como un conjunto de técnicas con base matemática y aplicadas por medio de la informática para ocultar información.

- Las guerras son el principal factor que promovió los avances criptográficos (y de la computación en general) a lo largo de la historia.
- Permite asegurar la confidencialidad, autenticidad, integridad y no repudio de la información.

- Como contramedida nace el **criptoanálisis** que consiste en el estudio de los sistemas criptográficos para descubrir sus debilidades y así romper la seguridad de estos.


## Clasificación
**Según la época de desarrollo**
- Criptografía clásica
- Criptografía moderna

 **Según el tipo de algoritmo utilizado**
- Algoritmos simétricos (clave privada)
- Algoritmos asimétricos (clave pública)

**Según el procedimiento**
- Por bloque de datos
- Bit por bit (algoritmos de flujo)

## Componentes

- **Emisor**: quien realiza el cifrado
- **Receptor** : quien realiza el descifrado.
- **Medio**: canal usado para intercambiar información
- **Algoritmo**: transformaciones aplicadas al mensaje para obtener el cifrado
- **Mensaje** información que se desea ocultar
- **clave o llave**: pieza de información que aplicada al algoritmo, permite transformar el mensaje en criptograma o viceversa.
- **Criptograma**: mensaje cifrado.
- **Protocolo**: conjunto de reglas para intercambiar información de una manera particular

# Criptografía clásica

## Escítala
Aplicaba el método de transposición de caracteres, utilizando el bastón de enrollado como "clave". Usada en el siglo V a.C. en Grecia.

<div style="text-align: center;">
	<figure>
    <img src="https://museo.inf.upv.es/wp-content/uploads/2021/05/cifrario-4.jpg" width=400>
    <figcaption></figcaption>
    </figure>
</div>



## El cifrado de Julio Cesar

$$
C = (M + k) \ mod \ |A\, |
$$

- *M*: mensaje original
- *K*: clave
- *C*: mensaje cifrado
- *A*: alfabeto

![[Pasted image 20240617154637.png]]

Para descifrar el mensaje tendríamos que aplicar la operación "inversa"
$$
M = (C - k) \ mod \ |A|
$$
## Disco de Alberti
Basado en un disco en el cual dependiendo de una clave, cada letra podría ser cifrado con un carácter diferente. Constaba con un disco exterior con 20 caracteres en latín más los números de 1 al 4, y un disco interior con caracteres latinos y el signo & y las letras H, K e Y.

<div style="text-align: center;">
	<figure>
    <img src="https://www.geogebra.org/resource/fhfk7fbu/8iyUS1la7OMeHjT3/material-fhfk7fbu.png" width=400>
    <figcaption></figcaption>
    </figure>
</div>

### Ejemplo
Por ejemplo si la palabra a cifrar es **REDES**. Se gira el disco interior hasta escoger una **letra clave**, esta clave se encontrará en la misma posición que la letra **A**. En nuestro ejemplo, la letra clave es la letra **J**. A partir de esta configuración buscamos las posiciones de las letras de nuestra palabra a cifrar y obtenemos las letras correspondientes en el disco exterior.

- R $\to$ J
- E $\to$ V
- D $\to$ U
- E $\to$ V
- S $\to$ K
Por tanto nuestra palabra cifrada es **JVUVK**.

![[ejemplo disco alberti.png]]


## Cifrado de Vernam
El sistema aplica la operación *XOR* y una secuencia aleatoria *S* obtenida en base a una clave previamente compartida. Se mejoro proponiendo que la clave tenga información aleatoria implementando las libretas de un solo uso.

![[Pasted image 20240617154801.png]]



Ejemplo
mensaje: vernam
llave: playas


| Mcla                | V         | E         | R         | N         | A         | M         |
| ------------------- | --------- | --------- | --------- | --------- | --------- | --------- |
| Dec/Hex             | 86/56     | 69/45     | 82/52     | 78/4E     | 65/41     | 77/4D     |
| Bin                 | 0101 0110 | 0110 0110 | 0101 0010 | 0100 1110 | 0100 0001 | 0100 1101 |
| Llave               | p         | l         | a         | y         | a         | s         |
| Dec/Hex             | 112/70    | 108/6C    | 97/61     | 121/79    | 97/61     | 115/73    |
| Bin                 | 0111 0000 | 0110 1100 | 0110 0001 | 0111 1001 | 0110 0001 | 0111 0011 |
| XOR                 | 0010 0110 | 0010 1001 | 0011 0011 | 0011 0111 | 0010 0000 | 0011 1110 |
| Criptograma (ASCII) | &         | )         | 3         | 7         |           | >         |


## Máquina enigma
Máquina de cifrado más famosa de la historia, por su uso en la II Guerra Mundial. Usaba rotores de 26  contactos eléctricos sobre un eje, se desplazaban a modo ondómetro. Un sistema con cinco rotores con un periodo de $26^5$.


<div style="text-align: center;">
	<figure>
    <img src="https://www.bbvaopenmind.com/wp-content/uploads/2017/01/1-Enigma-2.jpg" width=400>
    <figcaption></figcaption>
    </figure>
</div>


# Criptografía moderna

- Su auge comenzó en la segunda guerra mundial.
- En la década de los 70 los sistemas informáticos tuvieron una importante evolución, aplicando matemática a la criptografía, naciendo el cifrado asimétrico y simétrico.
- Se basa en 3 pilares: teoría de la información (transporte), teoría de números (congruencia) y complejidad algorítmica (recursos usados).

## Cifrado simétrico

- Fue el principal método de encriptación hasta fines de los años 70 cuando apareció el cifrado asimétrico.
- Es más rápido que la asimétrica, por tanto se utiliza en ocasiones donde se cifra gran cantidad de datos y en tiempo real.
- Usa la misma llave para encriptar y desencriptar la información.

<div style="text-align: center;">
	<figure>
    <img src="https://www.textoscientificos.com/imagenes/criptografia/clave-privada.gif" width=500>
    <figcaption></figcaption>
    </figure>
</div>

## Cifrado usando XOR
![[Pasted image 20240617155248.png]]
![[Pasted image 20240617155321.png]]


## Cifrado en bloque
Agrupan los bits del mensaje original en bloques de determinada longitud y luego cifran uno de tales bloques.

El tamaño del bloque depende del algoritmo, pero suelen ser de 64, 128 o 256 bits.

Presenta varias formas de uso entre las que destacan:
- ECB: Cada bloque se cifra con la misma clave.
- CBC: Cada bloque se aplica un xor con el bloque anterior antes de cifrarlo
- CFB: Similar a CBC pero el texto plano se aplica después del bloque cifrado.


| Algoritmo                      | Tamaño de la llave (bits) | Usos                                                                                    |
| ------------------------------ | ------------------------- | --------------------------------------------------------------------------------------- |
| DES (Data encryption standard) | 56 + 8 de paridad         | A inicios de la criptografía moderna, en desuso por su vulnerabilidad en la actualidad. |
| 3 DES                          | 112, 168                  | Mejora de DES. Usado en Office, Firefox entre otros. En desuso.                         |
| Advanced encryption standard   | 128, 192, 256             | El más usado en la actualidad                                                           |

## Cifrado de flujo
- Es un método de cifrado que cifra un bit o byte de texto sin formato a la vez mediante un flujo de claves. Un flujo de claves es una secuencia de bits o bytes generada por una clave y un algoritmo.
- La clave $S$ debe ser una secuencia pseudoaleatoria a partir de un algoritmo determinístico basado en una semilla $k$ de $n$ bits.
- Bastante usado para cifrado en tiempo real por la mayor rapidez en comparación con cifrado de bloque.

| Algoritmo                                      | Tamaño de la llave (bits) | Usado en                                                                                   |
| ---------------------------------------------- | ------------------------- | ------------------------------------------------------------------------------------------ |
| RC4 (Rivest Cipher 4)                          | 40-2048                   | Usado en el protocolo WEP de la red inalámbrica (WiFi), TKIP, BitTorrent, etc.             |
| Salsa20                                        | 128, 256                  | Ha permitido la creación de muchos variantes que han sido implementado en varios sistemas. |
| SEAL (Software-optimized Encryption Algorithm) | 2048                      | Usado en sistemas de encriptación de discos                                                |
| A5/1, A5/2, A5/3 (KASUMI)                      | 64-128                    | Comunicación celular GSM (A5/1, A5/2, A5/3), UMTS (A5/3) y GPRS (A5/3)                     |
**Otros algoritmos**
- PANAMA
- Scream
- Rabbit
- HC-256
- Grain


# Seguridad de cifrado

Dos principales ataques:
- **Criptoanálisis**.
- **Ataque por fuerza bruta**, una adecuada longitud de la llave previene que ésta pueda ser descubierta probando las posibles combinaciones hasta encontrar la llave.

| Tamaño de la llave (en bits) | Número de combinaciones de llaves | Tiempo requerido (1 desencriptación por $\mu s$) | Tiempo requerido ($10^6$ desencriptaciones por $\mu s$) |
| ---------------------------- | --------------------------------- | ------------------------------------------------ | ------------------------------------------------------- |
| 32                           | $2^{32}$                          | $2^{32} \ \mu s$ = 71.5 min                      | 1.54 horas                                              |
| 56                           | $2^{56}$                          | $2^{56} \ \mu s$ = 2316.6 años                   | 50.04 horas                                             |
| 128                          | $2^{128}$                         | $2^{128} \ \mu s$ = $1.09 \times 10^{25}$ años   | $1.09 \times 10^{19}$ años                              |
| 168                          | $2^{168}$                         | $2^{168} \ \mu s$ = $1.2 \times 10^{37}$ años    | $1.2 \times 10^{31}$ años                               |

# Cifrado asimétrico
- Hace uso de dos llaves, una pública y una privada.
- La llave pública no es secreta, mientras que la llave privada si lo es.
- Tanto el emisor como el receptor generan un par de llaves público - privado.
- Ambos comparten su llave pública con quien desea establecer una comunicación secreta. Las llaves privadas se mantienen en secreto y solo el dueño debe conocerlo.

Dos formas de uso:
- Encriptado con la llave pública del receptor, por lo que solo podrá ser desencriptada por la llave privada del receptor.
- Encriptado con la llave privada del origen, en el destino solo se podrá desencriptar el mensaje con la llave publica del emisor.


### Uso 1: Garantizar la confidencialidad de la información
- El mensaje cifrado solo podrá ser descifrado por el receptor con su llave privada, garantizando la confidencialidad, usado en seguridad ...

<div style="text-align: center;">
	<figure>
    <img src="https://economica.pe/wp-content/uploads/2024/04/5.png" width=600>
    <figcaption></figcaption>
    </figure>
</div>
### Uso 2: Verificar la autenticidad de la información
Cuando se encripta usando la clave privada del emisor, todos los receptores que tengan su llave pública podrán desencriptarlo, de esa forma se puede verificar que el emisor es realmente quien dice ser

<div style="text-align: center;">
	<figure>
    <img src="https://economica.pe/wp-content/uploads/2024/04/6.png" width=600>
    <figcaption></figcaption>
    </figure>
</div>

## Intercambio de claves Diffie-Hellman
- Es uno de los principales algoritmos de intercambio de claves.
- Permite acordar una clave en común entre dos usuarios, a través de un canal de comunicacióninseguro.
- Su efectividad esta basada en su dificultad para calcular logaritmos discretos.


### Pasos del algoritmo
1. Se eligen dos números $g$ y $p$ donde $g$ es una primitiva modulo $p$ y $p$ e un número primo. Se cumple que
$$
g^{p-1} \ mod \ p \equiv 1
$$
2. Cada parte selecciona un número, por ejemplo $a$ y $b$, tal que $a, \ b < p$ y cada parte genera una **clave pública** $A$ y $B$.
	1. $A \equiv g^a \ (mod \ p)$
	2. $B \equiv g^b \ (mod \ p)$
3. Las partes comparten sus claves públicas a través de un canal inseguro.
4. Cada parte utiliza su clave pública recibida para calcular la clave privada compartida ($K_a$ , $K_b$) dicha clave privada será calculada por cada parte de la siguiente manera.
	1. $K_a \equiv B^a \ (mod \ p)$
	2. $K_b \equiv A^b \ (mod \ p)$
5. La clave privada es la misma para cada parte ya que:
$$
K_a = B^a \ (mod \ p) = \dots = A^b \ (mod \ p) = K_b
$$
