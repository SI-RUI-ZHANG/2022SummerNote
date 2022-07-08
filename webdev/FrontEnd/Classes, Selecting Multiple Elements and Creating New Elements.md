---
created: 16-02-2022
e: ⭐
tags: CS/javascript
---

# Classes, Selecting Multiple Elements and Creating New Elements

## Function 'chaining'

JavaScript supports function 'chaining' which allows you to run additional functions directly on the return value of a function. For example, the following code updates the innerHTML of an element:

```js
let a = document.getElementById("foo");
a.innerHTML = "hello!";
```

This one line of code does the exact same thing:

```js
document.getElementById("foo").innerHTML = "hello!";
```

## Classes and the DOM

Every DOM element object contains a 'classList' property. This property contains information regarding which CSS classes are currently attached to this element. You can inspect this property by accessing it directly from any DOM element, like this:

```js
let a = document.getElementById('one');
console.log(a.classList);
```

You can dynamically add classes to a DOM element by using the "add" method on the classList object. For example, say you wanted to add the class 'foo' to an element – you can do so by using the following code:

```js
let a = document.getElementById('one');
a.classList.add( 'foo' );
```

Remember that elements can be assigned to contain any number of classes.

You can check to see if an element is a member of a class by using the 'contains' method on the classList object. This method returns a Boolean value reporting whether the class is currently assigned to that element.

```js
let a = document.getElementById('one');
console.log( a.classList.contains('foo') );
```

You can remove a class from an element using the 'remove' method on the classList object. Note that if you attempt to remove a class from an element that does not currently use that class it's totally OK – you won't generate an error and nothing will happen.

```js
let a = document.getElementById('one');
a.classList.remove( 'foo' );
```

## DOM Queries that Return Multiple Elements

So far our JavaScript programs have used DOM queries that return a single element on the page.

```js
document.getElementById('someId');
document.querySelector('someCSSSelector');
```

We can also query the DOM to obtain collections of elements that can contain more than one element. The three methods that we use to do this include:

```js
document.getElementsByClassName();
document.getElementsByTagName();
document.querySelectorAll();
```

The first two methods are fairly self explanatory – you can use them to obtain all elements that contain a specific class or are of a specific tag type. The third method is just like the `document.querySelector` method, but it can return multiple elements.
When you call one of these methods you will be given a collection object, which for all intents and purposes can be treated as though it was an Array. For example:

```js
let group = document.getElementByClassName('foo');
```

You can determine how many elements are in this group by using the 'length' property:

```js
console.log(group.length);
```

And you can iterate over the collection using a standard 'for' loop and index notation:

```js
for (let i = 0; i < group.length; i++) {
  console.log( group[i] );
}
```

**Important note**: `document.getElementsByClassName` and `document.getElementsByTagName` return an `HTMLCollection` object which contains references to the elements in question. This collection is "live" meaning that if you happen to add new elements to the page that fulfill the criteria for the query -- even AFTER the query has run -- the `HTMLCollection` object will update itself. This can cause unusual side effects if you expect the query to function as a "snapshot" of elements that existed at a particular time in your program.

`document.querySelectorAll` will return a `NodeList` which is a "static" collection of elements. This method will return to you a "snapshot" of elements that matches the query at a particular time. In this class this is the preferred method that we will be using to obtain multiple elements due to this feature.

## Creating New DOM Elements

Earlier in the semester we used document.write() to add new content to the page. Using this method we could inject Strings of data into the page that would be interpreted as HTML. This method works for pages that are written once. But as we have seen earlier in this lesson calling document.write() after the page has fully loaded will cause all content on the page to be overwritten.

We can programmatically create a new DOM element by asking the document object to construct one using the `createElement` function, like this:

```js
let brandNewP = document.createElement('p');
```

Next, you can add content to this tag using standard DOM manipulation techniques. For example:

```js
brandNewP.innerHTML = "Hello, world!";
```

You can also adjust CSS styles and HTML attributes on the tag as you would with any other element.

Creating a new tag using `createElement` will not add the tag to the page. The tag must be added to a specific node in the DOM in order for the browser to recognize where it should be displayed. You can do this using the appendChild function which is available on all DOM elements. For example:

```js
let container = document.getElementById('container');
container.appendChild( brandNewP );
```

You can create multiple elements using a standard 'for' loop. For example:

```js
let container = document.getElementById('container');
for (let i = 0; i < 10; i++) {
  let temp = document.createElement('p');
  temp.innerHTML = 'I am p#' + i;
  container.appendChild(temp);
}
```
