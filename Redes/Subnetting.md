	El *subnetting* o creación de subredes es la subdivisión de una red en segmentos más pequeños. Permite una gestión más eficiente de direcciones IP y una mejor organización de la red, lo que resulta en un rendimiento óptimo y una mayor seguridad. Se logra utilizando una máscara de subred para dividir una dirección IP en una parte de red y una parte de host, lo que permite identificar cada subred de manera única.
# Ventajas
- Permite **aislar el tráfico** entre las distintas subredes.
- Se reduce el tráfico global.
- Permite **limitar y proteger** el acceso a las distintas subredes.
- La **comunicación** entre estas se realiza mediante un router.
- Permite **organizar la red en áreas o departamentos**.
- Se asigna a cada departamento un subconjunto de direcciones IP.
- La gestión de las direcciones IP se puede delegar en la propia área o departamento:
	- Se **descentraliza la tarea de asignación** de direcciones.
	- Se **facilita** la tarea del administrador de la red.


# Definición
En el *subnetting* se toman bits del ID del [[Conceptos en Redes#Host|host]] *prestados* para crear una subred. Con solo **un bit** se tiene la posibilidad de generar **dos subredes**, puesto que solo se tiene en cuenta el 0 o el 1. Para una cantidad mayor de subredes se tienen que liberar más bits, de modo que hay menos espacio para direcciones de hosts.

![[Pasted image 20240505165350.png]]

![[Pasted image 20240505165417.png]]

![[Pasted image 20240505165422.png]]

# Cantidad de subredes y host

La cantidad de subredes se calcula a partir de la cantidad de bits separados de la porción de host. Si $M$ es esta cantidad, entonces

$$ \text{cantidad de subredes : } \quad 2^M  $$


La cantidad de host efectivo se calcula a partir de la cantidad de bits restantes de la porción de host. Si $H$ es esta cantidad, entonces
$$ \text{cantidad de host : } \quad 2^H - 2  $$
Se resta 2 del resultado para excluir la dirección de red p subred (todos los bits de host en 0) y la dirección de difusión (todos los bits de host en 1).

## Ejemplos

### Ejemplo 1
Se tiene una dirección de red con longitud de prefijo **24** y una sub red **192.168.44.0/27** producto del Subnetting. A partir de ello **¿cuál es la mascara usada, el número total de sub redes generadas y la cantidad de host en cada una?**

Mascara: **/27** nos dice que la máscara esta compuesta por 27 unos (1) de la siguiente forma:
$$ 11111111. 11111111. 11111111. 11100000 = 255.255.255.224 $$
Número de sub redes: se tomaron 3 bits de la sección de host por ende
$$ 2^3 = 8 \quad \text{ sub redes} $$
Número de hosts: Restan 5 bits de la sección de host por ende
$$ 2^5 - 2 = 30 \quad \text{host} $$
### Ejemplo 2
![[Pasted image 20240505173100.png]]

## División basada en necesidad de host o subredes
Factores a tomar en cuenta:
- El número de direcciones de host que se requieren para cada red.
- El número de subredes individuales necesarias.

![[Pasted image 20240505181311.png]]

### División basada en necesidad de subredes

Se tiene una dirección de red privada `172.18.0.0/22` se requiere dividir de tal forma que genere **14 subredes** como mínimo, ¿cuál es la máscara que debe usarse?

<div>
<span style="color:orange;"> IP: 172.18.0.0/22</span> <span>-> 10101100.00010010.00000000.00000000 </span>
</div>
<div>
<span style="color:orange;">Máscara</span> <span>->11111111.11111111.11111100.00000000</span>
</div>

Entonces $2^n \geq 14$ siendo $n$ el número de bits que se tomarán de la porción de host, el valor $n=4$

<div>
<span style="color:orange;"> IP: 172.18.0.0/22</span>
<span> -> 1 0 1 0 1 1 0 0 . 0 0 0 1 0 0 1 0 . 0 0 0 0 0 0</span>
<span style="color:orange;">0 0 . 0 0</span>
<span>0 0 0 0 0 0</span>
</div>
<div>
<span style="color:orange;">Máscara</span>
<span>->1 1 1 1 1 1 1 1 . 1 1 1 1 1 1 1 1 . 1 1 1 1 1 1</span>
<span style="color:orange;">1 1 . 1 1</span>
<span>0 0 0 0 0 0</span>
</div>
<div>
<span style="color:orange;">Máscara</span>
<span>-></span>
<span style="color:orange;">255.255.255.192</span>
</div>


### División basada en necesidad de host
![[Pasted image 20240505185317.png]]
![[Pasted image 20240505185343.png]]

# Máscaras de longitud variable (Variable Length Subnet Mask VLSM)

- VLSM permite dividir un espacio de red en partes desiguales.
- La máscara de subred varía según la cantidad de bits que se toman prestados para una subred específica.
- La red primero se divide en subredes y, a continuación, las subredes se vuelven a dividir en subredes.
- Este proceso se repite según sea necesario para crear subredes de diversos tamaños.
- En el proceso de crear subredes con VLSM se recomienda iniciar con las subredes más grandes y terminar con las más pequeñas.
## Caso práctico
Da flojera
# Asignación de IP a dispositivos

**Clientes usuarios finales**
La mayoría de las redes asignan direcciones de manera dinámica con [[Protocolos#DHCP (Dynamic Host Configuration Protocol)|DHCP]]. Esto reduce la carga sobre el personal de soporte de red y elimina de manera virtual los errores de entrada. Del mismo modo,  las direcciones solo se conceden por un periodo determinado. Cambiar el esquema de división en subredes significa que se necesita volver a configurar el servidor DHCP y que los clientes deben renovar sus direcciones IP. Los clientes IPv6 pueden obtener información de dirección mediante [[Protocolo IP#DHCPv6 (Dynamic Host Configuration Protocol for IPv6)|DHCPv6]] o [[Protocolo IP#SLAAC (Stateless Address Autoconfiguration)|SLAAC]].

**Servidores y periféricos**
Deben tener una dirección IP estática predecible. Utilice un sistema de numeración coherente para estos dispositivos.

**Servidores a los que se puede acceder mediante Internet**
En muchas redes los servidores deben ponerse a disposición de usuarios remotos. En la mayoría de los casos, a estos servidores se les asignan direcciones privadas internamente, y el router o firewall en el perímetro de la red debe estar configurado para traducir la dirección interna a una dirección pública.


**Dispositivos intermediarios**
A estos dispositivos se asignan direcciones para la administración, la supervisión y la seguridad de redes. Debido a que es necesario saber cómo comunicarse con dispositivos intermediarios, estos deben tener asignadas direcciones predecibles y estáticas.

**Gateway**
Los routers y los dispositivos de firewall tiene una dirección IP asignada para cada interfaz que sirve como gateway para los host de dicha red. Normalmente, la interfaz de router utiliza la dirección más baja o más alta de la red.

