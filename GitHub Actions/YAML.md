**YAML Ain't Markup Language**


| Característica | YAML                                      | JSON                     |
| -------------- | ----------------------------------------- | ------------------------ |
| Sintaxis       | Más legible, menos símbolos               | Más estricta, con llaves |
| Comentarios    | Si (`#`)                                  | No                       |
| Tamaño         | Más compacto                              | Más verboso              |
| Parsing        | Más complejo                              | Más fácil                |
| Uso común      | Configs (GitHub Actions, Docker, Ansible) | APIs, JS                 |


**Características**
- Formato clave-valor.
- Indentación con espacios.
- Tipos de datos.
- Manejo de texto multilínea.

**Herramientas que usan  YAML**
- GitHub Actions
- Ansible
- Docker
- Compose
- Kubernetes

#### Tipos primitivos

```yaml
ciudad: Madrid
comillas: "123"
edad: 25
temperatura: 36.6
masa: 1e6
activo: true
verificado: yes
descripcion: null
comentario: ~
```


#### Listas

```yaml
colores:
  - rojo
  - verde
  - azul
```

#### Mapas/Diccionarios

```yaml
persona:
  nombre: Juan
  edad: 30
```

#### Lista de valores
```
usuarios:
  - nombre: Ana
    edad: 30
  - nombre: Luis
    edad: 25
```


#### Modificadores String multilínea

```yaml
mensaje: |
  Hola,
  Esto es un texto multilínea.
```

```yaml
texto: >
  Esta es una línea
  que continuará en la siguiente.
```


### Herencia

```yaml
defaults: &defaults
  color: blue
  size: medium

item1:
  <<: *defaults
  color: red

item2:
  <<: *defaults
  size: small

# item1 hereda defaults y sobrescribe color.
# item2 herada defaults y sobrescribe size
```

```yaml
version: '3.8'

services:
  web:
    image: nginx:alpine
    ports:
    - "80:80"
    volumes:
    - ./nginx.conf:/etc/nginx/nginx.conf
    - .:/var/www/html
  php:
    image: php:8.2-fpm
    volumes:
    - .:/var/www/html
```



