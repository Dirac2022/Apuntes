
# 26-03-2025

- En grupo haremos las funciones de
	- Equipo de desarrollo
	- Equipo de QA
	- Equipo de operaciones (IaC)
- Adoptar las palabras técnicas para las exposiciones
	- Versión principal
- Para el despliegue de nuevas versiones en la nube se usa contenedores
- Hooks en git (revisar) -> genera un artefacto (¿Qué es un artefacto?)
- Staging es clave (revisar). Según en pipeline: Code -> Commit -> Build -> Unit Test -> Integration Test -> Review -> Staging -> Production
- Terraform: Aprovisionamiento
- Ansible: Configuración
- ¿Qué es Packer? (Hashicorp): Facilita la creación de imágenes
- Buena practica: limpieza automática (desde el repositorio)
- Secretos son: contraseñas, tokens, claves SSH, es clave en IaC
	- Inyectar dinámicamente estos secretos en ejecución
- ¿Qué es Vagrantfile?
	- Se combina con Terraform para aprovisionar entornos de desarrollo local o para crear CI/CD
	- Docker)
- Tener listo diapositiva y markdown