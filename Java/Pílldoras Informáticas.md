
# Threads

`Thread.sleep` para que se pause el hilo en ejecución
```java
Thread.sleep(<tipo_long>) // En milisegundos
```


- [x] Programación de hilos ⏳ 2024-09-25 ✅ 2024-09-25
## Crear hilos de ejecución
1. Crear clase que implemente la interfaz `Runnable` (método `run()`)
2. Escribir el código de la tarea dentro del método `run`
3. Instanciar la clase creada y almacenar la instancia en una variable de tipo `Runnable`
4. Crear instancia de la clase `Thread` pasando como parámetro al constructor de `Thread` el objeto `Runnable` anterior.
5. Poner en marcha el hilo de ejecución con el método `start()` de la clase `Thread`


```java

class MatrixMultiplier implements Runnable {

	private final int[][] A, B, C;
	private final int row;

	public MatrixMult(int[][] A, int[][] B, int[][] C, int row) {
		this.A = A;
		this.B = B;
		this.C = C
		this.row = row
	}

	@Override
	public void run() {
		int colsB = B[0].length;
		int colsA = A[0].length;

		for(int j=0; j<colsB; j ++) {
			int sum = 0;
			for(int k = 0; k < colsA; k ++) {
				sum += A[row][k] * B[k][j];
			}
			C[row][j] = sum
		}
	}
}
```

```java
public class MatrixMultiplication {

	public static void main(String[] args) {
		int[][] A = {
			{1, 2, 3},
			{4, 5, 6},
			{7, 8, 9}
		};

		int[][] B = {
			{9, 8, 7},
			{6, 5, 4},
			{3, 2, 1}
		};

		int rowsA = A.length, colsB = B[0].length;
		int[][] C = new int[rowsA][colsB];

		Thread[] threads = new Thread[rowsA];

		for(int = 0; i < rowsA; i ++) {
			threads[i] = new Thread(new MatrixMultiplier(A, B, C, i));
			threads[i].start();
		}


		// Esperar a que todos los hilos terminen
		for (int i = 0; i < rowsA; i ++) {
			try {
				theads[i].join();
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}

		// Mostrar resultado 
		System.out.println("Resultado de la multiplicación:"); 
		for (int[] row : C) { 
			for (int value : row) { 
				System.out.print(value + " "); 
			} 
			System.out.println(); 
		}
	}
}

```


## Hilos e interrupciones
- [x] Interrupción de hilos ⏳ 2024-09-25 ✅ 2024-09-26

### Métodos de interrupción

- `interrupt()`: void, interrumpe el hilo en ejecución
- `isInterrupted()`: boolean, valida si este hilo ha sido interrumpido
- `interrupted()`: void, valida si el hilo actual ha sido interrumpido
- `stop()`: en desuso

### Otros métodos
 `currentThread`: Devuelve la referencia del hilo ejecutándose.


### Detener varios hilos
- [x] Interrupción de varios hilos ⏳ 2024-09-25 ✅ 2024-09-26



## Sincronización de Threads

- [x] Sincronización de Threads I ⏳ 2024-09-25 ✅ 2024-09-27
### Estado de los Threads
- **Nuevo**: cuando el hilo se ha instanciado
- **Ejecutable**: Cuando hemos llamado al método `start()`
- **Bloqueado**: cuando el hilo esta bloqueado, por ejemplo, al usar el método `slee()`
- **Muerto**: Cuando el hilo termina su tarea o cuando ocurre una excepción y no se captura

- [x] Sincronización de Threads II ⏳ 2024-09-25 ✅ 2024-09-27


- [x] Sincronización de Threads III ⏳ 2024-09-25 ✅ 2024-10-03
- [x] Sincronización de Threads IV ⏳ 2024-09-25 ✅ 2024-10-03
- [x] Sincronización de Threads VI ⏳ 2024-09-25 ✅ 2024-10-03
- [x] Sincronización de Threads VII ⏳ 2024-09-25 ✅ 2024-10-03

### Clase ReentrantLock
- [x] Sincronización de Threads VIII ⏳ 2024-09-25 ✅ 2024-10-03

