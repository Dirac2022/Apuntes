# Prueba de entrada del curso CC3S2

## Proyecto completo: Juego de Trivia con FastAPI, PostgreSQL y DevOps

### Descripción del juego de trivia

El juego de Trivia es un juego de preguntas y respuestas donde los jugadores deben responder preguntas de opción múltiple presentadas en la consola. Cada pregunta contiene exactamente una respuesta correcta entre varias opciones. El juego es simple, pero debe ser implementado de manera que demuestre el manejo efectivo de la lógica básica de programación, estructuras de datos y pruebas unitarias.

#### Reglas y funcionamiento del juego

- **Inicio del juego:**  
  Al lanzar el juego, se muestra un mensaje de bienvenida junto con las instrucciones sobre cómo jugar.
  
- **Número de rondas:**  
  El juego constará de un total de 10 rondas, cada una con una pregunta única.
  
- **Preguntas:**  
  Se presenta una pregunta con cuatro opciones de respuesta numeradas. Solo una opción es correcta.
  
- **Selección de respuesta:**  
  El jugador elige su respuesta ingresando el número correspondiente a la opción elegida.
  
- **Puntuación:**  
  Cada respuesta correcta otorga un punto. No se penaliza por respuestas incorrectas.
  
- **Fin del Juego:**  
  Al finalizar las rondas, se muestra la puntuación total del jugador, junto con un desglose de respuestas correctas e incorrectas.

### Formato de salida en consola

- **Mensaje de inicio:**  
  ```
  Bienvenido al juego de trivia!
  Responde las siguientes preguntas seleccionando el número de la opción correcta.
  ```

- **Durante el juego:**  
  ```
  Pregunta 1: ¿Cuál es la capital de Francia?
  1) Madrid
  2) Londres
  3) París
  4) Berlín
  Tu respuesta: 3
  ¡Correcto!
  ```

- **Fin del juego:**  
  ```
  Juego terminado. Aquí está tu puntuación:
  Preguntas contestadas: 10
  Respuestas correctas: 8
  Respuestas incorrectas: 2
  ```

## Instrucciones por sprints

### Sprint 1: Estructura básica y preguntas

#### Objetivo

Configurar el entorno del proyecto y desarrollar la lógica básica para la manipulación y presentación de preguntas y respuestas.

#### Tareas

1. **Configuración del proyecto con FastAPI y Docker**
	- Crea un archivo Dockerfile para el entorno de FastAPI y PostgreSQL. 
2. **Desarrollo de la clase Question:**
	- Implementa la clase `Question` en Python para gestionar las preguntas y respuestas. 
3. **Implementación de la clase Quiz:**
	- Implementa la clase `Quiz` para manejar el flujo del juego, incluyendo la presentación de preguntas y la recepción de respuestas.
4. **Pruebas unitarias:**
	 - Configura `pytest` e implementa pruebas unitarias para la clase `Question`.
5. **Gestión de Git y branching:**
	- Configura Git y sigue las estrategias de branching.

### Sprint 2: Lógica del juego y puntuación

#### Objetivo

Implementar un sistema de puntuación y refinar la lógica del juego para manejar múltiples rondas y la terminación del juego.

#### Tareas

1. **Ampliar la clase Quiz:**
    - Amplía la clase `Quiz` para incluir un sistema de puntuación que rastree las respuestas correctas e incorrectas.  
2. **Pruebas unitarias para puntuación:**
	- Implementa pruebas para verificar el sistema de puntuación.
3. **Manejo de rondas y terminación del juego:**
	- Implementa la lógica para manejar las 10 rondas del juego y finalizarlo.
4. **Gestión de Git:**
    - Fusiona las ramas `feature` en `develop`.

### Sprint 3: Mejoras en la interfaz y refinamiento

#### Objetivo

Mejorar la interfaz de usuario en la consola y agregar características adicionales como niveles de dificultad.

#### Tareas

1. **Refinamiento de la interfaz de usuario:**
   - Mejora la presentación de preguntas y respuestas en la consola para hacerla más amigable.
