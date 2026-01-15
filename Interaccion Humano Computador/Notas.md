
Perfecto 🚀, vamos a estructurar el proyecto como si fuera un análisis inicial de **UX + requerimientos funcionales**, definiendo:

1. **User personas** (perfiles de usuarios con necesidades distintas).
    
2. **Requerimientos por usuario** (qué esperan lograr).
    
3. **Casos de uso** (cómo interactúan con la app para lograr esos objetivos).
    

---

# 👤 **User Personas**

### 1. **Ana — Usuaria Sorda (28 años, estudiante universitaria)**

- **Objetivo:** Comunicarse de manera fluida en contextos sociales y académicos.
    
- **Frustración:** Depender de intérpretes o que la gente no entienda sus señas.
    
- **Motivación:** Autonomía y rapidez en la comunicación.
    

---

### 2. **Marco — Padre Oyente (45 años, trabajador)**

- **Objetivo:** Aprender lenguaje de señas para comunicarse con su hija sorda.
    
- **Frustración:** No encontrar material didáctico claro ni correcciones personalizadas.
    
- **Motivación:** Tener mejor relación con su hija y practicar a diario.
    

---

### 3. **Laura — Profesora Universitaria (35 años)**

- **Objetivo:** Entender preguntas y aportes de estudiantes sordos en clase.
    
- **Frustración:** No poder aprender señas rápidamente, sentir barrera de comunicación.
    
- **Motivación:** Inclusión en el aula y comunicación fluida con estudiantes.
    

---

### 4. **Diego — Joven Sordo (22 años, gamer y usuario digital)**

- **Objetivo:** Usar la app en videollamadas y chats con amigos oyentes.
    
- **Frustración:** En llamadas por Zoom/WhatsApp, nadie entiende sus señas.
    
- **Motivación:** Integrarse sin limitaciones en interacciones digitales.
    

---

### 5. **Juan — Funcionario Público (50 años, ventanilla municipal)**

- **Objetivo:** Atender ciudadanos sordos sin necesidad de intérprete en todo momento.
    
- **Frustración:** Malentendidos que retrasan trámites o generan frustración.
    
- **Motivación:** Eficiencia y servicio inclusivo en la atención al público.
    

---

# 📋 **Requerimientos por usuario**

|Persona|Requerimientos principales|
|---|---|
|**Ana (sorda)**|(R1) Reconocimiento en tiempo real de señas. (R2) Traducción clara a texto y voz. (R3) Confirmación visual con avatar.|
|**Marco (oyente, aprendiz)**|(R4) Modo práctica con corrección de señas. (R5) Feedback del avatar y sistema de progreso.|
|**Laura (profesora)**|(R6) Modo aula: subtítulos automáticos en tiempo real. (R7) Opción de voz clara y pausada.|
|**Diego (sordo, digital)**|(R8) Integración con videollamadas / chat. (R9) Subtítulos + voz para oyentes en tiempo real.|
|**Juan (funcionario)**|(R10) Modo ventanilla: frases predefinidas comunes. (R11) Confirmación de intención para trámites.|

---

# 📑 **Casos de Uso (aprox. 10)**

### Caso de Uso 1 — Traducción en vivo de señas a voz/texto

- **Actor:** Ana (sorda).
    
- **Objetivo:** Que sus señas se traduzcan automáticamente para un oyente.
    
- **Flujo:** Ana hace señas → cámara captura → IA reconoce → LLM genera frase → salida en texto/voz.
    

---

### Caso de Uso 2 — Confirmación visual con avatar

- **Actor:** Ana.
    
- **Objetivo:** Asegurarse de que la app entendió bien lo que quiso decir.
    
- **Flujo:** App muestra al avatar reproduciendo la seña detectada → Ana confirma visualmente.
    

---

### Caso de Uso 3 — Práctica de señas con corrección

- **Actor:** Marco.
    
- **Objetivo:** Aprender señas nuevas practicando.
    
- **Flujo:** Marco selecciona seña → hace gesto frente a la cámara → app compara con referencia → feedback visual/avatar → corrección mostrada.
    

---

### Caso de Uso 4 — Seguimiento de progreso (gamificación)

- **Actor:** Marco.
    
- **Objetivo:** Motivar el aprendizaje.
    
- **Flujo:** App registra nivel de precisión → otorga puntos/insignias → desbloquea señas más complejas.
    

---

### Caso de Uso 5 — Subtítulos en tiempo real en clase

- **Actor:** Laura.
    
- **Objetivo:** Entender preguntas de estudiantes sordos.
    
- **Flujo:** Estudiante hace seña → app traduce → texto aparece en pantalla/proyector → Laura lee la pregunta.
    

---

### Caso de Uso 6 — Conversación en videollamada

- **Actor:** Diego.
    
- **Objetivo:** Hablar con amigos oyentes en Zoom.
    
- **Flujo:** Diego hace señas → app traduce → subtítulos + voz en la llamada → amigos oyentes entienden.
    

---

### Caso de Uso 7 — Avatar como enseñanza en llamada

- **Actor:** Diego + amigos.
    
- **Objetivo:** Que amigos aprendan señas poco a poco.
    
- **Flujo:** Además de subtítulos, el avatar muestra la seña exacta → amigos ven la representación visual.
    

---

### Caso de Uso 8 — Atención en ventanilla pública

- **Actor:** Juan.
    
- **Objetivo:** Atender ciudadanos sordos en trámites.
    
- **Flujo:** Ciudadano hace seña → app traduce → voz dice: “Quiero renovar mi licencia” → funcionario responde.
    

---

### Caso de Uso 9 — Confirmación de intención en trámites

- **Actor:** Juan.
    
- **Objetivo:** Evitar errores en la interpretación.
    
- **Flujo:** App muestra opciones (“¿renovar licencia o duplicado?”) → ciudadano confirma con seña → procede.
    

---

### Caso de Uso 10 — Ayuda contextual (asistencia al usuario)

- **Actor:** Cualquier usuario nuevo.
    
- **Objetivo:** Entender cómo usar la app.
    
- **Flujo:** Si la seña no se reconoce, la app muestra mensajes de ayuda (“asegúrate de tener buena iluminación”, “coloca la mano dentro del cuadro verde”).
    

---

# ✅ Resumen

- **5 user personas** → representan usuarios clave (sordos, oyentes aprendices, profesionales, digitales, funcionarios).
    
- **Requerimientos (11 principales)** → cada persona tiene necesidades claras que definen funciones de la app.
    
- **Casos de uso (10)** → cubren traducción en vivo, aprendizaje, enseñanza, integración digital y atención pública.
    

---

👉 ¿Quieres que te organice esto en un **diagrama de casos de uso UML** (con actores y relaciones) para visualizarlo mejor?