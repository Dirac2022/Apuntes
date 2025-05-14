**Traducción del artículo de Martin Fowler: [Patterns for Managing Source Code Branches](https://martinfowler.com/articles/branching-patterns.html)**

# Patrones para la gestión de ramas de código fuente - Parte 2

## Patrones de integración

El branching se trata de gestionar la interacción entre el aislamiento y la integración. Hacer que todos trabajen en un único código base  compartido todo el tiempo no funciona, porque no puedo compilar el programa si estás en medio de escribir el nombre de una variable. 
Así que, al menos en cierta medida, necesitamos la noción de un espacio de trabajo privado en el que pueda trabajar durante un tiempo. Las herramientas modernas de control de código fuente facilitan la creación de ramas y el monitoreo de los cambios en esas ramas. Sin embargo, en algún momento necesitamos integrar. Pensar en estrategias de branching se trata, en realidad, de decidir cómo y cuándo integramos.

### Integración en la rama principal

> Los desarrolladores integran su trabajo extrayendo (pull) de la rama principal, fusionando (merge) y –si todo está saludable– empujando (push) de vuelta a la rama principal

Una rama principal proporciona una definición clara de cómo se ve el estado actual del software del equipo. Uno de los mayores beneficios de usar una rama principal es que simplifica la integración. Sin una rama principal, se tiene la complicada tarea de coordinar con todos en el equipo que describí anteriormente. Con una rama principal, sin embargo, cada desarrollador puede integrar de forma independiente.

Voy a explicar un ejemplo de cómo funciona esto. Una desarrolladora, a quien llamaré Scarlett, comienza algún trabajo clonando la rama principal en su propio repositorio. Con git, si ella aún no tiene un clon del repositorio central, lo clonaría y haría checkout de la rama master. Si ya tiene el clon, extraería (pull) desde la rama principal hacia su master local. Luego puede trabajar localmente, realizando commits en su master local.

<img src="https://martinfowler.com/articles/branching-patterns/mainline-integration-checkout.png" alt="mainline integration checkout">

Mientras trabaja, su colega Violet sube algunos cambios a la rama principal. Mientras trabaja en su propia línea de código, Scarlett puede estar ajena a esos cambios mientras se concentra en su propia tarea.

<img src="https://martinfowler.com/articles/branching-patterns/mainline-integration-other-update.png" alt="actualización en mainline">

En algún momento, llega al punto en que quiere integrar. La primera parte de esto es obtener el estado actual de la rama principal en su rama master local, esto traerá los cambios de Violet. Mientras trabaja en su master local, los commits aparecerán en origin/master como una línea de código separada.

<img src="https://martinfowler.com/articles/branching-patterns/mainline-integration-pull.png" alt="pull de integración en mainline">

Ahora necesita combinar sus cambios con los de Violet. Algunos equipos prefieren hacerlo mediante fusiones (merge), otros mediante *rebasing*. En general, la gente usa la palabra *merge* cada vez que habla de unir ramas, ya sea que utilicen una operación de git merge o de rebase. 
Seguiré ese uso, así que, a menos que esté discutiendo las diferencias entre merge y *rebasing*, considera *merge* como la tarea lógica que puede implementarse con cualquiera de las dos.

Si Scarlett tiene suerte, la fusión del código de Violet será limpia; de lo contrario, tendrá algunos conflictos que resolver. Estos pueden ser conflictos textuales, la mayoría de los cuales el sistema de control de versiones puede manejar automáticamente. Pero los conflictos semánticos son mucho más difíciles de tratar, y aquí es donde el **self testing code** resulta muy útil. (Dado que los conflictos pueden generar una cantidad considerable de trabajo, y siempre introducen el riesgo de mucho trabajo, los marco con un alarmante bloque amarillo.)

<img src="https://martinfowler.com/articles/branching-patterns/mainline-integration-fuse.png" alt="fusión en mainline">

En este punto, Scarlett necesita verificar que el código fusionado cumple con los estándares de salud de la rama principal (suponiendo que la rama principal es una Healthy Branch). Esto usualmente significa compilar el código y ejecutar las pruebas que forman el conjunto de commits de la rama principal. Debe hacer esto incluso si la fusión es limpia, porque incluso una fusión limpia puede ocultar conflictos semánticos. Cualquier fallo en el conjunto de commits debería deberse únicamente a la fusión, ya que ambos padres de la fusión deberían estar en verde. 
Saber esto debería ayudarle a localizar el problema, ya que puede mirar las diferencias (diffs) en busca de pistas.

Con esta compilación y pruebas, ha incorporado con éxito la rama principal en su línea de código, pero –y esto es tanto importante como frecuentemente pasado por alto– aún no ha terminado de integrarse con la rama principal. Para finalizar la integración, debe empujar sus cambios hacia la rama principal. A menos que lo haga, el resto del equipo quedará aislado de sus cambios –esencialmente, sin integrarse. La integración implica tanto un pull como un push: sólo cuando Scarlett haya hecho push su trabajo estará integrado con el resto del proyecto.

<figure>
<img src="https://martinfowler.com/articles/branching-patterns/mainline-integration-integrate.png" alt="integración completa en mainline">
<figcaption>Muchos equipos hoy en día requieren un paso de revisión de código antes de que un commit sea agregado a la rama principal –un patrón que llamo pre-integration review.</figcaption>
</figure>


Ocasionalmente, alguien más integrará con la rama principal antes de que Scarlett pueda hacer su push. En cuyo caso, ella tiene que hacer pull y fusionar de nuevo. Usualmente, esto es solo un problema ocasional y se puede resolver sin mayor coordinación. He visto equipos con compilaciones largas usar un "batón de integración", de modo que sólo el desarrollador que tiene el batón pueda integrar. Pero no he oído tanto de eso en los últimos años a medida que los tiempos de compilación mejoran.

#### Cuándo usarlo

Como sugiere el nombre, sólo puedo usar la integración en la rama principal si también estamos usando la rama principal en nuestro producto.

Una alternativa a usar la integración en la rama principal es simplemente hacer pull desde la rama principal, fusionando esos cambios en la rama de desarrollo personal. Esto puede ser útil: el pull puede, al menos, alertar a Scarlett de los cambios que otras personas han integrado y detectar conflictos entre su trabajo y la rama principal. Pero hasta que Scarlett haga push, Violet no podrá detectar ningún conflicto entre lo que está trabajando y los cambios de Scarlett.

Cuando la gente usa la palabra "integrate", a menudo se pierden este punto importante. Es común escuchar a alguien decir que está integrando la rama principal en su rama cuando en realidad solo está haciendo pull. He aprendido a tener cuidado con eso y a indagar más para comprobar si se refieren solo a un pull o a una verdadera integración con la rama principal. Las consecuencias de ambos son muy diferentes, por lo que es importante no confundir los términos.

Otra alternativa es cuando Scarlett está en medio de realizar algún trabajo que no está listo para una integración completa con el resto del equipo, pero que se superpone con el de Violet y ella quiere compartirlo. En ese caso, pueden abrir una **rama de colaboración**.

### Feature branching

> Coloca todo el trabajo de una funcionalidad en su propia rama, e intégrala en la rama principal cuando la funcionalidad esté completa.

Con el feature branching (ramificación de funcionalidades), los desarrolladores abren una rama cuando comienzan a trabajar en una funcionalidad, continúan trabajando en esa funcionalidad hasta que terminan, y luego integran con la rama principal.

Por ejemplo, sigamos a Scarlett. Ella tomaría la funcionalidad de añadir la recolección de impuestos locales sobre las ventas a su sitio web. Comienza con la versión estable actual del producto, hará pull de la rama principal en su repositorio local y luego creará una nueva rama a partir del último commit de la rama principal. Trabaja en la funcionalidad durante el tiempo que sea necesario, realizando una serie de commits en esa rama local.

<img src="https://martinfowler.com/articles/branching-patterns/fb-start.png" alt="inicio de feature branch">

Podría hacer push de esa rama al repositorio del proyecto para que otros puedan ver sus cambios.

Mientras trabaja, otros commits se integran en la rama principal. Así que, de vez en cuando, puede hacer pull desde la rama principal para ver si hay cambios que puedan afectar su funcionalidad.

<img src="https://martinfowler.com/articles/branching-patterns/fb-pull.png" alt="pull de feature branch">

Nótese que esto no es integración tal como lo describí anteriormente, ya que no hizo push a la rama principal. En este punto, sólo ella está viendo su trabajo, los demás no.

> Algunos equipos prefieren asegurarse de que todo el código, ya esté integrado o no, se mantenga en el repositorio central. En este caso, Scarlett haría push de su rama de funcionalidad en el repositorio central. Esto también permitiría que otros miembros del equipo vieran en qué está trabajando, incluso si aún no está integrado en el trabajo de otros.

Cuando haya terminado de trabajar en la funcionalidad, realizará la integración en la rama principal para incorporar la funcionalidad al producto.

<img src="https://martinfowler.com/articles/branching-patterns/fb-integrate.png" alt="integración de feature branch">

Si Scarlett trabaja en más de una funcionalidad al mismo tiempo, abrirá una rama separada para cada una.

#### Cuándo usarlo

El feature branching es un patrón popular en la industria hoy en día. Para hablar de cuándo usarlo, necesito presentar su principal alternativa: la integración continua. Pero primero, debo hablar sobre el rol de la frecuencia de integración.

### Frecuencia de integración

La frecuencia con la que integramos tiene un efecto notablemente poderoso en cómo opera un equipo. Investigaciones del *State Of Dev Ops Report* indicaron que los equipos de desarrollo de élite integran notablemente más a menudo que los de bajo rendimiento, una observación que coincide con mi experiencia y la de tantos de mis colegas en la industria. Ilustraré cómo se desarrolla esto considerando dos ejemplos de frecuencia de integración protagonizados por Scarlett y Violet.

#### Integración de baja frecuencia

Empezaré con el caso de baja frecuencia. Aquí, nuestros dos protagonistas comienzan una sesión de trabajo clonando la rama principal en sus ramas, y luego realizando un par de commits locales que aún no quieren hacer push.

<img src="https://martinfowler.com/articles/branching-patterns/low-freq-start.png" alt="inicio de integración de baja frecuencia">

Mientras trabajan, otra persona hace un commit en la rama principal. (No puedo inventar rápidamente otro nombre de persona que sea un color – quizá Grayham?)

<img src="https://martinfowler.com/articles/branching-patterns/low-freq-M1.png" alt="commit M1 en integración de baja frecuencia">

Este equipo trabaja manteniendo una rama saludable y haciendo pull desde la rama principal después de cada commit. Scarlett no tenía nada que hacer pull en sus dos primeros commits ya que la rama principal no había cambiado, pero ahora necesita hacer pull de M1.

<img src="https://martinfowler.com/articles/branching-patterns/low-freq-SM.png" alt="pull de Scarlett en baja frecuencia">

He marcado la fusión con el recuadro amarillo. Esta fusiona los commits S1..3 con M1. Pronto Violet tendrá que hacer lo mismo.

<img src="https://martinfowler.com/articles/branching-patterns/low-freq-VM.png" alt="pull de Violet en baja frecuencia">

En este punto, ambos desarrolladores están al día con la rama principal, pero no se han integrado ya que ambos están aislados el uno del otro. Scarlett desconoce cualquier cambio que Violet haya realizado en V1..3.

Scarlett realiza un par de commits locales más y luego está lista para hacer la integración en la rama principal. Esto es un push fácil para ella, ya que ya había hecho pull de M1 anteriormente.

<img src="https://martinfowler.com/articles/branching-patterns/low-freq-S-push.png" alt="push de Scarlett en baja frecuencia">

Violet, sin embargo, tiene un ejercicio más complicado. Cuando hace la integración en la rama principal, ahora tiene que integrar S1..5 con V1..6.

<img src="https://martinfowler.com/articles/branching-patterns/low-freq-V-push.png" alt="push de Violet en baja frecuencia">

He calculado científicamente los tamaños de las fusiones basándome en la cantidad de commits involucrados. Pero, incluso si ignoras la protuberancia en forma de lengua en mi mejilla, apreciarás que la fusión de Violet es la que probablemente será más difícil.

#### Integración de alta frecuencia

En el ejemplo anterior, nuestros dos coloridos desarrolladores integraron después de unos pocos commits locales. Veamos qué sucede si hacen la integración en la rama principal después de cada commit local.

El primer cambio es evidente con el primer commit de Violet, ya que integra de inmediato. Dado que la rama principal no ha cambiado, se trata de un simple push.

<img src="https://martinfowler.com/articles/branching-patterns/high-freq-V1.png" alt="primer commit de Violet en alta frecuencia">

El primer commit de Scarlett también integra con la rama principal, pero como Violet llegó primero, ella necesita hacer una fusión. Pero dado que sólo está fusionando V1 con S1, la fusión es pequeña.

<img src="https://martinfowler.com/articles/branching-patterns/high-freq-S1.png" alt="primer merge de Scarlett en alta frecuencia">

La siguiente integración de Scarlett es un simple push, lo que significa que el siguiente commit de Violet también requerirá fusionar con los dos últimos commits de Scarlett. Sin embargo, sigue siendo una fusión bastante pequeña: uno de Violet y dos de Scarlett.

<img src="https://martinfowler.com/articles/branching-patterns/high-freq-V2S2.png" alt="merge de Violet con V2 y S2 en alta frecuencia">

Cuando aparece un push externo a la rama principal, se incorpora en el ritmo habitual de las integraciones de Scarlett y Violet.

<img src="https://martinfowler.com/articles/branching-patterns/high-freq-M1S3.png" alt="integración externa en alta frecuencia">

Aunque es similar a lo que ocurrió antes, las integraciones son más pequeñas. Scarlett sólo tiene que integrar S3 con M1 esta vez, porque S1 y S2 ya estaban en la rama principal. 

Esto significa que Grayham habría tenido que integrar lo que ya estaba en la rama principal (S1..2, V1..2) antes de hacer push de M1.

Los desarrolladores continúan con su trabajo restante, integrando con cada commit.

<img src="https://martinfowler.com/articles/branching-patterns/high-freq-V6.png" alt="última integración de Violet en alta frecuencia">

#### Comparando frecuencias de integración

Observemos nuevamente las dos imágenes generales:

<img src="https://martinfowler.com/articles/branching-patterns/low-freq-V-push.png" alt="push de Violet en baja frecuencia">

<img src="https://martinfowler.com/articles/branching-patterns/high-freq-V6.png" alt="última integración de Violet en alta frecuencia">

Hay dos diferencias muy evidentes aquí. En primer lugar, ==la integración de alta frecuencia, como sugiere el nombre, tiene muchas más integraciones== –el doble, sólo en este ejemplo simplificado.==Pero, lo que es más importante, estas integraciones son mucho más pequeñas que en el caso de baja frecuencia==. ==Integraciones más pequeñas significan menos trabajo==, ya que hay menos cambios de código que podrían generar conflictos. Pero, más importante que menos trabajo, ==también implica menor riesgo==. El problema con las fusiones grandes no es tanto el trabajo que conllevan, sino la incertidumbre de ese trabajo. La mayoría de las veces, incluso las fusiones grandes transcurren sin problemas, pero ocasionalmente salen muy, muy mal. Si comparo gastar diez minutos extra por integración con una posibilidad de 1 entre 50 de pasar 6 horas arreglando una integración –¿cuál prefiero? Si solo miro el esfuerzo, entonces el caso de 1 en 50 es mejor, ya que son 6 horas en lugar de 8 horas y veinte minutos. Pero la incertidumbre hace que el caso de 1 en 50 se sienta mucho peor, una incertidumbre que conduce al miedo a la integración.

==Miremos la diferencia entre estas frecuencias desde otra perspectiva. ¿Qué ocurre si Scarlett y Violet desarrollan un conflicto en sus primeros commits? ¿Cuándo detectan que ha ocurrido el conflicto? En el caso de baja frecuencia, no lo detectan hasta la fusión final de Violet, porque es la primera vez que se juntan S1 y V1. Pero en el caso de alta frecuencia, se detecta en la primera fusión de Scarlett==.

<figure>
<img src="https://martinfowler.com/articles/branching-patterns/low-freq-conflict.png" alt="conflicto en baja frecuencia">
<figcaption>Low Frequency</figcaption>
</figure>


<figure>
<img src="https://martinfowler.com/articles/branching-patterns/high-freq-conflict.png" alt="conflicto en alta frecuencia">
<figcaption>High Frequency</figcaption>
</figure>


La integración frecuente aumenta la cantidad de fusiones pero reduce su complejidad y riesgo. ==La integración frecuente también alerta a los equipos sobre conflictos mucho más rápidamente==. Estas dos cosas están conectadas, por supuesto. Las fusiones problemáticas suelen ser el resultado de un conflicto latente en el trabajo del equipo, que solo se manifiesta cuando ocurre la integración.

Quizás Violet estaba revisando un cálculo de facturación y vio que incluía la evaluación de impuestos, donde el autor había asumido un mecanismo impositivo particular. Su funcionalidad requiere tratamientos diferentes para los impuestos, por lo que la solución directa fue sacar el impuesto del cálculo de facturación y hacerlo como una función separada más adelante. 
El cálculo de facturación sólo se llamaba en un par de lugares, por lo que es fácil utilizar la técnica *Move Statements to Callers* y el resultado tiene más sentido para la evolución futura del programa. Sin embargo, Scarlett no sabía que Violet estaba haciendo esto y escribió su funcionalidad asumiendo que la función de facturación se encargaba de los impuestos.

El **self testing code** es nuestro salvavidas aquí. Si tenemos un conjunto de pruebas robusto, al usarlo como parte de la rama saludable se detectará el conflicto, de modo que hay muchas menos posibilidades de que un error llegue a producción. Pero incluso con un conjunto de pruebas fuerte actuando como guardián de la rama principal, las integraciones grandes complican la vida. Cuanto más código tengamos que integrar, más difícil es encontrar el error. También tenemos una mayor probabilidad de múltiples errores interferentes, que son extra-difíciles de entender. 

No solo tenemos menos que revisar con commits más pequeños, sino que también podemos usar **diff debugging** para ayudar a reducir cuál cambio introdujo el problema.

Lo que mucha gente no se da cuenta es que un sistema de control de versiones es una herramienta de comunicación. Permite a Scarlett ver lo que los demás en el equipo están haciendo. Con integraciones frecuentes, no solo se le alerta de inmediato cuando hay conflictos, sino que también está más al tanto de lo que todos están haciendo y de cómo está evolucionando el código base. Dejamos de ser individuos trabajando de manera independiente para ser un 
equipo que colabora.

> Aumentar la frecuencia de integración es una razón importante para reducir el tamaño de las funcionalidades, pero hay otras ventajas también. Cuanto más pequeña sea la funcionalidad, más rápido se construye, más rápido llega a producción y más pronto empieza a entregar su valor. Además, funcionalidades más pequeñas reducen el tiempo de retroalimentación, permitiendo al equipo tomar mejores decisiones sobre las funcionalidades a medida que aprenden más sobre sus clientes.

---

### Integración continua

Los desarrolladores realizan la integración en la rama principal tan pronto como tienen un commit saludable que pueden compartir, generalmente menos de un día de trabajo

Una vez que un equipo ha comprobado que la integración de alta frecuencia es tanto más eficiente como menos estresante, la pregunta natural que surge es "¿con qué frecuencia podemos hacerlo?". La ramificación de funcionalidades implica un límite inferior al tamaño de un conjunto de cambios: no puede ser más pequeño que una funcionalidad cohesionada.

La integración continua aplica un disparador diferente para la integración: se integra cada vez que se ha realizado un avance sustancial en la funcionalidad y la rama sigue estando saludable. No se espera que la funcionalidad esté completa, solo que se haya realizado una cantidad significativa de cambios en el código base. La regla general es que "todos hacen commit a la rama principal cada día", o más precisamente: nunca deberías tener más de un día de trabajo sin integrar en tu repositorio local. 

En la práctica, la mayoría de los practicantes de la integración continua integran muchas veces al día, contentos de integrar una hora de trabajo o menos.

Los desarrolladores que utilizan la integración continua deben acostumbrarse a la idea de alcanzar puntos de integración frecuentes con una funcionalidad parcialmente construida. Deben considerar cómo hacerlo sin exponer una funcionalidad incompleta en el sistema en ejecución.
A menudo esto es sencillo: si estoy implementando un algoritmo de descuento que depende de un código de cupón (lista de códigos autorizados), y ese código aún no está en la lista válida, entonces mi código no se invocará, incluso si está en producción. 

De manera similar, si estoy añadiendo una funcionalidad que pregunta a un reclamante de un seguro si es fumador, puedo construir y probar la lógica detrás del código y asegurarme de que no se utilice en producción dejando la interfaz de usuario que plantea la pregunta hasta el último día de desarrollo de la funcionalidad. 

Ocultar una funcionalidad parcialmente construida conectando una [interfaz Keystone](https://martinfowler.com/bliki/KeystoneInterface.html) al final es a menudo una técnica efectiva.

Si no hay forma de ocultar fácilmente la funcionalidad parcial, se pueden usar **feature flags**. Además de ocultar una funcionalidad incompleta, dichos flags también permiten que la funcionalidad se revele selectivamente a un subconjunto de usuarios, lo cual resulta útil para un despliegue paulatino de una nueva funcionalidad.

Integrar funcionalidades parcialmente construidas preocupa especialmente a quienes temen tener código defectuoso en la rama principal. En consecuencia, quienes usan la integración continua también necesitan **self testing code**, para tener la confianza de que contar con funcionalidades
incompletas en la rama principal no aumenta la probabilidad de errores. Con este enfoque, los desarrolladores escriben pruebas para las funcionalidades parciales mientras desarrollan el código de la funcionalidad y comiten tanto el código de la funcionalidad como las pruebas a la rama principal conjuntamente (quizás utilizando test driven development).

En términos de repositorio local, la mayoría de las personas que utilizan la integración continua no se complican con una rama local separada para trabajar. Normalmente es sencillo hacer commit en el master local y realizar la integración en la rama principal una vez terminado. Sin embargo, es perfectamente válido abrir una rama de funcionalidad y trabajar allí, si los desarrolladores lo prefieren, integrando de vuelta en el master local y en la rama principal a intervalos frecuentes. La diferencia entre la ramificación de funcionalidades y la integración continua no reside en si existe o no una rama de funcionalidad, sino en cuándo los desarrolladores integran con la rama principal.

#### Cuándo usarlo

> La integración continua es una alternativa a la ramificación de funcionalidades. 

### Comparación entre la ramificación de funcionalidades y la integración continua

La ramificación de funcionalidades parece ser la estrategia de branching más común en la industria en este momento, pero existe un grupo vocal de practicantes que argumentan que la integración continua suele ser un enfoque superior. La ventaja clave que ofrece la integración continua es que soporta una frecuencia de integración más alta, a menudo mucho más alta.

La diferencia en la frecuencia de integración depende de lo pequeñas que pueda hacer un equipo sus funcionalidades. 

Si todas las funcionalidades de un equipo pueden desarrollarse en menos de un día, entonces pueden aplicar tanto la ramificación de funcionalidades como la integración continua. Pero la mayoría de los equipos tienen funcionalidades que requieren más tiempo —y cuanto mayor sea la duración de la funcionalidad, mayor será la diferencia entre ambos patrones.

Como ya he indicado, una mayor frecuencia de integración conduce a integraciones menos complicadas y a un menor temor a integrar. Esto suele ser algo difícil de comunicar. Si has vivido en un mundo en el que se integra cada pocas semanas o meses, la integración es probablemente una actividad muy cargada de tensión. Puede resultar difícil creer que es algo que se puede hacer muchas veces al día. Pero la integración es una de esas cosas en las que la frecuencia reduce la 
dificultad. Es una noción contra intuitiva: "si duele, hazlo más a menudo". Pero cuanto más pequeñas sean las integraciones, menos probable es que se conviertan en una épica fusión de miseria y desesperación. 

Con la ramificación de funcionalidades, esto aboga por funcionalidades más pequeñas: días, no semanas (y los meses están descartados).

La integración continua permite a un equipo obtener los beneficios de una integración de alta frecuencia, al mismo tiempo que desacopla la duración de la funcionalidad de la frecuencia de integración. Si un equipo prefiere funcionalidades que duren una o dos semanas, la integración continua les permite hacerlo sin dejar de obtener todos los beneficios de la frecuencia de integración más alta. 

Las fusiones son más pequeñas, requiriendo menos trabajo para resolverlas. Más importante aún, como se explicó anteriormente, hacer fusiones más frecuentemente reduce el riesgo de una fusión desastrosa, lo que elimina las malas  sorpresas que esto conlleva y reduce el temor general a fusionar. Si surgen conflictos en el código, la integración de alta frecuencia los detecta rápidamente, antes de que provoquen esos desagradables problemas de integración. Estos beneficios son tan sólidos que hay equipos con funcionalidades que solo toman un par de días que aún aplican la integración continua.

La desventaja evidente de la integración continua es que carece del cierre de esa integración climática a la rama principal. No solo se pierde esa celebración, sino que también representa un riesgo si un equipo no es bueno en mantener una rama saludable. Mantener todos los commits de una funcionalidad juntos también posibilita tomar una decisión tardía sobre si incluir o no una funcionalidad en un próximo 
lanzamiento. 

Aunque los feature flags permiten activar o desactivar funcionalidades desde la perspectiva del usuario, el código de la funcionalidad  sigue estando en el producto. Las preocupaciones sobre esto suelen estar sobredimensionadas, ya que el código no pesa nada, pero sí implica que  los equipos que desean usar la integración continua deben desarrollar un régimen de pruebas sólido para tener la confianza de que la rama principal se mantiene saludable incluso con muchas integraciones al día. 

Algunos equipos encuentran difícil imaginar esta habilidad, pero otros la consideran tanto posible como liberadora. Este requisito implica que la ramificación de funcionalidades es más adecuada para equipos que no insisten en una rama saludable y requieren ramas de lanzamiento para estabilizar el código antes de publicarlo.

Si bien el tamaño e incertidumbre de las fusiones es el problema más obvio de la ramificación de funcionalidades, el mayor inconveniente de este enfoque puede ser que desalienta el refactoring. El refactoring es más efectivo cuando se realiza de manera regular y con poca fricción. El **refactoring** introducirá conflictos y, si estos no se detectan y resuelven rápidamente, la fusión se complica. Por ello, el refactoring funciona mejor con una alta frecuencia de integración, por lo que no es sorprendente que se popularizara como parte del extreme programming, que también tiene la integración continua como una de sus prácticas originales. La ramificación de funcionalidades también desincentiva a los desarrolladores a realizar cambios que no se vean como parte de la funcionalidad en desarrollo, lo que socava la capacidad del refactoring para mejorar de forma constante de un código base.

Cuando me encuentro con estudios científicos sobre prácticas de desarrollo de software, por lo general permanezco escéptico debido a serios problemas en su metodología. Una excepción es el `State Of Dev Ops Report`, que ha desarrollado una métrica de rendimiento en la entrega de software, la cual han correlacionado con una medida más amplia del rendimiento organizacional, que a su vez se correlaciona con métricas de negocio como el retorno de la inversión y la rentabilidad. En 2016, evaluaron por primera vez la integración continua y descubrieron que contribuía a un mayor rendimiento en el desarrollo de software, un hallazgo que se ha repetido en cada encuesta desde entonces.

Utilizar la integración continua no elimina las demás ventajas de mantener funcionalidades pequeñas. Publicar frecuentemente pequeñas funcionalidades proporciona un ciclo de retroalimentación rápido que puede hacer maravillas para mejorar un producto.
Muchos equipos que usan la integración continua también se esfuerzan por construir partes delgadas del producto y lanzar nuevas funcionalidades tan frecuentemente como sea posible.

---
### 🔍 **Feature Branching vs. Continuous Integration (CI)**

|**Aspecto**|**Feature Branching**|**Continuous Integration (CI)**|
|---|---|---|
|**Propósito principal**|Aislar el desarrollo de nuevas funcionalidades|Integrar cambios pequeños y frecuentes para evitar conflictos|
|**Frecuencia de commits/push**|Espaciada (al completar la feature)|Muy frecuente (varias veces al día)|
|**Duración de ramas**|Ramas largas (días o semanas)|Ramas cortas (horas o pocos días) o sin ramas (commits directos en main)|
|**Uso de `git pull`**|Poco frecuente; generalmente antes de integrar|Muy frecuente, para mantenerse sincronizado|
|**Uso de `git push`**|Al terminar la feature o en avances puntuales|Cada pequeño avance es push-eado|
|**Pull Requests (PR)**|Obligatorios; revisión extensa de código|Opcionales; revisión rápida o automatizada|
|**Automatización (CI/CD)**|Opcional; se puede hacer testing manual|Esencial; cada push/PR activa tests y validaciones automáticas|
|**Testing**|Manual o por PR|Automático en cada integración|
|**Build automático**|Generalmente al final (antes del merge)|En cada push o PR|
|**Detección de errores**|Tardía (al momento del merge)|Temprana (cada integración se prueba)|
|**Riesgo de conflictos**|Alto, especialmente si ramas viven mucho tiempo|Bajo, ya que los cambios se integran continuamente|
|**Requiere sincronización con main**|Sí, antes del merge|Sí, constantemente (idealmente antes de cada push)|
|**Ideal para**|Equipos grandes que trabajan en funcionalidades grandes y separadas|Equipos con buena disciplina y pipelines automatizados|
|**Revisión de código**|Detallada, antes del merge (normalmente en PR)|Rápida o continua, a veces automatizada|
|**Complejidad de integración**|Alta si la rama vive mucho|Baja, porque se integran pocos cambios por vez|
|**Mejor práctica moderna**|Ramas de vida corta + revisión automática (mezcla con CI)|Flujo CI/CD completo + testing y despliegue continuo (DevOps)|

### 📌 Nota:

- En la práctica moderna se recomienda **usar ramas cortas + CI**:
    
    - Crear una rama solo si es necesario (1-2 días máximo).
    - Hacer push seguido.
    - Automatizar la integración (tests, builds, análisis).
    - Usar Pull Requests con revisiones rápidas o automáticas.

---
