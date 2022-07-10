# Routing

[see official documentation](https://expressjs.com/en/guide/routing.html)

**Routing** refers to how an application's endpoints (URL) respond to client requests.

- `app.get()` to handle GET requests
- `app.post()` to handle post requests
- `app.all()` to handle all HTTP methods
- `app.use()` to specify middleware as the callback function

==example of basic route==

```javascript
const express = require('express');
const app = express();

// respond with "hello world" when a GET request is made to the homepage
app.get('/', (rep, res) => {
    res.send('hello world');
})
```

## `app.all()`

`app.all()` is a special method used to load middleware functions a a path of all HTTP request methods.

The following handler is executed for requests to the route "/secret" whether using GET, POST, PUT, DELETE, or any other HTTP request method.

```javascript
app.all('/secret', (req, res, next) => {
    console.log('Accessing the secret section...');
    next() // pass control to the next handler
})
```

## Route handlers

You can provide multiple callback functions that behave like `middleware` to handle a request.

A single callback function:

```javascript
app.get('/example/a', (req, res) => {
    res.send('Hello form A');
})
```

More than one callback function

```javascript
app.get('/example/a', (req, res, next) => {
    console.log('the response will be sent by the next function...');
    next()
}, (req, res) => {
    res.send('Hello from B!');
})
```

An array of callback functions

```javascript
const cb0 = function (req, res, next) {
    console.log('CB0');
}

const cb1 = function (req, res, next) {
    console.log('CB1');
}

const cb2 = function (req, res, next) {
    console.log('CB2');
}

app.get('/example/c', [cb0, cb1, cb2]);
```

Array of callback function combined with independent function

```javascript
app.get('/example/c', [cb0, cb1, cb2], (req, res, next) => {
    console.log('the response will be sent by the next function ...');
    next();
}, (req, res) => {
    res.send('Hello from D!);
});
```

## `app.route()`

You can create chainable route handlers for a route path using `app.route()`

```javascript
app.route('/book')
    .get((req, res) => {
        res.send('Get a random book');
    })
    .post((req, res) => {
        res.send('Add a book');
    })
    .put((req, res) => {
        res.send('Update the book');
    })
```

## `express.Router`

A `Router` instance is a complete middleware and routing system, it is often referred to as a "mini-app" for this reason.

==example==

```javascript
const express = require('express');
const router = express.Router()

// middleware that is specific to this router
router.use((req, res, next) => {
    console.log('Time: ', Date.now());
    next()
})
// define the home page route
router.get('/', (req, res) => {
    res.send('Birds home page');
})
// define the about route
router.get('/about', (req, res) => {
    res.send('About birds');
})

module.exports = router
```

load the router module in the app:

```javascript
const birds = require('./birds');

// ...

app.use('/birds', birds);
```