2. **Niveles de dificultad:**
   - Introduce niveles de dificultad y ajusta las preguntas basándose en el desempeño del jugador.
3. **Resumen detallado al final del juego:**
   - Implementa un resumen detallado al finalizar el juego, mostrando las respuestas correctas e incorrectas.     
4. **Pruebas unitarias adicionales:**
   - Implementa pruebas unitarias adicionales para validar las mejoras.
5. **Gestión de Git:**
   - Fusiona la rama `feature/ui-improvements` en `develop` y luego fusiona `develop` en `main`.
6. **Pipeline CI/CD con GitHub Actions:**
   - Configura GitHub Actions para ejecutar las pruebas y verificar el despliegue con Docker.
     
#### Evaluación

- Implementación correcta de la lógica del juego.
- Interfaz de consola funcional.
- Correcto uso de TDD y refactorización.
- Cobertura de código superior al 90%.
- Funcionamiento del pipeline CI/CD.


## Ejercicios adicionales para reforzar CI/CD y DevOps

### Ejercicio 1: Mejora del pipeline CI/CD con GitHub Actions

**Objetivo:**  
Ampliar el pipeline CI/CD para incluir pruebas avanzadas, análisis de código estático y despliegue automático.

**Descripción:**  
El pipeline actual de GitHub Actions se encarga de ejecutar las pruebas. Este ejercicio requiere que se mejore el pipeline para incluir:
- Análisis de código estático con SonarQube.
- Pruebas de integración.
- Despliegue automático a un servidor de staging.

#### Pasos

1. **Configurar análisis de código estático:**
   - Instala y configura SonarQube en tu entorno local o utiliza una instancia de SonarCloud.
   - Añade un nuevo job en el archivo de GitHub Actions (`.github/workflows/ci.yml`) para ejecutar el análisis de código estático.

2. **Incluir pruebas de integración:**
   - Implementa pruebas de integración para la API de FastAPI utilizando `httpx` y `pytest`. 
   - Añade la ejecución de pruebas de integración en el pipeline.
     
3. **Implementar despliegue automático a un servidor de Staging:**
   - Configura un servidor de staging con Docker para alojar la aplicación.
   - Añade un nuevo job en el pipeline para crear y desplegar la imagen Docker en el servidor de staging.

**Resultado esperado:**  
El pipeline CI/CD debería ejecutar análisis de código estático, pruebas de integración y desplegar la aplicación automáticamente en un servidor de staging después de una fusión exitosa en `develop`.

### Ejercicio 2: Gestión de configuración y variables de entorno

**Objetivo:**  
Implementar la gestión de la configuración utilizando archivos `.env` y mejorar la seguridad manejando secretos en el pipeline CI/CD.

**Descripción:**  
Garantizar que las credenciales sensibles y configuraciones específicas del entorno se gestionen de forma segura y eficiente.

#### Pasos

1. **Configurar un archivo `.env`:**
   - Crea un archivo `.env` para almacenar las variables de entorno sensibles, como las credenciales de la base de datos.
   - Modifica la aplicación para que cargue estas variables desde el archivo `.env`.
     
2. **Configurar el pipeline para cargar variables de entorno:**
   - Modifica el pipeline CI/CD para cargar las variables de entorno de manera segura.
     
3. **Almacenar credenciales sensibles como secretos en GitHub Actions:**
   - Almacena las credenciales sensibles (claves de la base de datos, tokens de API, etc.) en los secretos del repositorio de GitHub.
   - Actualiza el pipeline para utilizar estos secretos.

**Resultado esperado:**  
La aplicación debería cargar la configuración de manera segura utilizando las variables de entorno, y el pipeline CI/CD manejará los secretos de forma segura a través de GitHub Actions.

### Ejercicio 3: Implementar pruebas automatizadas de seguridad

**Objetivo:**  
Garantizar la seguridad de la aplicación mediante la implementación de pruebas automatizadas de seguridad, como la verificación de vulnerabilidades.

