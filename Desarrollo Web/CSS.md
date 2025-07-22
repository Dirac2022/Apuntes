
# Anatomía de una regla CSS


**Selector**
El elemento HTML en el que comienza la regla. Esta selecciona el(los) elemento(s) a dar estilo. 

**Declaración**
Una sola regla como `color: red;` especifica a cuál de las **propiedades** del elemento quieres dar estilo.


**Propiedades**
Maneras en las cuales puedes dar estilo a un elemento HTML. (En este caso `color` es una propiedad del elemento `<p>`). En CSS, seleccionas qué propiedad quieres afectar en tu regla.


**Valor de la propiedad**

A la derecha de la propiedad, después de los dos puntos `:`, tienes el **valor de la propiedad**, para elegir una de las muchas posibles apariencias para una propiedad determinada.


Otras partes importantes de la sintaxis:

- Cada una de las reglas (aparte del selector) deben estar encapsuladas entre llaves (`{}`).
- Dentro de cada declaración, debes usar los dos puntos (`:`) para separar la propiedad de su valor.
- Dentro de cada regla, debes usar el punto y coma (`;`) para separar una declaración de la siguiente.

Ejemplo

```css
p {
	color: red;
	width: 500px;
	border: 1px solid black
}
```


## Seleccionar varios elementos

```css
p,
li,
h1 {
	color: red;
}
```


# Tipos de selectores


| Nombre del selector                       | Qué selecciona                                                                                                             | Ejemplo                                                                       |
| ----------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| Selector de elemento (de etiqueta o tipo) | Todos los elementos HTML del tipo especificado.                                                                            | `p`. Selecciona `<p>`                                                         |
| Selector de identificación (ID)           | El elemento en la página con el ID especificado (en una página dada, solo se permite un único elemento por ID).            | `#mi-id`. Selecciona `<p id="mi-id">` y `<a id="mi-id">`                      |
| Selector de clase                         | Los elementos en la página con la clase especificada (una clase puede aparecer varias veces en una página).                | `.mi-clase`. Selecciona `<p class="mi-clase`> y `<a class="mi-clase">`        |
| Selector de atributo                      | Los elementos en una página con el atributo especificado.                                                                  | `img[src]`. Selecciona `<img src="miimagen.png">` pero no `<img>`             |
| Selector de pseudoclase                   | Los elementos especificados, pero solo cuando esté en el estado especificado, por ejemplo cuando el puntero esté sobre él. | `a:hover` Selecciona `<a>`, pero solo cuando el puntero esté sobre el enlace. |

# Fuentes y texto


### `font-family`
Se refiere a las fuentes que deseas usar en tu texto. 

```css
html {
    font-size: 10px;
    font-family: 
        "Open Sans", sans-serif;
}
```


# CSS is all about boxes

<div style="text-align:center">
<img src="https://developer.mozilla.org/en-US/docs/Learn_web_development/Getting_started/Your_first_website/Styling_the_content/box-model.png" width=500px >
</div>

- `padding`: The space around the content.
- `border`: The solid line just outside the padding
- `margin`: The space outside the border



# Centering the image

If we have an image, we use this rule:

```css
img {
	display: block;
	margin: 0 auto;
	max-width: 100%;
}
```

- We use the trick `margin: 0 auto`: When you set two values on a property like `margin` or `padding`, the first value affects the element's top _and_ bottom side (setting it to `0` in this case); the second value affects the left _and_ right side. `auto` is a special value that divides the available horizontal space evenly between left and right.
	
- The [`<body>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/body) element is a **block** element, meaning it takes up space on the page and can accept margin, padding, and other box properties. [`<img>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/img) (image) elements, on the other hand, are **inline** elements: by default, they don't accept margin values in the same way block elements do. For the auto-margin trick to work on this image, we must give it block-level behavior by using `display: block;`.
	
- Finally, we set the [`max-width`](https://developer.mozilla.org/en-US/docs/Web/CSS/max-width) property to `100%` to ensure that if the image is larger than the `width` set on the body (600 pixels), it will be constrained to `600px` and won't stretch wider.


# Other properties

- `width`: The width of an element.
- `background-color`: The color behind an element's content and padding.
- `color`: The color of an element's content (usually text).
- `text-shadow`: A drop shadow on the text inside an element.
- `display`: The display mode of an element (which basically refers to how it appears or is laid out on the web page).
- 