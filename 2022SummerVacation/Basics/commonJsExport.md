# Common JS Export

[official documentation for commonJS export](https://developer.mozilla.org/en-US/docs/web/javascript/reference/statements/export)

**NOTICE**: different from node.js export [see node.js export](../Node.js/ZTM/moduleSystem.md)

## Syntax

1. Named Exports (Zero or more exports per module)
2. Default Exports (One per module)

```javascript
// Exporting individual features
export let name1, name2, ..., nameN; // also var, const
export let name1 = ..., name2 = ..., ..., nameN; // also var, const
export function functionName(){...}
export class ClassName

// Export list
export {name1, name2, ..., name3};

// Renaming exports
export {variable1 as name1, variable2 as name2, ... nameN};

// Exporting destructured assignments with renaming
export const (name1, name2: bar) = o;
export const [name1, name2] = array;

// Default exports
export default expression;
export default function (...){...} // also class, function*
export default function name1(...){...} // also class, function*
export {name1 as default, ...};
```

## Description

There are two different types of export, **named** and **default**. You can have multiple exports per module but only one default export.
Each type corresponds to one the above syntax:

Named exports:

```javascript
// export features declared earlier
export {myFunction, myVariable};

// export individual features (can export var, let, const, function, class)
export let myVariable = Math.sqrt(2);
export function myFunction() {...};
```

Default exports

```javascript
// export feature declared earlier as default
export {myFunction as default}

// export individual features as default
export default function(){...}
export default class {}

// each export overwrites the previous one
```

## Import

It is mandatory to import named export within curly braces with the same name of the corresponding object.

To import default export

```javascript
// file tet.js
let k; export default k = 12;
```

```javascript
// other file
import m from './test'; // we have the freedom to use import m instead of import k
```

rename named export to avoid naming conflicts:

```javascript
export {myFunction as function1,
        myVariable as variable};
```
