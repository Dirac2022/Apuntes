La clase `Threading.Thread` es la forma más común de trabajar con hilos en Python.


## Constructores y argumentos

- **`group`:** No se utiliza actualmente; siempre es `None`.
    
- **`target`:** La función que se ejecutará en el hilo. Debe ser invocable.
    
- **`name`:** Un nombre para el hilo. Si no se proporciona, Python asigna un nombre automáticamente.
    
- **`args`:** Argumentos posicionales para la función `target`.
    
- **`kwargs`:** Argumentos clave-valor para la función `target`.
    
- **`daemon`:** Indica si el hilo debe ejecutarse como un hilo daemon (en segundo plano).

## Métodos

### `start()`
Inicia la ejecución del hilo. La función `target` se ejecuta en un nuevo hilo.

### `run()`
Este método contiene la lógica del hilo. Si se sobrescribe en una subclase, se debe llamar a `Thread.run()` para asegurar que se ejecuten las tareas de inicialización del hilo.

### `join(timeout=None)`
Bloquea el hilo actual hasta que el hilo al que se llama `join()` termine. Si se proporciona un `timeout`, el bloqueo se limita a ese tiempo.

### `is_alive()`
Devuelve `True` si el hilo está activo, `False` de lo contrario.

### `isDaemon()`
Devuelve `True` si el hilo es un hilo daemon, `False` de lo contrario.

### `setDaemon(daemonic)`
Establece si el hilo debe ejecutarse como un hilo daemon.

### `getName()`
Devuelve el nombre del hilo.

### `setName(name)`
Establece el nombre del hilo.