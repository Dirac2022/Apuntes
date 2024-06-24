

# Laboratorio 15 - 06/06/24
Por supuesto, aquí tienes el texto sin los asteriscos:

Para instalación de mongoDB

https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-windows/

Para acceder a mongo:
```
mongosh
```

Crear base de datos:
```
use nombre_bd
```

Un documento es un conjunto de objetos clave valor, como un diccionario en python,
o como los archivos JSON. Serian lo análogo a las tuplas o registros de
las tablas en bases de datos relacionales.

2. **Crear base de datos mibd:**
```
use mibd
```

3. **Muestre la base de datos actualmente en uso:**
```
db
```

4. **Ahora proceda a listar todas las bases de datos disponibles:**
```
show dbs
```

5. **Comando para eliminar la base de datos seleccionada actualmente**
```
db.dropDatabase()
```



Para eliminar una base de datos debemos estar en ella, si deseamos
borrar la bd ventas:
```
use ventas
db.dropDatabase()
```

Salir de la sesión:
```
exit()
```

6. **Crear la base de datos ventas**
```
use ventas
```

7. **Crear la coleccion productos**
```
db.createCollection("Productos")
```


8. **Utilice el método *insert* para crear la colección Pedidos**
```
db.Pedidos.insert([{"idepedido" : 100 , "cliente" : "Luis" , "fpedido" : "18/05/2024"}])
```

9. **Escriba el comando para mostrar todas las colecciones creadas hasta el momento**
```
show collections()
```


Eliminar una collection
```
db.NombreColeccion.drop()
```


10. **Proceda a eliminar la colección Productos**
```
db.Productos.drop()
```


Crear una coleccion:
```
db.createCollection("Clientes")
```


Insertar un documento (registro)
db.NombreColeccion.insertOne([{datos clave:valor}])

Insertar varios documentos
db.NombreColeccion.insertMany([{datos1 clave:valor}, ... , {datosn clave:valor}])



11. **Un documento en MongoDB es lo mismo que un registro en bases**
de datos. 

Primero creamos la coleccion Clientes:

```
db.createCollection("Clientes")
```

Para insertar varios registros, tomamos como ejemplo la tabla, el codigo es

```
db.Clientes.insertMany([
{"idcliente" : "C001", "nombre" : "RICK", "apellido" : "TAPIA", "edad" : 21}, 
{"idcliente" : "C002", "nombre" : "THALIA", "apellido" : "ARELLANO", "edad" : 22}, 
{"idcliente" : "C003", "nombre" : "ANTONIO", "apellido" : "QUINTANA", "edad" : 25}, 
{"idcliente" : "C004", "nombre" : "GUILLERMO", "apellido" : "SANCHEZ", "edad" : 39}, 
{"idcliente" : "C005", "nombre" : "JACKY", "apellido" : "SANCHEZ", "edad" : 43} 
])
```



pretty() nos da una visualización mas "estética" de los datos


12. **Obtener todos los documentos de la colección Clientes:**
```
db.Clientes.find().pretty()
```


Listar todos los documentos:
```
db.NombreColeccion.find()
```

Obtener el primer documento
```
db.NombreColeccion.findOne()
```


13. **Obtener el primero documento de la colección Clientes:**
```
db.Clientes.findOne()
```



14. **Recupere el documento que corresponde al cliente de código C002:**
```
db.Clientes.find({"idcliente" : "C002"}).pretty()
```


- $gt: greater than
- $gte: greater than or equal
- $lt: less than
- $lte: less than or equal
- $eq: equal
- $ne: not equal

15. *Recupere los documentos que corresponde a todos los clientes de edad mayor de 22:*
```
db.Clientes.find({"edad":{$gt:22}})
```

16. **Recupere los documentos que corresponden a todos los clientes de edad mayor o igual a 25**
```
db.Clientes.find({"edad":{$gte:25}})
```

17. **Recupere los documentos que corresponden a todos los clientes menores de 22 años**
```
db.Clientes.find({"edad":{$lt:22}})
```

18. **Recupere los documentos que corresponden a los clientes que no tengan 39 años**
```
db.Clientes.find({"edad" : {$ne:39}})
```

19. **Recupere los documentos que corresponden a los clientes de apellido SANCHEZ y edad 39 años**
```
db.Clientes.find({"edad" : {$eq:39}, "apellido" : "SANCHEZ"})
```
o también
```
db.Clientes.find({"edad" : 39, "apellido" : "SANCHEZ"})
```


20. **Recupere los dodumentos que corresponden a todos los clientes cuyo apellido es Sanchez o que tengan una edad de 25 años:**
```
db.Clientes.find({ $or:[ {"apellido" : "SANCHEZ"}, {"edad" : 25}]})
```


21. **Realice la búsqueda del quinto cliente mediante su clave *_id* y modifique su apellido por GARCIA:**
```
db.Clientes.update( {"_id":ObjectId("...")} , {$set:{"apellido":"GARCIA"}} )
```



En ObjectId("...") iria el ObjectId  del quinto cliente, por ejemplo:
```
db.Clientes.update( {"_id":ObjectId("6662545c2c1b282b4fa26a18")} , {$set:{"apellido":"GARCIA"}} )
```

El *ObjectId* se puede apreciar cuando usamos los comandos find() o find().pretty()

22. **Actualice al cliente que tiene 21 años modificando su nombre por STING:**
```
db.Clientes.update({"edad":21} , {$set:{"nombre":"STING"}})
```

Eliminar un documento:
```
db.NombreColeccion.remove(condicion)
```


23. **Elimine al cliente que tiene 25 años de edad**
```
db.Clientes.remove({"edad" : 25})
```

Sin embargo, este comando no es recomendable, se recomienda:
```
db.NombreColeccion.deleteMany(condicion)  // Si queremos eliminar muchos documentos
db.NombreColeccion.deleteOne(condicion)   // Si queremos solo eliminar uno, el primero
```

