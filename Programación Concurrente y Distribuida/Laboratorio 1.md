

```java
package Lab01.sistemaEcuaciones;

// Represent a pool of threads
import java.util.concurrent.ExecutorService;

// Provides static methods to create various kinds of ExecutorService
// implementations
import java.util.concurrent.Executors;

// Represents the result of an asynchronous computation
// A method where tasks can be initiated and run independently without waiting for other task to complete.
import java.util.concurrent.Future;

public class SolveParallel implements Runnable {

    double[][] A;
    double[] x;
    double[] x_next;
    double[] b;
    int i;


	// Here we capture the references to the shared arrays and the specific row index
    public SolveParallel(double[][] A, double[] b, double[] x, double[] x_next, int i) {

	
        this.A = A; // coeficient matrix
        this.x = x; // current aproximation to vector solution x
        this.x_next = x_next; // next aproximation
        this.b = b; // vector b
        this.i = i; // the row index that will update
    }

    @Override
    public void run() {
        double sum = 0; // here we inicialize the accumulator
        // This is the mathematical formulation we saw earlier.
        for (int j = 0; j < A[0].length; j++) {
            if (j != i) {
                sum += A[i][j] * x[j];
            }
        }

        x_next[i] = (1 / A[i][i]) * (b[i] - sum);
		// Because each task has a distinct 'i', no synchronization is needed
    }

	// Here we perform the Jacobi method in parallel until convergence or a maxIterations is reached
    public static double[] performJacobiParallel(double[][] A, double[] b, double[] x, double tol, int maxIterations, int numThreads) {

        int m = A.length;  // 'm' will be the numbers of rows (columns) (equations)
        double[] x_next = new double[m]; // 
        int iter = 1; 
        boolean converge = false;

		// We defined a thread pool with exactly numThreads threads, reused across iterations
        ExecutorService executor = Executors.newFixedThreadPool(numThreads);
        
        while (iter < maxIterations) {

            Future<?>[] futures = new Future<?>[m];
            for(int i = 0; i < m; i ++) {
                futures[i] = executor.submit(new SolveParallel(A, b, x, x_next, i));
            }   

			// We compare the old and new x vector
            converge = checkConvergence(x, x_next, tol);
            if (converge) {
                break;
            }

			// Here, we efficiently replace the content of x with x_next for the next iteration
            System.arraycopy(x_next, 0, x, 0, m);
            iter++;
        }

        executor.shutdown();

        if (!converge) {
            System.out.println("Numero maximo de iteraciones excedido para Jacobi paralelo");
        } else {
            System.out.println("Jacobi paralelo convergio en " + iter + " iteraiones");
        }
        return x;
    }


	// We compute if the change is small enough, if it is, we stop the iteration
    public static boolean checkConvergence(double[] x_0, double[] x_1, double tol) {
        double sum = 0.0;
        for (int i = 0; i < x_0.length; i++) {
            sum += Math.pow(x_0[i] - x_1[i], 2);
        }
        return Math.sqrt(sum) < tol;
    }

// Why did I use `ExecutorService`? We first tried with plain `Thread`, creating them // once and using `join()` after each iteration. It worked, but it kinda blocked
// everything and slowed it down. With `ExecutorService`, the threads are managed     // better, and tasks run smoother without all that manual control


	// To ckeck if the code is correct
    public static void main(String[] args) {

        double[][] A = {
            {10, -1, 2, 0, 3, -2, 1, 0},
            {-1, 11, -1, 3, -2, 1, 0, 2},
            {2, -1, 10, -1, 1, 0, 3, -2},
            {0, 3, -1, 8, -2, 2, -1, 1},
            {3, -2, 1, -2, 12, -3, 2, -1},
            {-2, 1, 0, 2, -3, 9, -1, 3},
            {1, 0, 3, -1, 2, -1, 7, -2},
            {0, 2, -2, 1, -1, 3, -2, 10}
        };

        double[] b = {5, 3, 7, 2, 4, 6, 1, 8};

        double[] x = new double[A.length];

        x = SolveParallel.performJacobiParallel(A, b, x, 0.00001, 1000, 8);

        System.out.println();
        for (double num : x) {
            System.out.print(num + " ");
        }

    }

}
```