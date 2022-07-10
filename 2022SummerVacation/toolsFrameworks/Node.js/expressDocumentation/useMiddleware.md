# Use Middleware

[see official documentation](https://expressjs.com/en/guide/using-middleware.html#)

> Express is a routing and middleware web framework that has minimal functionality of its own: An express application is essentially a series of middleware function calls
> `Middleware` functions are function that have access the the `request object(req)`, the `response object(res)`, and the `next` middleware function in the application's request-response cycle.

## Application-level middleware

> Bind application-level middleware to an instance of the app object by using the `app.use()` and `app.method()`

### no path

executed every time the app receives a request

```javascript
const express = require('express');
const app = express();

app.use((req, res, next) => {
    console.log('Time: ', Date.now());
    next();
})
```

### with path

executed for any type of HTTP request on the specified path

```javascript
app.use('/user/:id', (req, res, next) => {
    console.log('Request Type: ', req.method);
    next()
})
```

### with specified method

```javascript
app.get('/user/:id', (req, res, next) => {
    res.send('USER');
})
```

### loading a series of middleware function at a mount point

```javascript
app.use('/user/:id', (req, res, next) => {
    console.log('Request URL: ', req.originalUrl);
    next();
}, (req, res, next) => {
    console.log('Request Type: ', req.method);
    next();
})
```

### define multiple routes for a path

**`next('route')`**: call `next('route')` to skip the rest of the middleware functions from a router middleware stack.
**NOTE**: `next('route')` will only work in middleware functions that were loaded by using the `app.METHOD()` or `router.METHOD()` functions.

```javascript
app.get('/user/:id', (req, res, next) => {
    // if the use ID is 0, skip to the next route
    if (req.params.id === '0') next('route');
    else next();
}, (req, res, next) => {
    // send a regular response
    res.send('regular');
})

// handler for the /user/:id path, which sends a special response
app.get('/user/:id', (req, res, next) => {
    res.send('special');
})
```

## Router-level middleware

> Router-level middleware works in the same way as application-level middleware, except it is bound to an instance of `express.Router()`

```javascript
const router = express.Router();
```

Load router-level middleware by using the `router.use()` and `router.METHOD()` functions

```javascript
const express = require('express');
const app = express();
const router = express.Router();

// a middleware function with no mount path. This code is executed for every request to the router
router.use((req, res, next) => {
    console.log('Time: ', Date.now());
    next();
})

// a middleware sub-stack shows request info for any type of HTTP request to the /user/:id path
router.use('/user/:id', (req, res, next) => {
    console.log('Request URL: ', req.originalUrl);
    next();
}, (req, res, next) => {
    console.log('Request Type:', req.method);
    next()
})

// a middleware sub-stack that handles GET requests to the /user/:id path
router.get('/use/:id', (req, res, next) => {
    // if the user ID is 0, skip to the next router
    if (req.params.id === '0') next('route');
    // otherwise pass control to the next middleware function in this stack
    else next();
}, (req, res, next) => {
    // render a regular page
    res.render('regular')
})

// handler for the /user/:id path, which renders a special page
router.get('/user/:id', (req, res, next) => {
    console.log(req.params.id);
    res.render('special')
})

// mount the router on the app
app.use('/', router);
```

## Error-handling middleware

> Error-handling middleware always takes **four** arguments

```javascript
app.use((err, req, res, next) => {
    console.error(err.stack);
    res.status(500).send('Something broke!');
})
```
