> **Tarea teórica:**  
> - Investigar una herramienta de IaC (p. ej. Terraform) y describir cómo organiza sus módulos.  
> - Proponer la estructura de archivos y directorios para un proyecto hipotético que incluya tres módulos: `network`, `database` y `application`. Justificar la jerarquía elegida.



Es una herramienta IaC que permite definir y administrar recursos de infraestructura a través de archivos de configuración. Terraform permite gestionar de manera declarativa una variedad de servicios y automatizar cambios en ellos, reduciendo el riesgo de errores producidos por operaciones manuales.

# HCP Terraform

**HCP Terraform** amplía estas funcionalidades al gestionar las ejecuciones de Terraform en un entorno seguro, en lugar de hacerlo en tu máquina local. Almacena de forma segura el estado y los datos sensibles y puede conectarse a sistemas de control de versiones para que puedas desarrollar tu infraestructura con un flujo de trabajo similar al del desarrollo de aplicaciones. La interfaz de usuario de HCP Terraform proporciona una vista detallada de los recursos gestionados por un proyecto de Terraform y ofrece una mayor visibilidad de cada operación realizada.

HCP Terraform también incluye un registro privado para compartir módulos y proveedores de Terraform dentro de tu organización. HCP Terraform facilita la colaboración en cada etapa del desarrollo de infraestructura.

**Resumen**
- **Ejecución gestionada**: Corre Terraform en un entorno controlado en lugar de en máquinas locales.
- **Almacenamiento seguro**: Guarda de forma segura el estado de la infraestructura y datos sensibles.
- **Integración con control de versiones**: Permite trabajar con flujos similares al desarrollo de aplicaciones.
- **Interfaz de usuario**: Proporciona visibilidad detallada de los recursos y operaciones de Terraform.
- **Registro privado**: Facilita compartir módulos y proveedores dentro de una organización.
- **Funciones avanzadas (de pago)**: Incluye control de acceso, políticas de gobernanza, estimaciones de costos y más.
- **Colaboración segura**: Permite revisión y aprobación de cambios antes de aplicarlos.
- **Prevención de conflictos**: Bloquea automáticamente el estado para evitar modificaciones simultáneas.


# Workflows
En HCP Terraform, los recursos se organizan en *workspaces*, que contienen las definiciones de los recursos, variables de entorno, variables de entrada y archivos de estado. Cada operación de Terraform ocurre dentro de un *workspace* y Terraform usa su configuración y estado para modificar la infraestructura.

HCP Terraform admite tres flujos de trabajo para ejecutar Terraform:
1. **Flujo basado en CLI**: Usa las herramientas estándar de la línea de comandos de Terraform para ejecutar operaciones en HCP Terraform.
2. **Flujo basado en UI/Sistema de Control de Versiones (VCS)**: Los cambios en repositorios de control de versiones activan ejecuciones en el *workspace* asociado.
3. **Flujo basado en API**: Permite interactuar programáticamente con la API de HCP Terraform para crear herramientas personalizadas.


# Instalación Manual


