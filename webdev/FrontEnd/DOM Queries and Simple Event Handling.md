---
created: 07-02-2022
e: 📝
tags: CS/javascript
---

# DOM Queries and Simple Event Handling

## The Document Object Model

When your browser loads a webpage, it creates a JavaScript model of every HTML element and CSS rule used on the page. This is called the "DOM tree" and is stored in the browser's memory as long as the web page remains opened. Every element, attribute, piece of text in your HTML is stored in its own "DOM node" in this tree.

When JavaScript represents the HTML page as an object it translates all of your tags into "element nodes". Elements nodes are arranged in a hierarchy, starting with the 'Document' node at the top. Nodes organized under a given node are considered "child" nodes. Nodes at the same level are considered "sibling" nodes. Every node, except for the "Document" node, has a "parent" node.![[DOM-structure.png|700]]

## Element Nodes

Open up any web page and launch the JavaScript console. Next, type

```js
console.dir(document);
```

into the console. Expand the "document" object and look for the 'childNodes' property. Expand this node. You can see all of the 'top level' HTML tags in the document (`<html>`) – if you expand this node you can find the next set of 'childNodes' (`<head>` and `<body>`)

Element nodes have multiple sub-nodes attached to them which further describe that node, include:

- Attribute node: all HTML attributes associated with that tag
- Style node: all CSS styles associated with that tag
- Text node: the 'affected' text for that tag (i.e. `<strong>Affected</strong>`)

## DOM Queries

The DOM is a "living" object. Any changes made to the page are reflected in the DOM, and any changes made to the DOM are reflected on the page. With that said, the DOM is an ugly, big, messy object! It can be hard to find the node you want to work with. In order to do this we use one of many 'DOM query' functions to scan the DOM and find a desired element in the tree.

For single element queries (i.e. you only need to access and work with one element at a time) the following two functions are the ones we usually rely on:

```js
document.getElementById();
document.querySelector();
```

For multiple element queries (i.e. you want to work with many elements at the same time):

```js
document.getElementsByClassName();
document.getElementsByTagName();
document.querySelectorAll();
```

We will work with these functions in detail next week.

Consider the following HTML document:

```html
<html>
  <head>
    <title>Test Page</title>
  </head>
  <body>
    <p id="one">One</p>
    <p id="two">Two</p>
  </body>
</html>
```

To get a reference to the element on the page that has an ID of 'one' you could do the following:

```js
var a = document.getElementById('one')
```

The variable 'a' is now holding a reference to the first `>p<` tag.
You could also use the `document.querySelector` function to access the first `>p<` tag:

```js
var a = document.querySelector('p');
```

This will select the first element on the page that matches the CSS selector `p`.

## Working with Attributes, Styles & Text

You can change the HTML attributes of a node by doing the following:

```js
var element = document.getElementById('id');
element.src = 'pikachu.png';
// or
element.setAttribute('src', 'pikachu.png');
```

You can change the CSS attributes of a node by doing the following:

```js
var element = document.getElementById('id');
element.style.color = '#ffcc00';
```

Note that some CSS rules have dashes in their names. In order to update these properties you need to use index syntax, like this:

```js
element.style['background-color'] = 'red';
```

You can change the text value of a node (i.e. the 'affected text' - `<p>hello</p>`) by doing the following:

```js
var element = document.getElementById('id');
element.innerHTML = '<h1>hey!</h1>';
element.innerHTML = 'hey!';
```

You can treat 'innerHTML' as a String, so you can also concatenate to it as you would with any other string:

```js
element.innerHTML += 'hey!';
```

In addition to being able to change a property, you can also just read it and evaluate it as necessary. For example:

```js
var a = document.getElementById('foo');
if (a.src === 'pikachu.png') {
  // do something
}
```

You can test to see if an attribute exists on an element by calling the 'hasAttribute' function on the element, like this:

```js
if (a.hasAttribute('src')) {
  // it's safe to work with the src attribute
}
```

You can examine the inline CSS properties of an element by accessing it's 'style' attribute, like this:

```js
var a = document.getElementById('foo');
if (a.style.color === 'red') {
  // do something
}
```

Note that the value you are accessing may return 'undefined' if the style is not set on the element, or if the style was declared as an embedded or linked style. You can get ALL styles associated with an element by calling window.getComputedStyles() function, like this:

```js
var a = document.getElementById('foo');
var allStyles = window.getComputedStyles(a);
if (allStyles.color !== undefined) {
  // it's safe to work with the color 
}
```

## Simple Events

JavaScript is an "event-based' language. This means that it has an underlying architecture that constantly "listens" for behaviors by the user and can respond to them when they happen. Every element in the DOM has the ability to "listen" for any number of events. When this event occurs a function can be invoked to deal with the event.

Here are some common mouse events that can be responded to through JavaScript:

```markdown
click.      the user clicks on the element
dblclick    the user double clicks on the element
mousedown   the user presses the mouse down on the 
            element (and has not released)
mouseup     the user has released the mouse button
mouseover   the user has moved the mouse over the 
            element
mouseout    the user has moved the mouse away from the 
            element
mousemove   the user has moved the mouse while on top
            of the element
```

One way to set up an event handler for a specific type of event is to use an "in-line" event. This technique is very similar to "in-line" CSS, and is discouraged due to the tight coupling between content & actions. For example, this `<p>` tag will generate an alert when it is clicked:

```html
<p onclick="alert('!!!');">click here</p>
```

You can also have an element invoke a custom function that you create when an event occurs:

```html
<p onclick="doSomething();">click here</p>
```

You can also set up an event handler on an element using the DOM, like this:

```js
var element = document.getElementById('one');
one.onclick = function() { alert('hi'); }
```

This method is generally preferred over inline event handlers. Note that there are other methods of adding event listeners to elements (i.e. the "addEventListener" function) – we will cover these techniques later in the semester.

```js
Making elements invisible / visible
```

The CSS 'display' property allows you to define how an item reacts to the 'normal flow' of a document Common values for this rule include:

- block: default for block level elements (p, div, etc.) – items are stacked on top of one another
- inline: default for inline level elements (strong, a, etc.) – items are arranged next to each other horizontally
- inline-block: an inline element that has the ability to be styled using box model properties (width, height, border, padding, etc.) – default for elements such as `<button>` - items are arranged horizontally next to one another.
- none: the element is completely removed from normal flow

You can manipulate the CSS display property to hide / show elements in your document. We often use this technique to set up all of our possible elements ahead of time and then programmatically hide/show them as needed.
