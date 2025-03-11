
# Diferencia entre hilos y procesos
- Un **proceso** es un programa en ejecución. Se compone de
	- Instrucciones del programa
	- Estado de ejecución
	- Memoria de trabajo
	- Otra información para controlar su planificación
- Un **hilo** de ejecución es la unidad de procesamiento más pequeña que puede ser planificada por un sistema operativo. Permite a una aplicación realizar varias tareas a la vez (concurrencia).


|                             | PROCESOS      | HILOS      |
| --------------------------- | ------------- | ---------- |
| Creación                    | Costosa       | Ligera     |
| Recursos y memoria          | Independiente | Compartida |
| Comunicación                | Compleja      | Sencilla   |
| Complejidad en programación | Reducida      | Alta       |

![img005.gif (640×480)](https://home.ubalt.edu/abento/454/tsmpm/img005.gif)

# Programa secuencial
Es aquel en el que sus instrucciones se van ejecutando en serie, una tras otras, desde su inicio hasta el final. Por tanto, en un programa secuencial solo existe una única actividad o hilo de ejecución.

# Programa concurrente
- Se llegaran a crear múltiples actividades que progresaran de manera simultánea. Cada una de esas actividades será secuencial pero ahora el programa no avanzará siguiente una única secuencia pues cada actividad podrá seguir una serie de instrucciones distinta y todas las actividades avanzan de manera simultánea (o, al menos, esa es la imagen que ofrecen al usuario).
- Para que en un determinado proceso haya múltiples actividades, cada una de esas actividades estará soportada por un hilo de ejecución. **Para que un conjunto de actividades constituya un programa concurrente, todas ellas deben cooperar entre si para realizar una tarea común.**

# Concurrencia

- **Paralelismo real**: Se dará cuando tengamos disponibles múltiples procesadores, de manera que ubicaremos a cada actividad en un procesador diferente.

- En las arquitectura modernas, los procesadores pueden tener múltiples núcleos. En ese caso, basta con asignar un núcleo diferente a cada actividad. Todas ellas podrán avanzar simultáneamente sin ningún problema.

- Si solo disponemos de ordenadores con un solo procesador y un único núcleo, podremos todavía lograr la concurrencia real utilizando múltiples ordenadores.

- **Paralelismo lógico**: Como los procesadores actuales son rápidos y las operaciones de E/S suspenden temporalmente el avance del hilo de ejecución que las haya programado, se puede intercalar la ejecución de múltiples actividades y ofrecer la imagen de que éstas progresan simultáneamente.

- El usuario será incapaz de distinguir entre un sistema informático con un solo procesador y un solo núcleo de otro que tenga múltiples procesadores, pues los sistemas operativos ocultan estos detalles.

# Ventajas

- **Eficiencia**: El hecho de disponer de múltiples actividades dentro de la aplicación permite que esta puede concluir su trabajo de manera más rápida.

- **Escalabilidad**: Si una determinada aplicación puede diseñarse e implantarse como un conjunto de componentes que interactúen y colaboren entre si, generando al menos una actividad por cada componente, se facilitara la distribución de la aplicación sobre diferentes ordenadores.

- **Gestión de las comunicaciones**: El uso eficiente de los recursos, ya comentando en la primera ventaja citada en este apartado, permite que aquellos recursos relacionados con la comunicación entre actividades sean explotados de manera sencilla en una aplicación concurrente.

- **Flexibilidad**: Las aplicaciones concurrentes suelen utilizar un diseño modular y estructurado , en el que se presta especial atención a que es lo que debe hacer cada actividad, que recursos requerir y a que módulos del programa necesitara ejecutar.

- **Menor hueco semántico**: Un buen número de aplicaciones informáticas requieren el uso de varias actividades simultáneas (por ejemplo, en un videojuego suele utilizarse un hilo por cada elemento móvil que haya en la pantalla; en una hoja de calculo tenemos un hilo para gestionar la entrada de datos, otro para recalculo, otro para la gestión de los menús, otro para la actualización de las celdas visibles, etc.).


# Inconvenientes

- **Programación delicada**: Durante el desarrollo de aplicaciones concurrentes pueden llegar a surgir algunos problemas. **Condición de carrera** y puede generar inconsistencias imprevistas en el valor de las variables o atributos compartidos entre las actividades, cuando estas los modifiquen. Un segundo problema son los **interbloqueos**.

- **Depuración compleja**: Una aplicación concurrente, al estar compuesta por múltiples actividades, puede intercalar de diferentes maneras en cada ejecución las sentencias que ejecuten cada una de sus actividades.


# Aplicaciones reales

- **Programa de control del acelerador lineal**: Los aceleradores lineales se utilizan en los tratamientos de radioterapia para algunos tipos de cáncer, eliminando mediante ciertos clases de radiación (radiación de electrones, rayos X y rayos gamma, principalmente) a las células cancerígenas. 

- **Servidor web Apache**: Apache es un servidor web que emplea programación concurrente.  El objetivo de un servidor web es la gestión de cierto conjunto de paginas web ubicadas en ese servidor. En un servidor de este tipo interesa tener múltiples  hilos de ejecución, de manera que cada uno de ellos pueda atender a un cliente distinto, paralelizando así la gestión de múltiples clientes.

- **Videojuegos**: La mayoría de los videojuegos actuales (tanto para ordenadores personales como para algunas consolas) se estructuran como aplicaciones concurrentes compuestas por múltiples hilos de ejecución.

- **Navegador web**: Cuando Google presento su navegador Chrome (en diciembre de 2008), su arquitectura era muy distinta a la del resto de navegadores web (Microsoft Internet Explorer, Mozilla Firefox, Opera, etc.). En Chrome, cada pestaña abierta esta soportada por un proceso independiente.