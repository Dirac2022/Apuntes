
# Concurrencia
Los usuarios de computadores toma por hecho que su sistema puede realizar más de una tarea a la vez, asumen que pueden seguir trabajando en un procesador de texto mientras otras aplicaciones descargan archivos, manejan la cola de impresión y el stream de audio. Incluso se suele esperar que una sola aplicación pueda hacer más de una cosa a la vez, por ejemplo, un procesador de texto debería estar listo para responder a eventos de mouse y teclado sin importar lo ocupado que este modificando el texto o actualizando la pantalla.

Un software que sea capaz de realizar estas cosas es conocido como **software concurrente**

# Hilos y Procesos
En la programación concurrente hay dos unidades básicas de ejecución: hilos y procesos


>[!tip] Proceso
>Los procesos tienen un entorno de ejecución autónomo. Un proceso generalmente tiene un conjunto completo y privado de recursos; en particular, cada proceso tiene su propio espacio de memoria.


>Es una instancia en ejecución de un programa con su propio espacio de memoria y recursos. Los procesos son independientes entre sí y se comunican mediante mecanismos como **IPC**.

>[!tip] Hilo
>Es la unidad más pequeña de ejecución dentro de un proceso. Los hilos comparten la memoria y recursos del proceso al que pertenecen, lo que facilita la comunicación pero también introduce riesgos de concurrencia.

## Procesos
Los procesos tienen un entorno de ejecución autónomo. Un proceso generalmente tiene un conjunto completo y privado de recursos; en particular, cada proceso tiene su propio espacio de memoria.

Para facilitar la comunicación entre procesos, la mayoría de sistemas operativos admite el uso de recursos de comunicación entre procesos (**IPC**) como pipes o sockets. Los IPC permiten además la comunicación de procesos entre diferentes sistemas.

>[!tip] Inter-Process-Communication
>Son un conjunto de mecanismos que permiten a los procesos en un sistema operativo compartir información y coordinar su ejecución.
>- Shared Memory
>	- Los procesos comparten una región de memoria y sincronizan el acceso mediante mecanismos como **semáforos** y **mutex**
>- Pipes (Anonymous and Named Pipes - FIFOs)
>	- Pipes anónimos: Comunicación unidireccional entre procesos relacionados (padre-hijo)
>	- Named Pipes (FIFOs): Comunicación entre procesos no relacionados.
>- Message Queues
>	- Permiten el envío de bloques de datos estructurados entre procesos.
>	- Persisten incluso si el proceso receptor aún no los ha leído
>	- Ejemplo en C: `msgget()`, `msgsnd()`, `msgrcv()`, `msgctl()`.
>- Sockets
>	- Permiten la comunicación entre procesos en diferentes máquinas o dentro de la misma máquina.
>	- Se usan en programación de redes (`TCP/IP`, `UDP`).
>	- Ejemplo en C: `socket()`, `bind()`, `listen()`, `accept()`, `connect()`.
## Hilos
Los hilos también son llamados **procesos ligeros**. Tanto los procesos como los hilos proporcionan un entorno de ejecución, pero crear un nuevo hilo requiere menos recursos que crear un nuevo proceso.

Los hilos existen dentro de un proceso (cada proceso tiene al menos un hilo). Los hilos comparten los recursos del proceso, incluyendo memoria y los archivos abiertos. Esto permite una comunicación eficiente, pero potencialmente problemática.

Desde el punto de vista de un programador de aplicaciones, empezamos con un único hilo conocido como el **main thread**. Este hilo tiene la capacidad de crear hilos adicionales.


# Objetos Thread

## Thread
- Un thread o hilo de ejecución es la ejecución secuencial de una serie de instrucciones dentro de un programa.
- De forma simple se puede pensar que los threads son procesos ejecutados por un programa.
- La mayoría de lenguajes de programación son single threaded.
- El desarrollo del hardware ha llevado el concepto de thread a la CPU: **multinúcleo**.


![[ejemplo thread.png]]

## Multi-threading en la plataforma Java
- Cada aplicación tiene un thread, llamado el thread principal. Este thread tiene la habilidad de crear threads adicionales.
- La programación multi-thread es más compleja:
	- acceso compartido de objetos.
	- riesgo de condición de carrera.


## Estados de un Thread

- **Running**
	- En curso de ejecución.
	- En control de la CPU.
- **Runnable** (Ready to run)
	- Puede ejecutarse pero no se le ha dado la orden.
- **Resumed**
	- Ready to run después de haber estado suspendido o bloqueado.
- **Suspended**
	- Voluntariamente permite que otros threads se ejecuten.
