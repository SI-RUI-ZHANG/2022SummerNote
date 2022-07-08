---
created: 09-03-2022
e: ⭐
tags: CS/javascript
---

# JavaScript Language Fundamentals

## What is JavaScript?

HTML and CSS are the tools we use to describe the structure and presentation of a website. JavaScript is the functional layer that allows you to manipulate HTML & CSS and respond to user actions. If you think of HTML as the "nouns" and CSS as the "adjectives" of web development, JavaScript can be considered the "verbs."

JavaScript is a "front-end" programming language, meaning that it is delivered to and executed by the browser. All JavaScript actions take place on a client's computer. This means that any source code that you write in JavaScript will be delivered fully in-tact to your client to be executed. Because each browser is responsible for executing JavaScript on its own you can sometimes run into issues with compatibility (i.e. older browsers) and security (your code is fully visible)

## Incorporating JavaScript into your HTML documents

JavaScript can be placed directly into an HTML document using the `script` tag. For example:

```html
<!doctype html>
<html lang="en-us">
 <head>
  <meta charset="utf-8">
  <title>Web Development 2020</title>
 </head>
 <body>
  <h1>Web Development 2020</h1>
  <script>
   // this is some JavaScript code
   document.write("Hello, world!");
  </script>
 </body>
</html>

```

JavaScript can also be linked in from an external file in a manner similar to how you load in an external CSS document. Keep in mind that you need an opening and closing `script` tag when using this method:

```html
<!doctype html>
<html lang="en-us">
 <head>
  <meta charset="utf-8">
  <title>Web Development 2020</title>
 </head>
 <body>
  <h1>Web Development 2020</h1>
  **<script src="myFirstJavascriptProgram.js"></script>**
 </body>
</html>
```

Note that JavaScript completely ignores whitespace, just like HTML. It also ignores tabs (unlike Python) - you can format your code to appear however you like, but there are some conventions that most JavaScript programmers follow. We will discuss these conventions later in this class.

## JavaScript runs where it is found in the document

JavaScript code is executed on the client side at the moment in which it is encountered by the browser. For example, in the following document the words "Hello, world!" will show up before the `h1` tag:

```html
<!doctype html>
<html lang="en-us">
 <head>
  <meta charset="utf-8">
  <title>Web Development 2020</title>
 </head>
 <body>
  **<script>
   // this is some JavaScript code
   document.write("Hello, world!");
  </script>**
  <h1>Web Development 2020</h1>
 </body>
</html>

```

But in this example the words "Hello, world!" will appear after the `h1` tag:

```html
<!doctype html>
<html lang="en-us">
 <head>
  <meta charset="utf-8">
  <title>Web Development 2020</title>
 </head>
 <body>
  <h1>Web Development 2020</h1>
  **<script>
   // this is some JavaScript code
   document.write("Hello, world!");
  </script>**
 </body>
</html>
```

You can have as many `script` elements on your page as you wish, and the browser will execute them as they are encountered. Note that when you load in an external script (one that is not embedded in the document) the browser must pause and load in the script before it continues drawing the page. This means that if you are loading in a large script (say, the jQuery library from the jQuery website) your page will appear to take longer to load since the browser will not continue 'drawing' the remainder of the page until the script has fully loaded and executed. It is generally considered best practice to load in your scripts directly before the closing `html` tag at the bottom of your web page.

## JavaScript function calls & statements

JavaScript is similar to other functional programming languages such as Python and Java insofar as it is designed to respond to function calls and built-in statements. JavaScript code runs linearly (like Python), but the flow of execution can also "jump" around based on "events" that occur on the page (the user clicks on a button, enters a value in a form field, etc). We will cover "events" in a few weeks. For now, assume that your code will execute from top to bottom as it is encountered.

The basic structure of a JavaScript function call is similar to Python:

```javascript
alert("Hello, world!");
```

The line above is calling the `alert` function, which is accepting one argument (the string "Hello, world!"). Note how the line is terminated with a semicolon - this is required (just like it is in CSS).

Note a lines of JavaScript require a trailing semicolon - in general, control structures that define a block of execution (`if` statements, loops, function definitions, etc) do not require semicolons at the end of their lines.

## Generating output

JavaScript has numerous functions that can be used to generate output. Here are three that we commonly use, though there are many more (and honestly, better) ways of generating some of these output types.