1. Descargar zip: [Install | Terraform | HashiCorp Developer](https://developer.hashicorp.com/terraform/install)
2. Descomprimir y colocarlo en una ruta específica
3. Agregar esa ruta al Path de variables de entorno
4. Ejecutar `terraform -help` en la terminal para comprobar la instalación.

# Terraform Workflow
[A Beginner’s Guide to Infrastructure Automation with Terraform | by Deepa Mathan | Medium](https://medium.com/@deepamathan/terraform-infrastructure-as-a-code-1dbf0f7ed3e1)
**Terraform Init**
- Terraform inicializa el directorio de trabajo que contiene los archivos de configuración de terraform.
- Descarga e instala el plugin del **proveedor** para que posteriormente pueda ser ejecutado.
- Crea un archivo de bloqueo `.terraform.locl.hcl` para registrar las selecciones de proveedores que realizó anteriormente. Y también, inicializa las configuración del backend.

**Terraform fmt**
- Se utiliza para reescribir los archivos de configuración de Terraform a un formato y estilo canónicos.


**Terraform Validate**
- El comando terraform `validate` valida los archivos de configuración en directorio.
- El comando `validate` valida si una configuración es sintácticamente válida y, por lo tanto, es principalmente útil para la verificación general de módulos reutilizables, incluida la exactitud de los nombres de atributos y los tipos de valor.

**Terraform Plan**
- Se utiliza para crear un plan de ejecución. No va a modificar las cosas en la infraestructura. Compara el estado deseado de terraform con el estado actual en la nube.
- Este comando es una forma cómoda de comprobar si el plan de ejecución de un conjunto de cambios coincide con sus expectativas sin realizar ningún cambio en el estado.

**Terraform Apply**
Aplica los cambios necesarios para alcanzar el estado deseado de la configuración. Este comando ejecuta el plan que ya está creado. Compara el estado correcto con el estado deseado.

**Terraform Destroy**
El comando `destroy` se utiliza para eliminar los recursos creados en la infraestructura administrada por Terraform


---- 

# ¿Como funciona Terraform?


[🔥🚀¡Terraform Zero to Hero Series! ¡Domine la infraestructura como código con demostraciones del mundo real! 🔥🚀 | por DevOps Guru | Medio](https://medium.com/@anilbidary/terraform-zero-to-hero-series-master-infrastructure-as-code-with-real-world-demos-25792b62e280)


Terraform crea y administra recursos en plataformas en la nube y otros servicios a través de sus interfaces de programación de aplicaciones (API). Los proveedores (providers) permiten que Terraform funcione con prácticamente cualquier plataforma o servicio con una API accesible. 

![](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*jbYes44NaqNPwa1iYHR2gQ.png)


### Provider
Los proveedores son los complementos que Terraform utiliza para administrar esos recursos. Cada plataforma de servicio o infraestructura compatible tiene un proveedor que define qué recursos están disponibles y realiza llamadas a la API para administrar esos recursos. Por lo tanto, el proveedor comprende las interacciones de la API y expone los recursos.

> - Registry .... directory of providers `https://registry.terraform.io`
> - Provider ... understant API interactions and expose resources
> - terraform init ... download provider


### Variables
Una variable en Terraform es un contenedor que contiene un valor. Se puede utilizar para representar diferentes valores en diferentes momentos durante la ejecución de un programa. Las variables en Terraform son una excelente manera de definir valores reutilizables controlados centralmente. Terraform admite 3 tipos diferentes de variables: 
- **Variables de entrada** como argumento de función
- **Variable de salida**, valor de retorno de la función similar.
- **Variables locales** como la variable local temporal de una función.

> [!note] Variable preferences
> Terraform loads variables in following order
> - Environment variable
> - Terraform.tfvars
> - Terraform.tfvars.json
> - \*.auto.tfvars or \*.auto.tfvars.json
> - Command line arguments (-var & -var-file)

# Workspaces
Los **workspaces** de Terraform están asociados a un directorio de trabajo específico y aíslan varios archivos de estado en el mismo directorio de trabajo, lo que le permite administrar varios grupos de recursos con un solo archivo de configuración.

Terraform comienza con un único espacio de trabajo denominado `default` que no se puede eliminar. Al ejecutar el plan de terraform en un nuevo **workspace**, Terraform no accede a los recursos existentes en otros **workspaces**. Estos recursos siguen existiendo físicamente, pero debe cambiar de espacio de trabajo para administrarlos.

Un uso común de varios **workspaces** es crear una copia paralela y distinta de la infraestructura para probar un conjunto de cambios antes de modificar la infraestructura de producción.

![](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*RV0DwjGcqUSWVwaavrqcJA.png)


# Terraform Module
Los módulos son el ingrediente clave para escribir código de Terraform reutilizable, mantenible y comprobable. Los módulos son contenedores para varios recursos que se utilizan juntos. Un módulo consiste en una colección de archivos `.tf` que se mantienen juntos en un directorio. 

Un módulo de terraform (generalmente un módulo raíz) puede llamar a otros módulos para incluir sus recursos en la configuración. Un módulo que ha sido llamado por otro módulo se denomina módulo secundario. El módulo secundario se puede definir dentro del módulo raíz mediante el bloque de módulo, que especifica la fuente del módulo y cualquier variable de entrada que deba establecerse.