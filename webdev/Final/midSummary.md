# webdev mid summary

## basic Javascript

### `typeof()`

returns a string indicating the type of unevaluated operand

returned types:

- `string`
- `number`
  - includes `NaN`
  - float, integer
- `boolean`
- `object`
  - includes `null`
- `function`
- `undefined`
  - datatype of an undefined variable
  - datatype of a variable that has not been assigned a value

### parse datatype

- `parseInt()`
- `parseFloat()`
- `variable.toString()`

### array & object

#### array

```javascript
let arr = ["apple", "pear", "peach"];
```

#### object

```javascript
let pokemon = {
    name: "Pikachu",
    age: 6,
    power: ["thunder", "shock"],
    sayHello: function() {
        console.log("hello");
        console.log( this.name );
    }
};
```

### DOM

#### Attributes

```javascript
let element = document.getElementById('element');
element.href = "...";

element.target = "blank";
element.setAttribute("target", "blank");

element.id = element.getAttribute("id") // true

element.style.color = "green";
element.style["font-size"] = "200%";
```

#### Classes

```javascript
let a = document.getElementById('one');
if (a.classList.contains("foo")) {
    a.classList.remove("foo");
} else {
    a.classList.add("foo");
}
```

#### create new DOM elements

```javascript
let newTag = document.createElement("p");
let body = document.getElementById("body");
newTag.innerHTML = "Hello, world";
body.append(newTag);

// or body.appendChild(newTag);
```

### Cookies

#### set a cookie

```javascript
document.cookie = "name=Sirui";
// this will create a new cookie, will not overwrite other cookies
```

#### access cookie

`let x = document.cookie;`

- a cookie string delimited by `;`

### localStorage

#### set value

`window.localStorage.setItem(key, value);`

#### access value

`window.localStorage.getItem(key);`