**Descripción:**  
Utilizar herramientas como Bandit para escanear el código Python en busca de vulnerabilidades de seguridad.

#### Pasos

1. **Instalar y configurar Bandit:**
   - Instala Bandit para análisis de seguridad.
   - Añade un nuevo job en el pipeline de GitHub Actions para ejecutar Bandit.

2. **Configurar la política de seguridad:**
   - Configura una política de seguridad que defina las reglas y umbrales para las vulnerabilidades.

**Resultado esperado:**  
El pipeline CI/CD debería ejecutar `Bandit` para analizar el código en busca de vulnerabilidades, proporcionando un informe de seguridad en cada ejecución.


### Ejercicio 4: Implementar pruebas de carga y rendimiento

**Objetivo:**  
Garantizar que la aplicación pueda manejar múltiples usuarios simultáneos y verificar su rendimiento bajo estrés.

**Descripción:**  
Implementar pruebas de carga utilizando herramientas como Locust para simular múltiples usuarios y verificar el rendimiento.

#### Pasos

1. **Instalar y configurar Locust:**
   - Instala Locust y define un escenario de prueba.
   - Crea un archivo `locustfile.py` para simular la carga.

2. **Ejecutar pruebas de carga:**
   - Añade un paso en el pipeline para ejecutar Locust.
   
**Resultado esperado:**  
El pipeline CI/CD debería incluir pruebas de carga y rendimiento para asegurar que la aplicación puede manejar múltiples usuarios de manera eficiente.


## Implementación 

> Nota el código a continuación es de referencia.

### Día 1 - Configuración del entorno y estructura básica (Sprint 1 – Parte 1)

#### Objetivos
- **Configuración del proyecto:**  
  - Crear la carpeta del proyecto y configurar el entorno virtual.
  - Instalar FastAPI, Uvicorn, asyncpg, databases y otras dependencias.
- **Docker y Docker Compose:**  
  - Crear el `Dockerfile` para la aplicación.
  - Configurar el archivo `docker-compose.yml` para levantar PostgreSQL y el servicio web.
- **Inicialización en Git:**  
  - Iniciar el repositorio y crear la rama `develop` junto con la rama base para la estructura.

#### Tareas y comandos Git
- Crear la estructura del proyecto:
  ```bash
  mkdir trivia-game-python
  cd trivia-game-python
  python -m venv venv
  source venv/bin/activate
  pip install fastapi uvicorn asyncpg databases
  ```
- Crear archivos `Dockerfile` y `docker-compose.yml` con el contenido indicado.


----

```sh
mkdir trivia-game-python
cd trivia-game-python
python -m venv venv
venv\Scripts\activate
pip install fastapi uvicorn asyncpg databases
```


#### 📦 **Contenido del `Dockerfile`**

Primero te pongo el contenido del `Dockerfile` en un bloque de código, ya traducido y limpio:

```Dockerfile
FROM python:3.9-slim-buster

WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000", "--reload"]
```

---

#### 🧠 **Explicación línea por línea**

**`FROM python:3.9-slim-buster`**
- Esta línea indica la imagen base sobre la que se construirá el contenedor.
- Se está usando una versión liviana de Python 3.9 (`slim-buster`) para que el contenedor sea más pequeño y rápido de construir.

**`WORKDIR /app`**
- Establece el directorio de trabajo dentro del contenedor.
- Todas las siguientes instrucciones se ejecutarán desde `/app`.

**`COPY requirements.txt .`**
- Copia el archivo `requirements.txt` desde tu proyecto local al directorio de trabajo (`/app`) dentro del contenedor.

**`RUN pip install -r requirements.txt`**
- Ejecuta el comando para instalar todas las dependencias listadas en `requirements.txt` dentro del contenedor.

**`COPY . .`**
- Copia todos los archivos del directorio actual (donde está el `Dockerfile`) al directorio de trabajo en el contenedor (`/app`).

