**Documentación**: [Documentación de GitHub Actions - Documentación de GitHub](https://docs.github.com/es/actions)

- [x] Clase 1 - Introducción al programa -Conceptos fundamentales de GitHub Actions ✅ 2025-07-13
- [x] Clase 2 - YAML y Workflows ✅ 2025-07-13
- [x] Clase 3 - Integración continua con GitHub Actions ✅ 2025-07-13
- [ ] Clase 4 - Integración con GitHub Packages
- [ ] Clase 5 - GitHub Marketplace
- [ ] Clase 6 - Desarrollo moderno con GitHub
- [ ] Clase 7 - Mejores prácticas
- [ ] Clase 8 - Fundamentos de GitHub para empresas
- [ ] Clase 9 - Actions y Workflows a nivel empresarial pt 1
- [ ] Clase 10 - Actions y Workflows a nivel empresarial pt 2



GitHub Actions es una herramienta de GitHub que nos ayuda a automatizar tareas a nuestro repositorio.
- CI (Continuous integration)
- CD (Continuos Deployment)

GitHub Actions nos permite crear Workflows que serán ejecutados en eventos específicos.
- Push
- Merge
- Pull-Request

**Casos de Uso**
Automatización
- Build
- Testing
- Notificaciones (Slack, Correos, Notion, Asana... )
- Escaneo de seguridad.
- ...

**Conceptos claves**
- Workflows
- Triggers
- Jobs
- Steps
- Runners

**Ejemplo**

```yaml
name: CI Pipeline

on: [push]

jobs:
  build-and-test:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4    # Descarga el código
    - run: npm install             # Instala dependencias
    - run: npm test                # Ejecuta pruebas
    - run: echo "Todo listo!"      # Mensaje
```

#### Workflows
Conjunto de procesos automatizados definidos en un archivo YAML dentro de `.github/workflows`.
Un **workflow** es un archivo YAML que define una serie de acciones que se ejecutan automáticamente en respuesta a eventos.


#### Triggers
- Eventos que hacen que el workflow se ejecute
- Son disparadores que inician un workflow
- Se definen utilizando `on`.

#### Jobs
Unidades independientes de trabajo dentro de un workflow. Un workflow puede tener varios jobs, y cada uno de ellos puede ejecutarse en paralelo o secuencialmente.

- Se ejecutan en paralelo por defecto.
- Cada job corre en un runner
- Se definen utilizando jobs

#### Steps
Pasos individuales dentro de un job
- Un job puede poseer multiples pasos..
- Se ejecutan secuencialmente en el mismo runner.
- Tiene la capacidad de usar variables de entorno.
- Se definen utilizando steps.
	- Utilizan `name`, `uses / run`

#### Runners
Entornos (máquinas virtuales) donde se ejecutan los jobs.
- GitHub posee imágenes actualizadas de S.O como Ubuntu, Windows, MacOS.
- Se definen utilizando `runs-on`

#### Action
Es un bloque de código reutilizable que realiza una tarea específica en un step


### CI (Continuous Integration)

<div style="text-align:center">
<img src="https://www.tierpoint.com/wp-content/uploads/2023/08/Benefits-of-Continuous-Integration-I-1-1024x670-1.webp" width=400>
</div>

- Proceso donde los desarrolladores integran cambios frecuentemente en el repositorio.
- Cada integración dispara una construcción automática (build) y pruebas automáticas (tests).
- Ayuda a detectar errores pronto y reduce conflictos entre ramas.

### CD (Continuous Delivery)

<div style="text-align:center">
<img src="https://cdn.prod.website-files.com/622642781cd7e96ac1f66807/685993100ca03c4abf836a6d_673e9e1c2e93004f9e55bbd4_6231822f4ff7298b67b02e9c_image3-8-1024x504.png" width=500>
</div>

- Extiende CI al proceso de entrega de código a un entorno de staging o pre-producción
- Aunque el despliegue a producción no es automático, el artefacto está siempre listo para ser desplegado.
- Permite liberar versiones confiables bajo demanda.

### CD (Continuous Deployment)

- Similar a la entrega continua, pero además automatiza el despliegue a producción.
- Cada cambio aprobado pasa directamente a producción sin intervención manual.

### Beneficios

- Entregas más rápidas y frecuentes.
- Mejor calidad de software gracias a pruebas automáticas.
- Reducción de errores y conflictos.
- Más confianza en los despliegues.
- Feedback rápido.