The `alert` function will cause the browser to generate a pop-up window that must be clicked in order to be dismissed. This function is useful when you want to get your user's attention, but it tends to be incredibly annoying and we try not to use it much in actual practice. Still, it is an easy way to get information to display on the user's screen. The syntax for the `alert` function is as follows:

```js
alert( STRING_TO_DISPLAY );
```

Note that most browsers will render the `alert` pop-up window before drawing the rest of the page, which may result in the user seeing your alert box on top of a seemingly empty HTML document. This behavior can be minimized by calling the `alert` function after the page has fully loaded (which we will discuss in a later lecture).

The `console.log` function renders content to the JavaScript console, which is a separate browser space that is designed for web developers to inspect the result of their code. In Chrome you can launch the JavaScript console by clicking on the View -> Developer -> JavaScript Console command. Then, to print content to the console you can issue this command:

```js
// display a single value
console.log( VALUE_TO_PRINT );

// display multiple values (separated by spaces)
console.log( VALUE1, VALUE2, VALUE3 );

```

The JavaScript console is the primary way in which we inspect the inner workings of our programs, but it is hardly ever used to generate content that is designed to be consumed by our users.

`document.write` is a function that can be used to write content directly to the browser. For example:

```js
document.write( VALUE_TO_ADD_TO_PAGE );
```

You can write any value you wish to your page, and this value will be displayed as part of your HTML document to the user. This is an incredibly useful feature of JavaScript, which essentially gives you the ability to modify the content of your page in real-time. We often use this technique to add new HTML tags to the page, like this:

```js
document.write("<p>Hello, world!</p>l;");
document.write("<ul><li>Item 1</li><li>Item 2</li></ul>");
```

JavaScript contains other ways of adding content to the HTML page which may be more appropriate depending on the situation you find yourself in, but this is a great "starter" technique to help you get an idea of the types of things the language is capable of.

Note that when using `document.write` the source code of your HTML page is not amended - if you view the source code for a document after `document.write` has been executed you won't see any changes. However, you can see these changes in the "computed" version of the document - in Chrome this is visible under through View -> Developer -> Developer Tools within the 'Elements' panel.

## Commenting

JavaScript supports two types of comments - single line and multi-line. Single line comments are rendered using the `//` sequence and multi-line comments are rendered using `/*` and `*/` (the same as CSS)

```js
// this is a single line comment
 
/*
 this is a 
 multi-line comment
*/
```

## Variables, data types & data type conversion

JavaScript variables must be declared prior to being used (unlike with Python). Variables can be a mixture of any alphanumeric characters along with a number of special characters ("_" and "$"). Variable names cannot begin with a number. JavaScript programmers are heavy on 'camel case' syntax -- this means that variables should begin with all lowercase letters, but if the variable name is a compound word any future words should be uppercased (i.e. `myAwesomeNewVariable`).

You can declare a variable using one of three keywords - `var` or `let` (as well `const` which we will talk about in a moment). One of these keywords (and only one!) is used directly before the name of your variable the **first time** you reference that variable name. For example:

```js
var myVariable1;
let myVariable2;
```

This tells the browser that you are setting aside space for a variable with the name following the keyword. This does not assign any value to the variable, though - if you were to inspect the variable you would see that is currently holding an 'undefined' value:

```js
var myVariable;
console.log( myVariable ); // undefined
```

You can assign values to a variable using the assignment operator, like this:

```js
let myVariable;
myVariable = 5;
```

... and you can do this all on one line if you'd like (usually easier, but there are reasons why you wouldn't do this which we will cover later in the class):

```js
let myVariable = 5;
```

JavaScript is "loosely typed", meaning that you do not need to pre-declare the data type of the variable you are working with when declaring a new variable (same as in Python, but different from Java). The JavaScript interpreter will automatically determine the appropriate data type for your variable based on the content being stored. JavaScript has four fundamental data types - "number", "string", "boolean" and "Object" - and a variable can freely change data types throughout your program. Here's an example:

```js
let myVariable = 5; // data type = 'number'
myVariable = "hello"; // data type = 'string'
myVariable = 5.5; // back to being a 'number'
myVariable = true; // boolean
```

Note that JavaScript does not have a different data type for floats and ints - both of these types of values are stored within the 'number' data type.