**`CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000", "--reload"]`**
- Es el comando que se ejecuta cuando el contenedor arranca.
- Aquí se está lanzando un servidor ASGI con **Uvicorn**, que correrá el archivo `main.py` y expondrá la app FastAPI que se encuentra en la variable `app`.
- `"--host", "0.0.0.0"`: Permite que se pueda acceder al servidor desde fuera del contenedor.
- `"--port", "8000"`: El servidor escuchará en el puerto 8000.
- `"--reload"`: Activa recarga automática (solo recomendado para desarrollo, no producción).

---

```yml
version: '3.8'

services:
  web:
    build: .
    ports:
      - "8000:8000"
    volumes:
      - .:/app
    depends_on:
      - db
    environment:
      DATABASE_URL: "postgresql://user:password@db:5432/trivia_db"

  db:
    image: postgres:13
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
      POSTGRES_DB: trivia_db
    ports:
      - "5432:5432"
    volumes:
      - db_data:/var/lib/postgresql/data/

volumes:
  db_data:
```

¡Perfecto! Vamos a desglosar tu archivo `docker-compose.yml` línea por línea para que entiendas bien qué hace, por qué se usan ciertos valores y cómo todo encaja.

---

📜 **`version: '3.8'`**

- Define la **versión del esquema de Docker Compose** que se está utilizando.
- La versión `3.8` es compatible con Docker 18.06.0+ y permite características como `depends_on`, `volumes`, y otras que usamos aquí.

---

🧩 **`services:`**

Aquí defines los **servicios** (contenedores) que formarán parte de tu aplicación. En este caso hay dos: `web` y `db`.

---

#### 🚀 Servicio `web` (tu app en FastAPI con Uvicorn)

```yaml
  web:
    build: .
```
- Le dice a Docker que **construya la imagen usando el Dockerfile en el directorio actual (`.`)**.


```yaml
    ports:
      - "8000:8000"
```
- Expone el puerto **8000 del contenedor** al puerto **8000 de tu máquina host**.
- Esto permite que puedas acceder a tu API FastAPI desde tu navegador o Postman en `http://localhost:8000`.

```yaml
    volumes:
      - .:/app
```
- **Montaje de volumen** que hace que todo el código fuente local se sincronice con `/app` en el contenedor.
- Útil para desarrollo, porque si haces cambios en tus archivos locales, se reflejan directamente en el contenedor sin necesidad de reconstruir.

```yaml
    depends_on:
      - db
```
- Le dice a Docker que este servicio **depende del servicio `db`**.
- Esto asegura que el contenedor `db` (PostgreSQL) **se inicie antes** que el de `web`.

> ⚠️ Ojo: `depends_on` **no espera** a que la base de datos esté "lista", solo a que haya arrancado el contenedor. A veces necesitas lógica extra para esperar a que esté disponible.

```yaml
    environment:
      DATABASE_URL: "postgresql://user:password@db:5432/trivia_db"
```
- Variable de entorno que probablemente tu aplicación usará para conectarse a la base de datos.
- Desglose del valor:
    - `user`: nombre de usuario de la DB
    - `password`: contraseña de ese usuario
    - `@db`: hostname del servicio `db` (Docker lo resuelve automáticamente)
    - `5432`: puerto por defecto de PostgreSQL
    - `/trivia_db`: nombre de la base de datos

---

#### 🗄️ Servicio `db` (base de datos PostgreSQL)

```yaml
  db:
    image: postgres:13
```
- Usa una imagen oficial de PostgreSQL, versión 13.

```yaml
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
      POSTGRES_DB: trivia_db
```
- Estas variables le dicen a PostgreSQL que cree una base de datos llamada `trivia_db` y configure el usuario y contraseña.

```yaml
    ports:
      - "5432:5432"
```
- Expone el puerto 5432 del contenedor (PostgreSQL) al puerto 5432 de tu máquina.
- Así puedes conectarte a la DB desde herramientas externas como DBeaver o pgAdmin.

