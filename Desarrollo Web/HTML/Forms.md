Forms allow users to enter data, which is generally sent to a web server for processing and storage, or used on the client-side to immediately update the interface in some way (for example, add another item to a list, or show or hide a UI feature).

A web form's HTML is made up of one or more **form controls** (sometimes called **widgets**), plus some additional elements to help structure the overall form — they are often referred to as **HTML forms**. The controls can be single or multi-line text fields, dropdown boxes, buttons, checkboxes, or radio buttons, and are mostly created using the [`<input>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input) element, although there are some other elements to learn about too.

Form controls can also be programmed to enforce specific formats or values to be entered (**form validation**), and paired with text labels that describe their purpose to both sighted and visually impaired users.


# Implementing a form HTML

<div style="text-align:center">
<img src="https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Forms/Your_first_form/form-sketch-low.jpg" width=400>
</div>

## `<form>`

```html
<form action="/my-handling-form-page" method="post">…</form>
```

This element formally defines a form. It's a container element like a [`<section>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/section) or [`<footer>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/footer) element, but specifically for containing forms.

- The `action` attribute defines the location (URL) where the form's collected data should be sent when it is submitted.
- The `method` attribute defines which HTTP method to send the data with (usually `get` or `post`).

## `<label>`, `<input>` and `<textarea>` elements


```html
    <form action="/my-handling-form-page" method="post">
      <p>
        <label for="name">Name:</label>
        <input type="text" id="name" name="user_name" />
      </p>
      <p>
        <label for="email">Email:</label>
        <input type="email" id="Email" name="user_email" />
      </p>
      <p>
        <label for="msg">Message:</label>
        <textarea id="msg" name="user_message"></textarea>
      </p>
    </form>
```

The use of the [`for`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/for) attribute on all [`<label>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/label) elements, which takes as its value the [`id`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Global_attributes/id) of the form control with which it is associated — this is how you associate a form control with its label.

**Types of input in this form**

- In our simple example, we use the value [text](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input/text) for the first input — the default value for this attribute. It represents a basic single-line text field that accepts any kind of text input.
	
- For the second input, we use the value [email](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input/email), which defines a single-line text field that only accepts a well-formed email address. 

To define the default value of an [`<input>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input) element you have to use the [`value`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input#value) attribute like this:

```html
<input type="text" value="by default this element is filled with this text" />
```

On the other hand, if you want to define a default value for a [`<textarea>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/textarea), you put it between the opening and closing tags of the [`<textarea>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/textarea) element, like this:

```html
<textarea>
by default this element is filled with this text
</textarea>
```


# The `<button>` element


```html
<p class="button">
  <button type="submit">Send your message</button>
</p>
```

The [`<button>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/button) element also accepts a `type` attribute — this accepts one of three values: `submit`, `reset`, or `button`.

- A click on a `submit` button (the default value) sends the form's data to the web page defined by the `action` attribute of the [`<form>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/form) element.
	
- A click on a `reset` button resets all the form widgets to their default value immediately. From a UX point of view, this is considered bad practice, so you should avoid using this type of button unless you really have a good reason to include one.
	
- A click on a `button` button does _nothing_! That sounds silly, but it's amazingly useful for building custom buttons — you can define their chosen functionality with JavaScript.

>[!tip] Note
>You can also use the [`<input>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input) element with the corresponding `type` to produce a button, for example `<input type="submit">`. The main advantage of the [`<button>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/button) element is that the [`<input>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input) element only allows plain text in its label whereas the [`<button>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/button) element allows full HTML content, allowing more complex, creative button content.


# Sending form data to your web server

The [`<form>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/form) element defines where and how to send the data thanks to the [`action`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/form#action) and [`method`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/form#method) attributes.

We provide a `name` attribute for each form control. The names are important on both the client- and server-side; they tell the browser which name to give each piece of data and, on the server side, they let the server handle each piece of data by name. ==The form data is sent to the server as name/value pairs==.

To name the data in a form, you need to use the `name` attribute on each form widget that will collect a specific piece of data.

```html
<form action="/my-handling-form-page" method="post">
  <p>
    <label for="name">Name:</label>
    <input type="text" id="name" name="user_name" />
  </p>
  <p>
    <label for="mail">Email:</label>
    <input type="email" id="mail" name="user_email" />
  </p>
  <p>
    <label for="msg">Message:</label>
    <textarea id="msg" name="user_message"></textarea>
  </p>

  …
</form>
```

In our example, the form will send 3 pieces of data named `user_name`, `user_email`, and `user_message`. That data will be sent to the URL `/my-handling-form-page` using the [HTTP `POST`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods/POST) method.

On the server side, the script at the URL `/my-handling-form-page` will receive the data as a list of 3 key/value items contained in the HTTP request. The way this script will handle that data is up to you. Each server-side language (PHP, Python, Ruby, Java, C#, etc.) has its own mechanism of handling form data
