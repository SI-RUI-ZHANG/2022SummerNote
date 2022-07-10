# Getting Started With Node.js

## Run Node.js scripts from the command line

If your main Node.js application file is `app.js`

```bash
node app.js
```

## Restart the application automatically

To restart the application automatically whenever there is a change in the application, we use `nodemon` module.

Install nodemon module globally

```bash
npm i -g nodemon
```

to run the application

```bash
nodemon app.js
```

## Exit from a Node.js program

In the console: `ctrl-C`

Programmatically: `process.exit()`
When Node.js runs this line, the process is immediately forced to terminate.

You can also pass an exit code:

```javascript
process.exit(1);
```

## Accept arguments from the command line

You can pass any number of arguments when invoking a Node.js application

```bash
node app.js joe
```

To retrieve the arguments, we need to use `process` object built into Node.js

The `process` object will exposes an `argv` property, which is an array that contains all the command line invocation arguments.

Inside `argv`:

- the first element is the full path of the `node` command
- the second element is the full path of the file being executed
- all the additional arguments are present from the third position going forward

==Example==

```javascript
process.argv.forEach((val, index) => {
    console.log(`${index}: ${val}`);
})
```

console:

```bash
node play.js test1 test2 test3 
```

output:

```bash
0: /opt/homebrew/Cellar/node/18.2.0/bin/node
1: /Users/zhangsirui/WebstormProjects/node-test/play.js
2: test1
3: test2
4: test3
```
