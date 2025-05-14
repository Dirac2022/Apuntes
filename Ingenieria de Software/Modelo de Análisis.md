
# Análisis
- En el Workflow de Análisis se analizar, refinan y estructuran los requerimientos capturados con el propósito de estructurar el sistema completo.
- Los modelos que se desarrollan describen **qué** es lo que el sistema va a hacer.
- Los modelos que se desarrollan están orientados al problema y no al ambiente en el que el sistema va a ser desarrollado e implementado.
- El modelo de análisis proporciona una configuración conceptual del sistema que consiste de objetos de control, entidad e interfaces.

# Modelo de Casos de Uso vs Modelo de Análisis


| Use-Case Model                                                                                                   | Analysis Model                                                                                  |
| ---------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| Se describe usando el lenguaje del cliente                                                                       | Se describe usando el lenguaje del desarrollador                                                |
| Es la vista externa del sistema                                                                                  | Es la vista interna del sistema                                                                 |
| Se usa a manera de contrato entre clientes y desarrolladores para definir lo que el sistema debe y no debe hacer | Se usa para que los desarrolladores comprendan como el sistema debe ser diseñado e implementado |
| Puede contener redundancias e inconsistencias en el enlace con los requerimientos                                | No debe contener redundancias ni inconsistencias en la interpretación de los requerimientos     |
| Captura la funcionalidad del sistema                                                                             | Bosqueja como realizar la funcionalidad dentro del sistema                                      |

# Modelo de Análisis
- Es un modelo conceptual de objetos que ayudan a refinar los requerimientos y permite a los desarrolladores describir la estructura interna del sistema.
- Es una jerarquía de paquetes de análisis que agregan clases de análisis y realizaciones de casos de uso.
- Se describen las clases de análisis bajo sus tres estereotipos: Interfaz, Entidad y Control.

## Clases Interfaz o Frontera
- Las clases *Boundary* se usan para modelar la interacción entre el sistema y los actores.
- Esta interacción involucra recibir (y presentar) información y peticiones desde usuarios y sistemas externos.
- Representan la abstracción de ventanas, formularios, paneles, interfaces de comunicación, impresoras, sensores, terminales o dispositivos.
**Ejemplo**
La interfaz de pago es usada para soportar la interacción entre el actor **Cajero** y el caso de uso **Registrar Pago**

<figure>
<img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Ingenieria de Software\imgs\ejemplo-clase-interfaz.png" >
</figure>

## Clase Entidad
clase entidad (modelo conceptual - 19 categorias)

- Las clases Entidad (*Entity*) son usadas para modelar la información que tiene permanencia en el tiempo y es persistente.
- Modelan la información y el comportamiento asociado de algún concepto como una persona, evento u objeto del mundo real.
- Usualmente muestran la estructura de datos lógica que contribuye a la compresión de la información que depende el sistema
**Ejemplo**

<figure>
<img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Ingenieria de Software\imgs\ejemplo-clase-entidad.png" >
</figure>

## Clase Controladora
- Las clases **control** representan la coordinación, secuencia, gestión de transacciones y control de otros objetos.
- Usualmente se usan para encapsular el control relacionado con un caso de uso específico.
- También se usan para representar cálculos y derivaciones complejas, como la lógica del negocio que no se puede relacionar con ninguna entidad.
- La dinámica del sistema se modela en una clase controladora, que se encarga de delegar trabajo a otras clases.
**Ejemplo**
La controladora de pagos es responsable de la coordinación entre la interfaz de pagos y la entidad pago.

<figure>
<img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Ingenieria de Software\imgs\ejemplo-clase-controladora.png" >
</figure>

## Diagrama de Clases de Análisis
Es un diagrama que muestra las clases de análisis y sus relaciones
<figure>
<img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Ingenieria de Software\imgs\ejemplo-clase-controladora.png" >
</figure>