La clase `ReentrantLock` en Java pertenece al paquete `java.util.concurrent.locks` y es una de las implementaciones más utilizadas para manejar la sincronización en entornos multihilo. A diferencia de los bloques `synchronized`, `ReentrantLock` ofrece más control y flexibilidad sobre los bloqueos.

### Características principales de `ReentrantLock`

| Característica                         | Descripción                                                                                                                                                          |
| -------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Reentrante**                         | Un hilo puede adquirir el mismo bloqueo varias veces sin bloquearse a sí mismo. Cada vez que el hilo adquiere el bloqueo, debe liberarlo el mismo número de veces.   |
| **Bloqueo explícito**                  | El bloqueo y la liberación del mismo se manejan manualmente mediante los métodos `lock()` y `unlock()`, lo que da más control sobre cuándo ocurre la sincronización. |
| **Opcionalmente justo**                | Puede configurarse como un bloqueo "justo", en el que los hilos obtienen el bloqueo en el orden en que lo solicitaron (FIFO).                                        |
| **Condiciones asociadas**              | Ofrece soporte para múltiples objetos `Condition`, lo que permite hacer que los hilos esperen y sean notificados en condiciones específicas.                         |
| **Interrupciones y tiempos de espera** | Soporta bloqueo interruptible (con `lockInterruptibly()`) y permite tiempos de espera al intentar adquirir el bloqueo (con `tryLock(long timeout, TimeUnit unit)`).  |

### Métodos principales de `ReentrantLock`

| Método                | Descripción                                           |
|-----------------------|-------------------------------------------------------|
| `lock()`              | Adquiere el bloqueo. Si el bloqueo está ocupado, el hilo actual se suspenderá hasta que lo obtenga. |
| `unlock()`            | Libera el bloqueo. Debe ser llamado tras cada llamada a `lock()` para evitar que otros hilos se queden bloqueados indefinidamente. |
| `tryLock()`           | Intenta adquirir el bloqueo sin bloquear al hilo. Si el bloqueo no está disponible, devuelve `false`. Si está disponible, lo adquiere y devuelve `true`. |
| `tryLock(long timeout, TimeUnit unit)` | Intenta adquirir el bloqueo dentro de un tiempo determinado. Si no lo consigue en ese periodo, devuelve `false`. |
| `lockInterruptibly()` | Adquiere el bloqueo, pero permite que el hilo sea interrumpido mientras espera, lanzando una `InterruptedException` si esto ocurre. |

### Ejemplo básico de uso:

```java
import java.util.concurrent.locks.ReentrantLock;

public class EjemploReentrantLock {
    private final ReentrantLock lock = new ReentrantLock();

    public void metodoCompartido() {
        lock.lock(); // Adquiere el bloqueo
        try {
            // Sección crítica
            System.out.println("Hilo " + Thread.currentThread().getName() + " está                  ejecutando la sección crítica.");
        } finally {
            lock.unlock(); // Asegura que el bloqueo se libera al final
        }
    }

    public static void main(String[] args) {
        EjemploReentrantLock ejemplo = new EjemploReentrantLock();
        
        Runnable tarea = () -> {
            for (int i = 0; i < 5; i++) {
                ejemplo.metodoCompartido();
            }
        };
        
        // Crear dos hilos que comparten el mismo recurso
        Thread hilo1 = new Thread(tarea, "Hilo-1");
        Thread hilo2 = new Thread(tarea, "Hilo-2");
        
        hilo1.start();
        hilo2.start();
    }
}
```

En este ejemplo:
- Dos hilos (`Hilo-1` y `Hilo-2`) intentan acceder a un método compartido. 
- La clase `ReentrantLock` garantiza que solo un hilo a la vez entre en la sección crítica. El método `unlock()` en el bloque `finally` asegura que el bloqueo siempre se libera, incluso si ocurre una excepción.

Esta clase es útil cuando necesitas mayor control sobre la sincronización que lo que ofrece `synchronized`.

- [ ] Threads IX. Sincronización de threads VI. Condiciones en bloqueos I ⏳ 2024-10-11 
- [ ] Threads X. Sincronización de threads VII.
- [ ] Threads XI. Sincronización de threads VIII


