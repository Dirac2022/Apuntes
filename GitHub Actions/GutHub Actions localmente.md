### **Guía Completa: Ejecutar GitHub Actions Localmente con `act` en Ubuntu**  
*(Desde la instalación hasta la ejecución de tu workflow CI)*  

---

## **🔹 Paso 1: Instalar Homebrew (brew) en Ubuntu**
Si no tienes `brew` instalado, ejecuta:
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
Sigue las instrucciones en pantalla. Al finalizar, añade `brew` a tu `PATH`:
```bash
echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"' >> ~/.bashrc
source ~/.bashrc
```
**Verifica la instalación**:
```bash
brew --version
# Deberías ver algo como: Homebrew 4.x.x
```

---

## **🔹 Paso 2: Instalar Docker (requerido por `act`)**
`act` depende de Docker para crear contenedores. Instálalo con:
```bash
sudo apt update && sudo apt install docker.io
```
**Añade tu usuario al grupo Docker** (para evitar usar `sudo`):
```bash
sudo usermod -aG docker $USER
newgrp docker  # Recarga los permisos (o reinicia la terminal)
```
**Verifica que Docker funcione**:
```bash
docker run hello-world
# Deberías ver: "Hello from Docker!"
```

---

## **🔹 Paso 3: Instalar `act` con Brew**
```bash
brew install act
```
**Verifica la instalación**:
```bash
act --version
# Deberías ver algo como: act version 0.2.x
```

---

## **🔹 Paso 4: Configurar `act` (elección de imagen Docker)**
Al ejecutar `act` por primera vez, te pedirá elegir una imagen base:
```bash
cd ~/ruta/de/tu/proyecto  # Navega a tu proyecto
act -j test
```
Selecciona:
- **`Medium`** (recomendado para la mayoría de casos, ~500MB).  
  *(Usa flechas ↑/↓ y presiona Enter)*.

**Configuración permanente** (para evitar la pregunta en el futuro):
```bash
mkdir -p ~/.config/act
echo "defaults.image=ghcr.io/catthehacker/ubuntu:act-medium" > ~/.config/act/actrc
```

---

## **🔹 Paso 5: Ejecutar tu Workflow CI Localmente**
Desde la raíz de tu proyecto (donde está `.github/workflows/ci.yml`):
```bash
act -j test
```
**Opciones útiles**:
| Comando               | Descripción                                                                 |
|-----------------------|-----------------------------------------------------------------------------|
| `act -j test -v`      | Modo verbose (muestra más detalles)                                        |
| `act -j test -s GITHUB_TOKEN=tu_token` | Pasar secrets (simula variables de GitHub)               |
| `act -j test --env-file .env` | Usar variables de entorno desde un archivo `.env`                 |

---

## **🔹 Paso 6: Interpretar los Resultados**
- **✅ Éxito**: Verás una salida similar a la de GitHub Actions en tu terminal.  
- **❌ Error**: Revisa los logs para identificar en qué paso falló (ej: dependencias faltantes, errores en tests).

---

## **⚠️ Solución de Problemas Comunes**
1. **Error de permisos de Docker**:
   ```bash
   sudo chmod 666 /var/run/docker.sock
   ```
   *(O configura correctamente los permisos con `usermod` como en el Paso 2)*.

2. **`act` no encuentra tu workflow**:
   Asegúrate de que tu archivo YAML esté en:
   ```
   .github/workflows/ci.yml
   ```

3. **Problemas con Python o dependencias**:
   - Verifica que `requirements.txt` esté actualizado.
   - Ejecuta manualmente los comandos de tu workflow en un contenedor Docker para debuggear:
     ```bash
     docker run --rm -it -v $(pwd):/project ghcr.io/catthehacker/ubuntu:act-medium bash
     cd /project
     pip install -r requirements.txt
     pytest --cov=src
     ```

---

## **📌 Resumen de Comandos Clave**
```bash
# Instalar Brew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"' >> ~/.bashrc
source ~/.bashrc

# Instalar Docker y act
sudo apt install docker.io
sudo usermod -aG docker $USER
newgrp docker
brew install act

# Ejecutar CI local
cd ~/ruta/de/tu/proyecto
act -j test
```

---

### **🎯 ¿Por qué usar `act`?**
- **Evita commits/pruebas innecesarios** en GitHub.
- **Debug más rápido** al ver errores en tu máquina.
- **Prueba cambios en tu CI antes de subirlos**.

¡Con esto podrás iterar rápidamente sin frustraciones! 😊