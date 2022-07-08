# Module System

> The Node.js REPL
>
> - read
> - evaluate
> - print
> - loop

## The `require` Function

```javascript
const { get } = require('https');

const req = get('https://www.google.com', (res) => {
    res.on('data', (chunk) => {
        console.log(`Data chunk: ${chunk}`);
    });
    res.on('end', () => {
        console.log('No more data');
    })
})
```

## Why use Modules

1. Reuse existing code
2. Organize your code
3. Expose only what will be used

## Creating Our Own Modules

### request.js

```javascript
function encrypt(data) {
    return 'encrypted data';
}

function send(url, data) {
    const encryptedData = encrypt(data)
    console.log(`sending ${encryptedData} to ${url}`)
}

module.exports = { send }
```

### response.js

```javascript
function decrypt(data) {
    return 'decrypted data';
}

function read() {
    return decrypt('data');
}

module.exports = { read }
```

### https.js

```javascript
const request = require('./request');
const response = require('./response');

function makeRequest(url, data) {
    request.send(url, data);
    return response.read();
}

const responseData = makeRequest('www.google.com', '');
console.log(responseData);
```

the result

```javascript
sending encrypted data to www.google.com
decrypted data
```

## Exporting From Modules

```javascript
function decrypt(data) {
    return 'decrypted data';
}

function read() {
    return decrypt('data');
}

module.exports = { read }
```

another way of doing so

```javascript
function decrypt(data) {
    return 'decrypted data';
}

module.exports.read = function read() {
    return decrypt('data');
}
```

yet another shortcuts of doing so

```javascript
function decrypt(data) {
    return 'decrypted data';
}

exports.read = function read() {
    return decrypt('data');
}
```

==if we only export one function==

```javascript
function decrypt(data) {
    return 'decrypted data';
}

module.exports  = function read() {
    return decrypt('data');
}
```

==https.js==

```javascript
const request = require('./request');
const read = require('./response');

function makeRequest(url, data) {
    request.send(url, data);
    return read();
}

const responseData = makeRequest('www.google.com', '');
console.log(responseData);
```

### Recommend way of exporting and importing

#### request.js

```javascript
function encrypt(data) {
    return 'encrypted data';
}

function send(url, data) {
    const encryptedData = encrypt(data)
    console.log(`sending ${encryptedData} to ${url}`)
}

module.exports = { send }
```

#### response.js

```javascript
function decrypt(data) {
    return 'decrypted data';
}

function read() {
    return decrypt('data');
}

module.exports = { read }
```

#### https.js

```javascript
const { send } = require('./request');
const { read } = require('./response');

function makeRequest(url, data) {
    send(url, data);
    return read();
}

const responseData = makeRequest('www.google.com', '');
console.log(responseData);
```

## CommonJS vs ECMAScript Modules

The syntax we just introduced above is using CommonJS modules

### ECMAScript import

```javascript
import './App.css';
import {Component} from "react";
```

### ECMAScript export

```javascript
export default App;
```

==ECMAScript is now officially supported by node.js==

## Creating Our Own ECMAScript Modules

### response.mjs

```javascript
function decrypt(data) {
    return 'decrypted data';
}

function read() {
    return decrypt('data');
}

export {
    read,
}
```

### request.mjs

```javascript
function encrypt(data) {
    return 'encrypted data';
}

function send(url, data) {
    const encryptedData = encrypt(data)
    console.log(`sending ${encryptedData} to ${url}`)
}

export {
    send,
}
```

### https.mjs

```javascript
import { send } from './request.mjs'
import { read } from './response.mjs'

function makeRequest(url, data) {
    send(url, data);
    return read();
}

const responseData = makeRequest('www.google.com', '');
console.log(responseData);
```

## Module Caching

## Using index.js

==not recommended==

When you pass a folder to Node's `require()`, it will check `package.json` for an endpoint. If that isn't defined, it checks for `index.js`, and finally `index.node`.

The `index.js` is like a entry point for requiring a module
