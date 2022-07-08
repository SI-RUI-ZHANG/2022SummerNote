---
created: 03-03-2022
e: ⭐
tags: CS/javascript
---

# Closures & LocalStorage/Cookies

## More Function Mechanics

Recall that there are two ways to create functions in JavaScript - 'named' functions and 'anonymous' functions. A 'named' function is defined using the following syntax:

```js
function firstFunction() {
  console.log("this is firstFunction");
}
```

We can call this function by invoking its name with a set of parenthesis:

```js
firstFunction();
```

We can also store a REFERENCE to the function in a variable. Note the lack of parenthesis here – we are not calling the function, we are accessing its reference:

```js
let linkToFirstFunction = firstFunction;
```

Now we can call 'linkToFirstFunction' and 'firstFunction' will be called:

```js
linkToFirstFunction();
```

You can also create 'anonymous' functions - these are functions that have no formal name associated with them. In this case the function is accessible through the variable 'a' which has a link to it:

```js
let a = function() {        
  console.log("this is anonymous function #1");      
}
```

We can call 'a' to invoke the function:

```js
a();  // this is anonymous function #1
```

Note the data type of a -- it's a function! functions are actually data types in JavaScript, just like numbers and strings:

```js
console.log( typeof(a) );  // function
```

Because functions are formal data types, we can use them as we would any other variable. For example, here is a function that accepts two functions as arguments:

```js
function thirdFunction(x, y) {        
  x();        
  y();      
}
```

We can then pass references to the two previously created functions into the newly created function, and the newly created function will be able to call those functions:

```js
thirdFunction( linkToFirstFunction, a );
```

## setTimeout

`setTimeout` is a built-in JavaScript function. It is used to schedule a function call for some time in the future. It takes two arguments – a function to call and the amount of time to wait before calling that function. For example:

```js
function foo() {
  console.log("hello");
}
setTimeout(foo, 1000); // foo will be called in 1 second from now
```

You can also pass additional arguments to the `setTimeout` function that will be sent as arguments to the function being "scheduled" in the future. For example:

```js
let someFunction = function(x,y,z) { 
    console.log("Hello", x,y,z); 
}
setTimeout(someFunction, 1000); // in 1 second the function will log out "Hello" and the values undefined, undefined, undefined
setTimeout(someFunction, 2000, 4, 5, 6); // in 2 seconds the function will log out "Hello" and the values 4, 5, 6
```

## setInterval

`setInterval` is another built-in JavaScript function that can be used to schedule a function call for some time in the future. Unlike `setTimeout`, the `setInterval` function will continually be called over and over again, kind of like an infinite loop. `setInterval` takes two arguments – a function to call and a time value that describes how often to call that function in milliseconds. It returns an "interval id" which can be used to stop the interval at some point in the future. For example:

```js
function foo() {
  console.log("hello");
}

let id = setInterval(foo, 1000); // foo will be called in 1 second from now, and every 1 second after that
```

If you hold onto the "interval id" you can stop the interval from continuing to be called using the `clearInterval` function. For example:

```js
function foo() {
  console.log("hello");
}
let id = setInterval(foo, 1000); // foo will be called in 1 second from now, and every 1 second after that
document.getElementById('stop_button').onclick = function(event) {
    // clear the interval when this button is pressed
    clearInterval( id );
}
```

## addEventListener

So far when we have wanted to have our DOM elements react to events we have used the 'on-event' technique, like this:

```js
document.getElementById('foo').onclick = function() { }
```

This is a perfectly acceptable way to add an event to an element, but it comes with one major drawback – only one event of each type can be added to any given element. For example, in the code above there can only be one "onclick" function. But sometimes you will run into a situation where you want an object to react multiple times when an event is detected.

A more robust technique for dealing with events is to add an event listener to an element using the `addEventListener` method, which is available on all DOM elements. `addEventListener` requires two arguments (and an optional third argument, which we will discuss in a future class). The first argument is the event type you are listening for. The second argument is the function that should be fun when the event is detected.

```js
let a = document.getElementById('foo');
foo.addEventListener('click', function(event) { 
  console.log("I was clicked!");
});
```

We call the second argument a `callback function` – it is called by the `addEventListener` function when a certain event has been detected. A DOM element can have any number of event listener functions listening for the same event using this technique.

## The "clear text" Dilemma

Web pages are designed to be "human readable" – anyone can visit any webpage and view the source of that page using their web browser. This is a great feature as it keeps the web "open" – but from a security perspective this is a really, really bad thing! Anyone can use the 'view source' feature and see exactly how your code operates! In addition, the JavaScript console allows you to run code directly on a web page - if you know what you're looking for you can invoke functions and change variable values on any page that you visit.

## Minification

One way to get around this is to "minifiy" your JavaScript files. Minification is the process of stripping down extraneous content in your script so that the overall file size of your program is smaller. This process is generally used to make web pages load faster, but it also makes it more difficult to see what your code is actually doing. Note that this is a completely reversible process – you can "de-minifiy" a document easily, so you shouldn't rely solely on this technique. To give this a try visit this website and paste in some JavaScript code: [https://javascript-minifier.com/](https://javascript-minifier.com/).

