

Hello everyone... um, well... today I'm going to talk about two super important classes from our Multiplayer Space Invaders project: the `ClientHandler` class and the `Cliente` (Client) class. These two classes are like... the backbone of our game's network communication, you know?

### ClientHandler Class

First, let's look at `ClientHandler`. This class runs on the server for each client that connects. It's kind of like... imagine the server is a waiter and each `ClientHandler` is like... one of its individual arms serving different tables

When a client connects, the server creates a new `ClientHandler` that runs in its own thread. This is super important because it allows the server to attend to multiple clients simultaneously without blocking. It's like if the waiter (of our previous example) could clone themselves to serve all tables at once.

The `ClientHandler` has these fundamental components:

1. **Socket and Streams**: The socket is like a direct phone line between the server and a specific client. The `ObjectInputStream` and `ObjectOutputStream` streams are what allow us to send and receive complete Java objects. This is great because we can send complex objects like the game state.
    
2. **run() Method**: This method contains the main loop that constantly listens to what the client sends. It's like having your ear pressed to the phone waiting for instructions. The first thing it does is send the client their ID, like saying "you are player 3." After that, it enters a loop where it waits to receive actions from the client.

**HASTA AQUI**

-------

3. **Message Processing**: When it receives a `MessageAction` (which can be MOVE_LEFT, SHOOT, etc.), it calls the `procesarAccionCliente` method of the main server. It's as if the waiter received an order and passed it to the kitchen.
    
4. **Disconnection Handling**: If it detects that the client has disconnected, it notifies the server to remove it from the player list. This is crucial to keep the game updated.


-----
**LEER ESTO TMB**

5. **sendGameState() Method**: This method sends the current game state to the client. The `outputStream.reset()` is important because it prevents ObjectOutputStream from caching previously sent objects, ensuring the client always receives the most recent state.

-----

An interesting detail is that we handle various exceptions like `SocketException`, `IOException`, and `ClassNotFoundException`. This makes our game robust even when there are network problems. For example, if a client abruptly closes their window, the server doesn't crash, it simply detects the disconnection and continues functioning for everyone else.








### Client Class

Moving on to the `Cliente` class, this is the one that runs on each player's computer. It has two major responsibilities: managing the graphical interface and communicating with the server.

The client structure includes:

1. **Network Components**: Similar to the `ClientHandler`, it has a socket and streams to communicate with the server. The difference is that here we initiate the connection.
    
2. **Graphical Interface**: We create a window with Java Swing that includes fields for the server IP and port, a button to connect/disconnect, and the `GamePanel` where the game is drawn.
    
3. **Movement Control**: We use a `KeyListener` to detect when the player presses keys. We have flags like `movingLeft` and `movingRight` that activate when you press the corresponding keys. Then a `Timer` continuously sends these actions to the server while the keys are pressed.


-----

**LEER ESTO IMPORTANTE**


4. **Server Connection**: The `toggleConnection()` method is interesting because it handles both connection and disconnection. When you connect, it creates a new thread to not block the interface while waiting for the server response.
    
5. **State Reception**: The `run()` method constantly receives game state updates from the server and updates the `GamePanel`. This design allows all players to see the same thing in real-time.


----


4. **Error Handling**: We implemented quite a bit of error handling, like when the server is unavailable or the connection is lost. In these cases, we show clear messages to the user.
    


-----

**LEER ESTO**

A cool feature we implemented is Ngrok, which allows us to play on different networks without having to configure firewalls or routers. We simply share the Ngrok URL and anyone can connect, even from outside our local network.


------

To wrap up, these two classes work together in perfect harmony: each action you perform on the client is sent to the server through your specific `ClientHandler`, the server updates the game state, and then sends the new state to all connected clients. It's like a constant conversation that allows all players to share the same gaming experience in real-time.

And that's it! Any questions?