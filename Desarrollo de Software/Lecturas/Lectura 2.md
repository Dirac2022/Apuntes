## Infraestructura como código, configuración, seguridad y administración

La infraestructura como código (IaC) es uno de los fundamentos en la ingeniería de software contemporánea. En este enfoque, la infraestructura de TI –que incluye servidores, redes, sistemas de almacenamiento, contenedores, balanceadores de carga y otros recursos necesarios para ejecutar aplicaciones– se trata de la misma manera que el código fuente de una aplicación. Esto implica que ==la configuración, el aprovisionamiento y la administración de los recursos se definen mediante archivos de texto o configuraciones declarativas, generalmente almacenadas en repositorios de control de versiones como Git==.

#### Concepto y principios de IaC

El concepto de IaC se apoya en la idea de que ==toda la infraestructura debe poder reproducirse de forma consistente en distintos entornos (desarrollo, pruebas, producción)==. Entre los principios fundamentales se destacan:

- **Reproducibilidad:** Al definir la infraestructura mediante archivos de configuración, cualquier persona o proceso automatizado puede ==recrear un entorno idéntico en distintos contextos==, eliminando discrepancias que surgen de configuraciones manuales.
- **Idempotencia:** Las herramientas utilizadas en IaC (como Terraform o Ansible) aseguran que ==ejecutar múltiples veces el mismo código no generará cambios adicionales== si el estado del sistema ya coincide con la configuración declarada.
- **Composabilidad:** La infraestructura se descompone en ==módulos o componentes reutilizables== que pueden ensamblarse de forma flexible ==para crear arquitecturas más complejas==, facilitando la gestión y el escalado.
- **Evolución controlada:** La posibilidad de ==versionar cada cambio en los archivos de configuración== permite llevar un historial preciso de las modificaciones, ==facilitando rollbacks y auditorías==.

#### Beneficios y buenas prácticas en IaC

