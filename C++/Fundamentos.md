

# **Temario de Fundamentos de Programación en C++ (Enfoque Moderno)**

Este temario está diseñado para ser práctico y directo, utilizando las características modernas del lenguaje (C++17 y posteriores) que son el estándar en la industria.

---

### **Módulo 1: Configuración y Primer Vistazo al Ecosistema C++**

El objetivo aquí es entender las diferencias fundamentales en el flujo de trabajo y preparar tu entorno en VSCode sobre Windows.

1. **¿Por qué C++ es Diferente?**
    - Lenguaje compilado vs. interpretado (Python) o compilado a bytecode (Java).
    - El proceso de compilación: Preprocesador -> Compilador -> Ensamblador -> Enlazador (Linker). Entender esto es clave para resolver errores futuros.
    - La filosofía de C++: "No pagas por lo que no usas" y el control de bajo nivel.
        
2. **Configuración del Entorno en Windows + VSCode:**
    - Instalación del compilador **MinGW-w64** (el estándar de facto para compilar C++ en Windows fuera del ecosistema de Visual Studio).
    - Configuración de VSCode: Instalación de la extensión C/C++ de Microsoft.
    - Creación del `tasks.json` para compilar con `g++` y `launch.json` para depurar directamente desde VSCode.
        
3. **Tu Primer Programa: "Hola, Mundo" y el Proceso de Compilación.**
    
    - Estructura básica: `#include <iostream>`, la función `main()`.
    - El concepto de **namespaces**: Qué es `std::` y por qué `using namespace std;` puede ser una mala práctica en proyectos grandes.
    - Compilar y ejecutar desde la terminal de VSCode (Git Bash o CMD):
        Bash
        
        ```cpp
        # Compilar el código fuente en un archivo ejecutable
        g++ mi_programa.cpp -o mi_programa.exe
        
        # Ejecutar el programa compilado
        ./mi_programa.exe
        ```
        

---

### **Módulo 2: Sintaxis Esencial y Tipos de Datos (El Estilo C++)**

Nos enfocaremos en la sintaxis y las particularidades del sistema de tipos de C++.

1. **Variables y Tipos de Datos Primitivos:**
    - Sintaxis de declaración: `int numero = 10;`.
    - **Modificadores:** `short`, `long`, `long long`, `unsigned`.
    - Tipos de ancho fijo (`<cstdint>`): `int32_t`, `uint64_t`. **(Buena práctica para predictibilidad)**.
    - Inicialización moderna: `int a {10};` (Uniform Initialization). Previene ciertos tipos de errores de conversión.
        
2. **Estructuras de Control (Sintaxis Moderna):**
    
    - `if-else` y `switch`:
        - **If con inicializador (C++17):** `if (int val = get_value(); val > 5) { /* ... */ }`. Muy útil para limitar el alcance de las variables.
        - `switch` y el atributo `[[fallthrough]]` (C++17).
    - Bucles:
        - `for`, `while`, `do-while` (sintaxis similar a Java).
        - **Range-based for loop:** La forma moderna y segura de iterar.
            C++
            
            ```cpp
            #include <vector>
            std::vector<int> numeros = {1, 2, 3, 4};
            for (int num : numeros) {
                // ...
            }
            ```
            
1. **Entrada y Salida por Consola (`<iostream>`):**
    - `std::cout` para salida y `std::cin` para entrada.
    - El uso de los operadores `<<` (inserción) y `>>` (extracción).

---

### **Módulo 3: Funciones y Organización del Código**

Aquí empezamos a ver diferencias importantes en cómo se estructura el código.

1. **Declaración vs. Definición:** El concepto de declarar una función antes de usarla (prototipo) es fundamental en C++.
    
2. **Archivos de Cabecera (`.h` o `.hpp`) y Fuentes (`.cpp`):**
    
    - Cómo separar las declaraciones (en el `.h`) de las definiciones (en el `.cpp`) para organizar proyectos.
        
3. **Paso de Parámetros (¡CRUCIAL!):**
    
    - **Paso por Valor:** Se crea una copia (como los primitivos en Java).
        
    - **Paso por Puntero (`*`):** Se pasa la dirección de memoria (más adelante).
        
    - **Paso por Referencia (`&`):** Se pasa un alias del objeto original. No hay copia. Es la forma más eficiente y común para objetos complejos.
        
    - **La mejor práctica:** Usar **paso por referencia constante (`const &`)** cuando no necesitas modificar el argumento. Es seguro y evita copias innecesarias.
        
        C++
        
        ```
        // Evita copiar un string pesado, pero asegura que no será modificado.
        void imprimir_nombre(const std::string& nombre);
        ```
        
