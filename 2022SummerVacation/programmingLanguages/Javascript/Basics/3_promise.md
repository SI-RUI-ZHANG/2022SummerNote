# Promise

A `Promise` is an object representing the eventual completion or failure of an asynchronous operation.

> Promises are used to handle asynchronous operations in JavaScript. They are easy to manage when dealing with multiple asynchronous operations where callbacks can create callback hell leading to unmanageable code.
>
> Prior to promises events and callback functions were used but they had limited functionalities and created unmanageable code.
> Multiple callback functions would create callback hell that leads to unmanageable code. Also it is not easy for any user to handle multiple callbacks at the same time.

- **Benefits of Promises**
    1. Improved Code Readability
    2. Better handling of asynchronous operations
    3. Better flow of control definition in asynchronous logic
    4. Better Error Handling

To create a promise

```javascript
const promise = new Promise(function(resolve, reject){
    // do something
})
```

- parameters:
  - `Promise` constructor takes only one argument which is a callback function (and that callback function is also referred as anonymous function too)
  - Callback function takes two arguments, `resolve` and `reject`
  - Perform operation inside the callback function and if everything went well then call `resolve`.
  - If desired operation do not go well then call `reject`

==Example==

```javascript
const promise = new Promise(function(resolve, reject) {
  const x = "geeksforgeeks";
  const y = "geeksforgeeks";
  if(x === y) {
      resolve();
  } else {
      reject();
  }
});

promise.
    then(function () {
     console.log('Success, You are a GEEK');
    }).
    catch(function () {
     console.log('Some error has occurred');
    });
    // success, Yor are a GEEK
```

## Promise Consumers

Promises can be consumed by registering functions using `.then` and `.catch` methods

### 1. `.then`

invoked when a promise is either resolved or rejected. It may also be defined as a career which takes data from promise and further executes it successfully.

Parameters:

1. First function is executed if promise is resolved and a result is received.
2. Second function is executed if promise is rejected and an error is received. (optional since is better to using `.catch()`)

syntax

```javascript
.then(function(result)){
    // handle success
}, function(error){
    // (optional) handle error
}
```

==Example==

```javascript
// ===================================================== resolved
const promise = new Promise(function(resolve, reject) {
    resolve('Geeks For Geeks');
})

promise
    .then(function(successMessage) {
        //success handler function is invoked
        console.log(successMessage);
    }, function(errorMessage) {
        console.log(errorMessage);
    })
// ===================================================== rejected
const promise = new Promise(function(resolve, reject) {
    reject('Promise Rejected')
})

promise
    .then(function(successMessage) {
        console.log(successMessage);
    }, function(errorMessage) {
        //error handler function is invoked
        console.log(errorMessage);
    })
```

### 2. `.catch`

invoked when a promise is either rejected or some error has occurred in execution. It is used as an Error Handler whenever at any step there is a chance of getting an error

Parameters:

1. Function to handle errors or promise rejections

syntax

```javascript
.catch(function(error){
    // handle error
})
```

==Example==
when promise _rejected_

```javascript
const promise = new Promise(function(resolve, reject)) {
    reject('promise rejected');
}

promise
    .then(function(successMessage){
        console.log(successMessage);
    })
    .catch(function(errorMessage){
        console.log(errorMessage);
    })
    // Promise Rejected
```

## Promises Examples

### Chaining

In the old days, doing several asynchronous operations in a row would lead to the classic callback pyramid of doom:

```javascript
doSomething(function (result){
    doSomethingElse(result, function (newResult) {
        doThirdThing(newResult, function (finalResult) {
            console.log('Got the final result: ' + finalResult);
        }, failureCallback);
    }, failureCallback);
}, failureCallback);
```

With modern functions, we attach our callbacks to the returned promises instead, forming a promise chain:

```javascript
doSomething()
    .then( function (result) {
        return doSomethingElse(result);
    })
    .then( function (newResult) {
        return doThirdThing(newResult);
    })
    .then ( function (finalResult) {
        console.log('Got the final result: ' + finalResult);
    }) 
    .catch ( failureCallback );
```

Written in arrow functions

```javascript
doSomething()
    .then( result => doSomethingElse(result) )
    .then( newResult => doThirdThing(newResult) )
    .then( finalResult => {
        console.log('Got the final result: ' + finalResult);
    })
    .catch(failureCallback);
```

### Chaining after a catch

```javascript
new Promise((resolve, reject) => {
    console.log('Initial');
    resolve();
})
.then(() => {
    throw new Error('Something failed');
    console.log('Do this');
})
.catch(() => {
    console.error('Do that');
})
.then(() => {
    console.log('Do this, no matter what happened before');
})
```

### Error propagation

You might recall seeing `failureCallback` three times in the pyramid of doom earlier, compared to only once at the end of the promise chain:

```javascript
doSomething()
    .then( result => doSomethingElse(result) )
    .then( newResult => doThirdThing(newResult) )
    .then( finalResult => {
        console.log('Got the final result: ' + finalResult);
    })
    .catch(failureCallback);
```

## Real world example

```javascript
const urls = [
    'https://jsonplaceholder.typicode.com/users',
    'https://jsonplaceholder.typicode.com/posts',
    'https://jsonplaceholder.typicode.com/albums',
]

Promise.all(urls.map(url => {
    return fetch(url).then(resp => resp.json())
})).then(results => {
    console.log(results[0])
    console.log(results[1])
    console.log(results[2])
}).catch(() => console.log('error'))
// we need all those data to make our page
```

### `Promise.all()`

`Promise.all()` method takes an iterable of promises as an input, and returns a single `Promise` that resolves to an array of the results of the input promises.

The returned promise will resolve when all of the input's promises have resolved, or if the input iterable contains no promises. It rejects immediately upon any of the input promises rejecting or non-promises throwing an error, and will reject with this first rejection message/error.

`Promise.all(iterable)`

```javascript
const promise1 = Promise.resolve(3);
const promise2 = 42;
const promise3 = new Promise((resolve, reject) => {
    setTimeout(resolve, 3000, 'foo');
});

Promise.all([promise1, promise2, promise3])
    .then(values => {
        console.log(values)
    })
```

return result after 3 seconds

```javascript
[ 3, 42, 'foo' ]
```
