[Comparación entre la arquitectura monolítica y la arquitectura de microservicios](https://www.atlassian.com/es/microservices/microservices-architecture/microservices-vs-monolith)

Una aplicación monolítica se compila como una sola unidad unificada, mientras que una arquitectura de microservicios es una serie de servicios pequeños que se pueden implementar de forma independiente.


# Arquitectura Monolítica

Una arquitectura monolítica es un modelo tradicional de un programa de software que se compila como una unidad unificada y que es autónoma e independiente de otras aplicaciones. La palabra "monolito" suele evocar algo grande y glacial, una imagen que no está alejada de la realidad de las arquitecturas monolíticas para el diseño de software. Una arquitectura monolítica es una red informática grande y única, con una base de código que aúna todos los intereses empresariales. Para hacer cambios en este tipo de aplicación, hay actualizar toda la pila, lo que requiere acceder a la base de código y compilar e implementar una versión actualizada de la interfaz del lado del servicio. Esto hace que las actualizaciones sean restrictivas y lentas.



## Ventajas
- **Simple de desarrollar**- único ciclo de vida; IDEs preparadas para una única aplicación.
- **Simples de Probar (testing)** - pruebas sobre una única aplicación
- **Simples de desplegar**- copiar un archivo o un directorio, a un equipo (servidor)
- **Simple de escalar**- se pueden ejecutar múltiples copias de la aplicación detrás de un balanceador de carga.

## Desventajas
- **Complejo manejar cambios** - por cada cambio $\rightarrow +$  redesplegar toda la aplicación. $+$ Riesgos  $\rightarrow +$ miedos  $\rightarrow +$  tests  $\rightarrow +$ tiempos $\rightarrow +$ coordinación y $+$ comunicación.
- **Mayores tiempos**– el negocio debe esperar
- **Calidad no garantizada** – por dependencias en el código.
- **Escalabilidad y Resilencia disminuida** – si un módulo requiere escalar lo debemos hacer para toda la aplicación. Si algo falla, todo deja de funcionar.


# SOA (Service Oriented Architecture)

La Arquitectura Orientada a Servicios (SOA) es un paradigma de arquitectura para diseñar y desarrollar sistemas distribuidos. Las soluciones SOA han sido creadas para satisfacer los objetivos de negocio los cuales incluyen facilidad y flexibilidad de integración con sistemas legados, alineación directa a los procesos de negocio reduciendo costos de implementación, innovación de servicios a clientes y una adaptación ágil ante cambios incluyendo reacción temprana ante la competitividad.

# Microservicios
Una arquitectura de microservicios, o simplemente "microservicios", es un método de arquitectura que se basa en una serie de servicios que se pueden implementar de forma independiente. Estos servicios tienen su propia lógica empresarial y base de datos con un objetivo específico. La actualización, las pruebas, la implementación y el escalado se llevan a cabo dentro de cada servicio. Los microservicios desacoplan los principales intereses específicos de dominios empresariales en bases de código independientes. Los microservicios no reducen la complejidad, pero hacen que cualquier complejidad sea visible y más gestionable, ya que separan las tareas en procesos más pequeños que funcionan de manera independiente entre sí y contribuyen al conjunto global.

Es un estilo de arquitectura, una forma de desarrollar una aplicación, basado en un conjunto de pequeños servicios, cada uno corriendo en sus propios procesos y comunicándose mediante mecanismos livianos, generalmente un recurso API de HTTP.

Estos servicios son altamente desacoplados, construidos alrededor de funcionalidades de negocio y desplegados de manera independiente a través de una maquinaria de despliegue completamente automatizada.

# Arquitectura Monolítica vs Microservicios
- Una aplicación monolítica pone todas sus funcionalidades en un único proceso y escala replicando lo monolítico en múltiples servidores
- Una arquitectura de microservicios pone cada elemento de funcionalidad en un servicio separado y escala distribuyendo dichos servicios a través de los servidores, según se requiera.

<div style="text-align:center">
<figure>
<img src="https://wac-cdn.atlassian.com/dam/jcr:b2be0d53-f4b2-46d8-9a34-993048cc6225/Monolith%20Vs%20Microservice%20image.png?cdnVersion=2470" alt="">
<figcaption>
</figcaption>
</figure>
</div>

