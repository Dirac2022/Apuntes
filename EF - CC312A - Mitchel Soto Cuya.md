
1. [8.0 ptos.] Desarrollar 3 APIs y desplegarlas de manera local, similar al laboratorio de APIs, realizado en clase con Python y Flask. 
	1. La primera API consistirá en una API de Registro, a la cual se le enviará en una solicitud POST un campo denominado usuario que contendría una cadena de texto el cual servirá de cuenta o identificador, esta API recibirá la solicitud y guardará el usuario en una base de datos, archivo de texto o similar.
	2. La segunda API será de Autenticación, también recibirá una solicitud POST, en la que se incluirá el usuario, la API recibirá el texto y lo buscará dentro del archivo de información generado en el registro, si el usuario ya se encuentra guardado retornará su aprobación con un “Ok” caso contrario retornará “Usuario no Registrado”.

Primero procedí a instalar tinydb
![[Pasted image 20241214120234.png]]



## Para la primera api:

- Importo los módulos necesario, el documento indico usar `Flask` y recomendó usar `tinydb`
- Defino la base de datos que almacenara los usuarios para la posterior autenticación.
```python
from flask import Flask, jsonify, request
from tinydb import TinyDB, Query

app = Flask(__name__)

# Database para los usuarios
db = TinyDB('usuarios.json')
```


### Endpoint registrar

- Agrego validaciones para requerir campos no vacíos
- Agrego el usuario a la db 
```python
# Endpoint para el registro
@app.route('/registrar', methods=['POST'])
def registra_usuario():

    data = request.get_json()
    usuario = data.get('cliente')

    # Solo agrego una validación para que el campo usuario
    # no este vacio, ya que no se indica en el examen otra validacion
    if not usuario:
        return jsonify({'error': 'El campo "cliente" es requerido'}), 400
    User = Query()

    db.insert({'cliente': usuario})

    return jsonify({'mensaje': 'Cliente registrado exitosamente'}), 201
```

## Para la segunda api

```python
# Endpoint para la autenticacion
@app.route('/autenticar', methods=['POST'])
def autenticar_usuario():
    data = request.get_json()
    usuario = data.get('cliente')

    if not usuario:
        return jsonify({'error': 'El campo "usuario" es requerido'}), 400

    # Buscar el usuario en la base de datos
    User = Query()
    result = db.search(User.cliente == usuario)

    if result:
        return jsonify({'mensaje': 'Ok'}), 200
    else:
        return jsonify({'error': 'Usuario no Registrado'}), 401
```
Ejecute app1.py para validar el funcionamiento

![[Pasted image 20241214121010.png]]

## Para la tercera api

```python
# Database para los mensajes
db_mensajes = TinyDB('mensajes.json')

# Endpoint para escribir un mensaje
@app.route('/escribir', methods=['POST'])
def escribir_mensaje():
    data = request.get_json()
    usuario = data.get('cliente')
    mensaje = data.get('mensaje')

    # Agrego una validacion simple por si acaso
    if not usuario or not mensaje:
        return jsonify({'error': 'Los campos "usuario" y "mensaje" son requeridos'}), 400

    #if not autenticar_usuario(usuario):
    #    return jsonify({'error': 'Usuario no autorizado'}), 401

    db_mensajes.insert({'cliente': usuario, 'mensaje': mensaje})

    return jsonify({'mensaje': 'Mensaje registrado exitosamente'}), 201

# Endpoint para leer los mensajes de un usuario
@app.route('/leerTodo', methods=['GET'])
def leer_mensajes():
    data = request.get_json()
    usuario = data.get('cliente')

    if not usuario:
        return jsonify({'error': 'El campo "usuario" es requerido'}), 400

    #if not autenticar_usuario(usuario):
        #return jsonify({'error': 'Usuario no autorizado'}), 401
     #   return jsonify({'error': 'Mensaje de ${usuario} no se guarda ya que el usuario nunca se registro'}), 401

    usuario = data.get('usuario')
    if not usuario:
        return jsonify({'error': 'Mensaje de usuario no se guarda ya que el usuario nunca se registro'}), 401
    Mensaje = Query()
    # Obtengo la lista de mensajes correspondientes al 'usuario'
    mensajes = db_mensajes.search(Mensaje.cliente == usuario)
    # total_mensajes = len(mensajes)

    #return jsonify({'total_mensajes': total_mensajes}), 200
    return jsonify({'mensajes': [mensaje['mensaje'] for mensaje in mensajes]}), 200

if __name__ == '__main__':
    app.run(debug=True)
```


