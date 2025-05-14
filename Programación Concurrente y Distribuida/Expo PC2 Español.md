

## Versión en Español

Hola a todos... eh, bueno... hoy les voy a hablar sobre dos clases súper importantes de nuestro proyecto Space Invaders Multijugador: la clase `ClientHandler` y la clase `Cliente`. Estas dos clases son como... la columna vertebral de la comunicación en red de nuestro juego, ¿saben?

### Clase ClientHandler

Primero vamos con `ClientHandler`. Esta clase es la que se ejecuta en el servidor para cada cliente que se conecta. Como que, imaginen que el servidor es como un camarero y cada `ClientHandler` es como... sus brazos individuales atendiendo a diferentes mesas, ¿me explico?

Cuando un cliente se conecta, el servidor crea un nuevo `ClientHandler` que se ejecuta en su propio hilo. Esto es súper importante porque permite que el servidor atienda a varios clientes al mismo tiempo sin bloquearse. Es como si el camarero pudiera clonarse para atender todas las mesas a la vez.

El `ClientHandler` tiene estos componentes fundamentales:

1. **Socket y Streams**: El socket es como el teléfono directo entre el servidor y ese cliente específico. Los streams `ObjectInputStream` y `ObjectOutputStream` son los que permiten enviar y recibir objetos Java completos. Esto es genial porque podemos enviar objetos complejos como el estado del juego.
    
2. **Método run()**: Este método contiene el bucle principal que escucha constantemente lo que el cliente envía. Es como tener el oído pegado al teléfono esperando instrucciones. Lo primero que hace es enviar al cliente su ID, como diciéndole "tú eres el jugador 3". Después, entra en un bucle donde espera recibir acciones del cliente.
    
3. **Procesamiento de Mensajes**: Cuando recibe un `MessageAction` (que puede ser MOVE_LEFT, SHOOT, etc.), llama al método `procesarAccionCliente` del servidor principal. Es como si el camarero recibiera un pedido y lo pasara a la cocina.
    
4. **Manejo de Desconexiones**: Si detecta que el cliente se ha desconectado, notifica al servidor para que lo elimine de la lista de jugadores. Esto es crucial para mantener el juego actualizado.
    
5. **Método sendGameState()**: Este método envía el estado actual del juego al cliente. Es importante el `outputStream.reset()` porque evita que ObjectOutputStream cachee objetos enviados previamente, asegurando que el cliente siempre reciba el estado más reciente.
    

Un detalle interesante es que manejamos varias excepciones como `SocketException`, `IOException`, y `ClassNotFoundException`. Esto hace que nuestro juego sea robusto incluso cuando hay problemas de red. Por ejemplo, si un cliente cierra bruscamente su ventana, el servidor no se cae, simplemente detecta la desconexión y sigue funcionando para los demás.

### Clase Cliente

Pasando a la clase `Cliente`, esta es la que se ejecuta en la computadora de cada jugador. Tiene dos grandes responsabilidades: manejar la interfaz gráfica y comunicarse con el servidor.

La estructura del cliente incluye:

1. **Componentes de Red**: Similar al `ClientHandler`, tiene un socket y streams para comunicarse con el servidor. La diferencia es que aquí iniciamos la conexión.
    
2. **Interfaz Gráfica**: Creamos una ventana con Java Swing que incluye campos para la IP y puerto del servidor, un botón para conectar/desconectar, y el `GamePanel` donde se dibuja el juego.
    
3. **Control de Movimiento**: Usamos un `KeyListener` para detectar cuando el jugador presiona teclas. Tenemos banderas como `movingLeft` y `movingRight` que se activan cuando presionas las teclas correspondientes. Luego un `Timer` envía estas acciones continuamente al servidor mientras las teclas están presionadas.
    
4. **Conexión al Servidor**: El método `toggleConnection()` es interesante porque maneja tanto la conexión como la desconexión. Cuando te conectas, crea un nuevo hilo para no bloquear la interfaz mientras espera la respuesta del servidor.
    
5. **Recepción de Estado**: El método `run()` recibe constantemente actualizaciones del estado del juego desde el servidor y actualiza el `GamePanel`. Este diseño permite que todos los jugadores vean lo mismo en tiempo real.
    
6. **Manejo de Errores**: Implementamos bastante manejo de errores, como cuando el servidor no está disponible o la conexión se pierde. En estos casos, mostramos mensajes claros al usuario.
    

Una característica chévere que implementamos es Ngrok, lo que nos permite jugar en diferentes redes sin tener que configurar firewalls o routers. Simplemente compartimos la URL de Ngrok y cualquiera puede conectarse, incluso desde fuera de nuestra red local.

Para finalizar, estas dos clases trabajan juntas en perfecta armonía: cada acción que realizas en el cliente se envía al servidor a través de tu `ClientHandler` específico, el servidor actualiza el estado del juego, y luego envía el nuevo estado a todos los clientes conectados. Es como una conversación constante que permite que todos los jugadores compartan la misma experiencia de juego en tiempo real.

¡Y eso es todo! ¿Alguna pregunta?

