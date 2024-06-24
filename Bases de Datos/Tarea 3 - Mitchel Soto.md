
**TAREA 3 - MITCHEL SOTO**

**1. Seleccionar los empleados del departamento de Ventas o con más
de 4 años de antigüedad**

$$ \Pi_{Empleado} (\sigma_{Departamento = 'Ventas' \: \lor \: Antguedad > 4} (Empleado)) $$

**2. Dada una tabla Productos con los atributos ID_Producto, Nombre,
Precio, Stock, Categoria, seleccionar todos los productos que tienen
un precio diferente a $20 y que tienen menos de 3 unidades en
stock.**
$$ \sigma_{Precio \neq 20 \: \land \: Stock < 3}(Productos) $$
**3. Dada una tabla Productos con los atributos ID_Producto, Nombre,
Precio, Stock, Categoría, obtener los nombres y precios de los
productos.**

$$ \Pi_{Nombre, Precio} (Productos) $$
**4. Obtener el número de pedido, el nombre del cliente y el precio total
de los pedidos con un precio total mayor a $50**
$$ \Pi_{numPedido, Cliente, Precio Total}(\sigma_{Precio Total > 50} (Pedidos)) $$
Estoy asumiendo que la tabla se llama *Pedidos*

**5. De los clientes que compraron un producto en la última semana (a
partir del 2023-03-12) y que viven en la ciudad de Lima. Obtener sus
nombres, la fecha de compra y el total de la compra.**

$$ \Pi_{nombre, fecha_compra, total_compra} (\sigma_{fecha_compra > 2023-03-12 \: \land \: fecha_compra < 2023-03-19} (Clientes)) $$
Estoy asumiendo que la tabla se llama *Clientes* y el formato es yyyy/mm/dd


