# The `package.json` guide

The `package.json` file is kind of a manifest for your project. It can do a lot of things, completely unrelated. It's a central repository of configuration for tools.

- `version`: indicates the current version
- `name`: sets the application/package name
- `description`: a brief description of the app/package
- `main`: sets the entry point for the application
- `private`: if set to `true`, will prevents the app/package to be accidentally published on `npm`
- `scripts`: defines a set of node scripts you can run
- `dependencies`: sets a list of `npm` packages installed as dependencies
- `devDependencies`: sets a list of `npm` packages installed as development dependencies
- `engines`: sets which version of `Node.js` that package/app works on
- `browserlist`: used to tell which browsers you want to support

## The `package-lock.json` file

The goal of `package-lock.json` file is to keep track of the exact version of every package that is installed so that a produce is 100% reproducible in the same way even if packages are updated by their maintainers.
