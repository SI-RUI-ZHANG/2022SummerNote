---
created: 16-02-2022
e: ⭐
tags: CS/javascript
---

# DOM Augmentation, Pointers & Event Objects

- **Table of contents**

## DOM Pointers

The DOM is organized into a hierarchical "tree" structure. Every element has a place in this structure, and every element contains information about where it is currently situated. We often refer to the placement of an element in terms of a "family"

- Parents
- Siblings
- Children

## Parent Elements

Every DOM element has a `parentElement` property. This property is a live reference that "points" to the node directly above this one in the hierarchy. All elements have a parent, except for the document itself or newly created elements that have not been added to the page. If an element does not have a parent the property will be set to the value `null`

DOM Pointers can be thought of link 'hyperlinks' to the element in question in the DOM tree. You can use them as you would any other DOM element reference. This means that if you have a reference to an element, you automatically can get access to its parent and can apply styles or HTML attributes to that element.

## Sibling Elements

Two elements are siblings if they share the same `parentElement`. Every element keeps track of two siblings – the one directly before them, and the one directly after them. These are exposed as two properties in their DOM element.

- previousElementSibling
- nextElementSibling

## Child Elements

Every parent element can have 0 or more child elements. A parent has three pointers that it can use to access its children:

- firstElementChild
- lastElementChild
- children (array)

## Base Selector Elements

Up until this point in the semester we have been using the following to search for DOM elements on the page:

```js
document.getElementById('something');
```

In this example the `document` object is our 'base selector' – this means that we will be searching the entire document, starting at the `<html>` tag, for matching elements. The base selector does not always need to be the 'document' object though! For example, consider the following HTML:

```html
<div id="foo">
  <div class="zoo">a</div>
</div>

<div id="bar">
  <div class="zoo">b</div>
</div>
```

If we were to use the following query selector, we would target the first div with the class of 'a':

```js
document.querySelector('.a');
```

But if we wanted the second one we could ask the browser to begin its search with the `#bar` div, like this:

```js
let bar = document.getElementById('bar');
bar.querySelector('.a'); 
```

## Removing Elements

`remove` and `removeChild` are two DOM functions that we often use to remove an element from its current parent. The `remove` element simply detaches the element from its current parent and takes no arguments. The function is called on the element being removed. The `removeChild` method does the same thing, but is called on the parent element. This method requires a reference to this child being removed. For example:

```html
<div id="container">
  <div id="a">A</div>
  <div id="b">B</div>
  <div id="c">C</div>
</div>

<script>
  // DOM references
  const container = document.querySelector('#container');
  const a = document.querySelector('#a');
  const b = document.querySelector('#b');
  const c = document.querySelector('#c');

  // method #1: ask an element to remove itself from its parent
  a.remove();

  // method #2: ask the container to remove one of its children
  container.removeChild(b);

  // note: the element MUST be a child of the parent in order
  // for this to succeed -- the following line will generate a runtime error
  //container.removeChild(a); // a is no longer a child of the container

</script>
```

## Adding Elements at Specific Locations

We've already learned that the 'appendChild' method can be used to insert elements as 'children' of a parent element. This method always inserts the element as the LAST child of the parent. For example:

```js
let newP = document.createElement('p');
newP.innerHTML = 'New P - created via JavaScript!';

let theDiv = document.querySelector('#one');
theDiv.appendChild(newP); // will appear as the last element inside of the div #one
```

In addition to 'appendChild', you can also insert an element before any other element using the 'insertBefore' method. This method takes two arguments - the element you are inserting and the element that it should go before. For example, to insert an element at the beginning of a div we could do the following:

```js
let newP2 = document.createElement('p');
newP2.innerHTML = 'Another P - created via JavaScript!';

// insert the element before the first child 
theDiv.insertBefore( newP2, theDiv.firstElementChild ); // inserted as the first element, before all others
// theDiv must be the direct parent of theDiv
```

Note that you can insert an element anywhere using these two methods (appendChild and insertBefore)

- To add an element as the last child of an element use `appendChild`
  - or `append()`
- To add an element as the first child of an element use `insertBefore` in relation to the first child
- To add an element anywhere else you need to know what position you want it to go into. You can do this by referring to the 'children' array on the element. For example, to put something into the 2nd position you could do the following:

```js
    parentElement.insertBefore( newElement, parentElement.children[1] );
// of course, you can also use the prepend() method
 parentElement.append( newElement );
```

## Moving Elements

You can move elements from one parent to another using the following technique:

- Get a reference to the element you wish to move
- Remove the element using the `remove` method
- Get a reference to the new parent element
- Ask the new parent to add the child using the `appendChild` method

## A Quick word on JavaScript Function Mechanics

A function in JavaScript can be designed to accept 0 or more arguments:

```js
function fun1(a) {  
  console.log(a);
}
fun1(5);  // 5
```

However, there is no explicit rule that prevents you from sending more or less arguments to a JavaScript function. For example:

```js
fun1(); // will print the value undefined, but the program doesn't crash
```

Likewise, you can create a function that is designed to accept no arguments:

```js
function fun2() {  
  console.log("fun 2 was called");
}
```

And you can send this function an argument without the program crashing:

```js
fun2(5);  // fun 2 was called
```

## Event Objects

So far we have been attaching 'event listeners' to elements using the following technique:

```js
element.onclick = function() { }
```

This technique assigns a function to the DOM element that it will run every time the user clicks their mouse on the element. There are other ways of doing this (which we will cover next time), but for now this is the most straightforward way to associate an action with an event.

When an event is triggered JavaScript packages up everything it knows about that event into an 'event object'. This object is passed to your function automatically, though up until now we have been ignoring it. You can capture this object by adjusting your event listener function to look like the following:

```js
element.onclick = function(event) { }
```

This variable contains everything the browser knows about the event that triggered the function. There's a lot of stuff in this object! One of the most important and useful properties of this object is the 'currentTarget' property:
[[target vs currentTarget]]

```js
element.onclick = function(event) {
  console.log(event.currentTarget);
}
```

This property is a reference to the DOM element of the object that the event was triggered on. You can use this DOM element reference just like one you could obtain through a DOM query. For example:

```js
<button id="foo">Click<button>
<script>
  var a = document.getElementById('foo');
  a.onclick = function(event) {
    event.currentTarget.style['background-color'] = '#fc0';
  }
</script>
```

To see this technique in action please download today's code sample ZIP file - there are a series of examples that show how to use event objects and why this technique is so important.

## Event Mechanics

By default, when you register an element to listen for an event the events are handled through a process called "bubbling" (there is another process called "capturing" which is also available, but it's not the default and will be covered at a later time). The "bubbling" process works as follows:

- The innermost element that receives the event runs its function
- The event then "bubbles" outwards to the parent of the element. If the parent is also listening for the same event it will run its function
- The process continues until the upper-most parent is reached (the 'html' tag)
Any element in the bubbling "chain" can prevent elements above it from receiving the event. You can do this using the `stopPropagation` function which is available via the 'event' object.