- **Blocked**
	- Esperando por algún recurso o que ocurra un evento.



![](https://codexplo.wordpress.com/wp-content/uploads/2012/10/thread-state-diagram.png)

---
La imagen muestra los diferentes estados por los que puede pasar un hilo a lo largo de su existencia:

1. **Runnable (Ejecutable):**
    - Este es el estado inicial de un hilo después de que se ha creado y se ha llamado al método `start()`.
    - Un hilo en este estado está listo para ser ejecutado por el planificador (scheduler) del sistema operativo.
    - Es importante notar que "Runnable" no significa que el hilo se esté ejecutando _activamente_ en ese momento, sino que está _disponible_ para serlo.
2. **Running (Ejecutando):**
    - Este es el estado en el que el hilo está actualmente ejecutando sus instrucciones.
    - El planificador del sistema operativo es el que decide qué hilo pasa de "Runnable" a "Running".
    - Un hilo puede permanecer en este estado hasta que:
        - Complete su tarea (pase a "Dead").
        - Ceda el control al planificador (pase a "Runnable" mediante `Thread.yield()`).
        - Se bloquee esperando un recurso (pase a "Blocked I/O Synchronized").
        - Se ponga en espera (pase a "Waiting" mediante `Object.wait()`).
        - Se ponga a dormir (pase a "Sleeping" mediante `Thread.sleep()`).
3. **Sleeping (Durmiendo):**
    - Un hilo entra en este estado cuando se llama al método `Thread.sleep()`.
    - Durante el tiempo especificado en `sleep()`, el hilo no ejecuta ninguna instrucción y no compite por recursos del CPU.
    - Una vez que transcurre el tiempo de espera, el hilo vuelve al estado "Runnable".
4. **Waiting (Esperando):**
    - Un hilo entra en este estado cuando llama al método `Object.wait()`.
    - Este método se utiliza para sincronizar hilos, permitiendo que un hilo espere a que otro hilo le notifique de un evento.
    - Un hilo en "Waiting" solo puede volver a "Runnable" cuando otro hilo llama a `Object.notify()` o `Object.notifyAll()` para despertarlo.
5. **Blocked I/O Synchronized (Bloqueado E/S Sincronizado):**
    - Un hilo entra en este estado cuando está esperando a que se complete una operación de entrada/salida (I/O) o cuando está intentando acceder a una sección de código sincronizada que está siendo utilizada por otro hilo.
    - Por ejemplo, un hilo puede bloquearse al intentar leer datos de un archivo o al esperar a que lleguen datos a través de una conexión de red.
    - También puede ser que un hilo este intentando entrar a un bloque de código sincronizado, cuando otro hilo ya se encuentra dentro de este.
    - Una vez que la operación de I/O se completa o se libera el bloqueo de la sección sincronizada, el hilo vuelve al estado "Runnable".
6. **Dead (Muerto/Finalizado):**
    - Un hilo entra en este estado cuando su método `run()` ha terminado de ejecutarse.
    - Una vez que un hilo está en este estado, no puede volver a ejecutarse.

**Transiciones entre Estados:**

La imagen también muestra las transiciones entre los diferentes estados, indicando qué eventos o métodos provocan cada transición:

- **`start()`:** Inicia la ejecución de un hilo, llevándolo de un estado inicial (no mostrado) a "Runnable".
- **`Thread.sleep()`:** Pone un hilo en estado "Sleeping".
- **`Object.wait()`:** Pone un hilo en estado "Waiting".
- **`Object.notify()` / `Object.notifyAll()`:** Despiertan a un hilo que está en estado "Waiting", llevándolo a "Runnable".
- **Scheduler swap (Cambio de planificador):** El planificador del sistema operativo puede cambiar el hilo que se está ejecutando, llevando un hilo de "Running" a "Runnable".
- **`Thread.yield()`:** Un hilo cede voluntariamente el control al planificador, pasando de "Running" a "Runnable".
- **Done (Hecho):** Indica que el hilo ha completado su ejecución y pasa a "Dead".
- **Data / sync received (Datos/sincronización recibidos):** Indica que una operación de I/O se ha completado o que se ha liberado un bloqueo de sincronización, llevando un hilo de "Blocked I/O Synchronized" a "Runnable".
- **Another Thread closed socket (Otro hilo cerró el socket):** Indica que otro hilo cerro el socket, ocacionando que el hilo pase a estado "Dead".

**Conceptos Clave:**

- **Planificador (Scheduler):** El componente del sistema operativo que decide qué hilo se ejecuta en cada momento.
- **Sincronización:** El proceso de coordinar la ejecución de múltiples hilos para evitar condiciones de carrera y otros problemas de concurrencia.
- **Entrada/Salida (I/O):** Operaciones que implican la transferencia de datos entre la memoria del ordenador y dispositivos externos, como discos, redes o periféricos.
---

## Prioridades de un Thread

- Las prioridades determinan que thread recibe el control de la CPU y consiga ser ejecutado primero.
- En Java viene definidas por un valor entero de 1 a 10.
- A mayor valor de prioridad, mayor la oportunidad de ser ejecutado.
- Si dos threads tienen la misma prioridad, la ejecución depende del sistema operativo.


## Creación de hilos

Cada hilo en Java se encuentra asociado con una instancia de la clase Thread. Hay 2 formas de definir e iniciar un hilo.

1. Proporcionar un objeto `Runnable`. La interfaz `Runnable` define un único método, `run`, el cual debe contener el código a ejecutarse en el hilo.


```java
public class HelloRunnable implements Runnable {

	public void run() {
		System.out.println("Hello from a thread");
	}

	public static void main(String args[]) {
		new Thread(new HelloRunnable())).start();
	}
}

```

2. Crear una subclase de `Thread`. La clase `Thread` implementa por sí mismo la interfaz `Runnable`, aunque su método `run` no hace nada.

```java
public class HelloThread extends Thread {

	public void run() {
		System.out.println("Hello from a thread");
	}

	public static void main(String args[]) {
		(new HelloThread()).start();
	}
}
```

### Observaciones
- Ambas formas requieren invocar el método `Thread.start()` para iniciar el nuevo hilo.
- Notemos que al usar el método de la interfaz `Runnable` es necesario crear una instancia de la clase `Thread` entregando un objeto `Runnable` creado como argumento.
- El uso de `Runnable` es más general pues podemos crear una subclase de cualquier clase que no sea `Thread`.
- Hacer uso de la segunda forma nos facilita el trabajo en aplicaciones simples, pero nos limita a tener que usar una clase descendiente de la clase `Thread`.


## `Thread.currentThread()`

`Thread.currentThread()` es un método estático que retorno una referencia al objeto `Thread` ejecutándose actualmente.


```java

public class ThreadDemo implements Runnable {
	ThreadDemo() {
		// main thread
		Thread currThread = Thread.currentThread();
		Thread t = new Thread(this, "Admin Thread");
		System.out.println("current thread = " + currentThread);
		System.out.println("thread created = " + t);
		t.start();
	}

	public void run() {
		System.out.println("This is run() method");
	}

	public static void main(String args[]) {
		new ThreadDemo();
	}
}

```


## `Thread.sleep()`

`Thread.sleep()` provoca que el hilo actual suspenda su ejecución por un periodo de tiempo especificado.

```java
public class SleepMessages {
	
	public static void main(String args[]) throws InterruptedException {
		String importantInfo[] = {
			"Mares eat oats",
			"Does eat oats",
			"Little lambs eat ivy"
		};

		for(int i=0; i<importantInfo.length; i++) {
			// Pause for 4 seconds
			Thread.sleep(4000);
			System.out.println(importantInfo[i])
		}
	}
}
```


- No se garantizan que los tiempos de descanso sean precisos debido a que están limitados por las facilidades proporcionadas por el sistema operativo subyacente.
- El periodo de descanso puede ser detenido por interrupciones, no se puede asumir que invocar `sleep` suspenda el hilo exactamente por el periodo de tiempo indicado.
- En el ejemplo anterior se declara que `main` pueda arrojar (`throw`), una `InterruptedException`. Esta excepción es lanzada cuando algún otro hilo interrumpe el hilo actual mientras `sleep` está activo.


# Interrupciones

- Una **interrupción** es una indicación a un hilo de que debe detenerse y hacer algo más.
- Un hilo envía una interrupción invocando el método `interrupt()` sobre el objeto Thread para que el hilo sea interrumpido. Para que el mecanismo de interrupción funcione correctamente, el hilo a interrumpir debe ser capaz de manejar su propia interrupción.
- Es decisión del programador el qué hace exactamente un hilo para responder ante una interrupción, pero es bastante común que el hilo termine.

## Manejando Interrupciones
La forma de manejar las interrupciones depende de qué este haciendo el hilo en el momento. Si el hilo invoca métodos que arrojen `InterruptedException` con frecuencia, se suele simplemente retornar del método `run` luego de atrapar una excepción.

```java
for(int i=0; i < importantInfo.length; i ++) {
	// Pause for 4 seconds
	try {
		Thread.sleep(4000);
	} catch (InterruptedException e) {
		// We've been interrupted: no more messages
		return;
	}
	// Print a message
	System.out.println(importantInfo[i]);
}
```


## `Thread.interrupted()`
Si un hilo se ejecuta sin utilizar métodos que arrojen interrupciones, se puede hacer invocar periódicamente `Thread.interrupted()`, el cual retorna `true` si se ha recibido una interrupción.

```java
for(int i = 0; i < inputs.lenght; i ++) {
	heavyCrunch(inputs[i]);
	if(Thread.interrupted()) {
		// We've benn interrupted: no more crunching
		return;
	}
}
```

En aplicaciones más complejas, tiene más sentido arrojar un `InterruptedException` al detectar una interrupción.

```java
if(Thread.interrupted()) {
	throw new InterruptedException();
}
```


# La Bandera Interrupt Status

- El mecanismo de interrupción es implementado haciendo uso de una bandera interna conocida como `Interrupt Status`.
- Invocar `Thread.interrupt()` establece esta bandera.
- Cuando un hilo verifica por una interrupción haciendo uso del método estático `Thread.interrupted()`, la bandera es limpiada.
- El método no estático `isInterrupted()`, usado por un hilo para verificar el estado de otro, no modifica la bandera.
- Por convención, cualquier método que termine lanzando una `InterruptedException` limpia el **Interrupt Status** al hacerlo.


# Join
El método `join()` permite a un hilo esperar por la terminación de otro. Si `t` es un objeto `Thread` cuyo hilo se encuentra actualmente en ejecución, `t.join()` ocasiona que el hilo actual pause su ejecución hasta que el hilo de `t` termine.

- El uso adecuado de `join()` permite al programador especificar un periodo de espera.
- Al igual que `sleep()`, `join()` responde a una interrupción saliendo con un `Interrupted Exception`.


# Prioridad de hilos
Cada hilo cuenta con una prioridad representada por un número entre 1 y 10. Por lo general los hilos se programan acorde a su prioridad, sin embargo, ello no es garantizado debido a que depende de las especificaciones del **JVM** y cómo decida programar los hilos.

Se cuentan con 3 constantes en la clase Thread:
- `MIN_PRIORITY : 1`
- `NORM_PRIORITY : 5`
- `MAX_PRIORITY : 10`

La prioridad por defecto de un hilo es 5 (`NORM_PRIORITY`).

Para establecer la prioridad de un hilo u obtener la prioridad actual, se puede hacer uso de los métodos `setPriority()` y `getPriority()` respectivamente como se muestra a continuación.

```java
public class TestDaemonThread1 extends Thread {

    public TestDaemonThread1(String name) {
        super(name);
    }

    @Override
    public void run() {
        if(Thread.currentThread().isDaemon())
        {
            System.out.println("\ndaemon thread work, " + this.getName());
        }
        else
        {
            System.out.println("\nuser thread work" + this.getName());
        }
    }

    public static void main(String[] args) {
        
        TestDaemonThread1 t1 = new TestDaemonThread1("Hilo 1"); // creating thread
        TestDaemonThread1 t2 = new TestDaemonThread1("Hilo 2");
        TestDaemonThread1 t3 = new TestDaemonThread1("Hilo 3");

        t1.setDaemon(true); // now t1 is daemon thread
        t1.start();
        t2.start();
        t3.start();
    }

}
```

# Daemon Thread

- Un **Daemon Thread** en Java es un hilo de baja prioridad que proporciona servicios a los hilos de usuario.
- Cuando todos los hilos de usuario terminan, el JVM termina los daemon thread automáticamente.
- Un ejemplo de daemon thread es el garbage collector.

**Métodos**
- `public void setDaemon(boolean status)` : marca el hilo sobre el que se usa como daemon thread o user thread.
- `public boolean isDaemon()` : verifica si el hilo es un daemon thread.

```java
public class TestDaemonThread1 extends Thread {

    @Override
    public void run() {
        if(Thread.currentThread().isDaemon())
        {
            System.out.println("daemon thread work");
        }
        else
        {
            System.out.println("user thread work");
        }
    }

    public static void main(String[] args) {
        
        TestDaemonThread1 t1 = new TestDaemonThread1(); // creating thread
        TestDaemonThread1 t2 = new TestDaemonThread1();
        TestDaemonThread1 t3 = new TestDaemonThread1();

        t1.setDaemon(true); // now t1 is daemon thread
        t1.start();
        t2.start();
        t3.start();
    }

}
```

Si se quiere establecer un user thread como daemon, este no debe haberse iniciado o de lo contrario arrojará un `IllegalThreadStateException`.