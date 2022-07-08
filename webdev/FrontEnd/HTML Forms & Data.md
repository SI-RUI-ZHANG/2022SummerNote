---
created: 24-02-2022
e: 📄
tags: CS/javascript
---

# HTML Forms & Data

## HTML Forms

So far our users have only been able to interact with our web pages through clicking their mouse. In order to gather more information from the user we often rely on form fields that the user can fill in using their keyboard. We all do this every day on the web. Common form elements include:

- Text boxes (single line)
- Text areas (multiple line)
- Drop-down menus
- Radio buttons
- Checkboxes
- Ranges

The `<form>` tag is used in HTML to group together form UI elements. Technically all UI elements should go inside of a `<form>` tag, though many browsers will be OK if you don't use it. The `<form>` tag is required when you want the browser to send form data to another program or server – we will be doing that in the 2nd half of the class.

Note that if you do use the 'form' tag to create a form which contains a button the browser will attempt to package up all of the data stored within the form and send it off to a program on the server. This may be undesirable at this point in the semester, but you can use the `preventDefault` method on the `event` object to stop this from happening.

All form fields should be given both a 'name' and 'id' attribute. These attributes can contain the same value. The 'name' attribute is used when communicating with a server-side program. The DOM element associated with a `<form>` tag contains a special 'reset()' function which can be used to return all form fields to their original values.

## Text Boxes

A textbox is a single-line free form input tool that allows the user to supply a string of text.

```html
<form>
  <input type="text">
</form>
```

In order to get access to the data the user types into the textbox you will need to assign your box an 'id' property. For server communication you will need to also give in a 'name' property – these can (and should) be the same value. For example:

```html
<form>
  <input type="text" name="foo" id="foo">
</form>
```

A textbox can be given a default value using the 'value' attribute, and you can limit the amount of text a user types into a textbox using the `maxlength` property, like this:

```html
<form>
  <input type="text" name="foo" id="foo" maxlength="10" value="default">
</form>
```

You can access the value the user typed into a text box by doing the following:

- Get a DOM reference to the textbox, as with any other element
- Access the 'value' property on the DOM element – this contains a string version of what is currently being stored in the textbox.
Here's an example:

```js
<script>
  let foo = document.getElementById('foo');
  console.log( foo.value );
</script>
```

## Textareas

A textarea is a larger input box that allows the user to type in multiple lines of data. It is rendered using the `<textarea>` tag, like this:

```html
<textarea>Default text for textarea</textarea>
```

You will want to give your textarea an 'id' and 'name' just like with textboxes. You can access the value in a textarea using the same technique as a textbox, and you can freely style your textarea with CSS.

## Drop-down Menus

A drop-down menu provides a set of pre-determined options to the user. By default only one option can be selected at a time. Drop down menus require two tags – one for the menu and one for each option included in the menu. For example:

```html
<select name="food" id="food">
  <option value="pizza">I like pizza!</option>
  <option value="cake">I like cake!</option>
</select>
```

Accessing the value of a drop-down menu is an identical process to the other two input methods we just discussed. By default the first option in a drop-down menu is pre-selected. You can override this by using the 'selected' standalone attribute, like this:

```html
<select name="food" id="food">
  <option value="pizza">I like pizza!</option>
  <option value="cake" selected>I like cake!</option>
</select>
```

## Checkboxes

A checkbox is a stand-alone input mechanism that can be used to collect Boolean values (true & false). Checkboxes are implemented using the "input" tag, like this:

```html
<input type="checkbox" name="red" id="red">Red
<input type="checkbox" name="blue" id="blue">Blue
```

The value of a checkbox will always be its name. This isn't very useful since what you really want to know is whether the user has checked the box.You can do this by looking at the 'checked' property of the DOM element, like this:

```js
<input type="checkbox" name="red" id="red">Red
<input type="checkbox" name="blue" id="blue">Blue
<script>
  let r = document.getElementById('red');
  if (r.checked === true) {
    console.log("user selected red");
  }
</script>
```

## The 'data-' HTML Attribute

As you know, HTML tags can contain attributes to further describe how a tag should behave (i.e. the 'src' attribute on the 'img' tag tells the image which file it should load). HTML5 also supports custom attributes that can be set up by the programmer to store additional information. These custom attributes are always prefixed with "data-" followed by a string of your choice. For example:

```html
<img src="dog1.jpg" data-species="whippet">
<img src="dog2.jpg" data-species="poodle">
```

The 'data-' HTML attribute gives us the ability to store custom data on any HTML element. The stored data can be accessed by JavaScript through the "dataset" property. For example:

```html
<script>
  let a = document.querySelector('img');
  console.log( a.dataset.species ); // whippet
</script>
```

An HTML element can have any number of 'data-' attributes. They must consist of at least one character, and should not contain any spaces, and the data stored in this attribute is always a string. You can view, modify or create 'data-' attributes via JavaScript. See today's downloadable code samples for some practical examples of how to use this technique in action (rollover buttons, tabbing systems, image galleries, etc.)
