 
# Módulo 1: Introducción y Arquitectura de Tkinter

Tkinter es la librería estándar de Python para crear interfaces gráficas de usuario (GUI). Viene incluida con la mayoría de instalaciones de Python, por lo que no necesitas instalar nada extra.

<h5>¿Qué es Tkinter?</h5>  
Tkinter es un “wrapper” (capa de enlace) en Python para **Tcl/Tk**, que es una librería gráfica escrita en C.  
- **Tcl/Tk**: motor que realmente dibuja ventanas, botones, textos, etc.  
- **Tkinter**: interfaz en Python que permite usar Tcl/Tk con sintaxis Python.  

<h5>Ciclo de vida de una aplicación Tkinter</h5>  

1. Crear ventana principal con `Tk()`.
2. Añadir widgets (botones, etiquetas, entradas de texto, etc.).
3. Organizar widgets con un **geometry manager** (`pack`, `grid`, `place`).
4. Iniciar el bucle principal con `mainloop()`, que mantiene abierta la ventana y responde a eventos.

<h5>Conceptos básicos</h5>  
- **Raíz (root)**: la ventana principal creada con `Tk()`.  
- **Widget**: cada elemento gráfico (botón, label, etc.).  
- **Evento**: acción del usuario (clic, tecla, etc.).  

<h5>Buenas prácticas</h5>  
- Usar `Frame` para dividir la ventana en secciones (ej. cabecera, contenido, pie).  

---

## Ejemplos conceptuales

### Crear ventana principal

```python
# Importar Tkinter
import tkinter as tk

# Crear la ventana principal (raíz de la aplicación)
# Tk() inicializa la librería Tcl/Tk y devuelve la ventana base
ventana = tk.Tk()

# Establecer el título de la ventana principal
# title(texto) muestra el nombre en la barra superior
ventana.title("Mi primera ventana")

# Definir el tamaño inicial de la ventana
# geometry("ancho x alto")
ventana.geometry("400x300")

# Iniciar el bucle principal de eventos
# mainloop() mantiene la ventana abierta y espera interacciones del usuario
ventana.mainloop()
```

---

### Agregar un Label y un Button

```python
import tkinter as tk

ventana = tk.Tk()
ventana.title("Ejemplo Label y Button")
ventana.geometry("300x200")

# Crear un Label (etiqueta de texto)
# Label(padre, text="contenido")
etiqueta = tk.Label(ventana, text="Hola Tkinter")
etiqueta.pack()  # pack() coloca el widget en la ventana

# Crear un Button (botón que ejecuta una acción)
# Button(padre, text="contenido", command=funcion)
def saludar():
    print("¡Hola desde el botón!")

boton = tk.Button(ventana, text="Presióname", command=saludar)
boton.pack()

ventana.mainloop()
```

---

## Ejemplo integrador del módulo 1

Este ejemplo reúne lo visto: crear ventana, añadir un label, un botón y usar un frame para organización.

```python
import tkinter as tk

# Crear ventana principal
ventana = tk.Tk()
ventana.title("Ejemplo integrador - Módulo 1")
ventana.geometry("400x200")

# Crear un Frame superior
frame_superior = tk.Frame(ventana)
frame_superior.pack(pady=10)

# Agregar un Label en el Frame superior
label = tk.Label(frame_superior, text="Bienvenido a Tkinter")
label.pack()

# Crear un Frame inferior
frame_inferior = tk.Frame(ventana)
frame_inferior.pack(pady=20)

# Función que se ejecuta al presionar el botón
def accion():
    print("Botón presionado")

# Botón en el Frame inferior
boton = tk.Button(frame_inferior, text="Click aquí", command=accion)
boton.pack()

# Ejecutar la aplicación
ventana.mainloop()
```

En este ejemplo integrador:

* Creamos la ventana principal.
* Usamos dos `Frame` para organizar los widgets.
* Colocamos un `Label` arriba y un `Button` abajo.
* El botón imprime un mensaje en la consola.

---


Perfecto 👌, seguimos con el **Módulo 2: Widgets Fundamentales**. Aquí vamos a ver los widgets que usaremos más adelante para el visor de PDF y además añadimos algunos extras comunes (Checkbuttons, Radiobuttons y Menús).

---

# Módulo 2: Widgets Fundamentales

En Tkinter, los **widgets** son los bloques básicos de construcción de una interfaz gráfica. Cada widget tiene:

* Un **padre** (por lo general la ventana raíz o un `Frame`).
* **Propiedades** (texto, color, tamaño, etc.).
* **Métodos** (por ejemplo, `.pack()`, `.get()`, `.insert()`).

---

## Label

Sirve para mostrar texto o imágenes estáticas.

```python
import tkinter as tk

ventana = tk.Tk() # Crea la ventana principal
ventana.title("Ejemplo Label")
ventana.geometry("300x100") # Define el ancho x alto de la ventana

# Label: Widget para mostrar texto o imágenes estáticas
# padre: ventana contenedora (ventana)
# text: texto a mostrar en la etiqueta
etiqueta = tk.Label(ventana, text="Hola, soy un Label")
# pack(): organiza el widget en la ventana (posición por defecto: centro superior)
etiqueta.pack()

ventana.mainloop()
```

---

## Button

Botón que ejecuta una función cuando es presionado.

```python
import tkinter as tk

ventana = tk.Tk()
ventana.title("Ejemplo Button")
ventana.geometry("300x100")

# Función callback: se ejecuta al presionar el botón
def saludar():
    print("Hola desde el botón")

# Button: Widget interactivo que ejecuta comandos
# text: texto que aparece en el botón
# command: función a ejecutar al hacer clic (sin paréntesis)
boton = tk.Button(ventana, text="Presionar", command=saludar)
boton.pack()

ventana.mainloop()
```

---

## Entry

Campo de entrada para texto corto (ej. ruta de archivo, nombre).

