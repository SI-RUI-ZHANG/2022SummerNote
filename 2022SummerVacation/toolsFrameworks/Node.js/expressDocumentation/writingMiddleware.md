# Writing middleware

`middleware` functions are functions that have access to the request object, the response object, and the next function in the application's request-response cycle.

The `next` function is a function in the express router which, when invoked, executes the middleware succeeding the current middleware.

`middleware` functions can:

- Execute any code
- Make changes to the request and the response objects
- End the request-response cycle
- Call the next middleware in the stack

If the current middleware function doesn't end the request-response cycle, it must call `next()` to pass control to the next middleware function, Otherwise, the request will be left hanging.

```javascript
app.get('/', function(req, res, next) => {
    next();
})

app.listen(3000);
```

- `get`: HTTP method for which the middleware function applies
- `/`: Path (route) for which the middleware function applies
- `function`: The middleware function
- `req`: HTTP request argument to the middleware function
- `res`: The response argument to the middleware function
- `next`: Callback argument to the middleware function

## Example

### Middleware function `myLogger`

```javascript
const myLogger = function (req, res, next) => {
    console.log('LOGGED');
    next();
}
```

> `next()`: Calling this function invokes the next middleware function in the app. The `next()` function is not a part of the Node.js or Express API, but is a third argument that is passed to the middleware function.

To load the middleware function, call `app.use()`, specifying the middleware function.

```javascript
const express = require('express');
const app = express();

const myLogger = function(req, res, next) {
    console.log('LOGGED');
    next();
}

app.use(myLogger);

app.get('/', (req, res) => {
    res.send('Hello World');
})

app.listen(3000);
```

> Every time the app receives a request, it print the message "LOGGED" to the terminal.

The order of middleware loading is important: middleware function that are loaded first are executed first.

### Middleware function `requestTime`

```javascript
const requestTime = function (req, res, next) {
    req.requestTime = Date.now();
    next();
}
```

To use the `requestTime` middleware function.

```javascript
const express = require('express');
const app = express();

const requestTime = function(req, res, next) {
    req.requestTIme = Date.now();
    next();
}

app.use(requestTime);

app.get('/', (req, res) => {
    let responseText = 'Hello World!<br>";
    responseText += `<small>Requested at: ${req.requestTime}</small>`;
    res.send(responseText);
})

app.listen(3000);
```

### Middleware function validateCookies

```javascript
async function cookieValidator(cookies) {
    try {
        await externallyValidateCookie(cookies.testCookie);
    } catch {
        throw new Error('Invalid cookies');
    }
}
```

Use `cookie-parser` to parse incoming cookies

```javascript
const express = require('express');
const cookieParser = require('cookie-parser');
const cookieValidator = require('./cookieValidator') 

const app = express();

async function validateCookies (req, res, next) {
    await cookieValidator(req.cookies);
    next();
}

app.use(cookieParser());

app.use(validateCookies);

// error handler

app.use((err, req, res, next) => {
    res.status(400).sent(err.message);
})

app.listen(3000);
```
