
# Consultas IP

## `addr`
Muestra las direcciones IP e información asignadas a las interfaces de red.

Muestra información de todas las direcciones IP
```bash
ip addr
```

Muestra información de las direcciones IP solo para la interfaz `em1`
```bash
ip addr show dev em1
```

## `link`
Gestiona y muestra el estado de todas las interfaces de red

Muestra información de todas las interfaces de red.
```bash
ip link
```

Muestra información solo para la interfaz `em1`.
```bash
ip link show dev em1
```

Muestra estadísticas detalladas de las interfaces de red (envío, recepción de paquetes, etc.).
```bash
ip -s link
```

## `route`
Se usa para mostrar y modificar las rutas en la tabla de enrutamiento del kernel

Lista rotas las rutas en la tabla de enrutamiento del kernel
```bash
ip route
```

## `maddr`
Gestiona y muestra las direcciones IP multicast asignadas a las interfaces de red. Las direcciones multicast permiten que un paquete sea recibido por múltiples destinos.

Muestra información información multicast para todas las interfaces de red
```bash
ip maddr
```

Muestra la información multicast para la interfaz `em1`
```bash
ip maddr show dev em1
```

## `neigh`
Se usa para mostrar los objetos vecinos, también conocidos como la tabla [[Protocolos#ARP (Address Resolution Protocol)|ARP]] para IPv4.

Muestra los objetos vecinos para todas las interfaces de red.
```bash
ip neigh
```

Muestra la caché ARP solo para la interfaz `em1`
```bash
ip neigh show dev em1
```

## `help`
Proporciona una lista de comandos y argumentos específicos para cada subcomando

```bash
ip help
```

```bash
ip addr help
```

```bash
ip link help
```

```bash
ip neigh help
```


# Modificando las propiedades de dirección y enlace

## `addr add`
Agrega una dirección IP

Agrega la dirección 192.168.1.1 con la mascara de red 24 al dispositivo `em1`
```bash
ip addr add 192.168.1.1/24 dev em1
```

## `addr del`
Elimina una dirección IP

Elimina la dirección 192.168.1.1/24 del dispositivo `em1`
```bash
ip addr del 192.168.1.1/24 dev em1
```

## `link set`
Modifica el estado de una interfaz de red.

Activa la interfaz de red `em1`
```bash
ip link set em1 up
```

Desactiva la interfaz de red `em1`
```bash
ip link set em1 down
```

Activa el modo promiscuo, permitiendo que la interfaz capture todo el tráfico de red, no solo el destinado a ella
```bash
ip link set em1 promisc on
```


# Ajustando y visualizando rutas

## `route add`
Añade una entrada a la tabla de rutas

Añade una ruta por defecto (para todas las direcciones) a través del gateway local `192.168.1.1` usando la interfaz `em1`
```bash
ip route add default via 192.168.1.1 dev em1
```

Añade una ruta para la red `192.168.1.0/24` a través del gateway `192.168.1.1`
```bash
ip route add 192.168.1.0/24 via 192.168.1.1
```

Añade una ruta para la red `192.168.1.0/24` que puede ser alcanzada directamente en la interfaz `em1`
```bash
ip route add 192.168.1.0/24 dev em1
```

## `route delete`
Eliminar una entrada de la tabla de rutas. Este comando elimina una ruta específica de la tabla de enrutamiento.

Elimina la ruta para `192.168.1.0/24` que pasa a  través del gateway `192.168.1.1`
```bash
ip route delete 192.168.1.0/24 via 192.168.1.1
```

## `route replace`
Reemplaza o añade una entrada en la tabla de rutas. Este comando reemplaza una entrada de ruta existente o la añade si no está definida.

Reemplaza la ruta para `192.168.1.0/24` que pasa por la interfaz `em1`. Si no existe, la crea.
```bash
ip route replace 192.168.1.1/24 dev em1
```

## `route get`
Mostrar la ruta que tomará una dirección IP. Este comando muestra el camino o ruta que tomará un paquete al intentar alcanzar una dirección IP específica.

Muestra la ruta que tomará el paquete para llegar a `192.168.1.5`
```bash
ip route get 192.168.1.5
```


# Gestión de la tabla ARP
La tabla [[Protocolos#ARP (Address Resolution Protocol)|ARP]] almacena las asociaciones entre direcciones IP y direcciones MAC, permitiendo que el sistema pueda comunicar los paquetes de datos en una red local. El comando `ip neigh` se usa para gestionar estas entradas.

## `neigh add`
**Añade una entrada a la tabla ARP**

Añade la dirección IP `192.168.1.1` con la dirección MAC `1:2:3:4:5:6` a la interfaz `em1`
```bash
ip neigh add 192.168.1.1 lladdr 1:2:3:4:5:6 dev em1
```

## `neigh del`
Invalida (elimina) una entrada en la tabla ARP. 

Invalida la entrada de la IP `192.168.1.1` en la interfaz `em1`.
```bash
ip neigh del 192.168.1.1 dev em1
```

## `neigh replace`
Reemplaza una entrada existente o la añade si no está

Reemplaza la entrada de la IP `192.168.1.1` con la dirección MAC `1:2:3:4:5:6` en `em1`. Si no existe, la crea.
```bash
ip neigh replace 192.168.1.1 lladdr 1:2:3:4:5:6 dev em1
```

