
# Reconocimiento Facial

### Objetivo General
Proyecto de investigación que tiene como objetivo la monitorización de ingreso y salida de investigadores del Tech Lab mediante modelos de visión artificial.

### Objetivos Específicos

**Software (Investigación y Desarrollo) - 2 Investigadores**
- Desarrollar un software basado en visión artificial para el reconocimiento facial.

### Plan de Trabajo

**Investigación de modelos de IA actuales para el reconocimiento facial (I)**
- Documentar modelos de visión artificial orientados a reconocimiento facial (D)
- Entrenar modelos
- Comparar métricas

**Definir la infraestructura y arquitectura del software de reconocimiento facial (I)**

**Desarrollar el algoritmo de todo el software (D)**
- Desarrollar Back End
- Desarrollar APIs
- Desarrollar Front End

---


### **Fase 1: Investigación y Planificación (Semana 1-2)**

El objetivo de esta fase es establecer una base sólida de conocimiento sobre las herramientas y arquitecturas disponibles, y tomar decisiones clave sobre el enfoque técnico del proyecto.

| Tarea                                       | Responsable(s) | Entregable(s)                 | Detalles Específicos                                                                                                                                                                                                                                                                                                                           |
| ------------------------------------------- | -------------- | ----------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Investigación de Modelos de IA**          | I1             | Documento Comparativo         | Investigar y comparar modelos como **FaceNet**, **ArcFace**, **VGGFace**, y librerías como **DeepFace** y **Dlib**. Evaluar la facilidad para el _fine-tuning_, la precisión y los requisitos computacionales.                                                                                                                                 |
| **Definición de Arquitectura del Software** | I2             | Diagrama de Arquitectura      | Diseñar una arquitectura de microservicios. Considerar un servicio para la captura de video, uno para el procesamiento y reconocimiento facial, una API REST para la comunicación y una base de datos para registrar los accesos.                                                                                                              |
| **Plan de Creación de Dataset Propio**      | I3             | Protocolo de Captura de Datos | Definir cómo se tomarán las fotografías de los investigadores: condiciones de iluminación, ángulos de la cara, expresiones faciales, y el número de imágenes por persona para asegurar un buen entrenamiento.                                                                                                                                  |
| **Selección de Tecnologías (Stack)**        | I1, I2, I3     | Listado de Tecnologías        | Decidir el lenguaje de programación principal (e.g., **Python**), el framework para el back-end (e.g., **FastAPI**, **Flask**), la base de datos (e.g., **PostgreSQL**) y las librerías de visión artificial (e.g., **OpenCV**, **TensorFlow/PyTorch**). Dado que usas VSCode en Windows, asegúrense de que las herramientas sean compatibles. |

---

### **Fase 2: Preparación de Datos y Entrenamiento del Modelo (Semana 3-5)**

Esta fase es crucial. La calidad del dataset y el correcto entrenamiento del modelo determinarán la precisión del sistema.

|Tarea|Responsable(s)|Entregable(s)|Detalles Específicos|
|---|---|---|---|
|**Recolección de Imágenes**|I3|Dataset Inicial de Rostros|Ejecutar el protocolo de captura de datos con todos los investigadores del Tech Lab. Organizar las imágenes en una estructura de carpetas adecuada para el entrenamiento.|
|**Preprocesamiento de Datos**|I1|Scripts de Preprocesamiento|Desarrollar scripts en Python para: detectar rostros en las imágenes (usando **MTCNN** o similar), alinear los rostros, normalizar la iluminación y el tamaño, y realizar _data augmentation_ (leves rotaciones, cambios de brillo) para mejorar la robustez del modelo.|
|**_Fine-tuning_ del Modelo Seleccionado**|I2|Modelo Re-entrenado|Adaptar el modelo pre-entrenado seleccionado (e.g., FaceNet) con el dataset propio. El objetivo es que el modelo aprenda a generar "embeddings" (vectores de características) únicos para cada investigador del Tech Lab.|
|**Evaluación y Comparación de Métricas**|I1, I2|Reporte de Métricas|Medir la precisión (_accuracy_), la tasa de falsos positivos y falsos negativos del modelo re-entrenado. Si es necesario, realizar ajustes en el preprocesamiento o en los hiperparámetros y volver a entrenar.|

---

### **Fase 3: Desarrollo del Software (Semana 6-9)**

Con un modelo funcional, el equipo se enfocará en construir la aplicación que lo utilizará.

|Tarea|Responsable(s)|Entregable(s)|Detalles Específicos|
|---|---|---|---|
|**Desarrollo del Back-End**|I2|Código Fuente del Servidor|Implementar la lógica del servidor. Esto incluye la gestión de la base de datos para almacenar los registros de entrada/salida y los perfiles de los investigadores.|
|**Desarrollo de la API REST**|I2|Documentación de la API (Swagger/OpenAPI)|Crear los _endpoints_ necesarios. Por ejemplo: `POST /check-in` que recibirá un frame de video, procesará el rostro y registrará la entrada. `GET /logs` para obtener un historial de accesos.|
|**Desarrollo del Algoritmo de Reconocimiento**|I1|Módulo de Reconocimiento|Crear un módulo que integre el modelo entrenado. Este módulo se encargará de: recibir una imagen, detectar y preprocesar el rostro, obtener el _embedding_ y compararlo con los _embeddings_ de los investigadores almacenados en una base de datos vectorial (e.g., **FAISS**) o un archivo para identificar a la persona.|
|**Desarrollo del Front-End (Interfaz de Monitorización)**|I3|Interfaz Web Básica|Desarrollar una interfaz simple (puede ser con **Streamlit** para un prototipo rápido o con un framework como **React/Vue** para algo más robusto) que muestre el video en tiempo real, los rostros detectados y un log de las personas reconocidas y la hora de su ingreso/salida.|

---

### **Fase 4: Integración, Pruebas y Despliegue (Semana 10-12)**

En esta última fase se unirá todo el trabajo realizado para crear el sistema final y ponerlo a prueba en un entorno real.

|Tarea|Responsable(s)|Entregable(s)|Detalles Específicos|
|---|---|---|---|
|**Integración de Componentes**|I1, I2, I3|Sistema Integrado|Conectar el front-end con la API del back-end. Asegurar que el flujo de datos desde la cámara hasta el registro en la base de datos sea correcto y eficiente.|
|**Pruebas en Entorno Real**|I3|Reporte de Pruebas|Instalar una cámara en la entrada del Tech Lab y probar el sistema en condiciones reales con los investigadores. Identificar fallos, como reconocimientos incorrectos bajo diferentes condiciones de luz o con accesorios (gafas, mascarillas).|
|**Ajustes Finales y Optimización**|I1, I2|Versión Final del Software|Basado en el reporte de pruebas, realizar los ajustes necesarios en el modelo o en el código para mejorar el rendimiento y la precisión del sistema.|
|**Documentación Final y Presentación**|I1, I2, I3|Documentación del Proyecto y Presentación|Crear un documento final que detalle la arquitectura, el modelo utilizado, los resultados de las métricas y una guía de uso del sistema. Preparar una presentación para mostrar el proyecto finalizado.|

Este plan de trabajo proporciona una estructura clara y divide las responsabilidades, permitiendo un desarrollo paralelo y eficiente. ¡Mucho éxito con tu proyecto!