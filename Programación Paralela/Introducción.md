
# Introducción a la Programación Paralela
Permite realizar múltiples tareas al mismo tiempo, dividiendo un problema en subproblemas que pueden resolverse de manera independiente y en paralelo.

>[!info] Util cuando queremos aprovechar la potencia de procesadores multinúcleo o distribuimos una tarea entre varios sistemas

En Java, la programación paralela se puede lograr utilizando hilos `Threads` o ejecutores `Executors`. Los hilos son las unidades más básicas de ejecución, mientras que los ejecutores son una abstracción que facilita el manejo de múltiples hilos.


## Conceptos clave

### Hilo (Thread)
Unidad básica de ejecución en paralelo. Cada hilo tiene su propia pila de ejecución y pueden correr de manera independiente.

### Runnable
Interfaz funcional que permite definir una tarea que se ejecutará en un hilo.

### ExecutorService
Framework que facilita la gestión de hilos. Permite manejar pools de hilos, programar tareas y controlar la finalización de hilos.

### Synchronized
Palabra clave que asegura que solo un hilo pueda acceder a una sección crítica del código al mismo tiempo.

### Race Condition
Situación en la que múltiples hilos acceden a un recurso compartido al mismo tiempo, generando resultados inesperados.

### Deadlock
Situación en la que dos o más hilos se bloquean mutuamente al esperar recursos, lo que impide que alguno termine su tarea.