Strings need to be delimited the same way as they do in other languages - the valid delimiters in JavaScript are the single and double quotation marks. The following two Strings are identical:

```js
let myVar1 = "hello";
let myVar2 = 'hello';
```

We often change the delimiters of a String based on the contents the String is storing (i.e. if the string has a quotation mark in it you will probably use the apostrophe character as the delimiter). You can also 'escape' out offending characters using the backslash character as well (same as in Python):

```js
let myString = 'Hi, I\'m Craig - how are you?';
```

You can concatenate two strings using `+` operator, just like in Python. For example:

```js
let a = 'hello';
let b = 'world';
let c = a + ' ' + b;
```

You can also use JavaScript's "template literals" to simplify concatenation. This allows you to add the name of a variable directly within a string and have JavaScript substitute the variable value for you. You can do this using the following syntax:

```js
let a = 'hello';
let b = 'world';
let c = `a is holding ${a} and b is holding ${b}`
```

Note the use of the 'backtick' delimiter (attached to the `~` key on your keyboard). Also note the use of the curly-brace subdelimiter along with the dollar sign to indicate a 'template' reference to a variable.

Boolean variables in JavaScript can only contain one of two values - `true` or `false`. Note that in Python these two values are represented in all lowercase (unlike Python).

The Object datatype is a more complicated data structure that we will start to cover within the next few weeks. Objects are sequences (like lists in Python) and can hold multiple values.

You can use the `typeof` function to determine the data type of a variable. For example:

```js
myVariable = 'hello';
console.log( typeof(myVariable) ); // string
```

You can prompt the user to enter in a string using the `prompt` function. This function works similarly to the `alert` function - a pop-up dialog box will appear and the user will be asked to enter in a value. This value will be returned to your program as a string. Note that this is **not** the best way to get values from the user, but for now this will be a useful tool for us to explore since we haven't gotten to working with HTML forms yet. Plus this feature works in a manner not unlike the `input` function in Python. Here's an example:

```js
let userName = prompt("What is your name? ");
document.write("Thanks, " + username);
```

You can convert data from one type to another using a series of data type conversion functions. For example:

```js
let a = '5'; // string
let b = parseInt(a); // number, without any decimal point
let c = parseFloat(a); // number, with a decimal point
```

The `isNaN()` function can be used to determine if a value is NOT a valid number. For example:

```js
let a = 'Hello';
let b = parseInt(a);
console.log( isNaN(b) ); // true
```

you can convert numeric data back into a String using one of two methods:

```js
let d = 5;
let e = d.toString(); // call the 'toString' method on the number
let f = d + '';  // concatenate the number into an empty string, which will force it to become a string
```

## 'var' vs. 'let' vs. 'const

In JavaScript the keyword that you attach to a variable denotes its behavior and scope in your program. Here's a quick rundown of how this works - note that we will revisit this as we progress through the class as there are some nuances here that won't make sense until we get into more advanced JavaScript techniques.

