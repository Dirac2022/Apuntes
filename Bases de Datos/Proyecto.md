
**Mostrar todas las misiones que hayan tenido un resultado exitoso.**



**Mostrar el id_vehiculo y nombre_vehiculo de los vehiculos que pesen más de 1000kg**
{t.id_vehiculo, t.nombre | Vehiculo(t) AND t.peso > 1000 }

**Mostrar los cientificos que no participan en algún experimento**

{t.id_cientifico | Cientifico(t)  AND $\lnot$ ($\exists$ s) (Experimento(s) AND s.id_cientifico=t.id_cientifico) }