```yaml
    volumes:
      - db_data:/var/lib/postgresql/data/
```
- Monta un volumen persistente para que **los datos de la base de datos no se pierdan** cuando el contenedor se reinicie o elimine.
- `/var/lib/postgresql/data/` es donde PostgreSQL guarda sus datos internamente.

---

📦 **`volumes:`**

```yaml
volumes:
  db_data:
```
- Define el volumen llamado `db_data`, usado por el servicio `db`.
- Docker lo crea automáticamente y lo guarda fuera del contenedor (persistente entre reinicios).

---

🧠 **Resumen general**

Este `docker-compose.yml`:

- Levanta una API hecha con FastAPI (`web`) y una base de datos PostgreSQL (`db`).
- Sincroniza el código local con el contenedor.
- Usa variables de entorno para configurar la conexión a la base de datos.
- Usa volúmenes para persistencia de datos.

¿Te gustaría que también te enseñe cómo levantar todo esto con `docker-compose up` y cómo verificar que funcione?


----

#### Continuación

- Inicializar Git y ramas:
  ```bash
  git init
  git branch develop
  git checkout develop
  git branch feature/estructura-inicial
  ```
- Realizar el primer commit:
  ```bash
  git add .
  git commit -m "Configuración inicial del proyecto y archivos Docker"
  ```
- **Registro diario:** Utilizar `git diff` para ver los cambios y `git blame` en los archivos modificados para registrar el historial.




### Día 2 - Implementación de la clase Question y pruebas unitarias (Sprint 1 – Parte 2)

#### Objetivos
- **Clase Question:**  
  - Implementar la clase `Question` en Python para gestionar preguntas y respuestas.
- **Pruebas unitarias:**  
  - Configurar pytest e implementar pruebas básicas para validar la funcionalidad de `is_correct`.

#### Tareas y comandos Git
- Crear el archivo `trivia.py` con la clase:
  ```python
  class Question:
      def __init__(self, description, options, correct_answer):
          self.description = description
          self.options = options
          self.correct_answer = correct_answer

      def is_correct(self, answer):
          return self.correct_answer == answer
  ```
- Crear el archivo `test_trivia.py` con pruebas unitarias:
  ```python
  import pytest
  from trivia import Question

  def test_question_correct_answer():
      question = Question("What is 2 + 2?", ["1", "2", "3", "4"], "4")
      assert question.is_correct("4")

  def test_question_incorrect_answer():
      question = Question("What is 2 + 2?", ["1", "2", "3", "4"], "4")
      assert not question.is_correct("2")
  ```
- Ejecutar pytest para validar:
  ```bash
  pytest
  ```
- Realizar commit en la rama:
  ```bash
  git add .
  git commit -m "Implementación de la clase Question y pruebas unitarias básicas"
  ```
- **Registro diario:** Utilizar `git diff` para ver diferencias y `git blame test_trivia.py` para asignar responsabilidad en el código.



#### Registro

![[blame-trivia-day2.png]]

![[blame-test_trivia-day2.png]]



### Día 3 - Implementación de la clase Quiz y flujo básico del juego (Sprint 1 – Parte 3)

#### Objetivos
- **Clase Quiz:**  
  - Desarrollar la clase `Quiz` para manejar el flujo del juego (añadir preguntas y obtener la siguiente).
- **Integración básica:**  
  - Conectar la lógica de `Question` y `Quiz` para permitir la presentación de preguntas.
- **Gestión de ramas:**  
  - Trabajar en una rama específica para la estructura básica, por ejemplo, `feature/estructura-basic`.

#### Tareas y comandos Git
- Crear la clase `Quiz` en `trivia.py`:
  ```python
  class Quiz:
      def __init__(self):
          self.questions = []
          self.current_question_index = 0

      def add_question(self, question):
          self.questions.append(question)

      def get_next_question(self):
          if self.current_question_index < len(self.questions):
              question = self.questions[self.current_question_index]
              self.current_question_index += 1
              return question
          return None
  ```
