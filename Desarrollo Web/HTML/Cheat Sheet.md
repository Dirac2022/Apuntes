
# Documento Structure

- `<!DOCTYPE html>` Declara el tipo de documento y la version, en este caso HTML5.
- ``<html>`` Es la raíz del documento HTML. Todo el contenido del sitio web debe estar contenido dentro de esta etiqueta.
- ``<head>`` Contiene metadatos del documento, como el título, enlaces a estilos, scripts y configuraciones generales.
- ``<title>`` Define el titulo del documento, se encuentra dentro de la etiqueta `<head>`.
- ``<body>`` Contiene el contenido visible de la pagina web.

# Text Content

- ``<h1> - <h6>`` Representan los encabezados desde el nivel más alto.
- ``<p>`` Define un párrafo. Agrupa texto en bloques organizados.
- ``<span>`` Es un contenedor en línea usado para aplicar estilos o manipular partes específicas del texto.
- ``<div>`` Es un contenedor de bloque usado para agrupar contenido y aplicar estilos o diseño.
- ``<br>`` Inserta un salto de línea. Es una etiqueta vacía, sin contenido de cierre.
- ``<hr>`` Inserta una línea horizontal, generalmente usada para separar secciones de contenido.


# Links

- ``<a>`` Define un enlace.
- ``href`` Atributo de ``<a>`` que indica la URL.
- ``target`` Atributo de ``<a>`` que define dónde se abrirá el enlace. `_self` para el mismo tab, `_blank` para un nuevo tab.
- ``rel`` Atributo de ``<a>`` que especifica la relación entre la página actual y la de destino.
- ``download`` Atributo que indica que el enlace descargará el recurso en lugar e navegar a él.

# Lists

- ``<ul>`` Define una lista desordenada. Los elementos de la lista aparecen con viñetas o puntos.
- ``<ol>`` Define una lista ordenada. Los elementos aparecen numerados o con letras, según el estilo definido.
- ``<li>`` Define un elemento de lista.

# Tables

- ``<table>`` Define una tabla en HTML. Contiene todos los elementos relacionados con filas y celdas.
- ``<tr>`` Define una fila dentro de la tabla. Contiene celdas de datos (`<td>`) o encabezados (`th`).
- ``<td>`` Define una celda de datos dentro de una fila (`<tr>`)
- ``<th>`` Define una celda de encabezado dentro de una fila.
- ``<thread>`` Agrupa los encabezados de la tabla. Usualmente contiene filas (`<tr>`) con celdas de encabezado (`<th>`).
- ``<tbody>`` Agrupa el cuerpo principal de la tabla, con filas de datos (`<tr>` y `<td>`).
- ``<tfoot>`` Agrupa el pie de la tabla. Se utiliza para información adicional, como totales o notas.

## Ejemplo

<table border="1">
    <thead>
        <tr>
            <th>Nombre</th>
            <th>Edad</th>
            <th>Ciudad</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Juan</td>
            <td>25</td>
            <td>Madrid</td>
        </tr>
        <tr>
            <td>Ana</td>
            <td>30</td>
            <td>Barcelona</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">Fin de la tabla</td>
        </tr>
    </tfoot>
</table>


# Forms

- ``<form>``  Define un formulario HTML para recopilar datos. Usa atributos como `action` y `method` para configurar.
- ``<input type="text">`` Crea un campo de entrada de texto.
- ``<input type="password">`` Crea un campo de entrada para contraseñas.
- ``<input type="email">`` Crea un campo de entrada para correos electrónicos. Incluye validación automática para formato de email.
- ``<input type="radio">`` Crea una opción seleccionable de tipo "botón de radio".
- ``<input type="checkbox">`` Crea una casilla de verificación.
- ``<textarea>`` Proporciona un área de texto más grande para que el usuario ingrese contenido extenso.
- ``<select>`` Crea un menú despegable para seleccionar una opción.
- ``<option>`` Define una opción dentro de un menú `<select>`.
- ``<button>`` Crea un botón interactivo. Puede ser de envío (`type="submit`) o botón común (`type="button`).
- ``<label>`` Proporciona un texto descriptivo para un campo de formulario.
- ``<fieldset>`` Agrupa elementos relacionados dentro de un formulario, como un contenedor visual y lógico.
- ``<legend>`` Proporciona un título o descripción breve para un `<fieldset>`.

## Ejemplo

