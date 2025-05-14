Ansible es una plataforma de gestión de la configuración que automatiza el almacenamiento, los servidores y las redes. Cuando se utiliza Ansible para configurar estos componentes, las tareas manuales difíciles se vuelven repetibles y menos vulnerables a errores.

# ¿Cómo funciona Ansible?

Ansible simplifica la automatización de la tecnología al capturar grupos de recursos tecnológicos y admitir puestas en marcha multinivel desde el primer día. Ansible consolida los recursos de varios sistemas para gestionarlos desde una única plataforma en lugar de necesitar hacerlo de uno en uno. El código, el ciclo de vida y los cambios se pueden gestionar a través de inventario, libros de estrategia (*playbooks*) y funciones.

Un sistema de gestión de la configuración como Ansible se compone de varios componentes. Los sistemas que se gestionan pueden incluir servidores, almacenamiento, redes y software. Estos son los objetivos del sistema de gestión de la configuración. La finalidad es mantener estos sistemas en estados conocidos y determinados. Otro aspecto de un sistema de gestión de la configuración es la descripción del estado deseado para el sistema. El tercer aspecto principal de un sistema de gestión de la configuración es el software de automatización, el cual es responsable de garantizar que los sistemas y el software de destino se mantengan en el estado deseado.

El uso de Ansible reduce significativamente el tiempo de configuración y las puestas en 
marcha desde el primer día. El enfoque de Ansible, sin agentes y de fácil aprendizaje, 
convierte a esta gestión de la configuración en uno de los favoritos de los 
administradores de tecnología.