```python
import tkinter as tk

ventana = tk.Tk()
ventana.title("Ejemplo Entry")
ventana.geometry("300x120")

# Entry: Campo de entrada de texto de una línea
# Permite ingresar y editar texto corto
entrada = tk.Entry(ventana)
entrada.pack() # Empaqueta el campo de entrada

# .get(): método para obtener el texto ingresado en el Entry
def mostrar_texto():
    print("Texto ingresado:", entrada.get()) # get() devuelve el contenido como string

boton = tk.Button(ventana, text="Mostrar", command=mostrar_texto)
boton.pack()

ventana.mainloop()
```

---

## Text

Área de texto grande, permite múltiples líneas y edición.

```python
import tkinter as tk

ventana = tk.Tk()
ventana.title("Ejemplo Text")
ventana.geometry("400x200")

# Text: Área de texto multilínea editable
# height: número de líneas visibles (5)
# width: ancho en caracteres (40)
texto = tk.Text(ventana, height=5, width=40)
texto.pack()

# .insert(): inserta texto en una posición específica
# tk.END: constante que representa el final del contenido actual
# "\n": carácter de nueva línea
texto.insert(tk.END, "Escribe o edita aquí.\nSegunda línea.")

ventana.mainloop()
```

---

## Canvas

Área flexible para dibujar, mostrar imágenes o contenido desplazable.

```python
import tkinter as tk

ventana = tk.Tk()
ventana.title("Ejemplo Canvas")
ventana.geometry("400x300")

# Canvas: Área para dibujar gráficos, imágenes y formas
# width, height: dimensiones en píxeles del área de dibujo
# bg: color de fondo (background)
canvas = tk.Canvas(ventana, width=300, height=200, bg="white")
canvas.pack()

# create_line(): dibuja una línea desde (x1,y1) hasta (x2,y2)
# fill: color de la línea
canvas.create_line(10, 10, 200, 100, fill="blue")

# create_rectangle(): dibuja un rectángulo
# outline: color del borde del rectángulo
canvas.create_rectangle(50, 50, 150, 150, outline="red")

ventana.mainloop()
```

---

## Scrollbar

Permite desplazarse en widgets grandes (ej. `Text`, `Canvas`).

```python
import tkinter as tk

ventana = tk.Tk()
ventana.title("Ejemplo Scrollbar")
ventana.geometry("400x200")

# Text: Área de texto multilínea
# wrap="word": ajusta el texto por palabras (no corta palabras al final de línea)
texto = tk.Text(ventana, wrap="word")
# pack(): organiza el widget con parámetros específicos
# side="left": posiciona a la izquierda del espacio disponible
# fill="both": expande para llenar tanto horizontal como verticalmente
# expand=True: permite que el widget se expanda si hay espacio extra
texto.pack(side="left", fill="both", expand=True)

# Scrollbar: Barra de desplazamiento vertical
# command=texto.yview: conecta el scroll al movimiento vertical del texto
scroll = tk.Scrollbar(ventana, command=texto.yview)
# pack(): organiza la scrollbar
# side="right": posiciona a la derecha del espacio disponible
# fill="y": expande verticalmente para llenar la altura disponible
scroll.pack(side="right", fill="y")

# .config(): configura propiedades del widget después de su creación
# yscrollcommand=scroll.set: conecta el texto a la scrollbar (actualiza posición)
texto.config(yscrollcommand=scroll.set)

# Insertar mucho texto
for i in range(50):
	# tk.END: inserta al final del contenido existente
    texto.insert(tk.END, f"Línea {i+1}\n")

ventana.mainloop()
```

---

## Checkbutton

Casilla de verificación (opción múltiple).

```python
import tkinter as tk

ventana = tk.Tk()
ventana.title("Ejemplo Checkbutton")
ventana.geometry("300x150")

# IntVar: Variable de control para valores enteros
# Almacena 0 (desmarcado) o 1 (marcado)
opcion = tk.IntVar()

# Checkbutton: Casilla de verificación (selección múltiple)
# text: texto descriptivo junto a la casilla
# variable: variable asociada al estado del checkbutton
check = tk.Checkbutton(ventana, text="Aceptar términos", variable=opcion)
check.pack()

# .get(): obtiene el valor actual de la variable IntVar
def mostrar():
    print("Estado:", opcion.get())  # 1 = marcado, 0 = desmarcado

boton = tk.Button(ventana, text="Ver estado", command=mostrar)
boton.pack()

ventana.mainloop()
```

---

## Radiobutton

Selección única entre varias opciones.

```python
import tkinter as tk

ventana = tk.Tk()
ventana.title("Ejemplo Radiobutton")
ventana.geometry("300x150")

# StringVar: Variable de control para cadenas de texto
# value="Opción 1": establece el valor inicial por defecto
seleccion = tk.StringVar(value="Opción 1")

# Radiobutton: Botón de opción única (selección excluyente)
# variable: variable compartida entre todos los radiobuttons del grupo
# value: valor único que representa esta opción específica
rb1 = tk.Radiobutton(ventana, text="Opción 1", variable=seleccion, value="Opción 1")
rb1.pack()
rb2 = tk.Radiobutton(ventana, text="Opción 2", variable=seleccion, value="Opción 2")
rb2.pack()

# Botón para mostrar selección
def mostrar():
    # .get(): obtiene el valor de la variable StringVar (la opción seleccionada)
    print("Seleccionado:", seleccion.get())

boton = tk.Button(ventana, text="Mostrar", command=mostrar)
boton.pack()

ventana.mainloop()
```

---

## Menú

Barra de menú con opciones.

