# `async` `await`

## Example

```javascript
fetch('https://jsonplaceholder.typicode.com/users)
    .then(users => {
        const firstUser = users[0];
        console.log(firstUser);
        return fetch(
            'https://jsonplaceholder.typicode.com/posts?userId=' + firstUser.id
        );
    })
    .then(response => response.json())
    .then(posts => console.log(posts));
```

==is equivalent to==

```javascript
const myAsyncFunction = async () => {
    await fetch('https://jsonplaceholder.typicode.com/users);
    // all code below will wait for the fetch completed
    const users = await userResponse.json();
    const firstUser = user[0];
    console.log(firstUser);
    const postsResponse = await fetch(
            'https://jsonplaceholder.typicode.com/posts?userId=' + firstUser.id
    );
    const posts = await postResponse.json();

    console.log(posts);
}
```

==error handling==

```javascript
const myAsyncFunction = async () => {
    try {
        await fetch('https://jsonplaceholder.typicode.com/users);
        // all code below will wait for the fetch completed
        const users = await userResponse.json();
        const firstUser = user[0];
        console.log(firstUser);
        const postsResponse = await fetch(
                'https://jsonplaceholder.typicode.com/posts?userId=' + firstUser.id
        );
        const posts = await postResponse.json();

        console.log(posts);
    } catch (err) {
        //...
    }
}
```


`async` and `await` makes promises easier to write
`async` makes a function return a Promise
`await` makes a function wait for a Promise

## `async` Syntax

```javascript
async function {
    return "Hello";
}
```

is the same as

```javascript
function myFunction() {
    return promise.resolve("hello");
}
```

To use the promise

```javascript
async function myFunction() {
    return "Hello";
}

myFunction().then {
    function(value) { myDisplayer(value); },
    function(error) {
        myDisplayer(error);
    }
};
```

Or if you expect a normal value (not an error)

```javascript
async function myFunction() {
    return "Hello";
}

myFunction().then(
    function(value) {myDisplayer(value);}
)
```

---

## `await` Syntax

The keyword `await` before a function makes the function wait for a promise

```javascript
let value = await promise;
```

The `await` keyword can only be used inside an `async` function.

==example==

```javascript
async function myDisplay() {
    let myPromise = new Promise(function(resolve, reject) {
        resolve("I love you!");
    });
    document.getElementById("demo").innerHTML = myPromise;
}

myDisplay()
```
