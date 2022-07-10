# Package Management

## Initiate package

- `npm init`: initiate package
- `npm init -y`: initiate package with default options

==In case you accidentally deleted some modules==
`npm install` will install all dependencies listed in `package.json`

## Run file in terminal

```bash
npm run filename
```

==or==

```bash
nodemon run filename
```

## Using Third Party Modules

==Terminal==

```bash
npm i axios
```

```javascript
const axios = require('axios');

axios.get('https://www.google.com')
    .then((response) => {
        console.log(response);
    })
    .catch((err) => {
        console.log(err);
    })
    .then(() => {
        console.log('All done!');
    })
```

## The node_modules Folder

packages from `npm` is downloaded to `node_modules`

## package-lock.json

`package-lock.json` file gives more specific information about dependencies and versions than `package.json`.

## The NPM Tools: nodemon

```bash
npm install -g nodemon
```

`-g`: install package globally
