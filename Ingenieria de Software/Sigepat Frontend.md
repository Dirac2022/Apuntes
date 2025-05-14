
# Apuntes de frontend

- En el `package.json` estás las dependencias de Angular, similar a `pom.xml`
- En `node_modules` están todos los paquetes necesarios para la aplicación web, no se sube al repositorio remoto, en su caso se usa el comando `npm install`, esta genera la carpeta ``node_modules`` a partir de `package.json`
- La carpeta `src` se encuentra el código fuente de la aplicación
- El `main.ts`  es el archivo de arranque de la aplicación


Agregar un componente (Caso de Uso)
```bash
ng generate component <nombre_carpeta>\<nombre_componente>
```

```shell
ng generate component component\mostrar-hoteles
```


Agregar interface
```shell
ng generate interface <nombre_carpeta>\<nombre_interface>
```

```shell
ng generate interface model\hotel-response
```


Agregar servicio
```
ng generate service service\hotel
```
# Apuntes de html

Para que la aplicación web sea *responsive*
```html
<meta name="viewport" content="width=device-width, initial-scale=1" />
```
