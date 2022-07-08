# Functional Component

Live template `rsc` or `rsi`

## Pure & Impure Functions

A _pure function_ is a function that does not modify any external variable. And the _impure function_ modifies the external variable.

_Impure functions_  have side effects it does make changes on external variables.

## Hooks: `useState`

[Introduction Hooks](https://reactjs.org/docs/hooks-intro.html)
[Hooks vs Class](https://reactjs.org/docs/hooks-state.html)

The React `useState` Hooks allows us to track state in a function component.

State generally refers to data or properties that need to be tracking in an application.

### Import `useState`

To use the `useState` Hook, we first need to `import` it into our component.

```jsx
import { useState } from 'react';
```

### Initialize `useState`

`useState` accepts an initial state and returns two values:

- The current state.
- A function that updates the state.

```jsx
import { useState } from 'react';

function FavoriteColor() {
    const [color, setColor] = useState('');
    // destructuring
}
```

The initial state of `color` is `''`
`setColor()` is the function used to update our state `color`

### Read State

```jsx
import {useState} from 'react';
import ReactDOM form 'react-dom/client';

function FavoriteColor() {
    const [color, setColor] = useState('red');

    return <h1><My favorite color is {color}!/h1>
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<FavoriteColor />);
```

### Update State

we use state update function to update state

```jsx
import {useState} from 'react';
import ReactDOM form 'react-dom/client';

function FavoriteColor() {
    const [color, setColor] = useState('red');

    return {
        <div>
            <h1>My favorite color is {color}!</h1>
            <button
                type = 'button'
                onClick = {() => setColor('blue')}
                >
                Blue</button>
        </div>
    }
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<FavoriteColor />);
```

### Another Example

```jsx
import {useState} from 'react';
import ReactDOM form 'react-dom/client';

function Car() {
    const [brand, setBrand] = useState('Ford');
    const [model, setModel] = useState('Mustang');
    const [year, setYear] = useState('1964');
    const [color, setColor] = useState('red');

    return {
        <div>
            <h1>My {brand}!</h1>
            <p>
                It is a {color} {model} from {year}.
            </p>
        </div>
    }
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Car />);
```

## Hooks: `useEffect`

The `Effect Hook` lets you perform side effects in function components:

- fetching data
- directly updating the DOM
- times
- $\dots$

syntax

```jsx
useEffect(<function>, <dependency>) // The second argument is optional
```

### `dependency` No dependency passed

```jsx
useEffect(() => {
    //Runs on every render
});
```

### `dependency` An empty array

```jsx
useEffect(() => {
    //Runs only on the first render
}, []);
```

### `dependency` Props or state values

```jsx
useEffect(() => {
    //Runs on the first render
    //And any time any dependency value changes
}, [prop, state]);
```

## Function Component Re-rendering

Unlike class components, whenever React decides to re-render the component, it run the entire function.

_class component only run the `render()` method_

In functional component, re-render is triggered only when the state actually receive a different value. If we call method to update state and pass the same value, react will not re-render this component.