<form action="/enviar" method="post">
    <fieldset>
        <legend>Registro</legend>
        
        <label for="nombre">Nombre:</label>
        <input type="text" id="nombre" name="nombre"><br>
        
        <label for="email">Correo:</label>
        <input type="email" id="email" name="email"><br>
        
        <label for="password">Contraseña:</label>
        <input type="password" id="password" name="password"><br>
        
        <label>Género:</label>
        <input type="radio" id="masculino" name="genero" value="Masculino">
        <label for="masculino">Masculino</label>
        <input type="radio" id="femenino" name="genero" value="Femenino">
        <label for="femenino">Femenino</label><br>
        
        <label for="preferencias">Preferencias:</label><br>
        <input type="checkbox" id="noticias" name="preferencias" value="Noticias">
        <label for="noticias">Recibir noticias</label><br>
        <input type="checkbox" id="ofertas" name="preferencias" value="Ofertas">
        <label for="ofertas">Recibir ofertas</label><br>
        
        <label for="comentarios">Comentarios:</label><br>
        <textarea id="comentarios" name="comentarios" rows="4" cols="40"></textarea><br>
        
        <label for="pais">País:</label>
        <select id="pais" name="pais">
            <option value="ES">España</option>
            <option value="MX">México</option>
            <option value="AR">Argentina</option>
        </select><br>
        
        <button type="submit">Enviar</button>
    </fieldset>
</form>


# Semantic Elements

- ``<header>`` Representa el encabezado de una página o sección. Suele contener títulos, logotipos, menús de navegación, etc.
- ``<footer>`` Representa el pie de página. Contiene información como derechos de autor, enlaces a políticas, o contactos.
- ``<main>`` Contiene el contenido principal de la página. Debe ser único y relevante al propósito de la página.
- ``<section>`` Define una sección temática de contenido, generalmente con un encabezado. Ideal para agrupar contenido relacionado.
- ``<article>`` Representa contenido independiente y autocontenido, como publicaciones, noticias o blogs.
- ``<aside>``
- ``<nav>``
- ``<figure>``
- ``<figcaption>``

# Meta Tags
- ``<meta charset="UTF-8">`` Define la codificación de caracteres para que el navegador interprete correctamente el texto (UTF-8 es estándar).
- ``<meta name="viewport">`` Configura cómo se debe renderizar la página en dispositivos móviles.
- ``<meta name="description" content="">`` Proporciona una breve descripción del contenido de la página.
- ``<meta name="keywords" content="">`` Define palabras clave relacionadas con el contenido de la página.

# Attributes
- `id=""` Identificador único para un elemento. Se utiliza para referenciarlo en CSS o JavaScript.
- `class=""` Agrupa elementos en una misma clases para aplicar estilos o comportamientos comunes con CSS o JavaScript.
- `title=""` Proporciona información adicional que aparece como un cuadro de texto emergente cuando se pasa el cursor.
- `alt=""` Texto alternativo para imágenes, mostrando si la imagen no carga o leído por lectores de pantalla para accesibilidad.
- `src=""` Especifica la ruta del recurso externo, como una imagen o un archivo de video.
- `href=""` Define la URL de destino de un enlace o vínculo.
- `type=""` Indica el tipo de elemento, como un campo de entrada (`text`, `password`, etc.) o script (`text/javascript`).
- `value=""` Especifica el valor inicial de un campo de entrada o un botón.
- `placeholder=""` Texto que se muestra dentro de un campo de entrada como sugerencia o guía hasta que se escribe algo.
- `disabled` Desactiva un elemento, impidiendo la interacción con el usuario. No requiere un valor.
- `checked` Indica que un botón de opción o casilla de verificación está seleccionado por defecto.
- `required` Obliga a completar un campo de entrada antes de enviar un formulario.
- `readonly` Hace que un campo de entrada sea de solo lectura; se puede ver pero no editar.

# Media

- ``<audio>`` Permite incrustar archivos de audio en una página web. Requiere un archivo compatible como fuente.
- ``<source>`` Especifica diferentes fuentes para un elemento multimedia como `<audio>` o `<video>`
- ``<video>`` Permite incrustar archivos de video en una página web. Puede contener etiquetas `<source>`

# Scripting
- ``<script>`` Se utiliza para incluir o enlazar código JavaScript en una página HTML.
- ``<defer>`` Atributo para scripts externos que pospone la ejecución hasta que el DOM esté completamente cargado.
- ``<async>`` Atributo para scripts externos que permite la ejecución asíncrona.

# Linking & Imports
- ``<link rel="stylesheet" href="">`` Enlaza una hoja de estilos externa (CSS).
- ``<link rel="icon" href="">`` Especifica el ícono del sitio web que aparece en la pestaña del navegador (favicon).
- ``<style>`` Permite definir estilos CSS directamente dentro del documento HTML.