The `var` keyword scopes a variable to a function. This means that the variable is available within the most recently open function (curly braces). If the variable is not defined inside of a function (i.e. it's just inside of a `script` tag) it will be considered globally scoped. This is more or less how languages like Python treat their variables. For example:

```js
var a = "outside";

function doSomething() {
  var b = "function";

  console.log("a:", a);   // outside
  console.log("b:", b);   // function

  if (true) {
    var c = "ifstatement";
    console.log("a", a);  // outside
    console.log("b", b);  // function
    console.log("c", c);  // ifstatement
  }

  console.log("c", c);  // ifstatement
}

doSomething();
```

The `let` keyword, however, scopes variables to a block (a set of curly braces). If the variable is not defined inside of a function (i.e. it's just inside of a `script` tag) it will be considered globally scoped. This is more or less how languages like Java treat their variables. For example:

```js
let a = "outside";

function doSomething() {
  let b = "function";

  console.log("a:", a);   // outside
  console.log("b:", b);   // function

  if (true) {
    let c = "ifstatement";
    console.log("a", a);  // outside
    console.log("b", b);  // function
    console.log("c", c);  // ifstatement
  }

  console.log("c", c);  // ReferenceError: c is not defined
}

doSomething();
```

The `const` keyword works exactly like the `let` keyword (block scoped) but with one major difference - `const` variable bindings cannot be changed once they have been assigned a value. They are considered 'read-only' variables. For example, in this output you will see the exact same behavior as with the `let` keyword:

```js
const a = "outside"; function doSomething() { const b = "function"; console.log("a:", a); // outside console.log("b:", b); // function if (true) { const c = "ifstatement"; console.log("a", a); // outside console.log("b", b); // function console.log("c", c); // ifstatement } console.log("c", c); // ReferenceError: c is not defined } doSomething();

```

... but note when we try and change a value:

```js
const a = "outside";
a = "pikachu!";  // TypeError: Assignment to constant variable
console.log("a", a);
```

**Important note** - the `const` keyword declares that a variable's binding is read-only. This means that the memory address of the value that the variable is pointing to can never change. In the example above we were assigning a string to our variable. Strings are immutable data types, just like in Python. Making a change to a string creates a new string at a new memory address which would cause the program above to crash since a variable declared with `const` can never have its binding changed. However, data types that are mutable (such as arrays) can have their values changed without changing their binding. We will discuss this in greater detail in the section on arrays below.

## Generate a Random Number

Math.random() is a built-in JavaScript function that lets you generate a random floating point number in the range [0,1). For example:

```js
let num = Math.random();
```

If you wanted to turn this number into an integer you could do so using the `parseInt` function, like this:

```js
let num = parseInt( Math.random() );
```

However, because the random number falls within the range [0,1) the result of this statement will always be zero! This is because `parseInt` simply truncates a floating point number and leaves you with the integer component of the number.

In order to generate numbers in a larger range you need to perform some math operations on the number being generated. For example, if you'd like to generate an integer in the range [0,10) you could do the following:

```js
let num = parseInt( Math.random() * 10 );
```

The float being generated could be any float within the acceptable range (0.32433 is valid, as is 9.2345). Then you parse this float into an integer and you are left with the whole number component of the float.

If you'd like to create a number within a range that has a custom starting point (i.e. a number in the range [5,15) ) you could do the following:

```js
let num = parseInt( Math.random() * 10 + 5 )
```

To summarize, here is the algorithm for converting a 'uniform' float (a number in the range [0,1) ) into a custom range:

- Identify the size of the range
- Identify the starting point in the range
- Construct a statement like the following: `let num = Math.random() * range_size + starting`

## Conditional logic

Selection statements allow your program to evaluate the result of a boolean expression and respond accordingly. You can use relational operators to construct relational expressions that test the relationship between various entities. The relational operators available in JavaScript are as follows:

- < Less than
- <= Less than or equal to
- > Greater than
- >= Greater than or equal to
- == Equality
- === Identity
- != Inequality
- !== Inidentical

An "if" statement can be constructed in JavaScript using the following syntax:

```js
if (boolean-expression) 
{
  statement(s); 
}
```

Parenthesis are required around your Boolean expressions, Unlike in Python, indentation does not matter. An "if" statement does not require a semicolon. Having a block of curly braces is required for "if" statements that block contains more than 1 statement. It’s usually a good idea to always put curly braces in anyway.

A one-way "if" statement only allows you to respond to a condition if the Boolean expression in question evaluates to true. If you want to respond to when the condition evaluates to false you can use a two-way "if-else" statement using the following syntax. Note that in the example below one of the two sets of statements is guaranteed to execute – if the original boolean expression evaluates to false then the else clause automatically is invoked.

```js
if (boolean_expression) 
{
  statements(s); 
} 
else 
{
  statements(s); 
}
```

"if" statements can be placed inside of one another to form "nested" if statements using the following syntax:

```js
if (boolean_condition) 
{
  statement(s);
   if (boolean_condition_2)
  {
   statement(s);
  }
  else
  {
   statements(s);
  }
}

```

And you can always re-write your nested statements to use "else if" syntax, like this. Keep in mind that a conditional statement can contain any number of "else-if" blocks:

```js
if (boolean_expression) 
{
  statement(s); 
}
else if (boolean_expression) 
{
  statement(s); 
}  
else 
{
  statement(s); 
}
```

JavaScript has two operators that can be used to test the 'sameness' of two values. These operators, called the 'equality' and 'identity' operators have slight differences to one another.

The equality operator (`==`) tests to see if two values are the same. If they are of different data types they will be converted to the same data type and the result will then be evaluated.

```js
let a = 5;
let b = 5;
let c = "5";

if (a == b) {
 console.log("a == b"); // will print, because a and b are both 5
}
if (a == c) {
 console.log("a == c"); // will also print!
}

```

The identity operator (`===`) tests to see if two values are the same AND they are of the same data type. For example:

```js
let a = 5;
let b = 5;
let c = "5";

if (a === b) {
 console.log("a === b"); // will print, because a and b are both 5
}
if (a === c) {
 console.log("a === c"); // will not print
}
```

Just like in other programming languages, boolean expression can be combined with logical operators (and, or, not). In JavaScript these operators are expressed as `&&` (and), `||` (or) and `!` (not).

## Repetition structures

You can repeat statements in JavaScript using looping structures that should be familiar from your experience with other programming languages.

The `while` loop is a 'condition controlled loop' that can be used to repeat a series of statements as long as a condition evaluates to `true`. We tend to use `while` loops when we do not know how many times we will need to repeat a statement. The syntax for a `while` loop is as follows:

```js
let c = 0;
while (c < 10) {
 console.log(c);
 c += 1;
}
```

Note that `while` loops can easily become "infinite" if their associated condition never evaluates to `false`. It is important to ensure that your loops terminate at some point, otherwise the browser will hang up and eventually crash.

The `for` loop is a 'count controlled loop' that can be used to repeat a series of statements a known number of times. We often use `for` loops to execute tasks that have a defined number of iterations. The syntax for a `for` loop is as follows:

```js
for (let c = 0; c < 10; c+=1) {
 console.log(c); 
}
```

`for` loops need three pieces of information to operate - a target variable, the condition that controls when the loop should end and the amount the target variable changes by each iteration. You do not need to pre-declare the target variable for a `for` loop before the loop itself - you can use the `var` keyword in the loop declaration to set up your target variable.

Note that we often need to increase the value of a variable by 1 (i.e. c += 1) - JavaScript has a built-in feature to do this called the 'incrementor' operator, which works like this:

```js
let c = 0;
c++;
```

As you can guess, there is also a 'decrementor' operator which uses `--` instead of `++`

## Arrays

An array is a 'sequence structure' that can be used to store multiple values inside of the same identifier. In Python these structures are known as 'lists'.

You can create an empty array in JavaScript by using square bracket syntax, like this:

```js
let myArray = [];
```

You can also create an array that is pre-set with values, like this:

```js
let myArray = ['apple', 'pear', 'peach'];
```

Recall from your previous programming class that values in an arrays are 'indexed' using integers starting at 0. If you want to inspect the first value in an array you can do so use 'bracket notation' as follows:

```js
let myArray = ['apple', 'pear', 'peach'];
console.log( myArray[0] );
```

Remember that you can't access an element in an array that doesn't exist - if you try to do so (i.e. accessing `myArray[100]` on the above array) you will crash your program.

You can determine how many elements are in an array using the `length` property of an array, like this:

```js
let myArray = ['apple', 'pear', 'peach'];
console.log( myArray.length ); // 3
```

Arrays in JavaScript are mutable, and can be grow and shrink as necessary (unlike Java). You can add an element to the end of an array by using the `push` method as follows:

```js
let myArray = ['apple', 'pear', 'peach'];
myArray.push('lemon'); // 'lemon' is now at the end of the array, position 3
```

You can remove an element from an array using the `splice` method - this method takes two arguments: the position to remove from and the number of elements to remove. For example, to remove the string 'peach' from the array above you can do the following:

```js
let myArray = ['apple', 'pear', 'peach'];
myArray.splice(2, 1); // remove 1 element starting at index #2
```

The easiest way to iterate over all elements in an array is to use a `for` loop to iterate over all of the available indexes in the array. Here's an example:

```js
let myArray = ['apple', 'pear', 'peach'];
for (let i = 0; i < myArray.length; i++) {
 console.log( myArray[i] );
}
```

Arrays are mutable data types meaning that their binding (memory address) does not change even if you change the content of the array. For example:

```js
const foo = [10,20,30]; // binding of 'foo' can never change
console.log(foo); // [10,20,30]
// foo = [40,50,60]; // this is not allowed as it would change the binding of the variable to reference a new array
foo[0] = 999; // this is allowed. we are changing the existing array, but not changing its binding.


console.log(foo); // [999,20,30]
```
