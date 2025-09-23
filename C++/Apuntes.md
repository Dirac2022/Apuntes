
### `#ifndef`, `#define`, `#endif`

Estos son **guardas de inclusión** (include guards).  
Sirven para evitar que un mismo archivo de cabecera (`.h`) sea incluido varias veces en un proyecto.

- `#ifndef MATEMATICAS_h` → _If Not Defined_.  
    Pregunta: _¿Ya existe la macro `MATEMATICAS_h`?_
    
- `#define MATEMATICAS_h` → Si no existe, la define.
    
- `#endif` → Marca el final del bloque protegido.
    

👉 Así, si otro archivo vuelve a incluir `matematicas.h`, la macro ya estará definida y el compilador **ignorará** el contenido repetido.


**¿Por qué solo se pone la firma de la función?**

En los **archivos `.h`** se ponen **declaraciones** (firma: tipo de retorno, nombre y parámetros), no la implementación.  
La **implementación** va en un archivo `.cpp`.  
Esto permite separar la **interfaz** (lo que está disponible para usar) de la **implementación** (el código real).

**Ejemplo**

**matematicas.h**

```cpp
#ifndef MATEMATICAS_H
#define MATEMATICAS_H

int sumar(int a, int b);  // Declaración (firma)

#endif
```

**matematicas.cpp**

```cpp
#include "matematicas.h"

int sumar(int a, int b) {  // Implementación
    return a + b;
}
```

**main.cpp**

```cpp
#include <iostream>
#include "matematicas.h"

int main() {
    std::cout << sumar(3, 4) << std::endl;  // Usa la función
}
```

✅ Así se evita duplicación y se organiza el código.

# Compilar y Ejecutar un programa en C++

Se tiene la estructura

```text
MiPrimerPrograma/
├── main.cpp
├── matematicas.h
└── matematicas.cpp
```

**Para compilar en un solo paso:**

```sh
g++ main.cpp matematicas.cpp -o programa.exe
```

- `g++` -> compilador de C++
- `main.cpp matematicas.cpp` -> archivos fuente a compilar
- `-o programa.exe` -> nombre del ejecutable resultante.

**Ejecutar el programa**

```sh
./programa.exe
```

- `./` -> el archivo está en el directorio actual
- `programa.exe` -> ejecutable compilado

**Ejemplo de salida**

```text
El resultado de la suma es 8
```

