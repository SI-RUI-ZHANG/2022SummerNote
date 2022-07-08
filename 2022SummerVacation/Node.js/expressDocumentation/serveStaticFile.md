# Serving static Files in Express

To serve static files such as images, CSS files, and Javascript files, use the `express.static` built-in middleware function in Express.

Function signature

```javascript
express.static(root, [options])
```

> This is a build-in middleware function in Express. It serves static files and is based on serve-static

- `root`: specifies the root directory from which to serve static assets.
- `options`: [see official documentation](https://expressjs.com/en/4x/api.html#router)

Use the following code to serve image, CSS files, and JavaScript files in directory named `public`:

```javascript
app.use(express.static('public'));
```

You can call the `express.static` middleware function multiple times

```javascript
app.use(express.static('public'));
app.use(express.static('files'));
```

> Express will looks up the files in the order in which you set the static directories with the `express.static` middleware function

To create a virtual path prefix for files that are served by the `express.static` function, specify a mount path for the static directory

```javascript
app.use('/static', express.static('public'));
```

The path that you provide to the `express.static` function is relative to the directory from where you launch your node process. If you run the express app from another directory, it’s safer to use the absolute path of the directory that you want to serve:

```javascript
const path = require('path')
app.use('/static', express.static(path.join(__dirname, 'public')))
```