```python
import tkinter as tk

ventana = tk.Tk()
ventana.title("Ejemplo Menu")
ventana.geometry("300x200")

# Crear barra de menú
barra_menu = tk.Menu(ventana)
# .config(menu=barra_menu): establece la barra de menú para la ventana
ventana.config(menu=barra_menu)

# Menu desplegable: submenú dentro de la barra principal
# tearoff=0: elimina la línea punteada que permite separar el menú
menu_archivo = tk.Menu(barra_menu, tearoff=0)
# add_command(): añade opciones ejecutables al menú
menu_archivo.add_command(label="Nuevo") # label: texto que aparece en el menú
menu_archivo.add_command(label="Abrir")
# add_separator(): añade una línea divisoria entre opciones
menu_archivo.add_separator() 
# command=ventana.quit: función que se ejecuta al seleccionar esta opción
menu_archivo.add_command(label="Salir", command=ventana.quit)

# Añadir menú a la barra
barra_menu.add_cascade(label="Archivo", menu=menu_archivo)

ventana.mainloop()
```

---

## Ejemplo integrador del Módulo 2

Ahora reunimos varios widgets en una sola ventana.

```python
import tkinter as tk

ventana = tk.Tk()
ventana.title("Ejemplo Integrador - Módulo 2")
ventana.geometry("500x400")

# Label: Texto descriptivo estático
label = tk.Label(ventana, text="Visor de Widgets")
# pady=5: añade 5 píxeles de espacio vertical arriba y abajo
label.pack(pady=5)

# Entry: Campo para ingresar texto de una línea
entrada = tk.Entry(ventana)
entrada.pack(pady=5)

# Función que obtiene texto del Entry y lo inserta en el Text
def mostrar_texto():
    # .get(): obtiene el texto del Entry
    # tk.END: inserta al final del contenido existente en el Text
    # + "\n": añade salto de línea
    texto.insert(tk.END, entrada.get() + "\n")

# Button: Ejecuta la función mostrar_texto al hacer clic
boton = tk.Button(ventana, text="Agregar al Text", command=mostrar_texto)
boton.pack(pady=5)

# Frame: Contenedor para organizar widgets de forma agrupada
frame_texto = tk.Frame(ventana)
# fill="both": expande para llenar espacio horizontal y vertical
# expand=True: permite que el frame se expanda si hay espacio disponible
frame_texto.pack(pady=5, fill="both", expand=True)

# Text: Área de texto multilínea con scroll
texto = tk.Text(frame_texto, wrap="word")
# side="left": posiciona a la izquierda dentro del frame
# fill="both": expande para llenar el frame horizontal y verticalmente
# expand=True: permite expansión dentro del frame
texto.pack(side="left", fill="both", expand=True)

# Scrollbar: Barra de desplazamiento conectada al Text
scroll = tk.Scrollbar(frame_texto, command=texto.yview)
# side="right": posiciona a la derecha dentro del frame
# fill="y": expande verticalmente para llenar la altura del frame
scroll.pack(side="right", fill="y")

# Configuración bidireccional: Text notifica a Scrollbar de cambios
texto.config(yscrollcommand=scroll.set)

# Checkbutton: Opción de activar/desactivar
opcion = tk.IntVar()  # Variable de control entera
check = tk.Checkbutton(ventana, text="Activar opción extra", variable=opcion)
check.pack(pady=5)

# Radiobuttons: Selección única entre opciones
seleccion = tk.StringVar(value="Opción A")  # Variable de control string
rb1 = tk.Radiobutton(ventana, text="Opción A", variable=seleccion, value="Opción A")
rb1.pack()
rb2 = tk.Radiobutton(ventana, text="Opción B", variable=seleccion, value="Opción B")
rb2.pack()

# Menú: Barra de menú con opciones
barra_menu = tk.Menu(ventana)
ventana.config(menu=barra_menu)
menu_archivo = tk.Menu(barra_menu, tearoff=0)
menu_archivo.add_command(label="Salir", command=ventana.quit)
barra_menu.add_cascade(label="Archivo", menu=menu_archivo)

ventana.mainloop()
```


Este integrador incluye:

* `Label`, `Entry`, `Button`, `Text` con `Scrollbar`.
* `Checkbutton` y `Radiobutton`.
* Un `Menu` básico.

---

Perfecto 🙌, entendido. Ahora seguimos con el **Módulo 3: Layout y Organización**.
Aquí veremos cómo organizar widgets en la ventana, usando los **geometry managers** (`pack`, `grid`, `place`) y el uso de `Frame` para estructurar secciones.
Voy a respetar tu indicación: solo comentar métodos, parámetros u objetos que no se han visto en módulos anteriores.

---

# Módulo 3: Layout y Organización

En Tkinter, los **geometry managers** controlan cómo se colocan los widgets en la ventana o dentro de un `Frame`. Son **exclusivos entre sí**, es decir, no puedes usar `pack` y `grid` en el mismo contenedor.

---

## pack()

Distribuye widgets en bloques, uno tras otro, en una dirección (vertical u horizontal).

```python
import tkinter as tk

ventana = tk.Tk()
ventana.title("Ejemplo pack()")
ventana.geometry("300x200")

# pack(side) permite indicar en qué lado se coloca el widget
label1 = tk.Label(ventana, text="Arriba")
label1.pack(side="top")

label2 = tk.Label(ventana, text="Izquierda")
label2.pack(side="left")

label3 = tk.Label(ventana, text="Derecha")
label3.pack(side="right")

label4 = tk.Label(ventana, text="Abajo")
label4.pack(side="bottom")

ventana.mainloop()
```

---

## grid()

Coloca widgets en filas y columnas, como si fuera una tabla.

```python
import tkinter as tk

ventana = tk.Tk()
ventana.title("Ejemplo grid()")
ventana.geometry("300x200")

# grid(row, column) coloca un widget en una celda específica
tk.Label(ventana, text="Usuario:").grid(row=0, column=0)
entrada1 = tk.Entry(ventana)
entrada1.grid(row=0, column=1)

tk.Label(ventana, text="Contraseña:").grid(row=1, column=0)
entrada2 = tk.Entry(ventana, show="*")  # show="*" oculta caracteres
entrada2.grid(row=1, column=1)

boton = tk.Button(ventana, text="Ingresar")
boton.grid(row=2, column=0, columnspan=2)  # columnspan expande el widget en varias columnas

ventana.mainloop()
```

---

## place()

