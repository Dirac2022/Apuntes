# Actividad: Escribiendo infraestructura como código en un entorno local con Terraform

####  Contexto

Imagina que gestionas docenas de entornos de desarrollo locales para distintos proyectos (app1, app2, ...). En lugar de crear y parchear manualmente cada carpeta, construirás un generador en Python que produce automáticamente:

* **`network.tf.json`** (variables y descripciones)
* **`main.tf.json`** (recursos que usan esas variables)

Después verás cómo Terraform identifica cambios, remedia desvíos manuales y permite migrar configuraciones legacy a código. Todo sin depender de proveedores en la nube, Docker o APIs externas.


## Fase 0: Preparación 

1. **Revisa** el [proyecto de la actividad](https://github.com/kapumota/DS/tree/main/2025-1/Iac_orquestador_local)  :

   ```
   modules/simulated_app/
     ├─ network.tf.json
     └─ main.tf.json
   generate_envs.py
   ```
   
2. **Verifica** que puedes ejecutar:

   ```bash
   python generate_envs.py
   cd environments/app1
   terraform init
   ```

<img src="imgs20/Pasted image 20250528075903.png" >

<img src="imgs20/Pasted image 20250529183125.png" >


3. **Objetivo**: conocer la plantilla base y el generador en Python.

##  Fase 1: Expresando el cambio de infraestructura

* **Concepto**
Cuando cambian variables de configuración, Terraform los mapea a **triggers** que, a su vez, reconcilian el estado (variables ->triggers ->recursos).

* **Actividad**

  - Modifica en `modules/simulated_app/network.tf.json` el `default` de `"network"` a `"lab-net"`.
  - Regenera `environments/app1` con `python generate_envs.py`.
  - `terraform plan` observa que **solo** cambia el trigger en `null_resource`.

* **Pregunta**

  * ¿Cómo interpreta Terraform el cambio de variable?
  * ¿Qué diferencia hay entre modificar el JSON vs. parchear directamente el recurso?
  * ¿Por qué Terraform no recrea todo el recurso, sino que aplica el cambio "in-place"?
  * ¿Qué pasa si editas directamente `main.tf.json` en lugar de la plantilla de variables?

### Procedimiento

1. En `modules/simulated_app/network.tf.json`, cambia:

```diff
     "network": [
       {
   -     "default": "net1",
   +     "default": "lab-net",
         "description": "Nombre de la red local"
       }
     ]
```
   
2. Regenera **solo** el app1:

   ```bash
   python generate_envs.py
   cd environments/app1
   terraform plan
   ```

local-network

---

<img src="imgs20/Pasted image 20250528092602.png" >

```sh
 Error: Inconsistent dependency lock file
│ 
│ The following dependency selections recorded in the lock file are inconsistent with the current configuration:
│   - provider registry.terraform.io/hashicorp/null: required by this configuration but no version is selected
│ 
│ To make the initial dependency selections that will initialize the dependency lock file, run:
│   terraform init
```



<img src="imgs20/Pasted image 20250529183754.png" >

---




   Observa que el **plan** indica:

   > \~ null\_resource.app1: triggers.network: "net1" -> "lab-net"


## Fase 2: Entendiendo la inmutabilidad

### A. Remediación de 'drift' (out-of-band changes)

### 1. **Simulación**

---

Para ello primero inicialicé el directorio:

```sh
cd envirnments/app2
terraform init
terraform apply -auto-approve
```

<img src="imgs20/Pasted image 20250601181302.png" >


---

Ahora si puedo hacer los cambios

```bash
cd environments/app2
# edita manualmente main.tf.json: cambiar "name":"app2" ->"hacked-app"
```

### 2. Ejecuta:

```bash
terraform plan
```

Verás un plan que propone **revertir** ese cambio.

---
Al aplicar `terraform plan` obtuve

<img src="imgs20/Pasted image 20250601181510.png" >

Lo que indica que se gestionará un reemplazo en el valor de la clave `name` de `app2`  a `hacked-app`.
No aparece ningún plan que proponga revertir tal cambio.


---


### 3. **Aplica**

```bash
terraform apply
```

Y comprueba que vuelve a "app2".

---

Al ejecutar `terraform apply` puedo validar en `terraform-tfstate` que `"name":"hacked-app"`.


```json
// ...
      "instances": [
        {
          "schema_version": 0,
          "attributes": {
            "id": "1405531010122334671",
            "triggers": {
              "name": "hacked-app", // Aqui
              "network": "net2"
            }
          },
          "sensitive_attributes": [],
          "identity_schema_version": 0
        }
      ]
// ...
```

--- 
   
### B. Migrando a IaC

#### **Mini-reto**

##### 1. Crea en un nuevo directorio `legacy/` un simple `run.sh` + `config.cfg` con parámetros (p.ej. puerto, ruta).

```sh
echo 'PORT=8080' > legacy/config.cfg
echo '#!/bin/bash' > legacy/run.sh
echo 'echo "Arrancando $PORT"' >> legacy/run.sh
chmod +x legacy/run.sh
```
  
##### 2. Escribe un script Python que:

- Lea `config.cfg` y `run.sh`.
- Genere **automáticamente** un par `network.tf.json` + `main.tf.json` equivalente.
* Verifique con `terraform plan` que el resultado es igual al script legacy.

---

```python
import os
import json
import re

LEGACY_DIR = "legacy"
CONFIG_FILE = os.path.join(LEGACY_DIR, "config.cfg")
RUN_SCRIPT = os.path.join(LEGACY_DIR, "run.sh")
OUTPUT_DIR = "generate_from_legacy"
APP_NAME = "app_legacy"

def parse_config_cfg(filepath):
    params = {}
    with open(filepath, 'r') as f:
        for line in f:
            line = line.strip()
            if not line or line.startswith('#'):
                continue
            match = re.match(r'(\w+)=(.*)', line)
            if match:
                key, value = match.groups()
                if value.isdigit():
                    params[key.lower()] = int(value)
                else:
                    params[key.lower()] = value.strip("'\"")
    return params

def generate_terraform_config(params, run_script_content):
    env_dir = os.path.join(OUTPUT_DIR, APP_NAME)
    os.makedir(env_dir, exist_ok = True)

    variables = []
    for key, value in params.items():
        var_type = "string"
        if isinstance(value, int):
            var_type = "number"

        variables.append({
            key: [{
                "type": var_type,
                "default": value,
            }]
        })

    network_tf_data = {"variable": variables}
    with open(os.path.join(env_dir, "network.tf.json"), "w") as f:
        json.dump(network_tf_data, f, indent=4)

    triggers_map = {key: f"${{var.{key}}}" for key in params.key}

    command_parts = []
    current_command = "echo 'Arrancando'"
    if "port" in params:
        current_command += " en el puerto ${var.port}"
    if "app_path" in params:
        current_command += " con la ruta ${var.app_path}"
    current_command += "'"

    main_tf_data = {
        "resource" : [{
            "null_resource": [{
                APP_NAME: [{
                    "triggers": triggers_map,
                    "provisioner": [{
                        "local-exec": {
                            "command": current_command,
                        }
                    }]
                }]
            }]
        }]
    }

    with open(os.path.join(env_dir, "main.tf.json"), "w") as f:
        json.dump(main_tf_data, f, indent=4)

    print(f"Terraform config generada en: {env_dir}")
    print(f" network.tf.json define variables {list(params.keys())}")
    print(f" main.tf.json usa el comando: {current_command}")


if __name__ == "__main__":
    if not os.path.exist(CONFIG_FILE) or not os.path.exists(RUN_SCRIPT):
        print(f"Error: Asegurate que '{CONFIG_FILE}' y '{RUN_SCRIPT}' existan")
    else:
        legacy_params = parse_config_cfg(CONFIG_FILE)
        with open(RUN_SCRIPT, 'r') as f:
            legacy_run_script_content = f.read()

        generate_terraform_config(legacy_params, legacy_run_script_content)
```

---

## Fase 3: Escribiendo código limpio en IaC 

| Conceptos                       | Ejercicio rápido                                                                                               |
| ------------------------------------------ | -------------------------------------------------------------------------------------------------------------- |
| **Control de versiones comunica contexto** | - Haz 2 commits: uno que cambie `default` de `name`; otro que cambie `description`. Revisar mensajes claros. |
| **Linting y formateo**                     | - Instala `jq`. Ejecutar `jq . network.tf.json > tmp && mv tmp network.tf.json`. ¿Qué cambió?                 |
| **Nomenclatura de recursos**               | - Renombra en `main.tf.json` el recurso `null_resource` a `local_server`. Ajustar generador Python.           |
| **Variables y constantes**                 | - Añade variable `port` en `network.tf.json` y usarla en el `command`. Regenerar entorno.                     |
| **Parametrizar dependencias**              | - Genera `env3` de modo que su `network` dependa de `env2` (p.ej. `net2-peered`). Implementarlo en Python.    |
| **Mantener en secreto**                    | - Marca `api_key` como **sensitive** en el JSON y leerla desde `os.environ`, sin volcarla en disco.           |


## Fase 4: Integración final y discusión

1. **Recorrido** por:

   * Detección de drift (*remediation*).
   * Migración de legacy.
   * Estructura limpia, módulos, variables sensibles.
2. **Preguntas abiertas**:

   * ¿Cómo extenderías este patrón para 50 módulos y 100 entornos?
   * ¿Qué prácticas de revisión de código aplicarías a los `.tf.json`?
   * ¿Cómo gestionarías secretos en producción (sin Vault)?
   * ¿Qué workflows de revisión aplicarías a los JSON generados?


## Ejercicios

1. **Drift avanzado**

   * Crea un recurso "load\_balancer" que dependa de dos `local_server`. Simula drift en uno de ellos y observa el plan.

2. **CLI Interactiva**

   * Refactoriza `generate_envs.py` con `click` para aceptar:

     ```bash
     python generate_envs.py --count 3 --prefix staging --port 3000
     ```

3. **Validación de Esquema JSON**

   * Diseña un JSON Schema que valide la estructura de ambos TF files.
   * Lanza la validación antes de escribir cada archivo en Python.

4. **GitOps Local**

   * Implementa un script que, al detectar cambios en `modules/simulated_app/`, regenere **todas** las carpetas bajo `environments/`.
   * Añade un hook de pre-commit que ejecute `jq --check` sobre los JSON.

5. **Compartición segura de secretos**

   * Diseña un mini-workflow donde `api_key` se lee de `~/.config/secure.json` (no versionado) y documenta cómo el equipo la distribuye sin comprometer seguridad.
