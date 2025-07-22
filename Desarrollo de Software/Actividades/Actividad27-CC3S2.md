
### Actividad: **Migrando a Microservicios: Docker, Kubernetes y CI/CD**

#### Escenario general

Tu equipo está desarrollando dos microservicios en Python (Users y Orders) que forman el núcleo de una plataforma de pedidos en línea. Quieres:

* Asegurar builds reproducibles y rápidos.
* Desplegar en un entorno local para pruebas de integración continua (CI).
* Evolucionar a un clúster de Kubernetes administrado en producción.
* Automatizar tests, builds y despliegues con GitHub Actions.

>Utiliza como referencia el siguiente repositorio: [Microservicios, Kubernetes y Github Actions](https://github.com/kapumota/DS/tree/main/2025-1/microservices-k8s)

#### A. Docker y Docker Compose

**Contexto:** Al empaquetar tus servicios, debe primar la consistencia entre entornos (dev, staging, prod) y minimizar el tiempo de despliegue.

1. **Arquitectura de contenedores**

   * Explica cómo un contenedor encapsula la aplicación y sus dependencias. ¿Qué ventajas ofrece frente a una VM en términos de arranque, consumo de recursos y portabilidad?
   * En tu proyecto, ¿qué pasos ocurren al ejecutar `docker build -t user-service .` y por qué cada uno es crítico para garantizar una imagen fiable?

---
El contenedor aísla la aplicación y sus dependencias. Es más ligero que una VM ya que usa el mismo kernel del sistema operativo anfitrión (Linux). Esto hace que sea más rápido de ejecutar, consuma menos CPU y RAM ya que no necesitan virtualizar todo un SO como los VM y además son faciles de portar mediante las imaǵenes de docker. Se puede subir una imágen a DockerHub para la comunidad.

Cuando ejecuto `docker built -t user-service .` primero debo estar ubicando en la misma carpeta donde se encuentra el archivo `Dockerfile`, si no es el caso debo especificar la ubicación. Ahora, el comando crea una **imagen** a partir de las instrucciones (pasos) del `Dockerfile`. Donde cada instrucción añade una capa a la imagen.

---

2. **Optimización de Dockerfile**

   * Analiza el `Dockerfile` de `service-user` y (diagrama de capas) justifica el orden de instrucciones.
   * Propón optimizaciones (por ejemplo, combinar instrucciones RUN, usar imágenes base más ligeras) y detalla cómo mejorarían el tiempo de build o el tamaño de imagen.

---

1. `FROM python:3.10-slim`: Es la imagén base, usa una versión de `python3.10` pero mucho más ligera.
2. `WORKDIR /app`: Aqui se define el directorio de trabajo dentro del contenedor. Las instrucciones como `COPY`, `RUN` o `CMD` se ejecutaran en `/app`.
3. `COPY requirements.txt`: Copia `requirements.txt` del directorio de trabajo hacia el directorio `/app` dentro del contenedor.
4. `RUN pip install --no-cache-dir -r requirements.txt`: Ejecutamos el comando dentro del contenedor.
5. `COPY app.py .`: Copiamos el archivo `app.py` del directorio de trabajo hacia el directorio `/app` dentro del contenedor.
6. `EXPOSE 8001`: El contenedor va a escuchar en el puerto `8001`
7. `CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8001"]`: Aqui se define el comando que se ejecutará por defecto al correr el contenedor.

Al momento considero que el `Dockerfile` ya es bastante ligero de por sí. 

---

3. **Redes y volúmenes en un entorno real**

   * Si tu microservicio necesitara persistir sesiones o logs de auditoría, ¿cómo montarías un volumen Docker?
   * En producción, ¿qué tipo de red usarías para comunicar los servicios `user` y `order` si estuviesen en distintos hosts, y por qué?

---

Lo que podria hacer el definir un directorio fuera del contenedor para que se almacenen alli datos como sesiones o logs. Por ejemplo.

Crearía un volumen en docker con 

```sh
docker volumen create service-user-logs
```

Luego al correr un contenedor usando la imagen `user-service` añadiría el montaje

```sh
docker run -v service-user-logs:/app user-service
```


---

4. **Docker Compose para entornos de desarrollo**

   * Diseña un `docker-compose.yml` que arranque:

     * `service-user` y `service-order`.
     * Una base de datos Redis para gestionar caché de sesión.
     * Un contenedor de administración (por ejemplo, phpMyAdmin o RedisInsight).
   * Explica cómo Compose acelera el onboarding de nuevos desarrolladores y facilita simular entornos de staging locales.

#### B. Infraestructura como Código (IaC)

**Contexto:** En tu pipeline CI/CD quieres tratar los manifiestos de Kubernetes igual que el código: revisión por pull request, versionado, validación automática.

5. **Principios de IaC**

   * Define IaC y enumera sus tres beneficios principales (reproducibilidad, trazabilidad, rollback).
   * Compara un script Bash que ejecute `kubectl apply` (imperativo) con un manifiesto YAML que describa un Deployment (declarativo). ¿Qué control de versiones y auditoría permite cada enfoque?

6. **Manifiestos Kubernetes como código fuente**

   * En el directorio `k8s/`, identifica en cada YAML:

     * El tipo de objeto (`Deployment`, `Service`) y su propósito.
     * El selector de pods y la configuración de puertos.
   * ¿Cómo encajarías estos archivos en tu flujo de GitFlow para asegurar revisiones de infraestructura antes de merge?

7. **Parametrización y reutilización**

   * Diseña un `ConfigMap` o `Secret` para extraer la URL de una base de datos PostgreSQL, de modo que puedas reutilizar el mismo Deployment en staging y producción cambiando sólo valores.
   * Explica brevemente cómo Helm o Kustomize automatizarían la generación de estos manifiestos según variables de entorno o valores por entorno.


#### C. Fundamentos de Kubernetes

**Contexto:** En producción, la plataforma correrá en un clúster gestionado que debe escalar automáticamente y recuperarse de fallos.

8. **¿Por qué Kubernetes?**

   * Imagina que aumentas el tráfico en un 10× durante una campaña de Black Friday. ¿Cómo ayudaría Kubernetes frente a un orquestador casero hecho con scripts?
   * Compara rápidamente Kubernetes con Docker Swarm en cuanto a ecosistema, escalabilidad y extensibilidad.

9. **Modelado de la arquitectura**

   * Dibujarás un diagrama con al menos un nodo (VM), varias réplicas de Pods y dentro de cada Pod dos containers (uno de aplicación y otro sidecar de logging).
   * Explica cómo las probes (liveness/readiness) garantizan que el tráfico no llegue a Pods no preparados o con problemas.

10. **Estrategias de despliegue**

    * Describe el objeto `Deployment`, su historia de revisiones (`RevisionHistoryLimit`) y las estrategias de rollout (`RollingUpdate` vs `Recreate`).
    * Explica cuándo usar `ClusterIP`, `NodePort` o `LoadBalancer` para exponer cada uno de tus servicios y su impacto en entornos on-premise vs nube pública.


#### D. Kubernetes – Entorno local con Minikube

**Contexto:** Antes de integrar con el clúster real, tu pipeline de CI debe validar despliegues en un entorno local idéntico (lo más posible) al de producción.

11. **Instalación del CLI**

    * Detalla los pasos para instalar `kubectl` en tu SO preferido y cómo configurar el autocompletado.
    * Comenta los comandos `kubectl version`, `kubectl config view` y qué información esencial devuelven.

12. **Arranque de Minikube**

    * Explica qué sucede al lanzar `minikube start --driver=docker`: creación de VM, adaptación de red, instalación de kube-apiserver.
    * Compara Minikube con Kind en cuanto a facilidad de integración en CI y recursos requeridos.

13. **Script de despliegue local**

    * Desglosa el script `minikube-setup.sh` en secciones: inicialización, build de imágenes, despliegue de manifests.
    * ¿Qué ventajas y limitaciones tiene esta aproximación para pruebas de integración automática en GitHub Actions?

14. **Limpieza y recuperación**

    * Indica cómo listar y eliminar los recursos de Kubernetes creados (`kubectl get all`, `kubectl delete namespace`).
    * En caso de fallo de un Deployment, ¿qué pasos seguirías para recuperar el servicio sin downtime?


#### E. CI/CD con GitHub Actions

**Contexto:** El objetivo es lograr una pipeline end-to-end que valide código, construya imágenes y despliegue a Minikube (y más adelante a producción) sin intervención manual.

15. **Anatomía del workflow**

    * Describe cada sección de `.github/workflows/ci-cd.yaml`: disparadores (`on`), jobs, steps y acciones usadas.
    * ¿Cómo encajarías una etapa adicional de tests unitarios y de integración antes de la etapa de build?

16. **Acciones Docker y kubectl**

    * ¿Por qué se emplea `docker/setup-buildx-action`? Explica qué es Buildx.
    * En el contexto de un runner de Actions, ¿por qué `push: false` y cómo modificas el workflow para empujar imágenes a Docker Hub o un registry corporativo?

17. **Despliegue remoto**

    * Si migras a EKS/GKE en AWS/GCP, ¿qué credenciales y pasos cambiarían en tu workflow para autenticar `kubectl` y proteger secretos?
    * Propón una estrategia para usar `environments` de GitHub y aprobar despliegues a staging/producción manualmente.

#### F. Preparación para producción

**Contexto:** Tras validar todo localmente y en staging, debes diseñar cómo llevarlo a tu clúster de producción con seguridad, observabilidad y cero downtime.

18. **Canary y Blue-Green**

    * Diseña un manifiesto o describirías el proceso (usando herramientas como Argo Rollouts) para hacer un despliegue canary de tu `user-service`.

19. **Seguridad en contenedores**

    * Menciona tres buenas prácticas: escanear imágenes (Clair, Trivy), mínima base (`distroless`, **scratch**), políticas de PSP/OPA Gatekeeper.

20. **Monitoreo y logs**

    * Propón un stack basado en Prometheus, Grafana y ELK/EFK para métricas y logs de tus microservicios. Explica cómo integrar un sidecar de Fluentd o Filebeat.