Permite ubicar widgets en coordenadas absolutas (x, y). Es menos flexible porque no se adapta al cambio de tamaño de la ventana.

```python
import tkinter as tk

ventana = tk.Tk()
ventana.title("Ejemplo place()")
ventana.geometry("300x200")

# place(x, y) fija posición absoluta en píxeles
label = tk.Label(ventana, text="Texto en (50,50)")
label.place(x=50, y=50)

boton = tk.Button(ventana, text="Botón en (150,100)")
boton.place(x=150, y=100)

ventana.mainloop()
```

---

## Uso de Frame para organizar secciones

Un `Frame` es un contenedor dentro de la ventana, útil para dividir la interfaz en partes (cabecera, contenido, pie).

```python
import tkinter as tk

ventana = tk.Tk()
ventana.title("Ejemplo con Frames")
ventana.geometry("400x300")

# Frame superior (cabecera)
frame_superior = tk.Frame(ventana, bg="lightblue", height=50)
frame_superior.pack(fill="x")  # fill="x" hace que el frame ocupe todo el ancho

# Frame central (contenido)
frame_central = tk.Frame(ventana, bg="white")
frame_central.pack(fill="both", expand=True)  # expand=True permite crecer con la ventana

# Frame inferior (botones de navegación)
frame_inferior = tk.Frame(ventana, bg="lightgray", height=50)
frame_inferior.pack(fill="x")

# Widgets en cada frame
tk.Label(frame_superior, text="Menú arriba").pack()
tk.Label(frame_central, text="Área de contenido").pack()
tk.Button(frame_inferior, text="Anterior").pack(side="left", padx=10)
tk.Button(frame_inferior, text="Siguiente").pack(side="right", padx=10)

ventana.mainloop()
```

---

## Ejemplo integrador del Módulo 3

Ahora unimos todo: `pack`, `grid`, `place` y `Frame` en una misma aplicación pequeña.

```python
import tkinter as tk

ventana = tk.Tk()
ventana.title("Ejemplo Integrador - Módulo 3")
ventana.geometry("400x300")

# Frame superior con pack()
frame_superior = tk.Frame(ventana, bg="lightblue", height=40)
frame_superior.pack(fill="x")
tk.Label(frame_superior, text="Cabecera con pack").pack()

# Frame central con grid()
frame_central = tk.Frame(ventana, bg="white")
frame_central.pack(fill="both", expand=True, pady=10)

tk.Label(frame_central, text="Usuario:").grid(row=0, column=0, padx=5, pady=5)
entrada1 = tk.Entry(frame_central)
entrada1.grid(row=0, column=1, padx=5, pady=5)

tk.Label(frame_central, text="Clave:").grid(row=1, column=0, padx=5, pady=5)
entrada2 = tk.Entry(frame_central, show="*")
entrada2.grid(row=1, column=1, padx=5, pady=5)

# Botón usando place() dentro del frame central
boton = tk.Button(frame_central, text="Ingresar")
boton.place(x=150, y=80)

# Frame inferior con pack()
frame_inferior = tk.Frame(ventana, bg="lightgray", height=40)
frame_inferior.pack(fill="x", side="bottom")
tk.Button(frame_inferior, text="Salir", command=ventana.quit).pack(side="right", padx=10)

ventana.mainloop()
```

Este integrador muestra:

* `Frame` para separar secciones.
* `pack()` en cabecera y pie.
* `grid()` en el formulario central.
* `place()` para un botón puntual.


---

# **Módulo 4: Eventos y Callbacks en Tkinter**

Un **evento** en Tkinter es cualquier acción que ocurre en la interfaz gráfica, como un clic de ratón, pulsar una tecla o redimensionar la ventana.
Un **callback** es una función que se ejecuta automáticamente cuando ocurre un evento.

En Tkinter, hay **dos formas principales** de manejar eventos:

1. Usando el **parámetro `command`** en widgets como `Button`, `Checkbutton`, `Menu`, etc.
2. Usando el método **`.bind(evento, función)`** para asociar eventos más específicos (ej. teclado, ratón).

---

<h5>Uso de `command`</h5>

* Se usa en botones u otros widgets que aceptan acciones directas.
* Solo se pasa la **referencia** a la función, no se la llama con paréntesis.
* La función puede devolver valores, pero generalmente se usa para actualizar la interfaz o el estado del programa.

```python
import tkinter as tk

# Crear ventana principal
ventana = tk.Tk()

# Definir una función callback
# Esta función se ejecuta al presionar el botón
def saludar():
    # Devuelve un valor pero también actualiza interfaz
    return "Hola desde el botón"

# Crear un botón con command
boton = tk.Button(ventana, text="Saludar", command=saludar)
boton.pack()

ventana.mainloop()
```

Comentarios:

* `command=saludar` → ejecuta `saludar()` al presionar el botón.
* Si la función devuelve un valor, este no aparece directamente en pantalla. Para usarlo, necesitamos asignarlo o mostrarlo en un widget.



<h5>Uso de `.bind()`</h5>

* Se usa para asociar un **evento específico** a un widget.
* Sintaxis:

  ```python
  widget.bind("<evento>", funcion)
  ```
* La función recibe siempre un **objeto `event`** con información del evento.

Ejemplo:

```python
import tkinter as tk

ventana = tk.Tk()

def tecla_presionada(event):
    # event.keysym → nombre de la tecla (ej: 'a', 'Return', 'Escape')
    etiqueta.config(text=f"Tecla presionada: {event.keysym}")

etiqueta = tk.Label(ventana, text="Presiona una tecla")
etiqueta.pack()

# Asociar evento de teclado
ventana.bind("<Key>", tecla_presionada)

ventana.mainloop()
```

Comentarios:

* `<Key>` → cualquier tecla.
* `event.keysym` → obtiene el nombre de la tecla.
* Ejemplos comunes de eventos:

  * `"<Button-1>"` → clic izquierdo.
  * `"<Button-3>"` → clic derecho.
  * `"<Double-Button-1>"` → doble clic.
  * `"<KeyPress-Return>"` → tecla Enter.
  * `"<Escape>"` → tecla Escape.

