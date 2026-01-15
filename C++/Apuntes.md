
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



---

Buena pregunta — vamos a explicarlo claro, con **por qué** importa `noexcept` en el _move constructor_, **qué pasa si no lo pones**, y **cómo aplicarlo correctamente** en tu `CDoubleLinkedList`. Te doy ejemplos reales y recomendaciones prácticas.

---

# 1) ¿Qué significa `noexcept` en un constructor de movimiento?

`noexcept` declara que la función **no lanzará excepciones**. En un `move constructor`:

```cpp
CDoubleLinkedList(CDoubleLinkedList&& other) noexcept { /* ... */ }
```

estás prometiendo: _“este constructor de movimiento no lanzará”_.  
Si a pesar de la promesa termina lanzando, el programa llamará a `std::terminate()` y abortará.

---

# 2) ¿Por qué importa para contenedores (ej. `std::vector`)?

Los contenedores estándar (como `std::vector`) al realojar elementos prefieren **mover** elementos porque es más rápido que copiar. **Pero** sólo usan el _move_ si es _nothrow_:

- Si `T` **es `nothrow` movible** (i.e. `std::is_nothrow_move_constructible<T>::value == true`), `vector` moverá los elementos.
    
- Si **no** es `nothrow` movible, `vector` fallback a **copiar** los elementos (porque la política del contenedor busca garantizar seguridad ante excepciones en la realocación).
    

**Consecuencia práctica:** si tu tipo define un move constructor _sin_ `noexcept`, `std::vector<CDoubleLinkedList>` (u otros contenedores) pueden copiar en vez de mover — pérdida importante de rendimiento y más trabajo (posibles copias profundas).

---

# 3) ¿Qué pasa si marcas `noexcept` y el move lanza?

Si el move realmente lanza a pesar del `noexcept`, el programa termina (`std::terminate`). Por eso sólo debes marcar `noexcept` cuando **estés seguro** de que el código dentro no lanzará (o que lanzar sería un error inaceptable).

---

# 4) Tipos de miembros y `noexcept` implícito

Si no defines `noexcept`, el compilador puede **declarar implícitamente** el move constructor como `noexcept` si todos los movimientos de los miembros también son `noexcept`. Pero si tú defines manualmente el move (como en tu código) y no marcas `noexcept`, entonces **no** será `noexcept` por defecto.

---

# 5) En tu clase `CDoubleLinkedList` — ¿deberías poner `noexcept`?

Veamos lo relevante en tu `move constructor`:

- Mueves punteros `m_pRoot`, `m_pTail` y enteros `m_nElem`: **estos movimientos no lanzan**.
    
- `m_fCompare = std::move(other.m_fCompare);` → depende de `Func`. Si `Func` es, por ejemplo, un `std::function` o un functor cuyo move puede lanzar, entonces el movimiento puede lanzar. Si `Func` es un objeto trivial (p. ej. puntero a función o stateless functor), su move no lanza.
    
- `std::lock_guard<std::mutex> lock(other.m_mutex);` no lanza (bloquear `std::mutex` no lanza excepciones).  
    (Nota: `std::scoped_lock`/`lock_guard` no hacen que el constructor deje de ser `noexcept` — siempre que las operaciones que hagas dentro no lancen).
    

**Por tanto:** puedes marcar `noexcept` _si y sólo si_ las operaciones de movimiento de tus miembros no lanzan (o las envuelves en operaciones que no lanzan). Una opción es usar `noexcept(std::is_nothrow_move_constructible_v<Func>)` para reflejar exactamente la propiedad.

---

# 6) Ejemplo práctico de Move constructor para tu clase

Versión sencilla y segura (supone que `Func` es movible sin lanzar):

```cpp
CDoubleLinkedList(CDoubleLinkedList&& other) noexcept {
    std::lock_guard<std::mutex> lock(other.m_mutex); // sincroniza acceso a 'other'
    m_pRoot    = other.m_pRoot;
    m_pTail    = other.m_pTail;
    m_nElem    = other.m_nElem;
    m_fCompare = std::move(other.m_fCompare);

    other.m_pRoot = nullptr;
    other.m_pTail = nullptr;
    other.m_nElem = 0;
}
```

Mejor aún (sólo `noexcept` cuando `Func` es nothrow-movable):

```cpp
CDoubleLinkedList(CDoubleLinkedList&& other) 
    noexcept(std::is_nothrow_move_constructible_v<Func>)
{
    std::lock_guard<std::mutex> lock(other.m_mutex);
    m_pRoot    = other.m_pRoot;
    m_pTail    = other.m_pTail;
    m_nElem    = other.m_nElem;
    m_fCompare = std::move(other.m_fCompare);

    other.m_pRoot = nullptr;
    other.m_pTail = nullptr;
    other.m_nElem = 0;
}
```

