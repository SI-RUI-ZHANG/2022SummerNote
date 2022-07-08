# Basic Routing

**Routing** refers to determining how an application responds to a client request to a particular endpoint, which is a URL (or path) and a specific HTTP request method (`GET, POST,` and so on)

Each route can have one or more handler functions.

```javascript
app.METHOD(PATH, HANDLER)
```

- `app` is an instance of express
- `METHOD` is an _HTTP request method_
- `PATH` is a path on the server
- `HANDLER` is the function executed when the route is matched

## respond to different request

`get` request

```javascript
app.get('/', (req, res) => {
    res.send('Hello World!);
})
```

`post` request

```javascript
app.post('/', (req, res) => {
    res.send('Got a POST request');
})
```

`put` request

```javascript
app.put('/user', (req, res) => {
    res.send('Got a PUT request at /user')
})
```

`delete` request

```javascript
app.delete('/user', (req, res) => {
    res.send('Got a DELETE request at /user');
})
```
