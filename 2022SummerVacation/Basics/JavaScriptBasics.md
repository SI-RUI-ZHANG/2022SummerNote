# JavaScript Basics

## Summary

- Weakly Typed Language
  - No explicit type assignment
  - Data types can be switched dynamically
- Object-Oriented Language
  - Data can be organized in logical objects
  - Primitive and reference types
- Versatile Language
  - Runs in browser & directly on a PC/server
  - Can perform a broad variety of tasks

## Core Syntax

### Arrow Function

```javascript
const summarizeUser = (userName, userAge, userHasHobby) => {
    return ...
}
```

[==arrow function and this==](https://academind.com/tutorials?filter=javascript)

### Objects, Properties&Methods

```javascript
const person = {
    name: 'Sirui',
    age: 20,
    greet(){
        console.log('Hi, I am ' + this.name);
    }
}

console.log(person);
person.greet();
```

### Arrays, Array Methods

```javascript
const person = {
    name: 'Sirui',
    age: 20,
    greet(){
        console.log('Hi, I am ' + this.name);
    }
}

const hobbies = ['Sports', 'Cooking'];

for (let hobby of hobbies) {
    console.log(hobby);
}
// Sports
// Cooking

const arr_new = hobbies.map((hobby) => 'Hobby: ' + hobby);
```

### Spread & Rest Operators

```javascript
const hobbies = ['Sports', 'Cooking'];
const arr_new = hobbies.slice(); // copy array
const arr_new = [...hobbies]; // spread operator
```

#### `...` Spread syntax

Spread syntax `...` allows an iterable such as an array expression or string to be expanded i place where zero or more arguments or elements are expected, or an object expression to be expanded in places where zero or more key-value pairs are expected.

syntax

For function call:

```javascript
myFunction(...iterableObj); // pass all elements of iterableObj as arguments to function myFunction
```

For array literals:

```javascript
[...iterableObj, '4', 'five', 6]; // combine two array sby inserting all elements from iterableObj
```

For object literals (new in ECMAScript 2018):

```javascript
let objClone = {...obj}; // pass all key: value pairs from an object
```

#### Rest syntax (parameters)

The rest parameter syntax allows a function to accept an indefinite number of arguments as an array, providing a way to represent variadic function in javascript.

syntax

```javascript
function f(a, b, ...theArgs) {

}
```

==example==

```javascript
function myFun(a, b, ...manyMoreArgs) {
    console.log("a", a);
    console.log("b", b);
    console.log("manyMoreArgs", manyMoreArgs);
}

myFun("one", "two", "three", "four", "five", "six");
// a, one
// b, two
// mayMoreArgs, ["three", "four", "five", "six"]
```

_A function definition can have only one `...` restParam_

### Destructuring

```javascript
const person = {
    name: 'Sirui',
    age: 20,
}
```

to print the person's name

```javascript
const printName = (personData) => {
    console.log(personData.name);
}
```

Object Destructuring

```javascript
const printName = ({name}) => {
    console.log(name);
}

const {name, age} = person;
// name : 'Sirui'
// age : 20
```

Array Destructuring

```javascript
const hobbies = ["sports", "cooking"];
const [hobby1, hobby2] = hobbies;
// hobby1: "sports"
// hobby2: "cooking"
```

## Async Code & Promises

[Promise](promise.md)

## Template Literals

```javascript
const name = "sirui";
let age = 20;
console.log(`my name is ${name} and I am ${age} years old`);
```