## Obfuscation

Obfuscation is the process of obscuring your code so that it becomes unreadable to a viewer. This process relies on a variety of tricks, including variable renaming, character shifts, dead-code injection, and using functions to obscure the flow of a program. It's not an exact science, but it's usually "good enough" for most applications. Obfuscation, like minification, is reversible, though it is always more difficult to reverse. Obfuscation usually will also minifiy your code as well. To give this a try visit this website and paste in some JavaScript code: [https://javascriptobfuscator.herokuapp.com/](https://javascriptobfuscator.herokuapp.com/)

## JavaScript Functions & Memory Mechanics

You can design a function to immediately invoke (call) itself by wrapping the function in a set of parenthesis and then adding a second set of parenthesis to 'call' the function. For example:

```js
(function() {
  console.log("hello!");
})();
```

As you know, you can create variables inside of functions. These variables are considered 'local' to the function and can only be accessed from within the function. You can also create functions inside of functions. These functions are also considered 'local' to the function and can only be accessed from within the function. Functions that are nested in this way have access to their parent's variable scope.

JavaScript is a 'garbage collection' language - this means that values remain in memory as long as some region of the program is linking to them. When an element has no links attached to it the language will periodically de-allocate those values. This means that if you invoke a function and you maintain a link to some portion of that function the local variables associated with the function will persist after the function finishes execution. The region of memory constructed by a function is often referred to as a **Closure** - use the diagram below to see how JavaScript allocates memory with Closures below:
**Not supported**

## Closures and the DOM

A closure will not be de-allocated as long as there is a link to some function within the closure Setting up an event listener will count as a link, essentially keeping the closure active indefinitely (as long as the page is open by the browser). We can create a tamper-proof set of variables this way by doing the following:

- Wrap all of our application code in a function, including event listeners
- Immediately invoke that function

## State and the Web

The web is a "stateless" entity. For front-end pages like the ones we have been building this means that your variable values do not carry over between page loads. The page does not "remember" what it was doing the last time you visited it and will start from scratch.

## Cookies

One way to "remind" your page of what it was doing in a previous execution is to use a "cookie". A cookie is a text file that can be left on a client's computer by a web page. Cookies are organized by domain, and pages on that domain (such as i6.cims.nyu.edu) can leave multiple cookies on a client's computer. Every time a client connects to the domain ALL cookies associated with that domain on the client's computer are made available to the page. The page can decide to read those cookies to "remind" itself of what happened during a previous execution.

Every web browser has the ability to show you all cookies associated with a domain. Often these cookies seem to be completely random – we will discuss why this is when we get more into back-end web development. Here's how to view your own cookies:

- Chrome: Click on Chrome->Preferences and search for Cookies, find 'Content Settings' and click on it, click on 'Cookies' and then on 'See all Site Data'
- Safari: Click on Safari -> Preferences -> Privacy -> Manage Website Data
- Firefox: Click on Firefox -> Preferences, scroll down to Site Data, click on Settings

## Viewing Cookies via JavaScript

The `document` object contains a property called `cookie` - this is a String that holds all cookies that are associated with the domain of the page. The cookie string contains a series of NAME/VALUE pairs separated by semicolons. For example:

```js
name1=value1; name2=value2; name3=value3
```

You can create a cookie by simply assigning a new NAME/VALUE pair to the 'cookie' object. Note that this will not overwrite cookies that have already been set (unlike a regular string). For example, you can set up a new cookie holding the name of the user by doing the following:

```js
document.cookie = 'name=Craig';
```

The 'cookie' string contains all NAME/VALUE cookie pairs for the domain separated by the ';' character. You can use string mechanics to extract individual cookie values by using an algorithm similar to the following (note that there are libraries that are already written that make this process much easier!)

- Access the entire cookie string
- Split the string using the '; ' character sequence
- Visit each substring
- Split the substrings based on the '=' character
- Store the values in another structure (usually an object)
- Access this object as needed in your code

## localStorage

Cookies have been around for a *long* time. They are incredibly useful for storing information locally on a user's computer. They are also incredibly useful for 'reminding' the server as to who the user is. They do have some limitations, however:

- Maximum cookie size (for all cookies on a domain): 4,093 bytes
- Awkward API (weird pseudo-string)

HTML5 introduced a new construct that is designed to make it easier to store and access data on a user's computer. This new construct is called 'localStorage' and it has the following features:

- Stores key/value pairs that are accessible by all pages on your domain
- Maximum storage size: 10 MB per domain
- Keys and values must be strings (same as cookies)
- Used solely for local storage (no communication with server, unlike cookies)
- localStorage is more or less widely supported among the major browsers

localStorage methods:

```js
window.localStorage 
// main reference to all localStorage elements for a domain
window.localStorage.setItem(key, value);
window.localStorage.getItem(key);
// will return null if key does not exist
```
