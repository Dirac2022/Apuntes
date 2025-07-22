[HTML: Creating the content - Learn web development | MDN](https://developer.mozilla.org/en-US/docs/Learn_web_development/Getting_started/Your_first_website/Creating_the_content)

```html
<!doctype html>
<html>
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width" />
    <title>My test page</title>
  </head>
  <body>
    <img src="" alt="My test image" />
  </body>
</html>
```

- `<!doctype html>`: The [doctype](https://developer.mozilla.org/en-US/docs/Glossary/Doctype) is a required preamble. However, these days, they don't do much and are basically just needed to make sure your document behaves correctly. That's all you need to know for now.
	
- `<html></html>`: The [`<html>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/html) element wraps all the content on the entire page and is sometimes known as the **root element**. It also includes the `lang` [attribute](https://developer.mozilla.org/en-US/docs/Glossary/Attribute), which sets the primary language of the document.
- `<head></head>`: The [`<head>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/head) element acts as a container for all the stuff you want to include on the HTML page that _isn't_ the content you are showing to your page's viewers. This includes things like [keywords](https://developer.mozilla.org/en-US/docs/Glossary/Keyword) and a page description that you want to appear in search results, [CSS](https://developer.mozilla.org/en-US/docs/Glossary/CSS) to style the content, character set declarations, and more.
	
- `<meta charset="utf-8">`: This element sets the character set your document should use to [UTF-8](https://developer.mozilla.org/en-US/docs/Glossary/UTF-8), which includes most characters from the vast majority of written languages.
	
- `<meta name="viewport" content="width=device-width">`: This [viewport element](https://developer.mozilla.org/en-US/docs/Web/CSS/CSSOM_view/Viewport_concepts#mobile_viewports) ensures the page renders at the width of the browser viewport, preventing mobile browsers from rendering pages wider than the viewport and then shrinking them down
	
- `<title></title>`: The [`<title>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/title) element sets the title of your page, which is the title that appears in the browser tab the page is loaded in. It is also used to describe the page when you bookmark/favorite it.
	
- `<body></body>`: The [`<body>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/body) element contains _all_ the content that you want to show to web users when they visit your page, whether that's text, images, videos, games, playable audio tracks, or whatever else. At the moment it only contains a single `<img>` element, but we'll add more content later on.


# List

Marking up lists always consists of at least 2 elements. The most common list types are ordered and unordered lists:

1. **Unordered lists** are for lists where the order of the items doesn't matter, such as a shopping list. These are wrapped in a [`<ul>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/ul) element.
2. **Ordered lists** are for lists where the order of the items does matter, such as a list of cooking instructions in a recipe. These are wrapped in an [`<ol>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/ol) element.

Each item inside the lists is put inside an [`<li>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/li) (list item) element.

```html
<p>At Mozilla, we're a global community of</p>

<ul>
  <li>technologists</li>
  <li>thinkers</li>
  <li>builders</li>
</ul>

<p>working together…</p>

```


# Creating links

Links are very important — they are what makes the web a web! To add a link, we need to use an [`<a>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/a) element, "a" being short for "anchor". To make text within your paragraph into a link, follow these steps:

1. Choose some text. We chose the text "Mozilla Manifesto".
2. Wrap the text in an [`<a>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/a) element.
3. Give the [`<a>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/a) element an `href` attribute (*hypertext reference*).
4. Fill in the value of this attribute with the web address that you want the link to point to.

```html
<a href="https://www.mozilla.org/en-US/about/manifesto/">
  Mozilla Manifesto
</a>

```