- Agregar lógica de interacción básica en una función (por ejemplo, `run_quiz()` que imprima las preguntas en consola).
- Realizar commit en la rama:
  ```bash
  git checkout -b feature/estructura-basic
  git add .
  git commit -m "Implementación de la clase Quiz y flujo básico del juego"
  ```
- **Registro diario:** Utilizar `git diff` para revisar cambios y `git checkout` para navegar entre ramas.



#### Registro
![[diff-trivia-day2.png]]



### Día 4 - Sistema de puntuación, manejo de rondas y finalización del juego (Sprint 2)

#### Objetivos
- **Ampliar la clase Quiz:**  
  - Incluir atributos para puntaje: `correct_answers` y `incorrect_answers`.
  - Implementar el método `answer_question` para actualizar la puntuación.
- **Manejo de rondas:**  
  - Definir la lógica para las 10 rondas y la terminación del juego.
- **Pruebas unitarias:**  
  - Agregar tests para validar el sistema de puntuación.

#### Tareas y comandos Git
- Modificar la clase `Quiz`:
  ```python
  class Quiz:
      def __init__(self):
          self.questions = []
          self.current_question_index = 0
          self.correct_answers = 0
          self.incorrect_answers = 0

      def add_question(self, question):
          self.questions.append(question)

      def get_next_question(self):
          if self.current_question_index < len(self.questions):
              question = self.questions[self.current_question_index]
              self.current_question_index += 1
              return question
          return None

      def answer_question(self, question, answer):
          if question.is_correct(answer):
              self.correct_answers += 1
              return True
          else:
              self.incorrect_answers += 1
              return False
  ```
- Actualizar las pruebas unitarias para incluir la verificación de la puntuación:
  ```python
  from trivia import Quiz, Question

  def test_quiz_scoring():
      quiz = Quiz()
      question = Question("What is 2 + 2?", ["1", "2", "3", "4"], "4")
      quiz.add_question(question)
      assert quiz.answer_question(question, "4") == True
      assert quiz.correct_answers == 1
  ```
- Implementar la función `run_quiz()` para el flujo de 10 rondas.
- Realizar commit:
  ```bash
  git add .
  git commit -m "Implementación de sistema de puntuación, manejo de rondas y finalización del juego"
  ```
- **Registro diario:** Usar `git blame` para verificar el origen de cada cambio en la clase Quiz y documentar el progreso.

### Día 5 - Mejoras en la interfaz de usuario y refinamientos (Sprint 3)

#### Objetivos
- **Interfaz de consola:**  
  - Refinar la presentación de preguntas y respuestas en la consola.
  - Agregar mensajes de bienvenida y resumen final detallado.
- **Características adicionales:**  
  - Incorporar niveles de dificultad (por ejemplo, ajustar la selección de preguntas según el rendimiento).
- **Gestión de ramas:**  
  - Crear una rama `feature/ui-improvements` para estos cambios y posteriormente fusionarla en `develop`.

#### Tareas y comandos Git
- Mejorar la función `run_quiz()`:
  ```python
  def run_quiz():
      print("Bienvenido al juego de Trivia!")
      print("Responde las siguientes preguntas seleccionando el número de la opción correcta.")
      quiz = Quiz()
      # Aquí se cargarán 10 preguntas, por ejemplo:
      # quiz.add_question(Question(...))
      while quiz.current_question_index < 10:
          question = quiz.get_next_question()
          if question:
              print(f"Pregunta {quiz.current_question_index}: {question.description}")
              for idx, option in enumerate(question.options):
                  print(f"{idx + 1}) {option}")
              answer = input("Tu respuesta: ")
              if quiz.answer_question(question, answer):
                  print("¡Correcto!")
              else:
                  print("Incorrecto.")
          else:
              break
      print("Juego terminado.")
      print(f"Preguntas contestadas: {quiz.current_question_index}")
      print(f"Respuestas correctas: {quiz.correct_answers}")
      print(f"Respuestas incorrectas: {quiz.incorrect_answers}")
  ```