![][https://www.sokube.io/wp-content/uploads/014-a-ansible.png]



# Playbooks de Ansible

## Playbook
Un **playbook** es una lista de **plays** o **actos**. Un **play** es una lista de tareas que se aplican sobre un determinado conjunto de hosts. Si solo se tiene un conjunto de hosts, el playbook coincidirá con ese *play*. Cada tarea no es más que **una llamada a un módulo de Ansible**. 

<div style="text-align:center">
<figure>
<img src="https://i0.wp.com/rawstorage.wordpress.com/wp-content/uploads/2019/07/image.png?resize=624%2C335&ssl=1" alt="">
<figcaption>
Ansible Playbook Structure
</figcaption>
</figure>
</div>


# Ansible Tutorial: How Ansible Works?

Ansible se refiere a ==una plataforma o herramienta de automatización de código abierto que es útil para diferentes tareas de TI, como la gestión de configuraciones, orquestación entre servicios, despliegue de aplicaciones y aprovisionamiento==. La automatización es vital para gestionar entornos de TI complejos y simplificar las tareas complicadas de los desarrolladores. Ansible es una herramienta líder en automatización que ayuda a superar los desafíos de la automatización y garantiza una mejor productividad.

## Benefits of Ansible
Uno de los principales beneficios de Ansible es que **no requiere agentes**. No es necesario instalar ningún software adicional en el host o sistema para utilizar la herramienta de automatización. Ansible proporciona características flexibles y poderosas para gestionar sistemas operativos, servicios, redes e infraestructura. Ansible también es eficiente para permitir la personalización según las necesidades de los usuarios.

Algunos de los principales beneficios de Ansible son:

- **Gratis**: Ansible es una herramienta de código abierto que está disponible para los usuarios de forma gratuita.
- **Simple**: Muchos usuarios pueden preocuparse por cómo funciona Ansible. Pero en realidad, el proceso de configuración, así como su uso, es muy simple. El uso del software de Ansible no requiere habilidades excepcionales en codificación.
- **Eficiente**: Ansible es un software eficiente. No requiere software adicional para su instalación, pero ofrece espacio para los recursos de la aplicación en el servidor del usuario.
- **Poderoso**: Ansible es una herramienta poderosa que ayuda a los usuarios a modelar de manera eficiente los flujos de trabajo altamente complejos de la industria de TI.
- **Sin agentes**: El principal beneficio de usar Ansible es que no requiere agentes. Sin el uso de ningún software adicional, los clientes pueden automatizar fácilmente sus sistemas.
- **Flexible**: Independientemente de dónde se implemente el software, permite a los usuarios orquestar todo el entorno de la aplicación.
- **Extensible**: Dependiendo de las necesidades de red y automatización de los usuarios, Ansible puede ofrecer fácilmente extensiones.

## Uses of Ansible
Ansible has a long list of potencial methods and applications. The top uses of Ansible are:

### 1. Orchestration
Orchestration includes combing many different elements into a whole excellent operation. Ansible helps in making the orchestrations task easier. With the use of provisioning and automated workflows, it makes orchestration simple. Once the user defines the infrastructure with the use of Ansible playbooks, the user can make use of the same orchestration anywhere required.

### 2. Appplication Deployment
Application deployment is another important use of the ansible platform. It allows users to deploy multi-tier apps easily and quickly. There is no need for any custom for automating the system of the users. Only by listing the task and writing the playbooks, the automation can be done. With Ansible, there is no requirement of manual configuration.

### 3. Cloud Provisioning
Automating the life cycle of the user's application requieres the provisioning of the infrastructure. Ansible allows the users to provision virtualized hosts, cloud platforms, servers, and other network devices.

### 4. Security and Compliance
Ansible can help in ensuring security and compliance. When a user configures the security details on the control machine and runs the associated playbook, the remote hosts automatically update as per those security details. It enables the users to monitor all the machines for security compliance manually continuosly. Ansible, however, does not allow retrieving of the user ID and password of the admin in case of additional security needs.

## The Working of Ansible
Ansible works by connecting the server of the user through the [[Protocolos#SSH (Secure Shell)|SSH]] keys and pushing the small programs out. With the use of modules, the playbooks help the ansible clients in performing all the specific tasks. The particular functions can include the service of restarting, installing packages, rebooting servers, and much more. With the use of Ansible, a lot of things can be performed.

## The process in which Ansible works include:

<div style="text-align:center">
<figure>
<img src="https://miro.medium.com/v2/resize:fit:828/format:webp/1*ggZsV04skLhQNSV6cYH5ZQ.png" alt="">
<figcaption>
</figcaption>
</figure>
</div>


### 1. Setting the Architecture
The Ansible architecture consists of elements like modules, inventories, plugins, playbooks, and APIs. ==Ansible connects to the nodes and pushes out the ansible modules==. Modules refer to the small programs that the Ansible pushes out from the control machine to the remote hosts or nodes.

The written programs act as resource models for the desirable state of a system. With the use of playbooks, the modules get executed and control the files, services, and packages. Ansible uses all the Ansible modules for installing different updates or performing all the required tasks. After the completion of the task, Ansible removes the modules. 

Plugins are the extra codes that augment the functionality. All the nodes and control machines 
used with Ansible are listed under inventories with databases, IP addresses, and servers. 
Playbooks of the ansible architecture are like the instruction manuals for performing the tasks. 
They are the simple YAML written files that make ansible more popular. The APIs help in 
extending the connection types of Ansible, callbacks, and others.

### 2. SSH Keys
SSH keys are an essential part of how Ansible works. Even though passwords are supported, the SSH keys are one of the best ways of accessing Ansible. 

The authorized key to Ansible is an excellent way to use Ansible to control machines and access hosts. The authorization keys help in controlling the access of different modules to different users. The authorization keys come handy for varios IT systems 

### 3. Managing Inventory
Managing inventory is also an essential part of how Ansible works. Ansible represents all the 
machines that it manages on a simple INI file. It puts all the managed machines into groups 
according to the choice of the users. To add new machines, there is no requirement for 
additional SSL signings. It helps in eliminating all the issues relating to DNS or NTP. The 
elimination of SSL signing removes the hassle of linking a particular machine.

Ansible also offers to plugin to other sources available on the user’s infrastructure. It can 
easily plugin into groups, inventory, and other sources like OpenStack, EC2, Rackspace, and 
more. After the listing of the inventory hosts, the variables can be easily assigned to the text 
files in the inventory file. The use of dynamic inventory can help in pulling out the inventory 
of the user from data sources like Rackspace, OpenStack, or EC2
### 4. Using Ansible
Knowing how Ansible works, then it is the use. On availing the instance, the users can directly 
start using Ansible without any additional overhead. The users already have access to the 
running commands as well as the resource modules. It helps in making the use more 
straightforward. The modules of ansibles are very easy to write, and this makes the task 
execution even simpler

### 5. Ansible Playbooks
Playbooks of ansible help in finely orchestrating the infrastructure topology of the users. The simplicity of automation with Ansible is a feature that makes it more demanding.











