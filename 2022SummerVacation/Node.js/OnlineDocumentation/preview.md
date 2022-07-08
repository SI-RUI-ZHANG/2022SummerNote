# Preview

## Introduction to Node.js

Node.js is a JavasCript run time environment.

Node.js run the V8 JavaScript engine, outside of browser.

A Node.js app run in single process.

Node.js provides a set of asynchronous I/O primitives in its library that prevent JavaScript code form blocking.

I/O:

- reading from the network
- accessing database
- accessing filesystem
- $\dots$

Node.js will not block the thread while performs I/O operations, it will resume the operation when response comes back, which allows Node.js to handle thousands of concurrent connections with a single server without introducing the burden of managing thread concurrency.

[key to understand asynchronous programming](https://nodejs.dev/learn/how-much-javascript-do-you-need-to-know-to-use-nodejs) (Scroll to bottom)

## JavaScript

JavaScript is **synchronous** by default and is single threaded, the code cannot create new threads and run in parallel.

### callback

A callback is a simple function that's passed as a value to another function, and will only be executed when the event happens.

#### The problem with callbacks

Callbacks are great for simple cases.

However every callback adds a level of nesting, and when you have lots of callbacks, the code starts to be complicated  very quickly.

```javascript
window.addEventListener('load', () => {
    document.getElementById('button').addEventListener('click', () => {
        setTimeout(() => {
            items.forEach(item => {
                // your code here
            });
        }, 2000);
    });
});
```