- Realizar pruebas de la interfaz y ajustes en los mensajes.
- Crear y trabajar en la rama de mejoras:
  ```bash
  git checkout -b feature/ui-improvements
  git add .
  git commit -m "Mejoras en la interfaz de usuario y resumen final detallado"
  ```
- Revisar cambios con `git diff` y utilizar `git blame` para asegurar que cada parte del código se documente.
- Fusionar la rama en `develop`:
  ```bash
  git checkout develop
  git merge feature/ui-improvements
  ```
### Día 6 - Pipeline CI/CD y pruebas de integración 

#### Objetivos
- **CI/CD:**  
  - Configurar GitHub Actions para ejecutar pruebas unitarias e integración.
  - Incluir análisis de código estático (SonarQube/SonarCloud) y pruebas de integración para la API de FastAPI.
- **Pruebas de integración:**  
  - Implementar pruebas de integración utilizando httpx y TestClient de FastAPI.
- **Documentación del pipeline:**  
  - Crear y actualizar el archivo de workflow (por ejemplo, `.github/workflows/ci.yml`).

#### Tareas y comandos Git
- Crear el archivo `.github/workflows/ci.yml` con el siguiente contenido (adaptado a las necesidades):
  ```yaml
  name: Python CI

  on:
    push:
      branches: [develop, main]

  jobs:
    build:
      runs-on: ubuntu-latest
      steps:
        - uses: actions/checkout@v2
        - name: Set up Python
          uses: actions/setup-python@v2
          with:
            python-version: '3.9'
        - run: pip install -r requirements.txt
        - run: pytest
        - name: SonarQube Scan
          uses: sonarsource/sonarqube-scan-action@v1
          env:
            SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
          with:
            args: > 
              -Dsonar.projectKey=trivia-game-python 
              -Dsonar.sources=.
  ```
- Agregar pruebas de integración (por ejemplo, en `tests/integration/test_api.py`):
  ```python
  from fastapi.testclient import TestClient
  from main import app

  client = TestClient(app)

  def test_create_question():
      response = client.post("/questions/", json={
          "description": "What is 2 + 2?",
          "options": ["1", "2", "3", "4"],
          "correct_answer": "4"
      })
      assert response.status_code == 201
  ```
- Realizar commit:
  ```bash
  git checkout -b feature/ci-cd-integration
  git add .
  git commit -m "Configuración de pipeline CI/CD y pruebas de integración"
  ```
- **Registro diario:** Utilizar `git diff` para confirmar la correcta integración del pipeline y documentar cada cambio.

### Día 7 - Gestión de configuración, seguridad y pruebas de rendimiento

#### Objetivos
- **Gestión de variables de entorno:**  
  - Implementar un archivo `.env` para gestionar las credenciales sensibles.
  - Ajustar la aplicación para cargar configuraciones mediante `dotenv`.
- **Seguridad:**  
  - Agregar pruebas automatizadas de seguridad con Bandit.
- **Pruebas de carga:**  
  - Configurar pruebas de rendimiento utilizando Locust.
- **Revisión final:**  
  - Validar que la cobertura de código supere el 90%.
  - Preparar documentación final y realizar el merge final a `main` con tagging.

#### Tareas y comandos Git
- Crear un archivo `.env` con:
  ```env
  DATABASE_URL=postgresql://user:password@db:5432/trivia_db
  SECRET_KEY=mysecretkey
  ```
- Modificar la aplicación para cargar variables:
  ```python
  from dotenv import load_dotenv
  import os

  load_dotenv()
  DATABASE_URL = os.getenv("DATABASE_URL")
  SECRET_KEY = os.getenv("SECRET_KEY")
  ```
- Agregar pruebas de seguridad con Bandit en el pipeline:
  ```yaml
  - name: Run Security Scan
    run: bandit -r .
  ```
- Crear archivo `locustfile.py` para pruebas de carga:
  ```python
  from locust import HttpUser, task

  class TriviaUser(HttpUser):
      @task
      def play_trivia(self):
          self.client.get("/play")
  ```
