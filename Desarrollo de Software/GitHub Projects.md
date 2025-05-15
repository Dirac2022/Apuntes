
## Resumen

GitHub Projects es una herramienta integrada en GitHub para planificar y hacer seguimiento de tu trabajo (issues, pull requests y notas) mediante vistas configurables como tablas, tableros Kanban o roadmaps ([GitHub Docs](https://docs.github.com/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects?utm_source=chatgpt.com "About Projects - GitHub Docs")). Sus conceptos clave incluyen **Backlog**, **Icebox**, **Sprint Backlog**, **In Progress**, **Review/QA**, **Done**, entre otros, cada uno representando un estado o prioridad dentro del flujo de trabajo ágil ([Help Center](https://help.zenhub.com/support/solutions/articles/43000010338-agile-concepts-in-github-and-zenhub?utm_source=chatgpt.com "Agile Concepts in GitHub and Zenhub - Help Center"), [ATD Data & Technology Services Wiki](https://atd-dts.gitbook.io/wiki/product-ops/github-project-management?utm_source=chatgpt.com "Agile Project Management with GitHub + Zenhub")). Además, Projects permite **automaciones**, **campos personalizados** y **vistas** para adaptar el tablero a las necesidades de tu equipo ([GitHub Docs](https://docs.github.com/en/issues/planning-and-tracking-with-projects?utm_source=chatgpt.com "Planning and tracking with Projects - GitHub Docs")).

---

## 1. ¿Para qué sirve “Projects” en GitHub?

GitHub Projects es un espacio colaborativo donde puedes **planificar**, **visualizar** y **priorizar** el trabajo asociado a tu repositorio o a toda tu organización en GitHub ([GitHub Docs](https://docs.github.com/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects?utm_source=chatgpt.com "About Projects - GitHub Docs")).

- **Integración nativa** con issues y pull requests: cualquier cambio en GitHub se refleja en tiempo real en tu tablero ([GitHub Docs](https://docs.github.com/en/issues/planning-and-tracking-with-projects?utm_source=chatgpt.com "Planning and tracking with Projects - GitHub Docs")).
    
- **Múltiples vistas**: el mismo conjunto de elementos se puede ver como tabla, Kanban o roadmap, con filtrado, agrupado y ordenación personalizados ([GitHub Docs](https://docs.github.com/en/issues/planning-and-tracking-with-projects?utm_source=chatgpt.com "Planning and tracking with Projects - GitHub Docs")).
    
- **Automatización**: mueve tarjetas automáticamente al cambiar el estado de un issue o PR, añade etiquetas o actualiza campos sin intervención manual ([GitHub Docs](https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/quickstart-for-projects?utm_source=chatgpt.com "Quickstart for Projects - GitHub Docs")).
    

---

## 2. Conceptos clave de GitHub Projects

### 2.1 Items

Todo lo que gestiona un proyecto son **items**, que pueden ser issues, pull requests o incluso **notas** libres que asocias manualmente ([GitHub Docs](https://docs.github.com/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects?utm_source=chatgpt.com "About Projects - GitHub Docs")).

### 2.2 Vistas

- **Tablero Kanban**: columnas con pipelines (To do, In Progress, Done…) donde arrastras tarjetas.
    
- **Tabla**: filas con todos los campos en columnas, ideal para filtrado y ordenación.
    
- **Roadmap**: vista temporal que muestra hitos a lo largo del tiempo. ([GitHub Docs](https://docs.github.com/en/issues/planning-and-tracking-with-projects?utm_source=chatgpt.com "Planning and tracking with Projects - GitHub Docs")).
    

### 2.3 Campos Personalizados

Puedes añadir campos como **Prioridad**, **Esfuerzo (story points)** o **Tipo** (bug, feature) para clasificar y filtrar ([GitHub Docs](https://docs.github.com/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects?utm_source=chatgpt.com "About Projects - GitHub Docs")).

### 2.4 Automaciones

Reglas predefinidas que, al cumplirse (por ejemplo, al cerrar un issue), mueven la tarjeta a otra columna o actualizan un campo ([GitHub Docs](https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/quickstart-for-projects?utm_source=chatgpt.com "Quickstart for Projects - GitHub Docs")).

### 2.5 Integraciones

Se vincula con GitHub Actions, Dependabot y otras apps para reflejar estados de CI/CD, dependencias, etc.

---

## 3. Secciones habituales en un tablero (pipelines)

A continuación, las secciones más comunes y su propósito:

|Sección|Descripción|Ejemplo de uso|
|---|---|---|
|**New Issues**|Issues recién creados, aún sin priorizar ni planificar.|Un usuario abre un issue de bug; se arrastra luego al Backlog cuando se decida priorizar. ([GitHub Docs](https://docs.github.com/en/issues/tracking-your-work-with-issues/configuring-issues/planning-and-tracking-work-for-your-team-or-project?utm_source=chatgpt.com "Planning and tracking work for your team or project - GitHub Docs"))|
|**Icebox**|Issue de baja prioridad, en espera de definición o recursos.|Ideas de mejoras lejanas; se mantienen con mínima información para retomar más adelante ([Help Center](https://help.zenhub.com/support/solutions/articles/43000010338-agile-concepts-in-github-and-zenhub?utm_source=chatgpt.com "Agile Concepts in GitHub and Zenhub - Help Center"))|
|**Backlog**|Lista priorizada de tareas pendientes de planificar en un sprint.|En reunión de planificación, se arrastran al Sprint Backlog las issues con mayor prioridad ([ATD Data & Technology Services Wiki](https://atd-dts.gitbook.io/wiki/product-ops/github-project-management?utm_source=chatgpt.com "Agile Project Management with GitHub + Zenhub"))|
|**Sprint Backlog**|Conjunto de issues asignadas al sprint actual.|Historias de usuario seleccionadas para la iteración vigente; suelen tener estimación de esfuerzo. ([Knowledge Kitchen](https://knowledge.kitchen/content/courses/agile-development-and-devops/scrum/github-project-management/?utm_source=chatgpt.com "GitHub - How to Do Project Management - Knowledge Kitchen"))|
|**On Deck**|Muchas veces sinónimo de Sprint Backlog o tareas “ya listas” para iniciar.|Issues preparadas con todos los criterios de aceptación listos.|
|**In Progress**|Tareas en las que alguien está trabajando actualmente.|Una feature en desarrollo; al abrir un PR, puede auto-moverse aquí.|
|**Blocked**|Tareas pausadas por dependencias externas o esperando feedback.|Bug que requiere respuesta del cliente; se etiqueta y mueve a esta columna.|
|**Review/QA**|Pull requests o issues que requieren revisión de código o pruebas.|Un PR abierto por desarrollo se revisa y se aprueba o se solicita cambios. ([GitHub](https://github.com/ElijahLawal-7/agile-final-project?utm_source=chatgpt.com "Agile and Scrum Final Project: Overview and Scenario - GitHub"))|
|**Done**|Tareas completadas y cerradas.|Issues cerradas que ya no requieren más acción.|
|**Archive**|Espacio opcional para terminar de guardar sprints o milestones antiguos.|Personaliza según flujo de tu equipo.|

---

## 4. Ejemplo práctico de flujo Scrum en GitHub Projects

1. **New Issues → Backlog**: cada issue nueva va a “New Issues” y, tras revisión, se mueve a “Backlog” para priorizar.
    
2. **Backlog → Sprint Backlog**: en la planificación de sprint, arrastras las top N issues al “Sprint Backlog”.
    
3. **Sprint Backlog → In Progress**: al empezar a trabajar, cambias a “In Progress”.
    
4. **In Progress → Review/QA**: al abrir un PR, la tarjeta se mueve automáticamente a “Review/QA”.
    
5. **Review/QA → Done**: tras aprobar el PR y cerrar el issue, la tarjeta termina en “Done”.
    
6. **Sprint cerrado → Icebox**: las tareas no completadas pueden pasar al “Icebox” para revaluar en el siguiente sprint ([GitHub](https://github.com/material-foundation/material-automation/issues/6?utm_source=chatgpt.com "Move items from a previous sprint's backlog and in-progress to the ...")).
    

---

## 5. Otros conceptos y buenas prácticas

- **Roadmap view**: planifica lanzamientos de versiones con hitos temporales.
    
- **Filtros y agrupaciones**: muestra sólo bugs de alta prioridad o agrupa por etiquetas.
    
- **Automatizaciones recomendadas**: Mover al Backlog cuando un issue recibe etiqueta “priority/low”, cerrar automáticamente issues merged.
    
- **Comentarios y actualizaciones de estado**: usa la descripción del proyecto como README para documentar tu flujo ([GitHub Docs](https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/best-practices-for-projects?utm_source=chatgpt.com "Best practices for Projects - GitHub Docs")).
    
- **Revisión periódica**: revisa semanalmente el Icebox para no olvidar ideas valiosas.
    