---

<h5>Ejemplo integrador</h5>  

Vamos a combinar **command** y **bind**, además de usar funciones con valores de retorno.

```python
import tkinter as tk

class AppEventos:
    def __init__(self, root):
        self.root = root
        self.root.title("Ejemplo de Eventos y Callbacks")

        # Label para mostrar mensajes
        self.etiqueta = tk.Label(root, text="Interacción pendiente...")
        self.etiqueta.pack()

        # Botón que llama a una función con command
        self.boton = tk.Button(root, text="Generar saludo", command=self.mostrar_saludo)
        self.boton.pack()

        # Vincular evento de teclado
        root.bind("<Key>", self.mostrar_tecla)

    # Función que retorna un valor y lo usa
    def generar_saludo(self):
        return "¡Hola! Has usado el botón."

    def mostrar_saludo(self):
        mensaje = self.generar_saludo()
        self.etiqueta.config(text=mensaje)

    # Función que maneja eventos de teclado
    def mostrar_tecla(self, event):
        self.etiqueta.config(text=f"Has presionado: {event.keysym}")

# Crear ventana principal
ventana = tk.Tk()
app = AppEventos(ventana)
ventana.mainloop()
```

Comentarios clave:

* `command=self.mostrar_saludo` → ejecuta el callback sin parámetros.
* `root.bind("<Key>", self.mostrar_tecla)` → cualquier tecla se envía a `mostrar_tecla(event)`.
* `event.keysym` permite identificar la tecla.
* `generar_saludo()` retorna un string, y `mostrar_saludo()` lo usa para actualizar la interfaz.

---



# Módulo 5: Manejo de Archivos en Tkinter

En aplicaciones gráficas es común trabajar con archivos. Tkinter no puede procesar archivos por sí mismo, pero sí permite abrir cuadros de diálogo del sistema operativo mediante el submódulo **`filedialog`**.

Con `filedialog` podemos seleccionar archivos, directorios, o guardar archivos. El más usado es **`askopenfilename()`**, que abre una ventana para elegir un archivo y devuelve la ruta como cadena de texto.

<h5>filedialog.askopenfilename()</h5>  

- **`title`**: texto que aparece como título de la ventana.  
- **`filetypes`**: tupla que restringe los tipos de archivos visibles. Ejemplo: `[("Archivos PDF", "*.pdf")]`.  
- **Valor de retorno**: ruta absoluta del archivo seleccionado en formato string.  

---

### Ejemplo directo: abrir cualquier archivo

```python
import tkinter as tk              # Importa Tkinter
from tkinter import filedialog    # Importa el submódulo filedialog

# Crea la ventana principal
root = tk.Tk()

# Define una función para abrir un archivo
def abrir_archivo():
    # Abre un cuadro de diálogo para seleccionar archivo
    ruta = filedialog.askopenfilename(
        title="Selecciona un archivo",                 # Título de la ventana
        filetypes=[("Archivos de texto", "*.txt"),     # Permite .txt
                   ("Todos los archivos", "*.*")]      # Permite cualquier archivo
    )
    # Imprime en consola la ruta seleccionada
    print(ruta)

# Crea un botón que ejecuta la función anterior
boton = tk.Button(root, text="Abrir archivo", command=abrir_archivo)
boton.pack(pady=10)  # Empaqueta el botón con espacio vertical

# Inicia el bucle principal
root.mainloop()
```

---

<h5>Selección específica de PDF</h5>  
Podemos limitar la selección solo a PDFs cambiando el parámetro `filetypes`.

```python
import tkinter as tk
from tkinter import filedialog

root = tk.Tk()

def seleccionar_pdf():
    # Abre un cuadro de diálogo limitado a PDF
    ruta_pdf = filedialog.askopenfilename(
        title="Selecciona un archivo PDF",           # Título de la ventana
        filetypes=[("Archivos PDF", "*.pdf")]        # Solo archivos PDF
    )
    print(ruta_pdf)  # Imprime la ruta seleccionada

btn = tk.Button(root, text="Seleccionar PDF", command=seleccionar_pdf)
btn.pack(pady=5)

root.mainloop()
```

---

<h5>Lectura de PDF con librerías externas (concepto)</h5>  
Tkinter no interpreta PDFs, pero podemos usar librerías externas:

* **PyPDF2**: simple, para texto básico.
* **pdfplumber**: más potente, útil si el PDF contiene tablas o formatos complejos.

Ejemplo conceptual con PyPDF2 (sin GUI, solo ilustración):

```python
import PyPDF2

# Abre el archivo PDF en modo lectura binaria
with open("ejemplo.pdf", "rb") as archivo:
    lector = PyPDF2.PdfReader(archivo)       # Crea un lector de PDF
    pagina = lector.pages[0]                 # Obtiene la primera página
    texto = pagina.extract_text()            # Extrae el texto de la página
    print(texto)                             # Imprime el contenido
```

---

<h5>Mostrar contenido en Tkinter</h5>  
Una vez que se obtiene el texto, se puede insertar en un widget `Text` o `Canvas`.  
Ejemplo básico con `Text`:

```python
import tkinter as tk

root = tk.Tk()

# Crea un área de texto
text_area = tk.Text(root, height=10, width=50)
text_area.pack()

# Inserta texto dentro del área
text_area.insert(tk.END, "Aquí iría el contenido extraído de un PDF.")

root.mainloop()
```

---

## Ejemplo integrador del módulo 5

Este ejemplo abre un cuadro de diálogo, selecciona un PDF y muestra la ruta dentro de un `Text`.