- Realizar commit final y tagging:
  ```bash
  git checkout develop
  git merge feature/ci-cd-integration
  git merge feature/ui-improvements
  git merge feature/estructura-basic
  # Asegurarse de que todos los cambios están integrados en develop
  git checkout main
  git merge develop
  git tag -a v1.0 -m "Versión final del proyecto Trivia con CI/CD y pruebas de seguridad"
  git push --follow-tags
  ```
- **Registro diario:** Utilizar `git diff` y `git blame` para revisar todos los cambios realizados, y documentar cada ejercicio y ajuste final en el repositorio.

#### Consideraciones finales

- **Documentación:** Cada commit diario y el historial del repositorio deben evidenciar el avance del proyecto; se recomienda incluir comentarios en los commits que expliquen el propósito del cambio.
- **Uso de Git:** Se debe hacer uso intensivo de comandos como:
  - `git diff` para visualizar diferencias.
  - `git blame` para rastrear la autoría de las líneas.
  - `git checkout` y ramas para gestionar funcionalidades.
  - Tagging (`git tag`) para marcar versiones importantes.

El repositorio debe contener los avances diarios (commits) que demuestren el trabajo progresivo y no únicamente la versión final.

#### **Entrega**

1. **Ramas diarias:**  
   Crea una rama específica para cada día (por ejemplo, `feature/dia1`, `feature/dia2`, …, `feature/dia7`). Trabaja en cada rama durante el día y, al final, realiza un merge a la rama principal de desarrollo (por ejemplo, `develop`).

2. **Commits bien documentados:**  
   Realiza commits frecuentes durante el día con mensajes claros que reflejen los avances (por ejemplo, "Día 3: Implementación de la clase Quiz y flujo básico"). Esto permite rastrear fácilmente cada cambio usando `git log` o `git blame`.

3. **Uso de tags:**  
   Al finalizar cada día, asigna un tag que identifique el avance diario, por ejemplo:  
   ```bash
   git tag -a v1.0-day1 -m "Avance Día 1: Configuración inicial y Dockerfiles"
   git tag -a v1.0-day2 -m "Avance Día 2: Clase Question y pruebas unitarias"
   ```  

4. **CHANGELOG o archivo de registro:**  
   Incluye un archivo `CHANGELOG.md` donde resumas las actividades realizadas cada día, referenciando commits, ramas o tags específicos. Esto facilita una visión global del progreso.

5. **Subida final a GitHub:**  
   Una vez que se hayan integrado todos los avances en la rama `develop` y, posteriormente, se haya hecho el merge a `main`, al subir el repositorio a GitHub el instructor podrá:
   - **Revisar el historial de commits:** Con `git log` se evidenciarán los commits diarios y sus mensajes.
   - **Ver las ramas:** Las ramas diarias (`feature/dia1`, etc.) quedarán registradas en el repositorio, o bien se documentará en el `CHANGELOG.md` cómo se realizaron los merges.
   - **Consultar los tags:** Al listar los tags (con `git tag`), se podrán identificar rápidamente los hitos diarios.

> Sube esta tarea en tu repositorio personal en una carpeta que se llama `Prueba_entrada_CC3S2` y entrega el URL de ese repositorio en la plataforma del curso.


git tag -a v1.0-initial-commit 10a85e282a723c3ace00b15500285436b61b7a99 -m "Initial Commit: Basic project setup"

git tag -a v1.0-day1-question-class 4588fd964c0877ae72ef1374800aa77dd4761cb8 -m "Feature: Implementing Question class and tests"

git tag -a v1.0-day-2-quiz-class 0dd12c21f897fab7d00c34218db94bc88edaf4c1 -m "Feature: Implementing Quiz class and tests"

git tag -a v1.0-day2-changelog 0dd12c21f897fab7d00c34218db94bc88edaf4c1 -m "Docs: Added CHANGELOG.md file"