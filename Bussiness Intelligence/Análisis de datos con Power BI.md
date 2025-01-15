Diplomado Gratuito de Análisis de datos con Power BI
# Sesión 1

- BI (Business Intelligence) es la habilidad de transformar los datos en información, y a su vez esta información en conocimiento para la toma de decisiones.

**¿Por qué implementar Business Intelligence?
- Descubrir patrones ocultos en la historia (datos)
- Necesidad de mantener acceso rápido y oportuno a los datos
- Realizar análisis predictivo
- Falta de visibilidad para las áreas clave del negocio

## Composición de BI

### ETL (Data Discovery)
- Extracción de datos
- Consolidación de Fuentes
- Limpieza y Transformación
- Automatización

### Modelamiento (Data Modeling)
- Relaciones
- Indicadores
- Patrones
- Optimización
Generar [[Notes from Business Intelligence#Indicadores Clave de Rendimiento (KPI)|KPI]] bajo un patron de optimización de base de datos

### Reportes (Data Visualization)
- Reportes
- Dashboards
- Story Telling with Data
- Filtros


## ¿Qué es Power BI?

Es un servicio de análisis de negocio que proporciona una vista detallada de los datos más críticos de la organización.

> Power BI es un pool de servicios

- Permite generar reportes y dashboards de forma intuitiva
- Capaz de manejar fuentes de información en la nube u on-premise
- Se conecta a un gran número de fuentes de datos
- Permite además interactuar desde cualquier dispositivo

## Composición de la Suite de Power BI

- Power BI Desktop
- Power BI Service: para compartir los informes, ejemplo:  [Microsoft Power BI](https://app.powerbi.com/view?r=eyJrIjoiZjRlODUwMDctZmVkMC00YWE2LTliMDMtMTU4YmEzYmFkNjU4IiwidCI6IjI5NjQxMTY5LTExODYtNDc2Mi1iYzI2LTRhOWY2NDg1ZmU4NSJ9)
- Power BI Mobile


## Componentes de Power BI

![[Pasted image 20250113204658.png]]


## Conexión a fuentes de datos
![[Pasted image 20250113204915.png]]


## Tipos de conexiones

### Direct Query
Power BI consulta directamente los datos requeridos en las tablas previamente seleccionadas. Al ser una conexión en vivo no es necesario actualizar la conexión. Una limitación importante para esta opción es que todas las tablas requeridas deben provenir de una sola base de datos. Asimismo, solo se puede usar esta opción con la lista de datos previamente mencionada.

### Import
Esta opción permite que las tablas y columnas seleccionadas se importen a Power BI, es decir, se hace una copia exacta de los datos. Si la fuente de datos ha sufrido actualizaciones es necesario actualizar en la herramienta para importar el nuevo conjunto de datos. Las tablas pueden venir de fuentes de datos diferentes y podemos relacionarlas en el Power BI


![[Pasted image 20250113205930.png]]


## Modelado de datos

![[Pasted image 20250113213838.png]]

## Visualización en Power BI

![[Pasted image 20250113220418.png]]



![[Pasted image 20250113220455.png]]

![[Pasted image 20250113220512.png]]

![[Pasted image 20250113220548.png]]


# Informes en Power BI
- Se basan en un único **conjunto de datos**. Cada una de las visualizaciones de un informe representa un fragmento de información.
- Es una o varias páginas de visualizaciones. Estos pueden compartirse con la organización con los niveles de permiso necesarios.
- Las visualizaciones no son estáticas. Puede agregar y quitar datos, cambiar los tipos de visualización y aplicar filtros y segmentaciones de datos.
- Es interactivo y personalizable, y las visualizaciones se actualizan según van cambiando los datos subyacentes.


![[Pasted image 20250113220606.png]]
