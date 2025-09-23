
<h5>Configuracion inicial</h5>
1. Ir a Administrador de dispositivos (Windows)
	1. Revisar Puertos (COM y LPT) que reconozca Arduino
2. En Arduino IDE
	![[Pasted image 20250912164609.png]]
3. En Arduino IDE
	![[Pasted image 20250912164642.png]]



# Laboratorio  1



# Laboratorio 2


##  Problema 4

```c
// Programa que al girar el potenciometro, este varia de 0 a 255

int pinPot = A0;
int valor;
int valorEscalado;
int ledPin = 9;

void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  pinMode(ledPin, OUTPUT);

}

void loop() {
  // put your main code here, to run repeatedly:
  valor = analogRead(pinPot);
  valorEscalado = map(valor, 0, 1023, 0, 255);
  Serial.println(valorEscalado);
  analogWrite(ledPin, valorEscalado);
  delay(100);

}
```



# **🔌 Programa con Potenciómetro - Explicación Completa**

## 🎯 **Concepto del Proyecto**

Un **potenciómetro** es una **resistencia variable**. Al girarlo, cambia su resistencia eléctrica y Arduino puede medir este cambio, convirtiendo una **posición física** (giro) en un **valor digital** (número).

## 📊 **¿Cómo funciona Arduino con entradas analógicas?**

- **Pines analógicos** (A0-A5): Miden valores entre **0-5V**
- **Resolución**: 10 bits → **1024 valores** (0-1023)
- **0** = 0V (GND)
- **1023** = 5V (máximo voltaje)

## 📝 **Análisis del Código Línea por Línea**

### **Declaración de Variables**
```cpp
int pinPot = A0;       // Constante: A0 = pin analógico 0
int valor;             // Variable para lectura cruda (0-1023)
int valorEscalado;     // Variable para valor convertido (0-255)
```

### **Setup() - Configuración Inicial**
```cpp
void setup() {
  Serial.begin(9600);  // Inicia comunicación serial a 9600 baudios
}
```

### **Loop() - Programa Principal**
```cpp
void loop() {
  valor = analogRead(pinPot);  // Lee el potenciómetro (0-1023)
  
  valorEscalado = map(valor, 0, 1023, 0, 255);  // Escala a 0-255
  
  Serial.println(valorEscalado);  // Muestra valor en monitor serial
  
  delay(100);  // Espera 100ms entre lecturas
}
```

## 🧮 **La Magia de la Función MAP()**

```cpp
valorEscalado = map(valor, 0, 1023, 0, 255);
```

**¿Qué hace?**:
- Toma un valor entre **0-1023** (entrada analógica)
- Lo convierte proporcionalmente a **0-255**
- **Fórmula**: `(valor × 255) / 1023`

**Ejemplo**:
- Si `valor = 512` → `(512 × 255) / 1023 ≈ 128`
- Si `valor = 1023` → `255`
- Si `valor = 0` → `0`

## 📋 **Constantes Predefinidas de Arduino**

### **Pines Digitales**
```cpp
const int LED_BUILTIN = 13;  // LED incorporado en la placa
```

### **Niveles Lógicos**  
```cpp
#define HIGH 1  // 5V (encendido)
#define LOW 0   // 0V (apagado)
```

### **Modos de Pines**
```cpp
#define INPUT 0      // Pin como entrada
#define OUTPUT 1     // Pin como salida
#define INPUT_PULLUP 2  // Entrada con resistencia pull-up interna
```

## 🔧 **Métodos y Funciones Esenciales de Arduino**

### **Configuración de Pines**
```cpp
pinMode(pin, MODE);  // Configura pin como INPUT/OUTPUT
```

### **Lectura/Escritura Digital**
```cpp
digitalRead(pin);     // Lee valor digital (HIGH/LOW)
digitalWrite(pin, estado);  // Escribe valor digital
```

### **Lectura Analógica**
```cpp
analogRead(pin);      // Lee valor analógico (0-1023)
```

### **Tiempo y Delay**
```cpp
delay(ms);           // Pausa en milisegundos
delayMicroseconds(us);  // Pausa en microsegundos
millis();            // Tiempo transcurrido en ms
```

## 💡 **Aplicaciones Prácticas del Potenciómetro**

### **Control de Intensidad LED**
```cpp
int ledPin = 9;  // Pin PWM (~)

void setup() {
  pinMode(ledPin, OUTPUT);
}

void loop() {
  int valorPot = analogRead(A0);
  int brillo = map(valorPot, 0, 1023, 0, 255);
  analogWrite(ledPin, brillo);  // Controla intensidad LED
}
```

### **Selector de Modos**
```cpp
void loop() {
  int modo = map(analogRead(A0), 0, 1023, 1, 5);
  
  switch(modo) {
    case 1: funcionModo1(); break;
    case 2: funcionModo2(); break;
    // ... etc
  }
}
```

## 🎮 **Mejora del Código Original**

```cpp
const int PIN_POT = A0;  // Constante con mayúsculas (convención)

void setup() {
  Serial.begin(9600);
  Serial.println("Sistema de lectura de potenciómetro");
  Serial.println("Valor (0-255):");
}

void loop() {
  int valorCrudo = analogRead(PIN_POT);
  int valorEscalado = map(valorCrudo, 0, 1023, 0, 255);
  
  // Muestra ambos valores para debugging
  Serial.print("Crudo: ");
  Serial.print(valorCrudo);
  Serial.print(" | Escalado: ");
  Serial.println(valorEscalado);
  
  delay(100);
}
```

## 📊 **¿Qué verás en el Monitor Serial?**

```
Crudo: 0 | Escalado: 0
Crudo: 512 | Escalado: 128  
Crudo: 1023 | Escalado: 255
Crudo: 256 | Escalado: 64
```

## 🚨 **Errores Comunes y Soluciones**

1. **Valores erraticos**: 
   - Verifica conexiones del potenciómetro
   - Asegura que los 3 pines estén conectados: 5V, GND, y A0

2. **No lee correctamente**:
   - Usa `pinMode(A0, INPUT)` si es necesario (aunque analogRead() lo configura automáticamente)

3. **Valores siempre en 0 o 1023**:
   - Revisa que el potenciómetro esté bien conectado a 5V y GND

¿Te gustaría que profundice en algún concepto específico o tienes alguna otra duda? 😊

## Problema 5


```c
// Programa que al girar el potenciometro, este varia de 0 a 255

int pinPot = A0;
int valor;
int valorEscalado;
int ledPin = 9;

void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  pinMode(ledPin, OUTPUT);

}

void loop() {
  // put your main code here, to run repeatedly:
  valor = analogRead(pinPot);
  valorEscalado = map(valor, 0, 1023, 0, 255);
  Serial.println(valorEscalado);
  analogWrite(ledPin, valorEscalado);
  delay(100);

}
```

![[Pasted image 20250912185538.png]]