```python
import tkinter as tk
from tkinter import filedialog

root = tk.Tk()
root.title("Visor de PDF - Ejemplo integrador")

def seleccionar_pdf():
    ruta_pdf = filedialog.askopenfilename(
        title="Selecciona un PDF",
        filetypes=[("Archivos PDF", "*.pdf")]
    )
    if ruta_pdf:
        text_area.delete("1.0", tk.END)       # Limpia el área
        text_area.insert(tk.END, ruta_pdf)    # Inserta la ruta seleccionada

btn = tk.Button(root, text="Abrir PDF", command=seleccionar_pdf)
btn.pack(pady=5)

text_area = tk.Text(root, height=5, width=50)
text_area.pack(pady=5)

root.mainloop()
```

---

Perfecto, continuemos con el **Módulo 6: Widgets Avanzados para Navegación**, siguiendo las consideraciones que mencionaste: teoría clara, explicación de cada objeto/método/parámetro, ejemplos cortos y documentados línea por línea, y al final un ejemplo integrador sencillo.

---

# Módulo 6: Widgets Avanzados para Navegación

En este módulo veremos cómo manejar **contenido largo o paginado**, como un PDF, usando **scrollbars** y **botones de navegación**.

<h5>Scrollbar + Text</h5>  
El widget **`Scrollbar`** permite navegar contenido en widgets que lo soporten (como `Text` o `Canvas`).  

* Se crea con `tk.Scrollbar(root, orient="vertical")`.
* Se asocia al widget principal con métodos:

  * `yscrollcommand` en `Text` o `Canvas` (indica que use la scrollbar).
  * `config(command=widget.yview)` en la `Scrollbar` (define qué moverá).

Ejemplo con `Text` + `Scrollbar`:

```python
import tkinter as tk

root = tk.Tk()

# Crea un widget Text con soporte de scroll
text_area = tk.Text(root, wrap="word", width=40, height=10, yscrollcommand=lambda *args: scrollbar.set(*args))
text_area.pack(side="left", fill="both", expand=True)

# Crea la barra de scroll vertical
scrollbar = tk.Scrollbar(root, orient="vertical", command=text_area.yview)
scrollbar.pack(side="right", fill="y")

# Inserta texto de prueba largo
for i in range(50):
    text_area.insert(tk.END, f"Línea {i+1}\n")

root.mainloop()
```

---

<h5>Canvas + Frame + Scrollbar</h5>  
`Canvas` es más flexible: permite mostrar imágenes, gráficos, y dentro de él podemos **empaquetar un `Frame` desplazable**.  

* `Canvas.create_window()` crea un espacio dentro del lienzo para un `Frame`.
* Se conecta con `Scrollbar` de forma similar al caso anterior.

Ejemplo: un Frame desplazable dentro de un Canvas:

```python
import tkinter as tk

root = tk.Tk()

# Crea un canvas
canvas = tk.Canvas(root, width=300, height=200)
canvas.pack(side="left", fill="both", expand=True)

# Barra de scroll vertical
scrollbar = tk.Scrollbar(root, orient="vertical", command=canvas.yview)
scrollbar.pack(side="right", fill="y")

# Asocia el scroll al canvas
canvas.configure(yscrollcommand=scrollbar.set)

# Frame interno dentro del canvas
frame = tk.Frame(canvas)
canvas.create_window((0, 0), window=frame, anchor="nw")

# Agrega muchos labels dentro del frame
for i in range(30):
    tk.Label(frame, text=f"Elemento {i+1}").pack()

# Ajusta el scroll según contenido
frame.update_idletasks()
canvas.config(scrollregion=canvas.bbox("all"))

root.mainloop()
```

---

<h5>Botones de navegación</h5>  
Para documentos paginados (como un PDF), se usan botones **Anterior** y **Siguiente** que cambian un índice de página.  

Ejemplo conceptual con texto simulado:

```python
import tkinter as tk

root = tk.Tk()

# Simulamos un "documento" con varias páginas de texto
paginas = [
    "Página 1: Introducción al documento",
    "Página 2: Contenido principal",
    "Página 3: Conclusiones"
]
indice_actual = 0  # Página inicial

# Área de texto
text_area = tk.Text(root, width=40, height=5)
text_area.pack()
text_area.insert(tk.END, paginas[indice_actual])

# Función para cambiar de página
def mostrar_pagina(delta):
    global indice_actual
    indice_actual += delta
    indice_actual = max(0, min(len(paginas)-1, indice_actual))  # Controla límites
    text_area.delete("1.0", tk.END)
    text_area.insert(tk.END, paginas[indice_actual])

# Botones de navegación
btn_prev = tk.Button(root, text="Anterior", command=lambda: mostrar_pagina(-1))
btn_prev.pack(side="left", padx=5)

btn_next = tk.Button(root, text="Siguiente", command=lambda: mostrar_pagina(1))
btn_next.pack(side="right", padx=5)

root.mainloop()
```

---

## Ejemplo integrador del módulo 6

Este ejemplo junta todo:

* **Scrollbar + Text** para navegar contenido.
* **Botones** para cambiar de página simulada.

```python
import tkinter as tk

root = tk.Tk()
root.title("Visor con Scroll y Navegación")

# Documento simulado
paginas = [
    "Página 1: Texto introductorio\n" + "Linea extra\n" * 20,
    "Página 2: Texto intermedio\n" + "Más lineas\n" * 20,
    "Página 3: Texto final\n" + "Conclusión\n" * 20
]
indice_actual = 0

# Área de texto con scroll
text_area = tk.Text(root, wrap="word", width=50, height=15, yscrollcommand=lambda *args: scrollbar.set(*args))
text_area.pack(side="left", fill="both", expand=True)

scrollbar = tk.Scrollbar(root, orient="vertical", command=text_area.yview)
scrollbar.pack(side="right", fill="y")

# Muestra página inicial
text_area.insert(tk.END, paginas[indice_actual])

def mostrar_pagina(delta):
    global indice_actual
    indice_actual += delta
    indice_actual = max(0, min(len(paginas)-1, indice_actual))
    text_area.delete("1.0", tk.END)
    text_area.insert(tk.END, paginas[indice_actual])

# Botones de navegación
frame_botones = tk.Frame(root)
frame_botones.pack(fill="x", pady=5)

tk.Button(frame_botones, text="Anterior", command=lambda: mostrar_pagina(-1)).pack(side="left", padx=5)
tk.Button(frame_botones, text="Siguiente", command=lambda: mostrar_pagina(1)).pack(side="right", padx=5)

root.mainloop()
```