Utilizar infraestructura como código permite una gestión más eficiente de los cambios, con una trazabilidad completa gracias al versionado. Cada modificación se puede revisar mediante [[Desarrollo de Software/Miscelanea#Pull Request| Pull Requests]], lo que fomenta la colaboración y reduce errores. Además, ==el uso de IaC libera a los equipos de la dependencia en configuraciones manuales== y ayuda a compartir conocimiento mediante la documentación inherente en el código.

> La IaC facilita la administración de infraestructuras. En lugar de modificar entornos de forma manual, los cambios quedan registrados en herramientas como `Git`, permitiendo su revisión antes de aplicarlos.
> **Ejemplo**: Si un equipo de DevOps necesita modificar una configuración de red en AWS usando Terraform, pueden realizar un  [[Desarrollo de Software/Miscelanea#Pull Request|Pull Request]]  con la actualización del código en el repositorio. Antes de aplicar los cambios, otros miembros del equipo pueden revisar el código y ejecutar pruebas en un entorno preproductivo para asegurarse de que funciona correctamente.

Algunas buenas prácticas incluyen:

- **Control de versiones y [[Desarrollo de Software/Miscelanea#Linting|linting]]:** Mantener los archivos en repositorios Git permite gestionar ramas, realizar revisiones y ejecutar pruebas en entornos [[Desarrollo de Software/Miscelanea#Entorno preproductivo|preproductivos]] . Herramientas como *terraform fmt* o *ansible-lint* ayudan a estandarizar el formato y reducir errores.
> Herramientas de linting garantizan que el código siga estándares de calidad y estructura. Si un ingeniero escribe una configuración de Terraform sin seguir un formato consistente, `terraform fmt` puede corregir automáticamente el estilo del código, asegurando uniformidad en el equipo.

- **Nomenclatura coherente:** Establecer convenciones claras para el nombrado de recursos y variables evita confusiones y facilita la reutilización de módulos.
> En Terraform, un recurso de almacenamiento en AWS puede nombrarse como `s3_proyecto_x_backup` en lugar de `storage1`, para identificar su propósito fácilmente


- **Gestión de secretos:** Es fundamental manejar de forma segura información sensible (como contraseñas o tokens) utilizando soluciones especializadas como HashiCorp Vault o AWS Secrets Manager. Así ==se evita exponer datos en texto plano en los archivos de configuración==.
> El almacenamiento de credenciales en texto plano representa un riesgo de seguridad. Herramientas de gestión de secretos permiten encriptar y restringir el acceso a esta información.
> **Ejemplo**: En lugar de incluir una clave API dentro de un archivo de configuración en Ansible, se puede usar [[Desarrollo de Software/Miscelanea#HashiCorp Vault|HashiCorp Vault]] para almacenarla y recuperar dinámicamente en tiempo de ejecución.


- **Infraestructura inmutable:** Se promueve la creación de nuevas instancias o contenedores cuando se necesita aplicar cambios, en lugar de modificar en caliente sistemas en producción. Este enfoque reduce el riesgo de configuraciones obsoletas o “deriva” y facilita la reversión a estados conocidos y limpios.
> En vez de modificar un contenedor en ejecución, se despliega una nueva versión de la aplicación y se redirige el tráfico a esta nueva instancia, asegurando una transición sin interrupciones

> [!Note]
> - `terraform fmt`: Formatea archivos de Terraform (`.tf`) para mantener un código limpio y consistente
> - `ansible-lint`: Analiza playbooks de Ansible en busca de errores y malas prácticas


#### Herramientas de aprovisionamiento y configuración

En el mundo de IaC, destacan diversas herramientas que se encargan tanto del [[Desarrollo de Software/Miscelanea#Aprovisionamiento|aprovisionamiento]] de recursos como de la gestión de configuraciones:

- **Terraform y CloudFormation:** Estas herramientas ==permiten describir el estado deseado de la infraestructura de forma declarativa==. Con un lenguaje propio, ==Terraform==, por ejemplo, utiliza ==HCL para definir recursos como instancias EC2, bases de datos o redes virtuales==.

>[!Tip]
>- **Terraform**: Es una herramienta **multi-nube**, es decir, puede gestionar infraestructura en AWS, Azure, Google Cloud, etc.
>- **CloudFormation**: Es específica de AWS, utilizada para describir infraestructura en la nube


- **[[Administración de Redes/Lecturas/Ansible|Ansible]], Chef y Puppet:** Se enfocan en la ==gestión de la configuración del sistema operativo y de aplicaciones==, asegurando que cada máquina o contenedor se encuentre en el estado deseado.

> [!tip]
>- **Ansible**: Basado en YAML, no necesita agentes (intermediario que se comunique con el servidor), usa [[Protocolos#SSH (Secure Shell)|SSH]] para administrar servidores.
>- **Chef**: Usa un lenguaje llamado `Ruby DSL` requiere un "servidor Chef" para distribuir configuraciones.
>- **Puppet**: Usa su propio lenguaje declarativo, ideal para grandes infraestructuras con nodos que se sincronizan con un servidor central

- **Packer:** Facilita la ==creación de imágenes de máquinas, ya sean para entornos virtualizados o para contenedores==, integrando scripts de configuración que permiten estandarizar entornos de despliegue.

#### Ejemplo de IaC y uso de Variables

Un ejemplo típico en Terraform podría consistir en la definición de una instancia de AWS EC2, utilizando variables para parametrizar la configuración y permitir su reutilización:

```hcl
# Definimos una variable, se usa para asignar un nombre descriptivo
# a la aplicacion en AWS
variable "nombre_de_la_aplicacion" {
  type        = string
  description = "Nombre descriptivo para la aplicación"
  default     = "mi_aplicacion"
}

# Esta variable permite parametrizar el tipo
# de instancia de AWS EC2
variable "instance_type" {
  type        = string
  description = "Tipo de instancia"
  default     = "t2.micro"
}

# Definicion de un recurso de AWS: una instancia EC2
resource "aws_instance" "app_server" {
  ami           = "ami-12345678" # Identificador de la imagen de Amazon Machine Image
  instance_type = var.instance_type # Se usa la variable definida anteriormente
  # Etiquetas para la instancia, utiles para identificacion y administracion en AWS
  tags = {
    Name = var.nombre_de_la_aplicacion # Se asigna el nombre de la aplicacion a la instancia
  }
}
```

Este enfoque permite que cualquier cambio en la infraestructura se documente y se controle de forma automática, facilitando la colaboración y la detección de desviaciones mediante herramientas de “terraform plan” que comparan el estado actual con el definido en los archivos.

#### Automatización y Orquestación de Entornos Locales

Herramientas como Vagrant permiten definir ==entornos virtuales reproducibles a través de un archivo denominado [[Desarrollo de Software/Miscelanea#Vagrantfile|Vagrantfile]]==. Esto resulta especialmente útil para crear entornos de desarrollo locales que se asemejen a la infraestructura de producción. Por ejemplo, un Vagrantfile puede definir una máquina virtual basada en Ubuntu, configurar redes, carpetas compartidas y ejecutar scripts de aprovisionamiento (por ejemplo, instalar Apache) de forma automática.

---

## Contenerización y despliegue de aplicaciones modernas

El avance de la contenerización ha revolucionado la forma en que se empaquetan y despliegan las aplicaciones. Docker se ha consolidado como el estándar de facto en este ámbito, permitiendo que las aplicaciones se ejecuten en entornos aislados y portables, sin importar las diferencias en los sistemas operativos de los hosts.

#### Fundamentos de Docker y la creación de imágenes

Docker utiliza características del kernel de Linux como *namespaces* y *cgroups* para aislar procesos en contenedores. El proceso de contenerización se inicia con la definición de un Dockerfile, un archivo de texto en el que se describen, de forma declarativa, las instrucciones necesarias para construir una imagen de contenedor.

Por ejemplo, un Dockerfile básico para construir una imagen que instale Python 3 podría ser:

```dockerfile
# Servira como sistema operativo dentro del contenedor
FROM ubuntu:20.04

# Actualizamos la lista de paquetes y luego instalamos Python3
RUN apt-get update && apt-get install -y python3

# Definimos el comando por defecto que ehjecutara el contenedor cuando se inicie
CMD ["python3", "--version"]
```

Cada instrucción en el Dockerfile genera una capa en la imagen, lo que permite aprovechar la caché para acelerar futuras reconstrucciones cuando no se han realizado cambios en las capas anteriores.

#### Ejecución y gestión de contenedores

Una vez construida la imagen con el comando:

```bash
docker build -t mi_imagen:1.0 .
```

se pueden ejecutar contenedores a partir de esta imagen, asignándoles nombres y ejecutándolos en modo “detached” para que funcionen en segundo plano:

```bash
docker run --name contenedor_ejemplo -d mi_imagen:1.0
```

El manejo de contenedores incluye también comandos para acceder a ellos (por ejemplo, `docker exec -it` para entrar de forma interactiva y realizar tareas de depuración), inspeccionar su configuración, revisar su historial de capas y obtener métricas de uso de recursos en tiempo real mediante `docker stats`.

#### Registros y depuración

La gestión de logs en Docker es esencial para la solución de problemas. La salida estándar y de error de cada contenedor se almacena y puede consultarse con `docker logs`, permitiendo así la monitorización de la actividad de la aplicación y la detección de anomalías. Esta capacidad de obtener retroalimentación inmediata es fundamental en entornos de despliegue continuo.

#### Orquestación con Kubernetes

Cuando las aplicaciones escalan y el número de contenedores aumenta, la administración manual se vuelve inviable. Aquí es donde Kubernetes entra en juego, ofreciendo una plataforma robusta para la orquestación de contenedores. ==Kubernetes organiza los contenedores en unidades llamadas *Pods*==, que pueden estar compuestos por uno o varios contenedores, y se gestiona a través de recursos como *ReplicaSets* y *Deployments*.

[[Kubernetes]]
#### Componentes y recursos de Kubernetes

- **Pods:** Son la unidad mínima de despliegue, encapsulando uno o varios contenedores que comparten red y almacenamiento.
- **ReplicaSet:** Asegura que un número definido de réplicas de un Pod esté siempre en ejecución.
- **Deployments:** Facilitan actualizaciones progresivas y permiten realizar rollbacks si es necesario, gestionando versiones de la aplicación de forma declarativa.
- **StatefulSets:** Se utilizan para aplicaciones con estado que requieren identidades de red únicas y volúmenes persistentes.

Además, Kubernetes permite la gestión de servicios (Services) que exponen los Pods a través de direcciones IP estables y mecanismos de descubrimiento, y utiliza *Secrets* y *ConfigMaps* para administrar información sensible y configuraciones sin necesidad de modificar las imágenes de contenedor.

#### Ejemplo de despliegue en Kubernetes

Un archivo YAML para definir un Deployment de una aplicación basada en Nginx puede verse de la siguiente manera:

```yaml
# Especifica la API de Kubernetes utilizada para este recurso
apiVersion: apps/v1

# Indica que este manifiesto define un Deployment, que administra la creacion
# y escalado de Pods
kind: Deployment 
metadata:
  name: mi-deployment
spec: # Especificacion del Deplyment
  replicas: 3 # 3 replicas del Pod en ejecucion
  selector: # Define como Kubernetes encuentra los Pods administrados por este Depl
    matchLabels:
      app: mi-app # Kubernetes seleccionara los Pods que tengan esta etiqueta
  
  # Plantilla para definir como deben ser los Pods creados por este Deployment
  template:
    metadata:
      labels:
        app: mi-app # Se adigna la misma etiqueta que en el selector para que 
        # el Deployment administre estos Pods

	# Especificacion de los contenedores dentro de los Pods
    spec:
      containers:
      - name: contenedor-web # Nombre del contenedor dentro del Pod
        image: nginx:latest # Imagen de Ngnix en su ultima version
```


>[!Nota] Explicación
>- Crea un conjunto de **Pods** basados en la imagen de `nginx:latest`.
>- Asegura que siempre haya tres réplicas del Pod en ejecución.
>- Si un Pod falla, Kubernetes automáticamente lo reemplaza.

>[!note] Nginx
>Es un servidor web y proxy inverso utilizado para
>1. Servir páginas web estáticas y dinámicas.
>2. Actuar como un balanceador de carga entre múltiples servidores backend.
>3. Mejorar la seguridad y el rendimiento con funciones como caché y control de acceso.

Este manifiesto indica que Kubernetes debe mantener tres réplicas de un Pod que ejecute la imagen de Nginx. Para exponer la aplicación, se puede definir un recurso *Service* que distribuya el tráfico:

```yaml
# Especifica la API de Kubernetes utilizada para este recurso
apiVersion: v1

# Indica que este manifiesto difine un Service, que expone Pods a la red
kind: Service

# Metadatos del Service
metadata:
  name: mi-servicio # Nombre del Service

# Especificacion del Service
spec:
  selector:
    app: mi-app # El Service asociara trafico a los Pods con esta etiqueta

# Definicion de los puertos expuestos
  ports:
    - protocol: TCP
      port: 80 # Puerto en el Service (externo)
      targetPort: 80 # Puerto del contenedor en los Pods
```

>[!note] Explicación
> - Expone los Pods del Deployment a la red del clúster.
> - Usa un selector (`api: mi-app`) para identificar qué Pods deben recibir el tráfico.
> - Redirige el tráfico del puerto `80` del Service al puerto `80` de los Pods que ejecutan Nginx.


Mediante comandos como `kubectl apply -f deployment.yaml` y `kubectl apply -f service.yaml`, los administradores pueden desplegar y gestionar la aplicación en el clúster, supervisar el estado de los Deployments y ajustar el número de réplicas según la demanda.

1. Aplicar el Deployment y el Service
```sh
kubectl apply -f deployment.yaml
kubeclt apply -f service.yaml
```
2. Verificar el estado de los Pods
```sh
kubectl get pods
```
3. Verificar el estado del Service
```sh
kubectl get services
```

---

## Despliegue de código y pipelines CI/CD en entornos DevSecOps

El avance de la contenerización y la orquestación ha impulsado la adopción de [[Desarrollo de Software/Miscelanea#Pipeline|pipelines]] de integración continua y entrega continua (CI/CD). Estas prácticas permiten ==automatizar el ciclo completo de construcción, prueba y despliegue de aplicaciones==, asegurando que cada cambio en el código se refleje de manera rápida y segura en los entornos de producción.

#### Herramientas y flujo de trabajo

Plataformas como Jenkins, GitHub Actions, GitLab CI y CircleCI permiten configurar pipelines que ==inician procesos de construcción al detectar cambios en el repositorio==. Estas plataformas integran diversas etapas, que pueden incluir:

- ==**Compilación y construcción de imágenes==:** Se utiliza Docker para generar imágenes a partir de un Dockerfile, asignándoles etiquetas basadas en identificadores de commit o versiones.
- ==**Pruebas automatizadas==:** Se ejecutan pruebas unitarias, de integración o de aceptación dentro de contenedores que simulan el entorno de producción.
- **==Análisis de seguridad==:** Los pipelines integran [[Desarrollo de Software/Miscelanea#Escáneres de vulnerabilidades|escáneres de vulnerabilidades]] y [[Desarrollo de Software/Miscelanea#Análisis de código (SAST y DAST)|análisis de código]] para detectar problemas de seguridad antes del despliegue.
- ==**Despliegue en entornos de staging y producción==:** Utilizando herramientas como Kubernetes y orquestadores de contenedores, se despliegan las nuevas versiones de la aplicación y se implementan estrategias de actualización progresiva, como despliegues canarios o azul/verde [[Lectura 1#Estrategias de despliegue y observabilidad|detalle]].

#### Ejemplo de pipeline con Skaffold y GitHub Actions

==*Skaffold*== es una herramienta desarrollada por Google que ==facilita el desarrollo iterativo y el despliegue continuo en entornos Kubernetes==. Un archivo de configuración, por ejemplo *skaffold.yaml*, define cómo construir la imagen, el contexto de compilación y los manifiestos de Kubernetes a aplicar:

```yaml
# Define la version de la API de Skaffold que se esta usando
apiVersion: skaffold/v2beta19

# Indica que este archivo es una configuracion de Skaffold
kind: Config
metadata:
  name: mi-aplicacion # Nombre de la aplicacion en Skaffold

# Seccion que define como se contruye la imagen del contenedor
build:
  artifacts:
    - image: mi-aplicacion # Nombre de la imagen que se va a construir
      context: . # Indica que el contexto de construccion es el directorio actual

# Seccion que define como se desplegara la aplicacion en Kubernetes
deploy:
  kubectl: # Usa `kubectl` para aplicar los manifiestos de Kubernetes
    manifests:
      - k8s/*.yaml # Aplica todos los archivos YAML dentro de la carpeta `k8s/`
```

>[!note] Explicación
>- Este archivo define cómo **Skaffold** manejará la construcción y despliegue de una aplicación Kubernetes.
>- `buid` especifica cómo se generará la imagen del contenedor.
>- `deploy` indica que los archivos de Kubernetes en `k8s/*.yaml` se aplicarán para despegar la aplicación.
>- Esto facilita el desarrollo iterativo y la integración con herramientas como Github Actions


Complementariamente, se puede configurar un pipeline en GitHub Actions que realice la construcción y despliegue de la imagen. Un ejemplo de archivo *workflow* podría incluir pasos para autenticar en un registro de contenedores, construir la imagen, publicarla y ejecutar pruebas dentro del contenedor:

```yaml
name: CI/CD Pipeline # Nombre del pipeline

on: # Define cuando se ejecutara este workflow
  push: # Se activara cuando haya un `push` en la rama "main"
    branches: [ "main" ]
  pull_request: # Tambien se ejecutara cuando haya un `pull request` hacia "main"
    branches: [ "main" ]

jobs:
  build_and_push: # Nombre del job, que construira y publicara la imagen
    runs-on: ubuntu-latest # Se ejecutara en una maquina virtual con Ubuntu
    steps:
      - name: Check out repository # Paso 1: Clona el codigo del repositorio
        uses: actions/checkout@v2

		# Paso 2: Inicia sesion en Docker Hub o un registro privado
      - name: Log in to Docker registry 
        run: |
          echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin

		# Paso 3: Construye la imagen Docker con un tag basado en el SHA del commit
      - name: Build Docker image
        run: |
          docker build -t $DOCKER_USERNAME/mi-aplicacion:${{ github.sha }} .

	    # Paso 4: Publica la iamgen en el registro de Docker
      - name: Push Docker image
        run: |
          docker push $DOCKER_USERNAME/mi-aplicacion:${{ github.sha }}

		# Paso 5: (Opcional) Ejecuta pruebas dentro del contenedor antes de desplegar
      - name: Run tests (opcional)
        run: |
          docker run --rm $DOCKER_USERNAME/mi-aplicacion:${{ github.sha }} npm test
```


>[!note] Explicación
>1. **Eventos que activan el pipeline**
>	- Se ejecuta en `push` a la rama `main`
>	- También cuando se hace un `pull request` a `main`
>2. **Pasos del pipeline**
>	- Descarga el código del repositorio
>	- Autentica en Docker Hub (o cualquier otro registro de contenedores)
>	- Construye la imagen Docker y la etiqueta con el `SHA` del commit
>	- Sube la imagen al registro para que otros servicios la usen
>	- Ejecuta pruebas dentro del contenedor para verificar su funcionalidad
>

Este flujo permite que, ante cada modificación en la rama principal, se realice la construcción de la imagen, su publicación en el registro y la ejecución de pruebas, garantizando que la nueva versión cumple con los estándares de calidad y seguridad.

#### Estrategias de Rollback y Gestión de Versiones

En escenarios de despliegue continuo, es crucial contar con mecanismos para revertir a versiones anteriores en caso de fallos. Kubernetes facilita la realización de rollbacks a través de sus Deployments, permitiendo regresar a una versión estable de la aplicación sin interrumpir el servicio. El pipeline CI/CD registra cada despliegue, lo que facilita la trazabilidad y la toma de decisiones en caso de incidencias.

---

## Observabilidad y monitoreo en entornos distribuidos

La observabilidad es un componente esencial en el desarrollo y operación de sistemas modernos. En entornos DevSecOps, donde las aplicaciones se despliegan continuamente y operan en infraestructuras distribuidas, contar con un enfoque completo de monitoreo, registro de logs y trazabilidad es indispensable para detectar problemas antes de que afecten a los usuarios finales.

#### Fundamentos de la observabilidad

La observabilidad combina tres pilares principales:

- **Monitoreo (Metrics):** La ==recolección de métricas del sistema== (uso de CPU, memoria, latencia de respuestas, tasa de errores) permite evaluar el estado de salud de la aplicación.
- **Logging (Logs):** El registro centralizado de [[Desarrollo de Software/Miscelanea#logs|logs]] ==facilita el análisis de eventos==, permitiendo a los equipos ==identificar anomalías== y comportamientos inesperados.
- **Trazabilidad (Tracing):** La capacidad de seguir el ==recorrido de una petición a través de distintos microservicios o componentes== permite detectar ==cuellos de botella== y entender la ==interacción entre diferentes partes del sistema.==

#### Prometheus y Grafana

Una de las combinaciones más utilizadas en entornos modernos es la de Prometheus y Grafana. ==Prometheus es una herramienta de monitoreo que utiliza un modelo de series temporales== y un lenguaje de consultas llamado ==PromQL== para ==extraer y procesar métricas de las aplicaciones==. La configuración de Prometheus se realiza mediante archivos YAML en los que se especifica, por ejemplo, el intervalo de scrape y los endpoints de ==El monitoreo recopila métricas del sistema== (uso de CPU, memoria, latencia de respuestas, tasa de errores), ==mientras que la observabilidad cuenta con un enfoque completo de monitoreo, registro de logs y trazabilidad==. La observabilidad  es indispensable para detectar problemas antes de que afecten a los usuarios finales las aplicaciones que exponen métricas.

Un fragmento típico de configuración para Prometheus podría ser:

```yaml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'mi-app'
    static_configs:
      - targets: ['app-service:8080']
```

==Grafana se encarga de visualizar estas métricas mediante dashboards personalizables==. Los paneles de Grafana permiten a los equipos monitorizar en tiempo real indicadores críticos como la latencia de respuestas, el número de peticiones y el consumo de recursos, facilitando la identificación de problemas y la toma de decisiones informada.

#### Alertas y respuestas automatizadas

==Prometheus puede integrarse con Alertmanager para configurar alertas que se activen cuando ciertas métricas superan umbrales definidos==. Estas alertas se pueden canalizar a sistemas de notificación como Slack, correo electrónico o plataformas de gestión de incidentes, permitiendo que los equipos respondan de forma inmediata ante cualquier anomalía.

>[!note] Ejemplos
>- Si un servidor usa más del 90% de RAM por 5 minutos, Prometheus detecta el problema y Alertmanager envía un correo al administrador para prevenir fallos.
>- Si un servidor web deja de responder por 1 minuto, Prometheus lo identifica y Alertmanager envía una alerta a Slack para que los ingenieros lo restauren rápidamente.

#### Integración de la observabilidad en DevSecOps

La estrategia de [[#Fundamentos de la observabilidad|observabilidad]] se integra en el pipeline de desarrollo y operación para proporcionar retroalimentación continua. Durante la fase de despliegue, la monitorización de métricas y logs ayuda a validar que cada nueva versión se comporta según lo esperado. En caso de que se detecten problemas, los equipos pueden iniciar procesos de rollback o aplicar correcciones de manera inmediata.

En entornos de microservicios y contenedores, la observabilidad se vuelve aún más crítica debido a la complejidad de las interacciones entre servicios. La combinación de Prometheus, Grafana y otras herramientas de tracing (como Jaeger o Zipkin) permite obtener una visión completa de la salud del sistema, desde la infraestructura subyacente hasta cada servicio desplegado en el clúster.

#### Integración de infraestructura, contenedores y observabilidad en DevSecOps

La integración de estas prácticas y herramientas conforma la base del desarrollo de software moderno y de entornos DevSecOps. ==Al tratar la infraestructura como código, se establece un entorno reproducible y versionable en el que cada cambio es controlado y auditado==. La contenerización con Docker permite empaquetar aplicaciones con todas sus dependencias, garantizando portabilidad y consistencia en cada despliegue. Kubernetes orquesta la ejecución de estos contenedores en clústeres, facilitando escalabilidad, alta disponibilidad y estrategias de despliegue controladas.

Simultáneamente, ==la integración de pipelines CI/CD automatizados asegura que cada modificación en el código pase por un riguroso proceso de construcción, pruebas y análisis de seguridad, mientras que la observabilidad proporciona la retroalimentación necesaria para mantener la confiabilidad y el rendimiento del sistema==. Este conjunto de prácticas permite que los equipos desarrollen, desplieguen y operen aplicaciones en entornos complejos con un alto grado de agilidad y seguridad, alineándose con los principios de DevSecOps.

Cada componente –desde el uso de Terraform para definir recursos hasta la implementación de alertas en Prometheus– forma parte de un ecosistema que potencia la colaboración entre desarrolladores, operadores y expertos en seguridad. Esta integración no solo optimiza los procesos técnicos, sino que también fomenta una cultura de responsabilidad compartida y mejora continua en las organizaciones.

==La capacidad de gestionar la infraestructura de forma automatizada, de construir imágenes de contenedores reproducibles y de desplegar aplicaciones a gran escala a través de Kubernetes, combinada con la monitorización en tiempo real, permite anticipar y mitigar problemas antes de que se conviertan en incidentes críticos==. Los flujos de trabajo basados en CI/CD, complementados con estrategias de rollback y análisis de logs, ofrecen la flexibilidad necesaria para responder a las demandas cambiantes del mercado y a los desafíos propios de entornos distribuidos.

