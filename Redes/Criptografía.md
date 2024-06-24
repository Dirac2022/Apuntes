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

![[Pasted image 20240617154520.png]]

## El cifrado de Julio Cesar

$$
C = M + (k \ mod \ |A\, |)
$$

- *M*: mensaje original
- *K*: clave
- *C*: mensaje cifrado
- *A*: alfabeto

![[Pasted image 20240617154637.png]]


## Disco de Alberti


## Cifrado de Vernam
El sistema aplica la operación *XOR* y una secuencia aleatoria *S* obtenida en base a una clave previamente compartida. Se mejoro proponiendo que la clave tenga información aleatoria implementando las libretas de un solo uso.

![[Pasted image 20240617154801.png]]



Ejemplo
mensaje: vernam
llave: playas

![[Pasted image 20240617154827.png]]


## Máquina enigma
Máquina de cifrado más famosa de la historia, por su uso en la II Guerra Mundial. Usaba rotores de 26  contactos eléctricos sobre un eje, se desplazaban a modo ondómetro. Un sistema con cinco rotores con un periodo de $26^5$.

# Criptografía moderna

- Su auge comenzó en la segunda guerra mundial.
- En la década de los 70 los sistemas informáticos tuvieron una importante evolución, aplicando matemática a la criptografía, naciendo el cifrado asimétrico y simétrico.
- Se basa en 3 pilares: teoría de la información (transporte), teoría de números (congruencia) y complejidad algorítmica (recursos usados).

## Cifrado simétrico

- Fue el principal método de encriptación hasta fines de los años 70 cuando apareció el cifrado asimétrico.
- Es más rápido que la asimétrica, por tanto se utiliza en ocasiones donde se cifra gran cantidad de datos y en tiempo real.
- Usa la misma llave para encriptar y desencriptar la información.

![[Pasted image 20240617155116.png]]


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


| Algoritmo                      | Tamaño de la llave (bits) | Usos |
| ------------------------------ | ------------------------- | ---- |
| DES (Data encryption standard) | 56 + 8 de paridad         |      |
| 3 DES                          | 112, 168                  |      |
| Advanced encryption standard   | 128, 192, 256             |      |

## Cifrado de flujo
Es un método de cifrado que cifra un bit  o byte de un texto sin formato a la vez mediante un flujo de claves. Un flujo de claves es una secuencia de bit o bytes

| Algoritmo                 | Tamaño de la llave (bits) | Usado en |
| ------------------------- | ------------------------- | -------- |
| RC4                       | 40-2048                   |          |
| Salsa20                   | 128, 256                  |          |
| SEAL                      | 2048                      |          |
| A5/1, A5/2, A5/3 (KASUMI) | 64-128                    |          |

# Seguridad de cifrado
Dos principales ataques:
- **Criptoanálisis**.
- **Ataque por fuerza bruta**, una adecuada longitud de la llave previene que ésta pueda ser descubierta probando las posibles combinaciones hasta encontrar la llave.



# Cifrado asimétrico
- Hace uso de dos llaves, una pública y una secreta.
- La llave pública no es secreta, mientras que la llave privada si lo es.
- Tanto el emisor como el receptor generan un par de llaves público - privado.
- Ambos comparten su llave pública con quien desea establecer una comunicación secreta. Las llaves privadas se mantienen en secreto y solo el dueño debe conocerlo.

Dos formas de uso:
- Encriptador


### Uso 1: Garantizar la confidencialidad de la información
- El mensaje cifrado solo podrá ser descifrado por el receptor con su llave privada, garantizando la confidencialidad, usado en seguridad ...


### Uso 2: Verificar la autenticidad de la información
Cuando se encripta usando la clave privada del emisor, todos los receptores que tengan su llave pública podrán desencriptarlo, de esa forma se puede verificar que el emisor es realmente quien dice ser


## Intercambio de claves Diffie-Hellman
- Es uno de los principales algoritmos de intercambio de claves.
- Permite acordar una clave en común entre dos usuarios, a través
