# ES6 Refresher

## `let` vs `var` vs `const`

- `let` scoped to block
- `var` scoped to function
- `const` define constants, scoped to block

```javascript
function sayHello() {
    for (var i = 0; i < 5; i++) {
        console.log(i)
    }

    console.log(i)
}
```

## `Objects`

```javascript
const person = {
    name: "Sirui",
    walk() { },
    talk() { }
};

person.talk();
person['name'] = "Sirui Zhang"

const targetMember = 'name'
person[targetMember] = "Sirui"
```

## The `this` Keyword

In Javascript, the `this` keyword refers to an object.
Which object depends on how `this` is being invoked (used or called)

```javascript
const person = {
    name: "Sirui",
    walk() {
        console.log(this);
    },
};

person.walk();
// {name: "Sirui", walk: f}

const test = person.walk;
test();
// undefined
```

## Binding this

`bind()`: creates a new function that, when called, has its `this` keyword set to the provided value

```javascript
const person = {
    name: "Sirui",
    walk() {
        console.log(this);
    },
};

const walk = person.walk.bind(person);
walk();
// { name: 'Sirui', walk: [Function: walk] }
```

## Arrow Functions

```javascript
const square = function (number) {
    return number * number;
}

const square_one = (number) => {
    return number * number;
}

const square_two = (number) => number * number;
```

```javascript
const jobs = [
    {id: 1, isActive: true},
    {id: 2, isActive: true},
    {id: 3, isActive: false},
]

jobs.filter(function (job) {
    return job.isActive
})
jobs.filter(job => job.isActive)
```

## Arrow Function and this

```javascript
const person = {
    talk() {
        setTimeout(function (){
            console.log("this", this);
        }, 1000)
    }
}

person.talk()
// return window object
```

### to bind this to the object

#### the old method

```javascript
const person = {
    talk() {
        var self = this;
        setTimeout(function (){
            console.log("this", self);
        }, 1000)
    }
}

person.talk()
// this { talk: [Function: talk] }
```

#### use arrow function

```javascript
const person = {
    talk() {
        setTimeout( () => {
            console.log("this", this);
        }, 1000)
    }
}

person.talk()
// this { talk: [Function: talk] }
```

## Array.map Method

```javascript
const colors = ['red', 'green', 'blue'];
const items = colors.map(color => `<li>${color}</li>`);

// const items = colors.map(color => "<li>" + color + "</li>");

// const items = colors.map(function (color) {
//     return '<li>' + color + '</li>';
// });
```

## Object Destructuring

<div id="Object-Destructuring"></div>

```javascript
const address = {
    street: '',
    city: 'New York',
    country: ''
};

// const street = address.street;
// const city = address.street;
// const country = address.street;

const { street, city, country } = address;
console.log(city);
// New York

const { city: city_name } = address;
console.log(city_name);
// New York
```

## Spread Operator

### with array

```javascript
const first = [1, 2, 3];
const second = [4, 5, 6];

// const combined = first.concat(second);
const combined = [...first, ...second];
const clone = [...first];
```

### with object

```javascript
const first = { name : "sirui" };
const second = { job: "Student" };

const person = {...first, ...second, location: "New York"};
const clone = {...first};
```

## Classes

```javascript
class Person {
    constructor(name) {
        this.name = name
    }
    
    walk() {
        console.log("walk")
    }
}

const person = new Person("Sirui")
```

## Inheritance

```javascript
class Person {
    constructor(name) {
        this.name = name;
    }

    walk() {
        console.log("walk");
    }
}

class Student extends Person{
    constructor(name, degree) {
        super(name);
        this.degree = degree;
    }

    learn() {
        console.log("learn");
    }
}

const student = new Student("Sirui", "Sophomore");
console.log(student.degree);
```

## Modules

### Student.js

```javascript
import {Person} from "./Person";

export class Student extends Person{
    constructor(name, degree) {
        super(name);
        this.degree = degree;
    }

    learn() {
        console.log("learn");
    }
}
```

### Person.js

```javascript
export class Person {
    constructor(name) {
        this.name = name;
    }

    walk() {
        console.log("walk");
    }
}
```

### index.js

```javascript
import {Student} from "./Student";

const student = new Student("Sirui", "sophomore");
student.learn();
```

## Named and Default Exports

### Named export

#### Student.js

```javascript
import {Person} from "./Person";

export function takeExam(){}

export class Student extends Person{
    constructor(name, degree) {
        super(name);
        this.degree = degree;
    }

    learn() {
        console.log("learn");
    }
}
```

#### index.js

```javascript
import {Student} from "./Student";
import {takeExam} from "./Student";
```

### Default export

when you only export a single object from this file, use default export

#### Student.js

```javascript
import {Person} from "./Person";
export default class Student extends Person{
    constructor(name, degree) {
        super(name);
        this.degree = degree;
    }

    learn() {
        console.log("learn");
    }
}
```

#### index.js

```javascript
import Student from "./Student";
```

### Default export with named export

we can use default export mixed with named export

#### Student.js

```javascript
import {Person} from "./Person";
export function takeExam() {}
export default class Student extends Person{
    constructor(name, degree) {
        super(name);
        this.degree = degree;
    }

    learn() {
        console.log("learn");
    }
}
```

#### index.js

```javascript
import Student, {takeExam} from "./Student";
```
