---
created: 09-03-2022
e: ⭐
tags: CS/javascript
---

# Functions & Objects

## JavaScript Functions

Functions are pre-written units of code that can be invoked or 'called' by your program. We've explored many built-in JavaScript functions already such as `parseInt` and `Math.random()`.

You can declare a 'named function' in JavaScript by using the following syntax:

```js
function fun1() {
  document.write("<p>Fun 1 was called</p>");
}
```

Calling a 'named function' is as easy as using the name of the function along with a set of parenthesis to pass any arguments you may wish to send to the function:

```js
fun1(); // call fun1
```

Just like in other languages, JavaScript functions can be designed to accept arguments. To do this you can set up an number of local variables in the function definition, like this:

```js
function fun1(a, b) {
  document.write("<p>Fun 1 was called with:" + a + " and " + b + "</p>");
}
```

And just like in other languages, functions can 'return' values back to the caller using the `return` statement.

```js
function subtractTwoNumbers(a,b) {
  var answer = a - b;
  return answer;
}
```

Note that functions can return multiple values, but you should try and avoid this. Returning an 'Object' is the preferred method to use when returning multiple values.

```js
function doSomeMath(a,b) {
  var diff = a - b;
  var sum = a + b;
  return diff, sum;
}
var x, y = doSomeMath(2,1); // x will hold 1 and y will hold 3
```

Unlike other languages, function 'references' can be stored in variables. In the following example the variables 'q' and 'r' both refer to the 'fun2' function. Note how we omit the parenthesis - we don't need them because we aren't calling the function:

```js
function fun2() {
  console.log("hello");
}
 
let q = fun2;
let r = fun2;
```

Now we can call 'q' and 'r', but really we are just calling 'fun2':

```js
q();
r();
```

Note that 'named functions' are 'hoisted' - JavaScript will automatically scan your code and make all named functions available at the beginning of your script. This means that you can effectively call a function before it is defined, like this:

```js
fun3();

// define a 'named function'
function fun3() {
  console.log("fun 3 was called");
}
```

You can also create 'anonymous' functions which are essentially functions that do not have an explicit name attached to them. These functions become very important later in the semester when we will deal with 'callbacks' and 'events'. The following function is considered anonymous since it is stored directly in a variable without an explicit name:

```js
const anon1 = function() {
  console.log('I am anonymous!');
}
```

You can call an anonymous function just like a 'named' function, but anonymous functions are **not 'hoisted'** like named functions. You will need to ensure that your anonymous functions are defined prior to them being used before.

## The Object datatype

The 'Object' datatype is one of the fundamental programmatic units of JavaScript. It's a sequence structure (like an array) insofar as it exists as a single identifier that can contain multiple values. It is very similar to the 'dictionary' data type in Python. You can define a new object by using curly braces, like this:

```js
let testObject1 = {};
```

The object created above is totally devoid of any content - if you output it to the console you will see that it has nothing stored inside of it:

```js
console.log(testObject1);
```

Objects can contain any number of 'properties' which can be of any data type, including other objects. You can define a property on an object by using name:value syntax, like this:

```js
let testObject2 = {
  name:'Pikachu',
  age:6, 
  powers:['thunder','shock'] 
};
```

Now if you output this object to the console you will see an inspectable tree that lets you view each property associated with the object. In code you can access a property in one of two ways. The first method is to use 'dot syntax' which requires you to identify the object, followed by a period and then by the name of the property, like this:

```js
console.log( testObject2.name );
```

You can also access properties using 'index' or 'array' notation. This is especially useful if the property contains a special character such as the '-':

```js
console.log( testObject2['name'] );
```

Attempting to access a property that does not exist will not crash your program - instead, you will notice that the value being accessed will be set to `undefined`:

```js
console.log( testObject2.hello ); // undefined
```

Objects are 'mutable' (changeable) - you can modify a property at any time, and you can also add new properties to an object by simply referencing the property. For example:

```js
// update the name of our pokemon
testObject2.name = 'Charmander';

// add a new property to our pokemon
testObject2.bestFriend = 'Squirtle';

```

You can delete a property from an object through the use of the `delete` statement, like this:

```js
delete testObject2.bestFriend;
```

If you'd like to iterate over all properties in an object you can do so using a 'for' loop. This will iterate over all property names in the object. You can then use index notation to access the value of the property, like this:

```js
for (let property in testObject2) {
  console.log("Property name is: " + property);
  console.log("Property value is: " + testObject2[property]);
  console.log(); // empty line
}
```

Objects can store properties that refer to any data type, including functions! For example:

```js
let person = {
  firstName:'Jane',
  lastName:'Doe',
  sayHello: function() {
   console.log("Hello!");
  }
}
```

You can access functions stored within an object using dot notation, just as with any other property. Just make sure to call the function using parenthesis:

```js
person.sayHello();
```

Functions within objects can be 'self-referential' - meaning that the functions themselves can access the properties of the object directly. This can be done using the `this` keyword. For example, here's an updated version of the 'person' object that has the ability to log out the current value of the 'firstName' property.

```js
let person = {
  firstName:'Jane',
  lastName:'Doe',
  sayHello: function() {
   console.log( this.firstName );
  }
}

person.sayHello(); // Jane

```

## Working with pre-defined Objects

JavaScript is filled with Objects. Pretty much everything in JavaScript outside of the primitive values are represented as Objects.

For example, the current browser window is available to your JavaScript program as an object. This object, called the `window` object, is pre-created for you when the browser loads a page. You can inspect it using `console.log`, like this:

```js
console.log( window );
```

Note how this gives you a huge tree of properties! Some of those properties are functions (denoted with the italicized letter 'f') and some are standard values (numbers, strings, and even other Objects). You may even see some items that are familiar, such as the `alert` and `prompt` functions. When you call these functions you are really calling them on the `window` object. For example, calling `window.alert('hi')` is the same as calling `alert('hi');`.

We will dig deeper into the `window` object in a moment, but for now there are four useful values that we often use to figure out how much space is currently available in the user's browser. These values are as follows:

```js
let browserWidth = window.innerWidth;
let browserHeight = window.innerHeight;
let screenWidth = window.screen.width;
let screenHeight = window.screen.height;

console.log(browserWidth);
console.log(browserHeight);
console.log(screenWidth);
console.log(screenHeight);
```

The screen width and height is the actual size of the user's display - this value doesn't change unless the user adjusts their display size in their operating system. The browser width and height represent the current size of the user's browser. If you resize the browser and reload the page you will notice that these values change.

JavaScript also has the ability to work with dates and times. The following code will generate the current date and time based on your computer's internal clock:

```js
let rightNow = new Date();
```

Note the use of the 'new' keyword - this is a keyword used in JavaScript to create an 'instance' of a Date object. You can actually have more than one date objects in your program at the same time, and the 'new' keyword generates a brand new one for you. If you log out the date you will see something like the following:

```js
console.log( rightNow ): // Tue Feb 06 2020 07:29:57 GMT-0500 (EST)
```

Note how you immediately see the current time, not the list of properties available on the object. This is because this object is set up to include a 'toString' function which overrides the default behavior of displaying the object as an inspectable tree. You an override this behavior by using the `console.dir` function, like this:

```js
console.dir( rightNow ); // inspectable tree of properties
```

Note that there are many, many different properties listed here! Almost all of them are functions. You can call these functions directly using dot syntax, like this:

```js
console.log( rightNow.getHours() ); // returns the current hour, as an integer
console.log( rightNow.getMinutes() ); // returns the current minutes, as an integer
console.log( rightNow.getSectons() ); // returns the current seconds, as an integer
```