4. **Sobrecarga de Funciones (Function Overloading):** Mismo concepto que en Java, diferente sintaxis.
    
5. **Parámetros por Defecto:** Similar a Python. `void mi_funcion(int a, int b = 10);`
    

---

### **Módulo 4: El Corazón de C++: Punteros y Gestión de Memoria**

Este es el módulo más importante para ti, ya que estos conceptos no existen o están abstraídos en Java y Python.

1. **Modelos de Memoria: Stack vs. Heap.**
    
    - **Stack:** Memoria automática, rápida, de tamaño limitado. Las variables locales viven aquí. La gestión es automática (RAII).
        
    - **Heap (Free Store):** Memoria dinámica, más lenta, grande. Tú la gestionas. Aquí es donde ocurren los "memory leaks".
        
2. **Punteros (`*`):**
    
    - ¿Qué son? Variables que almacenan direcciones de memoria.
        
    - Operador de dirección (`&`): Para obtener la dirección de una variable. `int* ptr = &mi_variable;`
        
    - Operador de desreferencia (`*`): Para acceder al valor en la dirección apuntada. `int valor = *ptr;`
        
    - El puntero nulo moderno: `nullptr`. **(Usa siempre `nullptr`, nunca `NULL` o `0`)**.
        
3. **Asignación de Memoria Dinámica (El modo "viejo" y peligroso):**
    
    - Operador `new`: Reserva memoria en el Heap. `int* num = new int(10);`
        
    - Operador `delete`: Libera la memoria reservada con `new`. `delete num;`
        
    - Arrays dinámicos: `new int[10]` y su correspondiente `delete[]`. Olvidar los `[]` es un error común.
        
    - **Memory Leaks:** ¿Qué pasa si olvidas un `delete`?
        

---

### **Módulo 5: Abstracciones Modernas de C++ (El modo correcto)**

Aquí veremos las herramientas modernas que nos permiten evitar los peligros del Módulo 4.

1. **Arrays y Vectores:**
    
    - Arrays estilo C (`int arr[5];`): Rápido, pero rígido y propenso a errores. Se "decaen" a punteros fácilmente. **Evítalos si puedes.**
        
    - `std::array` (`<array>`): Un contenedor para arrays de tamaño fijo en el Stack. Es la versión segura y moderna de los arrays C.
        
    - **`std::vector` (`<vector>`):** La herramienta principal. Es un array dinámico que gestiona su propia memoria en el Heap. Crece y decrece según sea necesario. **Usa `std::vector` por defecto en lugar de `new[]`**.
        
2. **Cadenas de Texto (Strings):**
    
    - Strings estilo C (arrays de `char` terminados en `\0`): Peligrosos y difíciles de manejar. **Evítalos.**
        
    - **`std::string` (`<string>`):** La clase estándar para manejar texto. Es segura, eficiente y gestiona su propia memoria.
        

---

### **Módulo 6: Clases, Objetos y el Principio RAII**

Introducción a la POO en C++ con énfasis en la gestión de recursos.

1. **Structs vs. Classes:**
    
    - `struct`: Miembros públicos por defecto. Ideal para agrupar datos simples.
        
    - `class`: Miembros privados por defecto.
        
2. **Constructores y Destructores:**
    
    - **Constructor:** Se ejecuta al crear un objeto.
        
    - **Destructor (`~ClassName()`):** Se ejecuta automáticamente cuando un objeto sale del ámbito (si está en el Stack) o cuando se llama a `delete` (si está en el Heap). **Este es el mecanismo clave para la gestión automática de recursos en C++.**
        
3. **RAII (Resource Acquisition Is Initialization):**
    
    - La idea central de C++ moderno: La adquisición de un recurso (memoria, un archivo, un socket) se liga al tiempo de vida de un objeto. Cuando el objeto es destruido, su destructor libera el recurso.
        
    - `std::vector`, `std::string` y los punteros inteligentes son los mejores ejemplos de RAII.
        

---

### **Módulo 7: Gestión de Memoria Moderna con Punteros Inteligentes**

