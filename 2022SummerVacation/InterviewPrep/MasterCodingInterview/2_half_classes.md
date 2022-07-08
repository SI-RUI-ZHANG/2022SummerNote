# Classes In Javascript

## reference type

```javascript
let object1 = {value : 10}
let object2 = object1
let object3 = {value : 10}

console.log(object1===object2)
// true
console.log(object1===object3)
// false
```

## context vs scope

>_Scope_ has to do with the visibility of variables.

A variable can be defined in either local or global scope, which establishes the variables’ accessibility from different scopes during runtime. Any defined global variable, meaning any variable declared outside of a function body, will live throughout runtime and can be accessed and altered in any scope. Local variables exist only within the function body of which they are defined and will have a different scope for every call of that function.

Variables declared by **var** keyword are **scoped** to the immediate function body.
Variables declared by **let** keyword are **scoped** to the immediate enclosing block `{}`.

>_Context_ is related to objects. It refers to the object to which a function belongs.

We can refer to context with **this** keyword.

```javascript
function setName(name) {
    this.name = name;
}

setName('test')
console.log(name)
// test
// here this refers to the window object

const person = {
    name: 'Sirui',
    getName(){
        console.log(this.name)
    }
}

person.getName()
// Sirui
// here this refers to the person object
```

### `this` and arrow function `()=>{}`

Inside a regular function, this keyword refers to the function where it is called.

However, `this` is not associated with arrow functions. Arrow function does not have its own `this`. So whenever you call `this`, it refers to its parent scope.

using `function`

```javascript
function Person() {
    this.name = 'Jack',
    this.age = 25,
    this.sayName = function () {
        // this is accessible
        console.log(this.age);
        function innerFunc() {
            // this refers to the global object
            console.log(this.age);
            console.log(this);
        }
        innerFunc();
    }
}

let x = new Person();
x.sayName();

// 25
// undefined
// Window {}
```

using `this`

```javascript
function Person() {
    this.name = 'Jack',
    this.age = 25,
    this.sayName = function () {

        console.log(this.age);
        let innerFunc = () => {
            console.log(this.age);
        }

        innerFunc();
    }
}

const x = new Person();
x.sayName();

// 25
// 25
```

## Instantiation

```javascript
class Player {
    constructor(name, type) {
        this.name = name
        this.type = type
    }
    introduce(){
        console.log(`Hi I am ${this.name}, I'm a ${this.type}.`)
    }
}

class Wizard extends Player {
    constructor(name, type) {
        super(name, type);
    }
    play() {
        console.log('I am a wizard.')
    }
}

const player1 = new Player('Sirui', 'programmer')
const wizard1 = new Wizard('Shelly', 'Healer')

player1.introduce()
wizard1.play()
```
