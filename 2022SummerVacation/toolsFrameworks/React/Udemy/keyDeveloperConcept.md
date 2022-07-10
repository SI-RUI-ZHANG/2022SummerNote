# key Developer Concepts

## `map()`

creates a new array populated with the results of calling a provided function on every element in the calling array.

### syntax

```javascript
// Arrow function
map((element) => {})
map((element, index) => {})
map((element, index, array) => {})

// Callback function
map(callbackFn)
map(callbackFn, thisArg)

// Inline callback function
map(function(element){})
map(function(element, index){})
map(function(element, index, array){})
map(function(element, index, array){}, thisArg)
```

- `callbackFn`: Function that is called for every element of `arr`. Each time `callbackFn` executes, the returned value is added to `newArray`
  - `element`: The current element being processed in the array.
  - `index`: The index of the current element being processed in the array.
  - `array`: The array `map` was called upon.
- `thisArg`: Value to use as `this` when executing `callbackFn`

==Return a new array with each element being the result of the callback function==

`call back function:` A callback function is a function passed into another function as an argument, which is then invoked inside the outer function to complete some kind of routine or action.

## promise

[Promise Examples](../../../programmingLanguages/Basics/promise.md)

A `Promise` is an object representing the eventual completion or failure of an asynchronous operation.

> Promises are used to handle asynchronous operations in JavaScript. They are easy to manage when dealing with multiple asynchronous operations where callbacks can create callback hell leading to unmanageable code.
>
> Prior to promises events and callback functions were used but they had limited functionalities and created unmanageable code.
> Multiple callback functions would create callback hell that leads to unmanageable code. Also it is not easy for any user to handle multiple callbacks at the same time.
> Events were not good at handling asynchronous operations.
>
> Promises are the ideal choice for handling asynchronous operations in the simplest manner. They can handle multiple asynchronous operations easily and provide better error handling than callbacks and events. In other words also, we may say that, promises are the ideal choice for handling multiple callbacks at the same time, thus avoiding the undesired callback hell situation. Promises do provide a better chance to a user to read the code in a more effective and efficient manner especially it that particular code is used for implementing multiple asynchronous operations.

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
  - Promise constructor takes only one argument which is a callback function (and that callback function is also referred as anonymous function too)
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

### Promise Consumers

Promises can be consumed by registering functions using `.then` and `.catch` methods

#### 1. `.then`

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

#### 2. `.catch`

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

## `fetch()`

The `fetch` specification differs from `jQuery.ajax()` in the following significant ways

- The Promise returned from `fetch()` won't reject on HTTP error status even if the response is an HTTP 404 or 500. Instead, as soon as the server responds with headers, the Promise will resolve normally (with `ok` property of the response set to false if the response isn't in the range `200-299`), and it will only reject on network failure or if anything prevented the request from completing.
- Unless `fetch()` is called with the `credentials` option set to `include`, `fetch()`:
  - won't send cookies in cross-origin requests
  - won't set any cookies sent back in cross-origin responses

==Example==

```javascript
fetch('http://example.com/movies.json')
    .then(response => response.json())
    .then(data => console.log(data));
```

## `filter()`

The `filter` method creates new array with all elements that pass the test implemented by the provided function

syntax

```javascript
// Arrow function 
filter((element) => {})
filter((element, index) => {})
filter((element, index, array) => {})

// Callback function
filter(callbackFn)
filter(callbackFn, thisArg)

// Inline callback function
filter(function(element){})
filter(function(element, index){})
filter(function(element, index, array){})
filter(function(element, index, array){}, thisArg)
```

Parameters

- `callbackFn`: Function is a predicate, to test each element of the array. Return a value that coerces to `true` to keep the element, or to `false` otherwise
  - `element`: The current element being processed in the array
  - `index`: The index of the current element being processed in the array
  - `array` The array on on which `filter()` was called
- `thisArg`: (optional) Value to use as `this` when executing callbackFn

==Example==

```javascript
function isBigEnough(value) {
    return value >= 10;
}

let filtered = [12, 5, 8, 130, 44].filter(isBigEnough);
// filtered is [12, 130, 44]
```

## `includes()`

The `includes()` method determines whether an array includes a certain value among its entries, returning `true` or `false` as appropriate

syntax

```javascript
includes(searchElement)
includes(searchElement, fromIndex)
```

parameters

- `searchElement`: The value to search for.
- `fromIndex`: The position in this array at which to begin searching for `searchElement`.