La culminación del manejo de memoria. Esto es lo que usan los programadores profesionales para evitar `new` y `delete` manuales.

1. **Punteros Inteligentes (`<memory>`):** Objetos que envuelven un puntero "crudo" y usan RAII para gestionar su vida.
    
2. **`std::unique_ptr`:**
    
    - Representa **propiedad única** sobre un recurso. No se puede copiar, solo mover.
        
    - Cuando el `unique_ptr` se destruye, automáticamente llama a `delete` sobre el puntero que contiene.
        
    - Es la opción por defecto para gestionar memoria dinámica. **Cero sobrecarga de rendimiento.**
        
3. **`std::shared_ptr`:**
    
    - Representa **propiedad compartida**. Mantiene un contador de referencias.
        
    - El recurso solo se libera cuando el último `shared_ptr` que apunta a él es destruido.
        
    - Útil cuando múltiples partes del código necesitan compartir la propiedad de un objeto dinámico.
        

¡Con este temario tendrás una base sólida y moderna de C++, enfocada en los aspectos que realmente marcan la diferencia con los lenguajes que ya conoces!



¡Excelente! Comencemos con el primer módulo. Nos tomaremos el tiempo necesario para desglosar cada concepto, ya que sentar bien estas bases es crucial para todo lo que vendrá después.

---




# **Módulo 1: Configuración y Primer Vistazo al Ecosistema C++**

### **1. ¿Por qué C++ es Diferente?**

Viniendo de Java y Python, notarás un cambio de paradigma fundamental. No se trata solo de sintaxis, sino de filosofía.

- **Lenguaje Compilado (Nativamente):** A diferencia de Python (que es interpretado) o Java (que se compila a un `bytecode` intermedio para la JVM), el código C++ se traduce directamente a **código máquina**, el lenguaje que entiende el procesador de tu computadora.
    
    - **Analogía:** Imagina que quieres construir un mueble.
        
        - **Python (Interpretado):** Le das las instrucciones en español a un carpintero experto. Él lee una instrucción, la ejecuta, lee la siguiente, la ejecuta, y así sucesivamente. Es flexible, pero si hay un error en el paso 10, no lo sabrás hasta que llegue allí.
            
        - **Java (Bytecode + JVM):** Escribes tus instrucciones en un lenguaje universal para "carpinteros-robot" (el `bytecode`). Luego, necesitas un "carpintero-robot" específico para cada lugar (la JVM de Windows, la de Linux, etc.) que traduzca ese lenguaje universal a sus acciones específicas. Esto lo hace muy portable.
            
        - **C++ (Compilado):** Tomas tus instrucciones y las usas para fabricar una máquina-herramienta a medida, única y especializada para construir _ese_ mueble específico (el archivo `.exe`). Esta máquina es increíblemente rápida y eficiente, pero solo sirve para construir ese mueble y solo funciona con los enchufes de tu taller (tu sistema operativo).
            
- **El Proceso de Compilación:** Cuando ejecutas un comando como `g++`, no es un solo paso. Ocurre una secuencia de cuatro fases importantes:
    
    1. **Preprocesador:** Lee tu código y busca directivas que empiezan con `#`. La más común es `#include`, que literalmente copia y pega el contenido de otro archivo en tu código. También resuelve macros.
        
    2. **Compilador:** Toma el código "expandido" por el preprocesador y lo traduce a lenguaje ensamblador, que son instrucciones de bajo nivel muy cercanas al hardware. Aquí es donde se verifica la mayor parte de la sintaxis y los errores de tipo.
        
    3. **Ensamblador (Assembler):** Convierte el código ensamblador en código objeto (`.o` o `.obj`), que es puro código máquina (binario), pero aún no es un programa ejecutable.
        
    4. **Enlazador (Linker):** Es el paso final. Si tu programa usa código de otras partes (como la función para imprimir en pantalla de `<iostream>`), el enlazador toma tu código objeto y los fragmentos de código objeto de las librerías que necesitas y los "enlaza" todos juntos para crear el archivo ejecutable final (`.exe` en Windows).
        
- **La Filosofía de C++:**
    
    - **"No pagas por lo que no usas":** Si no utilizas una característica del lenguaje, esta no debería añadir ningún coste (en tiempo o memoria) a tu programa final.
        
    - **Control de bajo nivel:** Tienes acceso directo a la memoria a través de punteros. Esto te da un poder inmenso para optimizar, pero también la responsabilidad de gestionarla correctamente. Es como conducir un coche con transmisión manual en lugar de automática.
        

