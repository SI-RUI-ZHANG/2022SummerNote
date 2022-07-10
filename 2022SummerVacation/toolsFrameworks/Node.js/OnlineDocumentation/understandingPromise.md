# Understanding Javascript Promise

[Official Documentation](https://nodejs.dev/learn/understanding-javascript-promises)

A promise is commonly defined as a proxy for a value that will eventually become available.

Promises are one way to deal with asynchronous code, without getting stuck in callback hell.

## How promises work

Once a promise has been called, it will start in a pending state. This means that the calling function continues executing, while the promise is pending until it resolves, giving the calling function whatever data was being requested.

The created promise will eventually end in a `resolved state`, or in a `rejected state`, calling the respective callback functions (passed to `then` and `catch`) upon finishing.

Promises are used by standard modern Web APIs such as:

- the `Battery` API
- the `Fetch` API
- `Service Workers`

---

## Creating a promise

`Promise` API exposes a `Promise` constructor:
`new Promise()`

```javascript
const done = true;
const isItDoneYet = new Promise((resolve, reject) => {
    if (done) {
        const workDone = 'Here is the thing I built';
        resolve(workDone);
    } else {
        const why = 'Still working on something else';
        reject(why)
    }
});
```

Using `resolve` and `reject`, we can communicate back to the caller what the resulting promise state was, and what to do with it. They can return `string`, `object`, or `null` as well.

---

## Consuming a promise

```javascript
const done = true;

const isItDoneYet = new Promise((resolve, reject) => {
    setTimeout(() => {
        if (done) {
            resolve('fine');
        } else {
            reject('error');
        }
    }, 3000);
})

const check = () => {
    isItDoneYet
        .then(ok => {
            console.log(ok)
        })
        .catch(err => {
        console.log(err)
        })
}

check();
```

output

```javascript
// after 3 seconds
fine 
```

Running `check()` will specify functions to execute when the `isItDoneYet` promise resolves (in the `then` call) or rejects (in the `catch` call).

---

## Chaining promises

A promise can be returned to another promise, creating a chain of promises.

The `Fetch` API is a promise-based mechanism, and calling `fetch()` is equivalent to defining our own promise using `new Promise()`.

```javascript
const status = response => {
    if (response.status >= 200 && response.status < 300) {
        return Promise.resolve(response);
    }
    return Promise.reject(new Error(response.statusText));
};

const json = response => response.json();

fetch('/todos.json')
    .then(status) // status function is called here and it returns a promise
    .then(json) // json function is called and it returns a promise
    .then(data => {
        // after calling json function, data is returned here to `data`
        console.log('Request succeeded with JSON response', data);
    })
    .catch(error => {
        console.log('Request failed', error);
    })
```

Running `fetch()` returns a [response](https://fetch.spec.whatwg.org/#concept-response) which has many properties, and within those we have

- `status`: a numeric value representing the HTTP status code
- `statusText`: a status message, which is `OK` if the request succeeded
- `json()`: returns a promise that will resolve with the content of the body processed and transformed into JSON

---

## Handling errors

When anything in the chain of promises fails and raises an error or rejects the promise, the control goes to the nearest `catch()` statement down the chain.

---

## Orchestrating promises

### `Promise.all()`

`Promise.all()` will synchronize different promises.
It helps you define a list of promises, and execute something when they are all resolved.

==Example==

```javascript
const f1 = fetch('/something.json');
const f2 = fetch('/something2.json');

Promise.all([f1, f2])
    .then(res => {
        console.log('Array of results', res);
    })
    .catch(err => {
        console.error(err);
    })
```

==Using destructuring assignment==

```javascript
Promise.all([f1, f2]).then(([res1, res2]) => {
    console.log('results', res1, res2);
})
```

### `Promise.race()`

`Promise.race()` runs when the first of the promises you pass to it settles (resolves or rejects), and it runs the attached callback just once, with the result of the first promise settled.

==Example==

```javascript
const first = new Promise((resolve, reject) => {
    setTimeout(resolve, 500, 'first');
});
const second = new Promise((resolve, reject) => {
    setTimeout(resolve, 100, 'second');
});

Promise.race([first, second]).then(result => {
    console.log(result); // second
})
```

### `Promise.any()`

`Promise.any()` settles when any of the promises you pass to it fulfill or all of the promises get rejected. It returns a single promise that resolves with the value from the first promise that is fulfilled.
If all promises are rejected, then the returned promise is rejected with an `AggregateError`.

==Example==

```javascript
const first = new Promise((resolve, reject) => {
    setTimeout(reject, 500, 'first');
});
const second = new Promise((resolve, reject) => {
    setTimeout(reject, 100, 'second');
});

Promise.any([first, second]).catch(error => {
    console.log(error); // AggregateError
})
```
