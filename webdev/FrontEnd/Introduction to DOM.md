---
created: 07-02-2022
e: 📝
tags: CS/javascript
---

# Introduction to DOM

## The Document Object Model

When we last met we spent some time digging into the `window` object. This object contains a ton of information about what's happening in the user's browser window, including the current browser size and the size of the user's display. However, that's only the beginning of what you can find inside of this object!

One of the most important properties of the `window` object is the `document` property. This property references an object, which is essentially JavaScript's view of the current HTML document. In essence, when your browser loads any web page it will translate the HTML and CSS code of the page into a JavaScript object, which is fully available to your program. We call this representation the **Document Object Model (DOM)**.

The **DOM** can be thought of a 'tree' of objects that represent the current HTML page as a hierarchy. For example, consider the following HTML document:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>My Title</title>
  </head>
  <body>
    <h1>My header</h1>
    <a href="#">My link</a>
  </body>
</html>
```

This could be visually represented using the following hierarchical graphic:
![[DOM-tree.png|500]]

With the DOM, JavaScript has the ability to natively interact with any element in the currently loaded document. The DOM exposes the following capabilities to your JavaScript programs:

- Add / change HTML attributes
- Add / change CSS styles
- Add new HTML elements
- Remove existing HTML elements
- Listen for and react to 'events' that occur on a web page

## Accessing the 'document' Object

You can access the 'document' object through the 'window' object, like this:

console.log(window.document);

But since we do this all of the time we can use a 'shortcut' object that the browser creates for us, like this:

```js
console.log(document);

// just to prove that they are the same object!
console.log(window.document === document);  // true
```

Note that the default representation of the DOM is an HTML tree, but you can view it as an Object by using `console.dir` like this:

```js
console.dir(document);
```

## Getting a reference to an individual HTML element

We can ask JavaScript to search the DOM for elements based on a number of criteria:

- By ID
- By class
- By tag name
- By contextual selector

If you know the ID of the element you wish to access you can get a reference by using the 'getElementById' function, like this:

```js
// assuming there is an element on the page with an ID of 'first_a_tag'
var element1 = document.getElementById('first_a_tag');
console.log(element1);
console.dir(element1);
```

You can adjust and add any HTML attributes on this element using dot syntax. For example:

```js
/ update the hyperlink reference to point to a different page
element1.href = 'http://www.nyu.edu';

// set the link to open in a new browser window
element1.target = '_blank';
```

Another way to do this is to use the `setAttribute` function, like this:

```js
element1.setAttribute('target', '_blank');
```

There is also a corresponding `getAttribute` function that you can call to retrieve an attribute.

```js
var currentTarget = element1.getAttribute('target');
```

You can adjust the CSS styles on this element by using the 'style' property on the element as well:

```js
element1.style.color = 'green';
```

Note that is you need to adjust a style that has a '-' in it you will need to use 'index notation' when accessing the object:

```js
element1.style['font-family'] = 'Fantasy';
element1.style['font-size'] = '200%';
element1.style['text-decoration'] = 'none';
```

To adjust the text being rendered inside of a tag (i.e. `<p>This text</p>`) you can use the `innerHTML` property, like this:

```js
element1.innerHTML = 'Click here to go to NYU';
```
