

## Task 1: Create a New EBS Volume

- Seleccioné el servicio **EC2** en el cuadro de búsqueda
- Seleccioné **Instances** en el panel lateral izquierdo
	- Como se observa, ya existen dos instancias EC2, con Zonas de disponibilidad **us-east-1a**

![[Pasted image 20250922183338.png]]

- Seleccioné **Volumes**
	- Pude observar los **volumes** usados por las instancias EC2 recién creadas.


![[Pasted image 20250922183657.png]]
![[Pasted image 20250922183533.png]]

**Crear Volume**

Procedí a crear un **Volume** con las siguientes especificaciones
- **Volume Type:** _General Purpose SSD (gp2)_
- **Size (GiB):** `1`. 
- **Availability Zone:** `us-east-1a`.
- Choose Add tag
- Tags:
    - **Key:** `Name`    / **Value:** `My Volume`

![[Pasted image 20250922183930.png]]


## Task 2: Attach the Volume to an Instance

- Seleccioné **My Volume**
- En el menú **Actions** seleccioné **Attach volume**

![[Pasted image 20250922184310.png]]

- Seleccioné **Lab** instance
- En **Device**, elegí `/dev/sdf`

![[Pasted image 20250922184504.png]]


## Task 3: Connect to Your Amazon EC2 Instance

- Selección **Instances** en el panel lateral izquierdo del servicio **EC2**
- Seleccioné la instancia **Lab**
- Seleccioné el botón **Connect**

![[Pasted image 20250922184723.png]]


- Seleccioné el botón **Connect** de **EC2 instance Connect**

![[Pasted image 20250922184900.png]]

## Task 4: Create and Configure Your File System


**Comandos usados dentro de la terminal**

Mostré el espacio de uso en disco:

```sh
df -h
```

![[Pasted image 20250922185229.png]]


- Creé el sistema de archivos `ext3` en el nuevo volumen
reate an ext3 file system on the new volume:

```sh
sudo mkfs -t ext3 /dev/sdf
```

![[Pasted image 20250922185608.png]]

- Creé un directorio para montar el volumen

```sh
sudo mkdir /mnt/data-store
```

*No hubo salida*

- Montar el nuevo volumen:

```sh
sudo mount /dev/sdf /mnt/data-store
```

*No hubo salida*

- Ver el archivo de configuración, la ultima línea:

```sh
cat /etc/fstab
```

![[Pasted image 20250922190509.png]]

- Revisé nuevamente el espacio disponible:

```sh
df -h
```

![[Pasted image 20250922190600.png]]

Se puede observar que en la última línea aparece el volumen montado


- Creé un archivo (`file.txt`) en el volumen montado

```sh
sudo sh -c "echo some text has been written > /mnt/data-store/file.txt"
```

- Lo validé

```sh
cat /mnt/data-store/file.txt
```

![[Pasted image 20250922190856.png]]


## Task 5: Create an Amazon EBS Snapshot

- Me situé en **Volumes**
- Seleccioné **My Volume**
- Seleccioné **Create snapshot** del menú **Actions**

![[Pasted image 20250922191046.png]]

- Procedí a crear el **snapshot**
	- Añadi el tag: key: `Name`, value: `My snapshot`

![[Pasted image 20250922191303.png]]


Una vez que el **snapshot** se creó con éxito (status: Completed) procedí a volver a la sesión de **EC2 Instance Connect**


- Eliminé el archivo previamente creado en el volumen

```sh
sudo rm /mnt/data-store/file.txt
```

- Se pudo observar que el archivo fue correctamente eliminado:

```sh
ls /mnt/data-store/
```

![[Pasted image 20250922191807.png]]


## Task 6: Restore the Amazon EBS Snapshot

**Procedí a crear un nuevo volumen a partir del snapshot**

- Seleccioné **My snapshot**
- En el menú **Actions** seleccioné **Create volume from snapshot**

![[Pasted image 20250922192042.png]]


**Para crear el volumen a partir del snapshot**

- Seleccione el mismo Zona Availability
- Añadí el tag: key: `Name`, value: `Restored Volume`

![[Pasted image 20250922192135.png]]

Vemos que se creó exitosamente:

![[Pasted image 20250922192328.png]]

Una vez seleccionado **Restored Volume**

- En el menú **Actions** seleccioné **Attach volume**
- Elegí la instancia **Lab**
- En **Device** seleccioné _`/dev/sdg`


![[Pasted image 20250922192659.png]]


### Mount the Restored Volume

Luego procedí a montar el volumen y pude confirmar que el archivo creado `file.txt` persiste:

```sh
sudo mkdir /mnt/data-store2
```

```sh
sudo mount /dev/sdg /mnt/data-store2
```

```sh
ls /mnt/data-store2/
```

```sh
cat /mnt/data-store2/file.txt
```

![[Pasted image 20250922193026.png]]


**Laboratorio concluido**