---


Perfecto, vamos con el **Módulo 7: Integración y Buenas Prácticas**, cerrando el curso express y preparando las bases para un visor de PDF estructurado.

---

# Módulo 7: Integración y Buenas Prácticas

Hasta ahora hemos trabajado con ejemplos pequeños y separados, pero cuando la aplicación crece es fundamental **organizar el código** para que sea fácil de mantener y ampliar.

La mejor manera en Tkinter es usar **clases** para encapsular la lógica de la interfaz y separar funciones específicas en métodos cortos.

---

<h5>Separación en clases</h5>  
Creamos una clase principal que hereda de `tk.Tk` o que recibe un objeto `tk.Tk` como raíz.  
Dentro de ella:  
- Definimos los **widgets principales**.  
- Creamos **métodos** para abrir archivos, mostrar páginas, navegar, etc.  
- Mantenemos un índice de página como atributo de la clase.  

---

<h5>Funciones cortas y claras</h5>  
Ejemplos:  
- `abrir_pdf()`: abre el archivo PDF.  
- `mostrar_pagina()`: muestra el texto o imagen de la página.  
- `navegar()`: cambia el índice y actualiza la vista.  

---

<h5>Evitar mezclar lógica</h5>  
- Tkinter se encarga de la **interfaz** (ventanas, botones, texto).  
- Librerías externas (PyPDF2, pdfplumber) se encargan de la **lectura del PDF**.  
- El código debe mantener esta separación.  

---

<h5>Extensibilidad</h5>  
Un patrón común es añadir un menú (`Menu`) con opciones como:  
- Abrir archivo.  
- Salir.  
- Ayuda.  

Esto se hace con `tk.Menu` y `add_command()`.

---

## Ejemplo integrador del módulo 7

Aplicación organizada en una clase, con menús, botones y área de texto para mostrar contenido simulado de un PDF.

```python
import tkinter as tk
from tkinter import filedialog

class PDFViewerApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Visor PDF - Demo")
        
        # Índice de página actual
        self.indice_actual = 0
        # Documento simulado (en práctica se usaría PyPDF2 o pdfplumber)
        self.paginas = [
            "Página 1: Introducción\n" + "Texto de prueba\n" * 10,
            "Página 2: Desarrollo\n" + "Más contenido\n" * 10,
            "Página 3: Conclusiones\n" + "Fin del documento\n" * 10
        ]
        
        # Configura la barra de menús
        self._crear_menu()
        # Configura los widgets principales
        self._crear_widgets()
        # Muestra la primera página
        self.mostrar_pagina()
    
    def _crear_menu(self):
        """Crea el menú principal"""
        menubar = tk.Menu(self.root)
        
        menu_archivo = tk.Menu(menubar, tearoff=0)
        menu_archivo.add_command(label="Abrir PDF", command=self.abrir_pdf)
        menu_archivo.add_separator()
        menu_archivo.add_command(label="Salir", command=self.root.quit)
        
        menu_ayuda = tk.Menu(menubar, tearoff=0)
        menu_ayuda.add_command(label="Acerca de", command=self.mostrar_ayuda)
        
        menubar.add_cascade(label="Archivo", menu=menu_archivo)
        menubar.add_cascade(label="Ayuda", menu=menu_ayuda)
        
        self.root.config(menu=menubar)
    
    def _crear_widgets(self):
        """Crea el área de texto con scroll y los botones de navegación"""
        # Área de texto
        self.text_area = tk.Text(self.root, wrap="word", width=60, height=20)
        self.text_area.pack(side="left", fill="both", expand=True)
        
        # Scrollbar
        scrollbar = tk.Scrollbar(self.root, orient="vertical", command=self.text_area.yview)
        scrollbar.pack(side="right", fill="y")
        self.text_area.config(yscrollcommand=scrollbar.set)
        
        # Frame inferior con botones de navegación
        frame_botones = tk.Frame(self.root)
        frame_botones.pack(fill="x", pady=5)
        
        tk.Button(frame_botones, text="Anterior", command=lambda: self.navegar(-1)).pack(side="left", padx=5)
        tk.Button(frame_botones, text="Siguiente", command=lambda: self.navegar(1)).pack(side="right", padx=5)
    
    def abrir_pdf(self):
        """Abre un archivo PDF (solo muestra la ruta por ahora)"""
        ruta_pdf = filedialog.askopenfilename(
            title="Selecciona un PDF",
            filetypes=[("Archivos PDF", "*.pdf")]
        )
        if ruta_pdf:
            self.text_area.delete("1.0", tk.END)
            self.text_area.insert(tk.END, f"Archivo seleccionado:\n{ruta_pdf}\n\n(Contenido no implementado)")
    
    def mostrar_pagina(self):
        """Muestra el contenido de la página actual"""
        self.text_area.delete("1.0", tk.END)
        self.text_area.insert(tk.END, self.paginas[self.indice_actual])
    
    def navegar(self, delta):
        """Cambia de página"""
        self.indice_actual += delta
        self.indice_actual = max(0, min(len(self.paginas)-1, self.indice_actual))
        self.mostrar_pagina()
    
    def mostrar_ayuda(self):
        """Muestra un cuadro de ayuda simple"""
        ayuda = tk.Toplevel(self.root)
        ayuda.title("Acerca de")
        tk.Label(ayuda, text="Visor PDF Demo\nHecho con Tkinter", padx=20, pady=20).pack()

# Ejecuta la aplicación
if __name__ == "__main__":
    root = tk.Tk()
    app = PDFViewerApp(root)
    root.mainloop()
```

---

Este ejemplo reúne:

* Separación en clase `PDFViewerApp`.
* Menús (`Menu`).
* Área de texto con scroll (`Text + Scrollbar`).
* Botones de navegación con índice de página.
* Funciones cortas y claras (`abrir_pdf`, `mostrar_pagina`, `navegar`).

---

Perfecto, entendido.
Si el **Menu** ya lo expliqué antes, entonces lo reemplazo y en su lugar incluyo otro complemento útil que no hemos visto: **Scale (deslizador numérico)**, que sirve para seleccionar valores dentro de un rango.

Aquí te dejo el **módulo final revisado**:

---

# **Módulo Final: Diálogos y Complementos Útiles en Tkinter**

Este módulo cierra el curso mostrando herramientas adicionales que enriquecen las aplicaciones: **ventanas de diálogo**, **ventanas secundarias (Toplevel)** y **sliders (Scale)**.


<h5>messagebox</h5>

Sirve para mostrar mensajes emergentes.
Se importa desde `tkinter.messagebox`.

Métodos más usados:

* `showinfo(title, message)` → información.
* `showwarning(title, message)` → advertencia.
* `showerror(title, message)` → error.
* `askyesno(title, message)` → devuelve `True` o `False`.
* `askokcancel(title, message)` → devuelve `True` o `False`.

```python
import tkinter as tk
from tkinter import messagebox

ventana = tk.Tk()

def mostrar_info():
    # Ventana emergente de información
    messagebox.showinfo("Información", "Este es un mensaje informativo.")

boton = tk.Button(ventana, text="Mostrar Mensaje", command=mostrar_info)
boton.pack()

ventana.mainloop()
```

---

<h5>simpledialog</h5>

Permite **pedir datos** al usuario.
Se importa desde `tkinter.simpledialog`.

Métodos más usados:

* `askstring(title, prompt)` → pide texto.
* `askinteger(title, prompt)` → pide un número entero.
* `askfloat(title, prompt)` → pide un número decimal.

```python
import tkinter as tk
from tkinter import simpledialog

ventana = tk.Tk()

def pedir_nombre():
    # Abre ventana emergente solicitando texto
    nombre = simpledialog.askstring("Entrada", "Escribe tu nombre:")
    if nombre:
        etiqueta.config(text=f"Hola, {nombre}!")

etiqueta = tk.Label(ventana, text="Esperando nombre...")
etiqueta.pack()

boton = tk.Button(ventana, text="Ingresar nombre", command=pedir_nombre)
boton.pack()

ventana.mainloop()
```

---

<h5>Toplevel</h5>

Sirve para abrir una **ventana secundaria independiente**.
Se usa mucho para mostrar detalles adicionales o formularios.

```python
import tkinter as tk

ventana = tk.Tk()

def abrir_ventana():
    # Crear ventana secundaria
    nueva = tk.Toplevel(ventana)
    nueva.title("Ventana secundaria")
    tk.Label(nueva, text="Soy otra ventana").pack()

boton = tk.Button(ventana, text="Abrir nueva ventana", command=abrir_ventana)
boton.pack()

ventana.mainloop()
```

---

<h5>Scale</h5>

Un deslizador para seleccionar valores numéricos en un rango.

Parámetros importantes:

* `from_` → valor mínimo.
* `to` → valor máximo.
* `orient` → orientación (`tk.HORIZONTAL` o `tk.VERTICAL`).
* `command` → función que recibe el valor cuando cambia.

```python
import tkinter as tk

ventana = tk.Tk()

def mostrar_valor(valor):
    # Actualiza etiqueta con el valor actual del slider
    etiqueta.config(text=f"Valor seleccionado: {valor}")

# Crear slider de 0 a 100 en horizontal
slider = tk.Scale(ventana, from_=0, to=100, orient=tk.HORIZONTAL, command=mostrar_valor)
slider.pack()

etiqueta = tk.Label(ventana, text="Valor seleccionado: 0")
etiqueta.pack()

ventana.mainloop()
```

---

<h5>Ejemplo integrador</h5>  

Este ejemplo combina **messagebox, simpledialog, Toplevel y Scale**.

```python
import tkinter as tk
from tkinter import messagebox, simpledialog

class AppFinal:
    def __init__(self, root):
        self.root = root
        self.root.title("Módulo Final - Diálogos y Complementos")

        self.etiqueta = tk.Label(root, text="Bienvenido")
        self.etiqueta.pack()

        # Botón para pedir nombre
        tk.Button(root, text="Ingresar nombre", command=self.pedir_nombre).pack()

        # Botón para mostrar información
        tk.Button(root, text="Mostrar info", command=self.mostrar_info).pack()

        # Slider de ejemplo
        self.slider = tk.Scale(root, from_=1, to=10, orient=tk.HORIZONTAL, command=self.actualizar_valor)
        self.slider.pack()

        self.etiqueta_valor = tk.Label(root, text="Valor: 1")
        self.etiqueta_valor.pack()

    def mostrar_info(self):
        messagebox.showinfo("Información", "Este es un ejemplo final con Tkinter.")

    def pedir_nombre(self):
        nombre = simpledialog.askstring("Entrada", "Escribe tu nombre:")
        if nombre:
            self.etiqueta.config(text=f"Hola, {nombre}!")
            self.abrir_ventana_secundaria(nombre)

    def abrir_ventana_secundaria(self, nombre):
        nueva = tk.Toplevel(self.root)
        nueva.title("Ventana secundaria")
        tk.Label(nueva, text=f"Bienvenido, {nombre}, a esta ventana.").pack()

    def actualizar_valor(self, valor):
        self.etiqueta_valor.config(text=f"Valor: {valor}")

ventana = tk.Tk()
app = AppFinal(ventana)
ventana.mainloop()
```

En este integrador:

* `messagebox` muestra mensajes emergentes.
* `simpledialog` pide texto al usuario.
* `Toplevel` abre una ventana secundaria.
* `Scale` permite seleccionar un número y lo refleja en pantalla.

---

