# CUDA
**Digital image processing using parallel computing based on CUDA technology**
### Análisis del documento: **"Digital Image Processing Using Parallel Computing Based on CUDA Technology"**

Este documento explora el uso de **CUDA**, una tecnología de computación paralela basada en GPU, para acelerar el procesamiento de imágenes digitales, específicamente en la eliminación de ruido mediante algoritmos intensivos en recursos como **Non-Local Means (NLM)**.

---

### **Resumen del contenido**

|Aspecto|Detalle|
|---|---|
|**Tecnología principal**|CUDA, desarrollada por NVIDIA, para realizar computación paralela en tarjetas gráficas (GPU).|
|**Problema abordado**|Procesamiento de imágenes con ruido digital, que afecta la calidad de análisis y segmentación.|
|**Solución propuesta**|Implementar el algoritmo NLM en GPU para acelerar la eliminación de ruido en imágenes.|
|**Ventajas de CUDA**|Capacidad de ejecutar miles de hilos en paralelo, maximizando la eficiencia en tareas repetitivas.|

---

### **Conceptos principales**

|Concepto|Descripción|
|---|---|
|**Ruido digital**|Variaciones aleatorias de brillo o color en imágenes, causadas por sensores o circuitos electrónicos.|
|**Non-Local Means (NLM)**|Algoritmo avanzado para eliminación de ruido que utiliza toda la imagen para calcular nuevos valores de píxeles.|
|**Computación paralela**|Ejecución simultánea de múltiples tareas independientes, ideal para algoritmos intensivos como NLM.|
|**CUDA (Compute Unified Device Architecture)**|Plataforma de computación paralela diseñada para GPUs de NVIDIA.|

---

### **Implementación con CUDA**

#### **Proceso de trabajo en GPU**

1. **Transferencia de datos**:
    - Copiar los datos de la imagen desde la RAM a la memoria de la GPU.
2. **Cálculo en paralelo**:
    - Cada hilo de la GPU calcula un nuevo valor de píxel basándose en los vecinos.
    - Los cálculos son independientes, facilitando el paralelismo.
3. **Transferencia de resultados**:
    - Copiar los valores calculados desde la memoria de la GPU de vuelta a la RAM.

#### **Diagrama del flujo de trabajo**

1. **Leer datos de imagen**.
2. **Copiar datos a memoria de la GPU**.
3. **Realizar cálculos paralelos para cada píxel**:
    - Calcular distancias euclidianas.
    - Calcular coeficientes de peso y valores finales de píxeles.
4. **Copiar datos procesados de vuelta a la RAM**.
5. **Guardar la imagen procesada**.

---

### **Resultados experimentales**

El documento compara tres enfoques para el algoritmo NLM:

1. **Sin paralelismo (secuencial)**: Realizado en CPU con un solo hilo.
2. **CPU con múltiples hilos**: Paralelismo en CPU usando 2 hilos.
3. **CUDA en GPU**: Paralelismo masivo en GPU.

#### **Tiempos de ejecución**

|Método|Imagen (160x128 píxeles)|Imagen (210x182 píxeles)|
|---|---|---|
|1 hilo (CPU)|184.1 s|628.0 s|
|2 hilos (CPU)|196.9 s|714.0 s|
|GPU (CUDA)|29.9 s|111.7 s|

- **Aceleración**: La implementación en GPU es hasta **6 veces más rápida** que la versión secuencial.

---

### **Requisitos técnicos**

#### **Hardware**

|Requisito|Detalle|
|---|---|
|**GPU NVIDIA**|Compatible con CUDA (serie GTX, RTX, etc.).|
|**CPU**|Procesador multinúcleo para tareas de apoyo.|
|**RAM**|Memoria suficiente para manejar imágenes grandes (mínimo 4 GB).|
|**Espacio en disco**|Capacidad para almacenar imágenes de entrada y salida.|

#### **Software**

|Requisito|Detalle|
|---|---|
|**Sistema operativo**|Linux o Windows.|
|**CUDA Toolkit**|Herramientas de desarrollo de NVIDIA, incluye compilador NVCC.|
|**Lenguaje de programación**|C o C++ con extensiones de CUDA.|
|**Visor de imágenes**|Herramientas como ImageMagick para analizar los resultados.|

