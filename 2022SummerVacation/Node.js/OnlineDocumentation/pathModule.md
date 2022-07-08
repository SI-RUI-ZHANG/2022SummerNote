# Path Module

[see official documentation](https://nodejs.dev/learn/the-nodejs-path-module#pathjoin)

requiring path module

```javascript
const path = require('path');
```

## `path.basename()`

Return the last portion of a path. A second parameter can filter out the file extension

```javascript
require('path').basename('/test/something'); // something
require('path').basename('/test/something.txt'); // something.txt
require('path').basename('/test/something.txt', '.txt'); // something
```

## `path.dirname()`

Return the directory part of a path

```javascript
require('path').dirname('/test/something'); // /test
require('path').dirname('/test/something/filet.txt'); // /test/something
```

## `path.extname()`

Return the extension part of a path

```javascript
require('path').extname('/test/something'); // ''
require('path').extname('/test/something/file.txt'); // '.txt'
```

## `path.format()`

Returns a path string from an object
Accepts an object as argument with the following keys:

- `root`: the root
- `dir`: the folder path starting from the root
- `base`: the file name + extension
- `name`: the file name
- `ext`: the file extension

`root` is ignored if `dir` is provided
`ext` and `name` are ignored if `base` exists

```javascript
// POSIX
require('path').format({ dir: '/Users/joe', base: 'test.txt' }); //  '/Users/joe/test.txt'

require('path').format({ root: '/Users/joe', name: 'test', ext: '.txt' }); //  '/Users/joe/test.txt'

// WINDOWS
require('path').format({ dir: 'C:\\Users\\joe', base: 'test.txt' }); //  'C:\\Users\\joe\\test.txt'
```

## `path.join()`

Joins two or more parts of a path

```javascript
const name = 'joe';
require('path').join('/', 'users', name, 'notes.txt'); 
// '/users/joe/notes.txt'
```