**Codigo completo**
```python
# La primera API consistirá en una API de Registro, a la cual se le enviará en una solicitud POST un 
# campo denominado usuario que contendría una cadena de texto el cual servirá de cuenta o 
# identificador, esta API recibirá la solicitud y guardará el usuario en una base de datos, archivo de 
# texto o similar.

from flask import Flask, jsonify, request
from tinydb import TinyDB, Query

app = Flask(__name__)

# Database para los usuarios
db = TinyDB('usuarios.json')

# Endpoint para el registro
@app.route('/registrar', methods=['POST'])
def registra_usuario():

    data = request.get_json()
    usuario = data.get('cliente')

    # Solo agrego una validación para que el campo usuario
    # no este vacio, ya que no se indica en el examen otra validacion
    if not usuario:
        return jsonify({'error': 'El campo "cliente" es requerido'}), 400
    User = Query()


    db.insert({'cliente': usuario})

    return jsonify({'mensaje': 'Cliente registrado exitosamente'}), 201

# La segunda API será de Autenticación, también recibirá una solicitud POST, en la que se incluirá 
# el usuario, la API recibirá el texto y lo buscará dentro del archivo de información generado en el 
# registro, si el usuario ya se encuentra guardado retornará su aprobación con un “Ok” caso contrario 
# retornará “Usuario no Registrado”. 

# Endpoint para la autenticacion
@app.route('/autenticar', methods=['POST'])
def autenticar_usuario():
    data = request.get_json()
    usuario = data.get('cliente')

    if not usuario:
        return jsonify({'error': 'El campo "usuario" es requerido'}), 400

    # Buscar el usuario en la base de datos
    User = Query()
    result = db.search(User.cliente == usuario)

    if result:
        return jsonify({'mensaje': 'Ok'}), 200
    else:
        return jsonify({'error': 'Usuario no Registrado'}), 401



# La tercera API será similar a un buzón o registro de mensajes y tendrá dos endpoints, el primer 
# endpoint será uno de escritura, recibirá dos atributos el usuario junto con un mensaje, y así mismo 
# guardará ambos en una base de datos o similar, el segundo endpoint será de lectura también 
# necesitará recibir el nombre de usuario que leerá los mensajes y retornará al cliente que realizó la 
# solicitud el total de mensajes registrados, siempre tomando en cuenta para ambos endpoints, que el 
# usuario que realice la solicitud se encuentre registrado, llamando internamente a la API de 
# Autenticación. 

# Database para los mensajes
db_mensajes = TinyDB('mensajes.json')

# Endpoint para escribir un mensaje
@app.route('/escribir', methods=['POST'])
def escribir_mensaje():
    data = request.get_json()
    usuario = data.get('cliente')
    mensaje = data.get('mensaje')

    # Agrego una validacion simple por si acaso
    if not usuario or not mensaje:
        return jsonify({'error': 'Los campos "usuario" y "mensaje" son requeridos'}), 400

    #if not autenticar_usuario(usuario):
    #    return jsonify({'error': 'Usuario no autorizado'}), 401

    db_mensajes.insert({'cliente': usuario, 'mensaje': mensaje})

    return jsonify({'mensaje': 'Mensaje registrado exitosamente'}), 201

# Endpoint para leer los mensajes de un usuario
@app.route('/leerTodo', methods=['GET'])
def leer_mensajes():
    data = request.get_json()
    usuario = data.get('cliente')

    if not usuario:
        return jsonify({'error': 'El campo "usuario" es requerido'}), 400

    #if not autenticar_usuario(usuario):
        #return jsonify({'error': 'Usuario no autorizado'}), 401
     #   return jsonify({'error': 'Mensaje de ${usuario} no se guarda ya que el usuario nunca se registro'}), 401

    usuario = data.get('usuario')
    if not usuario:
        return jsonify({'error': 'Mensaje de usuario no se guarda ya que el usuario nunca se registro'}), 401
    Mensaje = Query()
    # Obtengo la lista de mensajes correspondientes al 'usuario'
    mensajes = db_mensajes.search(Mensaje.cliente == usuario)
    # total_mensajes = len(mensajes)

    #return jsonify({'total_mensajes': total_mensajes}), 200
    return jsonify({'mensajes': [mensaje['mensaje'] for mensaje in mensajes]}), 200

if __name__ == '__main__':
    app.run(debug=True)


```

**Para los ejemplos de ejecución**

Registrar usuario:
![[Pasted image 20241214124344.png]]

Autenticar usuario registrado:
![[Pasted image 20241214124448.png]]


Autenticar usuario no registrado:

![[Pasted image 20241214123149.png]]

Registrar usuario ``"fc"``
![[Pasted image 20241214130912.png]]


Escribir mensajes para usuario ``"uni"``
![[Pasted image 20241214130854.png]]

![[Pasted image 20241214130959.png]]

Escribir mensajes para usuario ``"fc"``
![[Pasted image 20241214131024.png]]

Escribir mensajes para usuario ``"faua"``



Leer mensajes de usuario ``"uni"``
![[Pasted image 20241214131723.png]]


Leer mensajes de usuario ``"faua"``
![[Pasted image 20241214131936.png]]