#### **Conocimientos necesarios**

|Área|Detalle|
|---|---|
|**Programación en C/C++**|Uso de memoria dinámica, punteros y estructuras de datos.|
|**CUDA**|Sintaxis y construcción de kernels CUDA para paralelismo.|
|**Procesamiento de imágenes**|Algoritmos como convolución, eliminación de ruido y métricas de calidad.|

---

### **Pasos para implementar el algoritmo en CUDA**

1. **Configura el entorno**:
    
    - Instala el CUDA Toolkit desde [NVIDIA](https://developer.nvidia.com/cuda-downloads).
    - Configura el compilador `nvcc` en tu entorno de desarrollo.
2. **Escribe el programa**:
    
    - Define un kernel CUDA para procesar cada píxel de forma independiente.
    - Maneja la transferencia de datos entre RAM y memoria de GPU.
3. **Ejemplo básico de kernel CUDA**:
    
    ```cpp
    __global__ void nlm_filter(float *image, float *output, int width, int height) {
        int x = blockIdx.x * blockDim.x + threadIdx.x;
        int y = blockIdx.y * blockDim.y + threadIdx.y;
    
        if (x < width && y < height) {
            // Calcular el nuevo valor del píxel (simplificado)
            float new_value = 0.0;
            // Operaciones de cálculo de NLM aquí...
            output[y * width + x] = new_value;
        }
    }
    ```
    
4. **Compila y ejecuta**:
    
    - Usa `nvcc` para compilar el código CUDA:
        
        ```bash
        nvcc -o nlm_filter nlm_filter.cu
        ```
        
    - Ejecuta el programa en tu GPU:
        
        ```bash
        ./nlm_filter
        ```
        
5. **Prueba y optimiza**:
    
    - Mide el tiempo de ejecución para evaluar la ganancia de rendimiento.
    - Ajusta el tamaño de bloques e hilos para maximizar el rendimiento.

---

### **Conclusión**

Tu máquina virtual con CPU no es suficiente para probar CUDA, ya que necesitas una **GPU NVIDIA**. Sin embargo, puedes implementar una versión paralela en CPU usando threads (OpenMP) para comparar resultados. Si tienes acceso a hardware con GPU, CUDA es una herramienta potente para acelerar este tipo de procesamiento. ¿Te interesa profundizar en alguna parte específica?


Dado que tu hardware actual es una máquina virtual sin GPU dedicada, no podrás implementar CUDA de manera nativa en tu entorno local. Sin embargo, tienes varias **opciones viables** para implementar y probar programas basados en GPU, ya sea usando simulaciones de paralelismo en CPU o aprovechando plataformas en la nube con acceso a **GPU**.

Aquí te dejo algunas opciones y plataformas recomendadas para implementar y probar CUDA en la nube:

---

### **Opciones de implementación viables para tu entorno actual**

1. **Implementación con paralelismo en CPU usando OpenMP**:
    
    - Aunque no tienes una GPU, puedes implementar paralelismo en CPU con **OpenMP**. Esta opción te permitirá realizar procesamiento paralelo en tu máquina virtual y ver mejoras de rendimiento con el uso de múltiples núcleos.
    - **OpenMP** es fácil de usar en C y permite crear hilos paralelos en CPU.
    
    **Ejemplo básico de OpenMP en C**:
    
    ```c
    #include <omp.h>
    #include <stdio.h>
    
    void process_pixel(int x, int y) {
        // Operación de procesamiento de píxel
    }
    
    int main() {
        int width = 1024, height = 768;
    
        // Paralelismo en CPU
        #pragma omp parallel for collapse(2)
        for (int x = 0; x < width; x++) {
            for (int y = 0; y < height; y++) {
                process_pixel(x, y);
            }
        }
    
        return 0;
    }
    ```
    
    - **Compilar**:
        
        ```bash
        gcc -fopenmp -o image_processing image_processing.c
        ```
        
    
    Si quieres simular paralelismo en CPU, **OpenMP** es una opción factible y sencilla, pero no te dará el rendimiento que lograrías con CUDA en una GPU.
    

---

### **Plataformas en la nube con acceso a GPU**

Para ejecutar y probar tus implementaciones con CUDA, la mejor opción es utilizar plataformas en la nube que te proporcionen acceso a GPU. Aquí te detallo algunas de las más utilizadas:

#### **1. Google Colab (con GPU gratuita)**

- **Google Colab** es una plataforma en la nube que ofrece acceso gratuito a GPUs **NVIDIA Tesla K80**, **T4**, **P100**, o **V100**.
- Puedes escribir código CUDA dentro de notebooks de **Python** o **C++** utilizando Colab.
- **Ventaja**: Es gratuito con acceso a GPU (limitado en tiempo de uso).

**Cómo usar Google Colab con CUDA**:

1. Abre un notebook en Colab.
2. Ve a _Entorno de ejecución_ -> _Cambiar tipo de entorno de ejecución_ -> _Hardware acelerado_ y selecciona **GPU**.
3. Para ejecutar código CUDA:
    
    ```bash
    !nvcc --version  # Verifica la instalación de CUDA
    ```
    
4. Puedes escribir código CUDA en un archivo `.cu` y compilarlo con `nvcc`:
    
    ```bash
    %%writefile my_program.cu
    __global__ void hello_cuda() {
        printf("Hello from GPU\n");
    }
    int main() {
        hello_cuda<<<1,1>>>();
        cudaDeviceSynchronize();
        return 0;
    }
    !nvcc my_program.cu -o my_program
    !./my_program
    ```
    

[Google Colab](https://colab.research.google.com/) es una excelente opción para comenzar.

---

#### **2. AWS (Amazon Web Services) con instancias EC2 con GPU**

- **AWS EC2** ofrece instancias con GPU dedicadas, como la **p2** o **p3** con GPUs **NVIDIA Tesla K80** o **V100**.
- **Ventaja**: Gran flexibilidad y escalabilidad. Puedes elegir el tipo de GPU que necesitas, y pagas solo por el tiempo de uso.
- **Desventaja**: No es gratuito, pero tiene opciones de pago por hora.

**Pasos**:

1. Crea una cuenta en AWS.
2. Lanza una instancia EC2 con soporte para GPU (como **p2.xlarge**).
3. Instala CUDA Toolkit en tu instancia.
4. Sube tu código y compílalo usando `nvcc` como en un entorno local.

[AWS EC2 con GPU](https://aws.amazon.com/ec2/instance-types/p2/) es adecuado si necesitas más control y flexibilidad.

---

#### **3. Microsoft Azure con instancias NC (NVIDIA GPU)**

- **Microsoft Azure** ofrece instancias virtuales con GPU de la serie **NC**, que incluyen GPUs **NVIDIA Tesla K80** y **P100**.
- Similar a AWS, pagas por el tiempo que usas la instancia.
- **Ventaja**: Buena integración con otros servicios de Microsoft si trabajas en entornos empresariales.

**Pasos**:

1. Regístrate en Azure y crea una VM con GPU.
2. Elige una instancia **NC**.
3. Instala el toolkit de CUDA y compila tu código CUDA.

[Microsoft Azure](https://azure.microsoft.com/en-us/pricing/details/virtual-machines/linux/) es una opción competitiva para trabajos serios con GPU.

---

#### **4. Paperspace (Acceso barato a GPUs en la nube)**

- **Paperspace** es una plataforma en la nube que proporciona acceso económico a GPUs **NVIDIA**.
- Tiene planes accesibles y también permite probar con GPUs en una máquina virtual configurada con CUDA.
- **Ventaja**: Precio más accesible que AWS o Azure para proyectos personales.

**Pasos**:

1. Crea una cuenta en [Paperspace](https://www.paperspace.com/).
2. Lanza una instancia con GPU (por ejemplo, **P4000** o **P5000**).
3. Sube tu código CUDA y ejecútalo en el entorno configurado.

---

#### **5. Kaggle Notebooks (GPU gratuita)**

- **Kaggle** también ofrece notebooks gratuitos con acceso a GPU (NVIDIA K80).
- Similar a Google Colab, es más limitado en tiempo de uso, pero es una excelente opción si buscas algo rápido y gratuito.

**Cómo usar Kaggle**:

- Accede a [Kaggle](https://www.kaggle.com/), crea un nuevo notebook y selecciona la opción **GPU** en el entorno de ejecución.

---

### **Conclusión: Viabilidad de la implementación en la nube**

Con tu hardware actual (una máquina virtual sin GPU), **no es viable implementar CUDA** localmente. Sin embargo, las plataformas en la nube como **Google Colab** o **Paperspace** te permitirán desarrollar y probar tus programas CUDA en **GPU** sin necesidad de invertir en hardware costoso. Google Colab es una excelente opción gratuita para empezar, mientras que AWS y Azure ofrecen más flexibilidad para proyectos más grandes.

Si te gustaría comenzar con alguna plataforma en particular, te puedo guiar paso a paso en su uso. ¿Te gustaría proceder con Google Colab?




# MPI
**MPI Casestudy: Parallel Image Processing**
### Análisis del documento: **"MPI Case Study: Parallel Image Processing"**

El documento presenta un caso práctico de procesamiento de imágenes paralelizado usando MPI (Message Passing Interface). Su objetivo principal es implementar un programa paralelo que reconstruya imágenes a partir de sus bordes detectados, utilizando técnicas de intercambio de límites entre procesos y operaciones iterativas.

---

### **Conceptos principales**

|Concepto|Descripción|
|---|---|
|**MPI (Message Passing Interface)**|Librería estándar para programar aplicaciones paralelas distribuidas, permitiendo comunicación entre procesos.|
|**Dominio de descomposición**|Dividir una imagen (matriz 2D) en subregiones procesadas en paralelo.|
|**Intercambio de límites (halo swap)**|Técnica para compartir datos de los bordes entre procesos vecinos en el contexto de paralelización.|
|**Reconstrucción inversa**|Cálculo de una imagen original a partir de los valores de sus bordes mediante operaciones iterativas.|

---

### **Técnicas y métodos utilizados**

|Técnica|Propósito|
|---|---|
|**Cálculo iterativo**|Reconstruir imágenes mediante una fórmula que actualiza píxeles iterativamente.|
|**Descomposición unidimensional**|Dividir la matriz de la imagen en rebanadas (slices) para asignarlas a procesos diferentes.|
|**Intercambio de límites (halo swap)**|Sincronizar valores de bordes entre procesos para garantizar cálculos consistentes.|
|**Operaciones de Scatter y Gather**|Distribuir y recolectar datos de forma eficiente entre procesos en paralelo.|

---

### **Pasos principales del caso de estudio**

#### 1. **Código secuencial**

- Se inicia con un programa que:
    - Lee un archivo de bordes de imagen (formato PGM).
    - Reconstruye la imagen a través de iteraciones basadas en valores vecinos.
    - Utiliza operaciones básicas para establecer los valores de los píxeles.

#### 2. **Paralelización inicial**

- **Descomposición**: La imagen se divide en regiones (rebanadas) asignadas a diferentes procesos.
- **Sin comunicación inicial**: Cada proceso calcula su parte de la imagen sin intercambiar límites con los procesos vecinos.
- **Operaciones de entrada/salida (IO)**: Un proceso maestro gestiona la lectura y escritura de datos.

#### 3. **Código paralelo completo**

- **Intercambio de límites (halo swap)**:
    - Cada proceso comunica sus bordes con los procesos vecinos antes de realizar los cálculos.
    - Se utiliza una topología cartesiana 1D para simplificar la gestión de procesos y límites.
- **Operaciones de comunicación**:
    - Enviar y recibir filas/columnas completas dependiendo de la orientación de la descomposición.
    - Uso de operaciones MPI como `MPI_Sendrecv`.

---

### **Requisitos técnicos**

|Aspecto|Detalles|
|---|---|
|**Hardware**|Cluster o supercomputadora con múltiples nodos y soporte para MPI.|
|**Software**|Biblioteca MPI (como OpenMPI o MPICH), compiladores C/Fortran y visor de imágenes PGM.|
|**Conocimientos previos**|Programación paralela, operaciones con matrices, manejo de archivos en formato PGM.|

---

### **Implementación del código**

#### Ejemplo básico de halo swap en C (parcial):

```c
// Intercambio de halos para procesos en una topología cartesiana 1D
MPI_Sendrecv(&old[MP][0], N, MPI_DOUBLE, rank+1, 0,
             &old[0][0], N, MPI_DOUBLE, rank-1, 0, 
             MPI_COMM_WORLD, MPI_STATUS_IGNORE);

// Similar para el intercambio en la dirección opuesta
```

#### Flujo de reconstrucción paralela:

1. **Inicialización**:
    
    - Configurar MPI y determinar la topología de procesos.
    - Leer datos en el proceso maestro y distribuir con `MPI_Scatter`.
2. **Cálculo iterativo**:
    
    - Realizar intercambios de límites entre iteraciones.
    - Calcular valores actualizados de la imagen en cada iteración.
3. **Recolección y salida**:
    
    - Usar `MPI_Gather` para unir resultados y escribir la imagen final.

---

### **Extensiones sugeridas**

1. **Criterio de parada**:
    
    - Terminar cuando la diferencia máxima entre iteraciones sea menor a un umbral.
    - Calcular esta diferencia global usando `MPI_Reduce`.
2. **Superposición de comunicación y cálculo**:
    
    - Utilizar comunicación no bloqueante para realizar cálculos mientras se transfieren datos.
3. **Tipos de datos derivados**:
    
    - Simplificar IO paralela definiendo estructuras específicas para datos sin halos.

---

Si necesitas un desglose más detallado de algún paso o ayuda con la implementación, indícalo y lo desarrollamos.


### **Implementación del caso de estudio: Procesamiento de imágenes paralelizado con MPI**

A continuación, detallo todo lo que necesitas en términos de **lenguajes**, **librerías**, **frameworks**, **hardware** y **conocimientos** para implementar el caso de estudio.

---

### **Lenguajes de programación**

- **C**: Lenguaje recomendado en este caso por su eficiencia y facilidad de integración con MPI. Es ideal para manipulación de datos en memoria (matrices) y comunicación a bajo nivel.
- **Fortran**: Otra opción recomendada, especialmente si ya tienes experiencia en programación científica.

---

### **Librerías necesarias**

1. **MPI (Message Passing Interface)**:
    
    - **OpenMPI** o **MPICH**: Dos implementaciones populares de MPI. Estas librerías son esenciales para la comunicación entre procesos.
    - Instalación típica:
        
        ```bash
        sudo apt install openmpi-bin libopenmpi-dev
        ```
        
2. **Librerías de manejo de archivos PGM**:
    
    - En el documento se mencionan las rutinas `pgmread` y `pgmwrite` que debes incluir en tu proyecto. Estas se encargan de leer y escribir imágenes en formato Portable Grey Map (PGM).
3. **Herramientas de compilación**:
    
    - **Compilador C**: `gcc` con soporte para MPI (`mpicc`).
    - **Compilador Fortran** (si usas Fortran): `gfortran` con soporte MPI (`mpif90`).

---

### **Frameworks y herramientas de desarrollo**

- **MPI ejecutado directamente**:
    
    - No necesitas un framework adicional, solo herramientas de MPI.
    - Ejecución típica:
        
        ```bash
        mpirun -np <número de procesos> ./mi_programa
        ```
        
- **Visor de imágenes PGM**:
    
    - Herramientas como `display` o **ImageMagick** para visualizar los resultados:
        
        ```bash
        sudo apt install imagemagick
        display output_image.pgm
        ```
        

---

### **Hardware recomendado**

1. **Clúster o supercomputadora**:
    
    - Ideal para aprovechar al máximo MPI, con múltiples nodos conectados a través de red.
    - Cada nodo debe tener:
        - **CPU multinúcleo**: Al menos 4 núcleos por nodo.
        - Memoria suficiente para manejar imágenes grandes (512 MB por núcleo como mínimo).
2. **Computadora personal** (para pruebas iniciales):
    
    - Procesador multinúcleo (CPU moderna con 4 núcleos o más).
    - Sistema operativo basado en Linux para facilidad de instalación de MPI y herramientas asociadas.

---

### **Conocimientos necesarios**

#### **Programación**

- **C o Fortran**: Conocer sintaxis básica y manejo de memoria.
- **Programación paralela**:
    - Conceptos como sincronización, comunicación entre procesos y partición de datos.
    - Uso de primitivas MPI como:
        - `MPI_Init`, `MPI_Finalize`
        - `MPI_Scatter`, `MPI_Gather`
        - `MPI_Sendrecv`, `MPI_Bcast`

#### **Procesamiento de imágenes**

- Operaciones básicas como convolución y manipulación de bordes.
- Comprensión del formato PGM (matrices 2D de valores de píxeles).

#### **Matemáticas**

- Iteraciones con esquemas tipo Jacobi o Gauss-Seidel.
- Manipulación de matrices y comprensión de algoritmos basados en diferencias finitas.

---

### **Pasos para la implementación**

1. **Configuración del entorno**:
    
    - Instalar OpenMPI y un compilador adecuado.
    - Configurar el entorno de ejecución de MPI (`hostsfile` para clústeres).
2. **Escribir el programa secuencial**:
    
    - Leer y escribir imágenes PGM.
    - Implementar la fórmula iterativa para reconstruir la imagen.
3. **Paralelizar el programa**:
    
    - Dividir la matriz en subregiones (por filas).
    - Implementar intercambio de límites (halo swap) con `MPI_Sendrecv`.
4. **Probar y optimizar**:
    
    - Comparar los tiempos de ejecución entre las versiones secuencial y paralela.
    - Optimizar el número de iteraciones y la frecuencia de sincronización.
5. **Extender la funcionalidad (opcional)**:
    
    - Implementar comunicación no bloqueante para superponer cálculo y comunicación.
    - Reducir el uso de memoria mediante estructuras de datos derivadas.

---

### **Ejemplo básico de implementación**

Código en **C** para la reconstrucción inicial de imágenes con MPI:

```c
#include <mpi.h>
#include <stdio.h>
#include <stdlib.h>

void initialize_image(double **image, int rows, int cols, double value) {
    for (int i = 0; i < rows; i++)
        for (int j = 0; j < cols; j++)
            image[i][j] = value;
}

int main(int argc, char *argv[]) {
    MPI_Init(&argc, &argv);

    int rank, size;
    MPI_Comm_rank(MPI_COMM_WORLD, &rank);
    MPI_Comm_size(MPI_COMM_WORLD, &size);

    // Dimensiones de la imagen (asumidas para este ejemplo)
    int M = 128, N = 128; 
    int local_rows = M / size; 

    // Asignar memoria para la imagen local
    double **local_image = malloc((local_rows + 2) * sizeof(double *));
    for (int i = 0; i < local_rows + 2; i++)
        local_image[i] = malloc(N * sizeof(double));

    // Inicializar la imagen local
    initialize_image(local_image, local_rows + 2, N, 255.0);

    // Halo swap (ejemplo básico)
    if (rank > 0) {
        MPI_Sendrecv(local_image[1], N, MPI_DOUBLE, rank - 1, 0,
                     local_image[0], N, MPI_DOUBLE, rank - 1, 0,
                     MPI_COMM_WORLD, MPI_STATUS_IGNORE);
    }

    if (rank < size - 1) {
        MPI_Sendrecv(local_image[local_rows], N, MPI_DOUBLE, rank + 1, 0,
                     local_image[local_rows + 1], N, MPI_DOUBLE, rank + 1, 0,
                     MPI_COMM_WORLD, MPI_STATUS_IGNORE);
    }

    // Limpieza
    for (int i = 0; i < local_rows + 2; i++)
        free(local_image[i]);
    free(local_image);

    MPI_Finalize();
    return 0;
}
```

Este código realiza una configuración básica de MPI y un intercambio de halos para un dominio paralelo.

---

Si necesitas ayuda adicional con la implementación o conceptos específicos, ¡indícalo! 


Con los recursos que mencionas y tus conocimientos básicos en **C**, puedes comenzar a implementar este caso de estudio en tu máquina virtual. Aunque es un entorno limitado, será suficiente para aprender, experimentar y realizar pruebas iniciales. Aquí tienes un análisis detallado:

---

### **Análisis de tu configuración**

|Recurso|Estado|Observación|
|---|---|---|
|**Lenguaje C (básico)**|Adecuado|Es suficiente para comenzar, pero podrías necesitar aprender sobre manejo de matrices y punteros.|
|**Máquina virtual (Ubuntu)**|Ideal para desarrollo|Ubuntu ofrece buen soporte para herramientas de desarrollo como OpenMPI y compiladores de C.|
|**4 GB de RAM virtual**|Limitado|Suficiente para imágenes pequeñas (128x128 píxeles), pero podría ser insuficiente para imágenes grandes.|
|**4 núcleos virtuales**|Adecuado|Permite probar el paralelismo básico con hasta 4 procesos MPI, lo cual es suficiente para aprender.|

---

### **Limitaciones**

1. **Tamaño de las imágenes**:
    
    - Dado que tienes solo 4 GB de RAM, el tamaño de las imágenes debe ser pequeño (e.g., 128x128 o 256x256 píxeles).
    - Procesar imágenes más grandes podría generar problemas de memoria.
2. **Ejecución en un solo nodo**:
    
    - Al estar en una máquina virtual, todos los procesos paralelos se ejecutarán en un único nodo (misma máquina).
    - Esto no te permitirá probar las ventajas de MPI en un clúster real, pero es perfecto para entender la lógica paralela.
3. **Conocimientos básicos de C**:
    
    - Necesitarás familiarizarte con estructuras como matrices dinámicas, punteros y uso básico de librerías como MPI.

---

### **Pasos sugeridos para empezar**

1. **Configura tu entorno**:
    
    - Instala MPI y herramientas de desarrollo:
        
        ```bash
        sudo apt update
        sudo apt install build-essential openmpi-bin libopenmpi-dev
        ```
        
    - Verifica la instalación de MPI:
        
        ```bash
        mpicc --version
        mpirun --version
        ```
        
2. **Empieza con programas simples**:
    
    - Escribe un programa MPI que simplemente reparta y recolecte datos:
        
        ```c
        #include <mpi.h>
        #include <stdio.h>
        
        int main(int argc, char *argv[]) {
            MPI_Init(&argc, &argv);
            int rank, size;
            MPI_Comm_rank(MPI_COMM_WORLD, &rank);
            MPI_Comm_size(MPI_COMM_WORLD, &size);
        
            printf("Hola desde el proceso %d de %d\n", rank, size);
        
            MPI_Finalize();
            return 0;
        }
        ```
        
    - Compila y ejecuta:
        
        ```bash
        mpicc -o hello_mpi hello_mpi.c
        mpirun -np 4 ./hello_mpi
        ```
        
3. **Implementa el programa secuencial**:
    
    - Escribe el código para reconstruir la imagen de forma secuencial (sin MPI).
    - Lee y escribe imágenes en formato PGM.
4. **Paraleliza el programa**:
    
    - Divide la imagen en regiones y distribúyelas entre procesos usando `MPI_Scatter`.
    - Implementa el intercambio de límites (halo swap) entre procesos vecinos con `MPI_Sendrecv`.

---

### **Recomendaciones para trabajar en tu entorno**

1. **Optimiza el uso de memoria**:
    
    - Trabaja con imágenes pequeñas (e.g., 128x128 píxeles).
    - Libera memoria dinámica al finalizar cada operación.
2. **Verifica el paralelismo**:
    
    - Usa 2 o 4 procesos para entender cómo funciona la comunicación entre ellos.
    - Asegúrate de que los resultados del código paralelo coincidan con los del secuencial.
3. **Aprende los conceptos necesarios de C**:
    
    - Manejo de memoria dinámica (`malloc` y `free`).
    - Uso de estructuras de datos bidimensionales.
    - Familiarízate con funciones básicas de MPI (`MPI_Init`, `MPI_Finalize`, `MPI_Scatter`, `MPI_Gather`).
4. **Extiende tu máquina virtual si es necesario**:
    
    - Si en el futuro procesas imágenes más grandes, considera aumentar la RAM virtual.

---

### **Conclusión**

Con tu máquina virtual y conocimientos básicos, tienes un entorno adecuado para comenzar. Este caso de estudio es ideal para aprender los fundamentos de paralelismo con MPI. Si necesitas más ayuda con ejemplos o explicaciones específicas, no dudes en preguntar.

