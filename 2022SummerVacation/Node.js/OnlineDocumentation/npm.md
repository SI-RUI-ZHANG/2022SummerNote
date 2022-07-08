# Understanding npm

## An Introduction to the npm package manager

`npm` is a standard package manager for `Node.js`

### Downloads

#### Install all dependencies

```bash
npm install
```

It will install everything the project needs, in the `node_modules` folder, creating it if it's not existing already.

#### Installing a single package

```bash
npm install <package-name>
```

This command adds `<package-name>` to the `package.json` file.

flags added to this command:

- `--save-dev` installs and adds the entry to the package.json file devDependencies
- `--no-save` installs but does not add the entry to the package.json file dependencies
- `--save-optional` installs and adds the entry to the package.json file optionalDependencies
- `--no-optional` will prevent optional dependencies from being installed

Shorthands of the flags:

- `-S`: `--save`
- `-D`: `--save-dev`
- `-O`: `--save-optional`

`devDependencies` vs `dependencies`: the former contains development tools, like testing library, while the latter is bundled with the app in production.

#### Updating packages

```bash
npm update
# updates all dependencies

npm update <package-name>
# updates specified dependency 
```

### Running Tasks

The `package.json` file supports a format for specifying command line tasks that can be run by using

```bash
npm run <task-name>
```

For example

```json
{
    "scripts": {
        "start-dev": "node lib/server-development",
        "start": "node lib/server-production"
    }
}
```

## Where does npm install the packages?

### local

By default

```bash
npm install lodash
```

The package is installed in the current file tree, under the `node_modules` subfolder.

### global

```bash
npm install -g lodash
```

Install `lodash` using a global location

==global location==

```bash
npm root -g
```

## Use package installed using npm

### packages in `node_modules`

```bash
npm install lodash
```

```javascript
const _ = require('lodash');
```

### `exe` packages

```bash
npx cowsay Good Morning
```

## Find the installed version of an npm package

```bash
npm list
npm list -g
```

## Install an older version of an npm package

```bash
npm install <package>@<version>
```

## Semantic Versioning

[Semantic Versioning using npm](https://nodejs.dev/learn/semantic-versioning-using-npm)

## Uninstalling npm packages

### locally

```bash
npm uninstall <package-name>
```

Using the `-S` flag, or `--save`, will also remove the reference in the `package.json` file.

### globally

```bash
npm uninstall -g <package-name>
```
