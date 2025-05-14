
# Introducción

- Kubernetes es una plataforma open source para la organización en contenedores que automatiza muchos de los procesos manuales involucrados en la implementación, la gestión y el ajuste de las aplicaciones que se alojan en ellos.
- Kubernetes es una plataforma open-source para orquestar ,automatizar el despliegue, escalar, gestionar y operar contenedores a través de clusters de hosts.

**Objetivo principal:** Administrar aplicaciones contenedorizadas para que sean:

- **Portables**: Ejecutables en cualquier entorno (local, nube, híbrido).
- **Escalables**: Soporten aumento o disminución de recursos según la demanda.
- **Resilientes**: Se recuperen automáticamente ante fallas.

<div style="text-align:center">
<figure>
<img src="https://cdn.prod.website-files.com/5e6befb8c88b0e98c69b1333/6054fec86ef332ff3651bc92_1581514013775.png" alt="">
<figcaption>
</figcaption>
</figure>
</div>

# Clusters de Kubernetes

Un clúster es un conjunto de máquinas (físicas o virtuales) que trabajan juntas para ejecutar y gestionar aplicaciones en contenedores. 

Puede agrupar en clústeres conjuntos de hosts que ejecuten contenedores de Linux, y Kubernetes lo ayudará a gestionarlos con facilidad y eficacia. 

Los clústeres de Kubernetes pueden contener hosts locales y en nubes públicas, privadas o híbridas. Por eso, es la plataforma ideal para alojar aplicaciones desarrolladas directamente en la nube que deben ajustarse rápidamente, como la transmisión inmediata de datos a través de Apache Kafka.

# Nodes
Un **node** es una máquina física o virtual que forma parte del clúster de Kubernetes. Es el lugar donde se ejecutan las aplicaciones (contenedores) y otros componentes para el funcionamiento del clúster.

Es una colección de máquinas que son tratadas como una sola unidad lógica por Kubernetes.

# Pods
Un **Pod** es la unidad mínima de despliegue en Kubernetes. Representa una capa de abstracción por encima de los contenedores. Cada Pod puede contener uno o más contenedores que comparten:

| Recurso compartido | Descripción                                                                                                          |
| ------------------ | -------------------------------------------------------------------------------------------------------------------- |
| Red                | Todos los contenedores en un Pod comparten la misma dirección IP y pueden comunicarse entre ellos usando `localhost` |
| Almacenamiento     | Los Pods pueden compartir volúmenes para persistir datos entre contenedores                                          |


Mínima unidad lógica desplegable en Kubernetes.
- Contiene un grupo de contenedores co-localizados (usualmente uno) y volúmenes.
- Share Namespace, Ip por Pod, localhost dentro del Pod.




<div style="text-align:center">
<figure>
<img src="https://matthewpalmer.net/kubernetes-app-developer/articles/networking-overview.png" alt="">
<figcaption>
</figcaption>
</figure>
</div>

# Scheduler
El **scheduler** o programador es un componente del nodo maestro que se encarga de asignar **Pods**  a **Nodes** dentro del clúster. Su principal función es decidir dónde se ejecutará cada Pod, basándose en varios criterios.

- Elige el lugar y levanta el Pod dentro de los nodos.
- El mejor lugar es elegido en base a los requerimientos del Pod

# Replication Controllers
El **Replication Controller** es un objeto que asegura que un número especifico de Pods esté siempre ejecutándose en el clúster. Si un Pod falla el **RC** se encargará de recrearlo automáticamente.

Maneja un conjunto replicado de Pods.
- Asegura que un número especificado de *réplicas* siempre se estén ejecutando
- Self Healing


# Services
Un **Service** en Kubernetes es una abstracción que proporciona una forma  estable de acceder a un conjunto de Pods. Esto es importante porque los Pods son efímeros y pueden moverse entre Nodes o ser recreados, lo que cambia sus direcciones IP

Service Discovery para los Pods.
- Endpoints persistentes para los Pods.
- Backend dinámicos basado en Labels.