Así el `noexcept` se aplica condicionalmente — buena práctica cuando no estás seguro de `Func`.

---

# 7) ¿Y la sincronización (mutex) en move? ¿Está bien bloquear `other.m_mutex`?

- Bloquear `other.m_mutex` para mover su estado es razonable: estás extrayendo internals de `other` mientras otros hilos podrían usarlo. Eso hace la operación _thread-safe_ respecto a `other` mientras dura el bloqueo.
    
- No bloqueas `this->m_mutex` porque el objeto destino del move está recién creado y no es accesible por otros hilos (salvo casos raros). Bloquear únicamente `other` es suficiente.
    
- `std::lock_guard<std::mutex>` no lanza, así que no impide marcar `noexcept`.
    

Caveat: si hay otras operaciones que pueden bloquear ambos mutexes en orden distinto puedes introducir riesgo de deadlock — aunque en un move típico no es problema porque `this` aún no es visible fuera.

---

# 8) Ejemplo que muestra la diferencia en comportamiento de `std::vector` (move con/without noexcept)

Código ilustrativo:

```cpp
#include <iostream>
#include <vector>

struct A {
    A() = default;
    A(const A&) { std::cout << "copiar\n"; }
    A(A&&) /* noexcept */ { std::cout << "mover\n"; }
};

int main() {
    std::vector<A> v;
    v.reserve(2);
    v.push_back(A{}); // inserta, sin realocación
    // fuerza reallocation: si A::A(A&&) es noexcept, vector moverá,
    // si no es noexcept, vector copiará (si está disponible).
    for (int i = 0; i < 10; ++i) v.push_back(A{});
}
```

- Si `A(A&&) noexcept` → verás muchas “mover”.
    
- Si no es `noexcept` → `std::vector` prefiere copiar (verás “copiar”), perdiendo rendimiento.
    

---

# 9) Ventajas / Desventajas de marcar `noexcept` en tu move

Ventajas:

- **Mejor rendimiento**: contenedores usan move en vez de copy.
    
- **Menos trabajos innecesarios** y menos copias profundas.
    
- **Optimización** por parte del compilador.
    

Desventajas / riesgos:

- Si realmente el move puede lanzar y marcas `noexcept`, fallo → `std::terminate()` (abort).
    
- Si tienes miembros cuyo move puede lanzar (`std::function`, contenedores con asignador que puede lanzar, etc.), no conviene prometer `noexcept` sin comprobar.
    

Recomendación: usar `noexcept(...)` con la expresión basada en traits (`std::is_nothrow_move_constructible_v<Func>` o una conjunción sobre todos los miembros) para que la garantía siga siendo verdadera cuando los miembros sean no-throw.

---

# 10) Consejos prácticos para tu clase

1. **Haz `move ctor` y `move assignment` `noexcept` siempre que sea seguro**.
    
    - Para tipos “managers” que sólo mueven punteros y resetean origen (como tu lista), normalmente es seguro.
        
2. **Usa traits** para condicionar `noexcept` si tienes miembros cuya seguridad depende del tipo `Traits::Func`:
    
    ```cpp
    CDoubleLinkedList(CDoubleLinkedList&& other) 
      noexcept(std::is_nothrow_move_constructible_v<Func>);
    ```
    
3. **Corrige pequeños errores**: en tu código vi una línea faltante de `;` en el move ctor (asegúrate de compilar).
    
4. **Marca también el `move assignment`** como `noexcept` si tiene las mismas propiedades.
    
5. **Prueba**: escribe tests que construyan `std::vector<CDoubleLinkedList<Traits>>` y observa si usa mover o copiar; medir rendimiento si es crítico.
    

---

# 11) Resumen corto y contundente

- `noexcept` en el move: **promesa** de no lanzar.
    
- Si lo pones y **tu move no lanza**, mejor rendimiento (contenedores moverán).
    
- Si lo pones y **tu move lanza**, el programa aborta (`std::terminate`).
    
- Mejor práctica: usar `noexcept(...)` con una expresión basada en `std::is_nothrow_move_constructible_v<...>` para reflejar exactamente cuándo el move es no-throw.
    

---

Si quieres, te hago **dos cosas concretas ahora**:

1. Te devuelvo **una versión corregida** de tu move constructor con la forma recomendada `noexcept(std::is_nothrow_move_constructible_v<Func>)` y con bloqueo correcto del mutex.
    
2. Te doy un **mini-programa** que muestra la diferencia en comportamiento de `std::vector` cuando el move es `noexcept` o no (para que ejecutes y veas “mover” vs “copiar”).
    

¿Quieres que te muestre ya ambas opciones con el código listo para copiar/pegar?