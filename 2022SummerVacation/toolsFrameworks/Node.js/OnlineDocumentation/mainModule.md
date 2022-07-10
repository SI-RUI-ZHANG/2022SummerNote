# To access the main module

```javascript
path.dirname(require.main.filename);
```

`require.main.filename` returns the entry point of your application

## `require.main`

The `Module` object representing the entry script loaded when the Node.js process launched

In `entry.js` script

```javascript
console.log(require.main);
```

```bash
node entry.js
```

```bash
Module {
  id: '.',
  path: '/absolute/path/to',
  exports: {},
  filename: '/absolute/path/to/entry.js',
  loaded: false,
  children: [],
  paths:
   [ '/absolute/path/to/node_modules',
     '/absolute/path/node_modules',
     '/absolute/node_modules',
     '/node_modules' ] }
```