---

### **2. Configuración del Entorno en Windows + VSCode**

Vamos a instalar el compilador **MinGW-w64** (una versión para Windows del popular compilador GCC de Linux) y a configurar VSCode para que trabaje con él. Usaremos el instalador de **MSYS2**, que facilita mucho la gestión de estas herramientas.

1. **Instalar MSYS2:**
    
    - Ve a [la página oficial de MSYS2](https://www.msys2.org/) y descarga el instalador.
        
    - Ejecútalo y sigue los pasos. Déjalo en la ruta por defecto (`C:\msys64`).
        
2. **Instalar el Compilador C++ (MinGW-w64):**
    
    - Una vez instalado MSYS2, se abrirá una terminal especial. Si no, búscala en el menú de inicio como "MSYS2 MSYS".
        
    - Primero, actualiza la base de paquetes. Escribe el siguiente comando y presiona Enter. Te pedirá cerrar la ventana al final, hazlo.
        
        Bash
        
        ```
        pacman -Syu
        ```
        
    - Vuelve a abrir la terminal de MSYS2 y ejecuta el mismo comando de nuevo para terminar de actualizar.
        
        Bash
        
        ```
        pacman -Syu
        ```
        
    - Ahora, instala la cadena de herramientas del compilador. Este comando instalará `g++`, `gcc`, el depurador `gdb` y otras utilidades necesarias.
        
        Bash
        
        ```
        pacman -S --needed base-devel mingw-w64-ucrt-x86_64-toolchain
        ```
        
    - Presiona Enter para seleccionar todo por defecto y `Y` para confirmar la instalación.
        
3. **Añadir el Compilador al PATH de Windows:**
    
    - Este es un paso **crítico**. Le dice a Windows dónde encontrar el ejecutable `g++.exe` desde cualquier terminal (como la de VSCode).
        
    - Abre el menú de inicio y busca "Editar las variables de entorno del sistema".
        
    - En la ventana que se abre, haz clic en "Variables de entorno...".
        
    - En la sección "Variables del sistema", busca la variable `Path` y haz clic en "Editar...".
        
    - Haz clic en "Nuevo" y añade la ruta a la carpeta bin de tu compilador. Si instalaste MSYS2 en la ruta por defecto, será:
        
        C:\msys64\ucrt64\bin
        
    - Acepta todas las ventanas. Para verificar, abre una **nueva** terminal de VSCode o un nuevo CMD y escribe `g++ --version`. Deberías ver la versión del compilador que instalaste.
        
4. **Configurar VSCode:**
    
    - **Instalar la Extensión:** En VSCode, ve a la pestaña de Extensiones (Ctrl+Shift+X) y busca e instala el paquete **"C/C++ Extension Pack"** de Microsoft. Este paquete incluye IntelliSense (autocompletado inteligente), depuración y formato de código.
        
    - **Crear tu Proyecto:**
        
        1. Crea una carpeta en tu PC, por ejemplo, `C:\Users\TuUsuario\Desktop\CppCurso`.
            
        2. Abre esa carpeta en VSCode (`Archivo > Abrir carpeta...`).
            
        3. Crea un nuevo archivo llamado `main.cpp`.
            

---

### **3. Tu Primer Programa: "Hola, Mundo"**

Pega el siguiente código en tu archivo `main.cpp`. Ahora, vamos a desmenuzarlo símbolo por símbolo.

C++

```cpp
#include <iostream>

int main() {
    // Imprime un mensaje en la consola
    std::cout << "Hola, Mundo!" << std::endl;
    
    return 0;
}
```

#### **Análisis Detallado del Código:**

- `#include <iostream>`
    
    - `#`: Este símbolo le indica al **Preprocesador** que lo que sigue es una directiva, no código C++.
        
    - `include`: Es la directiva que le ordena al preprocesador buscar un archivo y pegar todo su contenido en esta línea.
        
    - `<...>`: Los corchetes angulares le indican que busque el archivo en las carpetas de **inclusión estándar** del compilador, donde viven las librerías oficiales de C++. Si usaras comillas (`"mi_archivo.h"`), lo buscaría primero en la carpeta de tu proyecto actual.
        
    - `iostream`: Es el nombre del archivo de cabecera (header file) que contiene las declaraciones para las funcionalidades de **I**nput/**O**utput **Stream** (flujo de entrada/salida). Gracias a esta línea, podemos usar `std::cout` y `std::endl`.
        
- `int main() { ... }`
    
    - `int`: Es el **tipo de dato de retorno** de la función. La función `main` siempre debe devolver un entero (`int`). Este valor se le entrega al sistema operativo para indicar si el programa terminó con éxito o no.
        
    - `main`: Es el nombre especial de la función que el sistema operativo buscará para **iniciar la ejecución de tu programa**. Es el punto de entrada obligatorio.
        
    - `()`: Los paréntesis indican que `main` es una función. Dentro de ellos irían los parámetros, pero en este caso no recibe ninguno.
        
    - `{ ... }`: Las llaves definen el **cuerpo** o **ámbito (scope)** de la función. Todo el código que pertenece a `main` debe ir dentro de estas llaves.
        
- `std::cout << "Hola, Mundo!" << std::endl;`
    
    - `std`: Es un **namespace** (espacio de nombres). Las funcionalidades de la librería estándar de C++ están dentro de este namespace para evitar colisiones de nombres con tu propio código o con otras librerías.
        
    - `::`: Es el **operador de resolución de ámbito**. Se usa para especificar a qué namespace (o clase) pertenece un miembro. `std::cout` significa "quiero usar el `cout` que está definido dentro de `std`".
        
    - `cout`: Es un **objeto** (una instancia de la clase `ostream`) que representa el flujo de salida estándar, que por lo general es la consola o terminal. Su nombre viene de **C**haracter **OUT**put.
        
    - `<<`: Es el **operador de inserción de flujo**. Suena complejo, pero su trabajo es tomar lo que está a su derecha y "meterlo" o "insertarlo" en el flujo que está a su izquierda. Puedes encadenarlos.
        
    - `"Hola, Mundo!"`: Esto es un **literal de cadena de texto**. Es una secuencia de caracteres constante.
        
    - `std::endl`: Es un **manipulador de flujo** (de **End L**ine). Hace dos cosas: 1) Inserta un carácter de nueva línea (`\n`) en el flujo, haciendo que el cursor de la terminal baje a la siguiente línea. 2) **Vacía (flush) el búfer de salida**. Esto garantiza que el texto se muestre inmediatamente. Para impresiones simples, usar `"\n"` es a menudo más eficiente, ya que no fuerza el vaciado del búfer.
        
    - `;`: El punto y coma es el símbolo que **termina una instrucción** en C++. Es obligatorio al final de la mayoría de las líneas de código ejecutables.
        
- `return 0;`
    
    - `return`: Es la palabra clave para devolver un valor desde una función.
        
    - `0`: Es el valor entero que devolvemos. Por convención, devolver `0` desde `main` significa **"El programa se ejecutó sin errores"**. Cualquier otro número (como `1`) suele indicar que ocurrió algún tipo de error.
        

#### **Compilar y Ejecutar desde la Terminal de VSCode**

1. Abre una terminal en VSCode (`Ctrl + Ñ` o `Ver > Terminal`).
    
2. Escribe el siguiente comando y presiona Enter:
    
    Bash
    
    ```sh
    g++ main.cpp -o main.exe
    ```
    
    - `g++`: El programa compilador que instalamos.
        
    - `main.cpp`: El archivo de código fuente que queremos compilar.
        
    - `-o`: Una **bandera (flag)** que le dice al compilador "quiero especificar el nombre del archivo de **o**utput".
        
    - `main.exe`: El nombre que le daremos a nuestro programa ejecutable.
        
3. Si no aparece ningún error, verás que se ha creado un nuevo archivo `main.exe` en tu carpeta. Para ejecutarlo, escribe en la misma terminal:
    
    Bash
    
    ```
    ./main.exe
    ```
    
    - `./`: Le indica a la terminal que busque el ejecutable en el **directorio actual**.
        
    - `main.exe`: El nombre de nuestro programa.
        


# **Módulo 2: Sintaxis Esencial y Tipos de Datos (El Estilo C++)**

El objetivo de este módulo es que domines la sintaxis fundamental para crear variables, tomar decisiones y ejecutar bucles, utilizando las mejores prácticas del C++ moderno.

---

### **1. Variables y Tipos de Datos Primitivos**

En C++, la declaración de una variable siempre sigue el formato `tipo nombre;` o `tipo nombre = valor;`. La diferencia clave con Python es que **C++ es un lenguaje de tipado estático**, lo que significa que el tipo de una variable se fija en tiempo de compilación y no puede cambiar, similar a Java.

#### **Tipos de Datos Fundamentales**

Estos son los tipos más básicos que C++ ofrece.

|Tipo en C++|Descripción|Ejemplo|Equivalente Aprox. (Java)|Equivalente Aprox. (Python)|
|---|---|---|---|---|
|`int`|Número entero. Su tamaño suele ser de 4 bytes, pero depende de la arquitectura del sistema.|`int edad = 25;`|`int`|`int`|
|`double`|Número de punto flotante de doble precisión. Es el tipo por defecto para decimales.|`double precio = 19.99;`|`double`|`float`|
|`char`|Un único carácter. Ocupa 1 byte y se escribe con comillas simples.|`char inicial = 'A';`|`char`|`str` (de longitud 1)|
|`bool`|Valor booleano. Solo puede ser `true` o `false`.|`bool esValido = true;`|`boolean`|`bool`|
|`float`|Número de punto flotante de precisión simple. Usa menos memoria que `double` pero es menos preciso.|`float distancia = 3.5f;`|`float`|`float`|

#### **Modificadores de Tipo: El Poder de C++**

Aquí C++ te da un control que no tienes en Java o Python. Puedes modificar los tipos numéricos con estas palabras clave:

- **`signed` / `unsigned`**: Por defecto, los tipos enteros como `int` son `signed`, lo que significa que pueden representar tanto números positivos como negativos (la mitad del rango para cada uno). Si declaras un entero como `unsigned`, le dices al compilador que esta variable **solo contendrá valores no negativos (cero y positivos)**. A cambio, duplicas su rango máximo positivo.
    
    - **Analogía**: Imagina una regla de 30 cm. Una `signed int` sería como poner el "0" en el medio, pudiendo medir de -15 cm a +15 cm. Una `unsigned int` pone el "0" al principio, permitiéndote medir de 0 cm a 30 cm.
        
    - **Ejemplo**:
        
        C++
        
        ```
        // Un int de 4 bytes (32 bits) típicamente va de -2,147,483,648 a 2,147,483,647
        int numeroConSigno = -100;
        
        // Un unsigned int de 4 bytes (32 bits) va de 0 a 4,294,967,295
        unsigned int contador = 4000000000; // Esto daría error en un 'int' normal
        ```
        
- **`short` / `long` / `long long`**: Estos modifican el tamaño (y por tanto el rango) de un tipo de dato.
    
    - `short int`: Pide al compilador que use menos memoria para el entero (usualmente 2 bytes).
        
    - `long int`: Pide que use más o igual memoria que un `int` (usualmente 4 u 8 bytes).
        
    - `long long int`: Pide que use al menos 8 bytes, garantizando un rango enorme.
        

#### **Mejor Práctica: Tipos de Ancho Fijo (`<cstdint>`)** 🤓

El tamaño de un `int` puede variar entre un sistema de 32 bits y uno de 64 bits. Para escribir código que se comporte de manera idéntica en cualquier plataforma (código portable), los programadores profesionales usan tipos de ancho fijo. Para ello, debes incluir la cabecera `<cstdint>`.

- `int8_t`, `int16_t`, `int32_t`, `int64_t`: Enteros con signo de exactamente 8, 16, 32 y 64 bits.
    
- `uint8_t`, `uint16_t`, `uint32_t`, `uint64_t`: Enteros sin signo de exactamente 8, 16, 32 y 64 bits.
    

**Ejemplo**:

C++

```cpp
#include <cstdint> // No olvides incluirlo

// Sabes con 100% de certeza que esta variable tiene 32 bits, sin importar el sistema.
int32_t id_usuario = 12345678;
```

#### **Inicialización de Variables: La Forma Moderna**

Existen varias formas de dar un valor inicial a una variable, pero la más recomendada hoy en día es la **inicialización uniforme** usando llaves `{}`.

C++

```cpp
// 1. Estilo C (funciona, pero es antiguo)
int a = 10;

// 2. Estilo Constructor (parece una llamada a función)
int b(20);

// 3. Inicialización Uniforme (¡La forma moderna y segura!)
int c {30};
double d {45.5};
```

**¿Por qué usar llaves `{}`?** Porque previenen un tipo de error llamado "narrowing conversion" (conversión con pérdida de datos). El compilador te avisará si intentas inicializar una variable con un valor que no cabe en su tipo.

C++

```
// int d = 3.14;   // MAL: El .14 se pierde silenciosamente. d vale 3.
// int e(3.14);    // MAL: Igual, e vale 3.

int f {3.14};   // ¡BIEN! El compilador dará un ERROR, protegiéndote.
```

---

### **2. Estructuras de Control (Sintaxis Moderna)**

La lógica es la misma que ya conoces, pero la sintaxis tiene algunos trucos modernos y útiles.

#### **Condicionales: `if`, `else if`, `else`**

La estructura es idéntica a la de Java.

C++

```cpp
int edad = 18;
if (edad >= 18) {
    std::cout << "Es mayor de edad." << std::endl;
} else {
    std::cout << "Es menor de edad." << std::endl;
}
```

**Novedad de C++17: `if` con inicializador**

Esta es una característica fantástica para mantener el código limpio y las variables contenidas en el ámbito donde se necesitan. Puedes declarar e inicializar una variable dentro del propio `if`.

- **Antes (estilo antiguo):**
    
    C++
    
    ```cpp
    // 'puntos' existe fuera del if, "contaminando" el ámbito exterior.
    int puntos = calcularPuntos();
    if (puntos > 100) {
        std::cout << "¡Nivel completado!" << std::endl;
    }
    ```
    
- **Ahora (estilo C++17):**
    
    C++
    
    ```cpp
    // 'puntos' solo existe y es visible DENTRO del if y su else.
    if (int puntos = calcularPuntos(); puntos > 100) {
        std::cout << "¡Nivel completado!" << std::endl;
    }
    // Aquí fuera, la variable 'puntos' ya no existe. ¡Más limpio y seguro!
    ```
    

#### **Condicional Múltiple: `switch`**

Útil cuando tienes múltiples casos para una sola variable. Es muy similar a Java.

Novedad de C++17: [[fallthrough]]

En switch, si omites un break, la ejecución "cae" al siguiente caso (fallthrough). Antes, esto era una fuente de errores. Ahora, C++17 te permite ser explícito, indicando que la caída es intencional.

C++

```cpp
char opcion = 'B';
switch (opcion) {
    case 'A':
        std::cout << "Seleccionaste la opción A." << std::endl;
        break; // No olvides el break!
    case 'B':
        std::cout << "Seleccionaste B. Se ejecutará también C." << std::endl;
        [[fallthrough]]; // AVISO: La caída al siguiente case es intencional.
    case 'C':
        std::cout << "Esto se ejecuta para la opción B y C." << std::endl;
        break;
    default:
        std::cout << "Opción no válida." << std::endl;
        break;
}
```

#### **Bucles: `while`, `do-while`, `for`**

- `while` y `do-while` son sintácticamente idénticos a Java.
    
    C++
    
    ```cpp
    int i = 0;
    while (i < 5) {
        std::cout << i << std::endl;
        i++;
    }
    ```
    
- El bucle `for` clásico también es idéntico.
    
    C++
    
    ```cpp
    for (int j = 0; j < 5; ++j) {
        std::cout << "Iteración: " << j << std::endl;
    }
    // Pequeña nota: Usar ++j (pre-incremento) es a veces un poco más eficiente que j++
    // (post-incremento) para tipos de datos complejos, así que es una buena costumbre.
    ```
    
- La joya de la corona: Range-based for loop (Bucle for de rango)
    
    Esta es la forma moderna, segura y legible de iterar sobre una colección de elementos, muy similar a los bucles for de Python. Deberías preferir esta forma siempre que sea posible.
    
    C++
    
    ```cpp
    #include <vector> // Necesitamos incluir esto para usar std::vector
    
    // std::vector es un "array dinámico". Lo veremos en detalle más adelante.
    // Por ahora, piénsalo como una lista.
    std::vector<int> numeros = {10, 20, 30, 40, 50};
    
    // Para cada 'numero' en la colección 'numeros', haz lo siguiente:
    for (int numero : numeros) {
        std::cout << "El número es: " << numero << std::endl;
    }
    ```
    

---

### **3. Entrada y Salida por Consola (`<iostream>`)**

Ya conoces `std::cout` para la salida. Su contraparte para la entrada es `std::cin`.

- **`std::cin`**: Es el objeto de flujo de entrada estándar (normalmente el teclado).
    
- **`>>`**: Es el **operador de extracción de flujo**. Saca datos del flujo (`cin`) y los guarda en la variable que está a su derecha.
    

**Ejemplo simple**:

C++

```cpp
int edad_usuario {}; // Inicializada a cero
std::cout << "Por favor, introduce tu edad: ";
std::cin >> edad_usuario; // El programa se detendrá aquí esperando tu entrada
std::cout << "Tienes " << edad_usuario << " años." << std::endl;
```

¡Cuidado! El gran problema de std::cin >>

El operador >> deja de leer en cuanto encuentra un espacio en blanco (espacio, tab, enter). Esto causa problemas al leer texto.

C++

```
std::string nombre_completo; // std::string es para texto. Necesitas #include <string>
std::cout << "Introduce tu nombre completo: ";
std::cin >> nombre_completo; // Si escribes "Juan Perez"
std::cout << "Hola, " << nombre_completo << std::endl; // Imprimirá "Hola, Juan"
// "Perez" se quedó en el buffer de entrada, esperando a la siguiente lectura.
```

La solución: std::getline

Para leer una línea completa, incluyendo espacios, se usa la función std::getline.

C++

```
#include <string> // Necesario para std::string

std::string nombre_completo;
std::cout << "Introduce tu nombre completo: ";
std::getline(std::cin, nombre_completo); // Lee toda la línea hasta el 'Enter'
std::cout << "Hola, " << nombre_completo << "!" << std::endl; // Ahora sí funciona
```

**Nota:** A veces, si mezclas `std::cin >> var;` con `std::getline`, puede que necesites limpiar el buffer de entrada. Pero por ahora, centrémonos en el uso correcto.

---

### **4. Ejemplo Completo del Módulo**

Este programa combina todo lo que hemos visto: declaración de variables con tipos modernos y `{}` , entrada/salida con `cin` y `getline`, un `if` con inicializador, y un bucle `for` de rango.

Crea un archivo llamado `registro.cpp` y pega este código:

C++

```
#include <iostream>
#include <string>
#include <vector>
#include <cstdint> // Para usar int32_t

int main() {
    // ---- VARIABLES Y ENTRADA DE DATOS ----
    std::string nombre_usuario {};
    int32_t anio_nacimiento {};

    std::cout << "=== Sistema de Registro Simple ===" << std::endl;
    
    std::cout << "Por favor, introduce tu nombre completo: ";
    // Usamos getline para capturar nombres con espacios
    std::getline(std::cin, nombre_usuario);

    std::cout << "Introduce tu anio de nacimiento: ";
    std::cin >> anio_nacimiento;

    // ---- LÓGICA CON ESTRUCTURAS DE CONTROL ----
    // Usamos 'if' con inicializador (C++17) para calcular la edad
    if (int32_t edad = 2025 - anio_nacimiento; edad >= 18) {
        std::cout << "Hola " << nombre_usuario << ". Tienes " << edad << " anios, eres mayor de edad." << std::endl;
    } else {
        std::cout << "Hola " << nombre_usuario << ". Eres menor de edad." << std::endl;
    }

    // ---- BUCLE DE RANGO PARA PROCESAR DATOS ----
    std::cout << "\nLos caracteres de tu nombre son:" << std::endl;
    // Iteramos sobre cada caracter 'c' en el string 'nombre_usuario'
    for (char c : nombre_usuario) {
        // Imprimimos cada caracter separado por un espacio
        std::cout << c << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

#### **Compilación y Ejecución**

1. Abre la terminal de VSCode en la carpeta donde guardaste `registro.cpp`.
    
2. **Compila** el programa con el siguiente comando:
    
    Bash
    
    ```
    g++ registro.cpp -o registro.exe
    ```
    
3. **Ejecuta** el programa:
    
    Bash
    
    ```
    ./registro.exe
    ```
    

**Salida de ejemplo:**

```
=== Sistema de Registro Simple ===
Por favor, introduce tu nombre completo: Ana Sofia Torres
Introduce tu anio de nacimiento: 2003
Hola Ana Sofia Torres. Tienes 22 anios, eres mayor de edad.

Los caracteres de tu nombre son:
A n a   S o f i a   T o r r e s
```



