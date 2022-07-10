# React Overview

## Use react in a static HTML file

This method is not very efficient and hard to maintain

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script src="https://unpkg.com/react@^16/umd/react.production.min.js"></script>
    <script src="https://unpkg.com/react-dom@16.13.0/umd/react-dom.production.min.js"></script>
    <script src="https://unpkg.com/babel-standalone@6.26.0/babel.js"></script>
    <title>Hello React!</title>
</head>
<body>

<div id="root"></div>

<script type="text/babel">
    class App extends React.Component {
        render() {
            return <h1>Hello World</h1>;
        }
    }
    ReactDOM.render(<App/>, document.getElementById('root'));
</script>

</body>
</html>
```

- `React`: the React top level API
- `React DOM`: adds DOM-specific methods
- `Babel`: a javaScript compiler that lets us use ES6+ in old browsers
- `render()` the only required method in a class component

## Create React App

```bash
npx create-react-app react-tutorial
cd react-tutorial
npm start
```

## JSX: JavaScript + XML

With JSX, we can write what looks like HTML, and also we can create and use our own XML-like tags

### with JSX

```jsx
const heading = <h1 className = "site-heading">Hello, React</h1>
```

### without JSX

```jsx
const heading = React.createElement('h1', {className: 'site-heading'}, 'Hello, react')
```

### key differences to not when writing JSX

- `className` instead of `class` for CSS classes, since `class` is a reserved keyword in JavaScript
- `onClick` instead of `onclick`: properties and methods in JSX are camelCase
- `<img />` instead of `<img>`: self-closing tags must end in slash

### use Javascript in JSX with `{}`

```jsx
const name = "Sirui";
const heading = <h1>Hello, {name}</h1>;
```

## Components

Almost everything in React consists of components, which can be `class components` or `simple components`.

Most React apps have many small components, and everything loads into the main `App` component. Components also often get their own file.

### Example

#### index.js

```jsx
import React from 'react';
import {createRoot} from "react-dom/client";
import App from './App'
import './index.css';

const root = createRoot(document.getElementById('root'))
root.render(<App/>)
```

#### App.jsx

```jsx
import React, {Component} from 'react';

class App extends Component {
    render() {
        return (
            <div className="App">
                <h1>Hello, React!</h1>
            </div>
        );
    }
}

export default App;
```

In this way we export the component as `App` and load it in `index.js`

## Class Components

### Table.jsx

```jsx
import React, {Component} from 'react';

class Table extends Component {
    render() {
        return (
            <table>
                <thead>
                <tr> <th>Name</th> <th>Job</th> </tr>
                </thead>
                <tbody>
                <tr> <td>Charlie</td> <td>Janitor</td> </tr>
                <tr> <td>Mac</td> <td>Bouncer</td> </tr>
                <tr> <td>Dee</td> <td>Aspiring actress</td> </tr>
                <tr> <td>Dennis</td> <td>Bartender</td> </tr>
                </tbody>
            </table>
        );
    }
}

export default Table;
```

### App.jsx

```jsx
import React, {Component} from 'react';
import Table from "./Table";

class App extends Component {
    render() {
        return (
            <div className="App">
                <h1>Hello, React!</h1>
                <Table/>
            </div>
        );
    }
}
export default App;
```

## Simple Components

`simple component` is a function.

### Table.jsx (modified)

```jsx
import React, {Component} from "react";

const TableHeader = () => {
    return (
        <thead>
        <tr>
            <th>Name</th>
            <th>Job</th>
        </tr>
        </thead>
    )
}

const TableBody = () =>{
    return (
        <tbody>
        <tr>
            <td>Charlie</td>
            <td>Janitor</td>
        </tr>
        <tr>
            <td>Mac</td>
            <td>Bouncer</td>
        </tr>
        <tr>
            <td>Dee</td>
            <td>Aspiring actress</td>
        </tr>
        <tr>
            <td>Dennis</td>
            <td>Bartender</td>
        </tr>
        </tbody>
    )
}

class Table extends Component {
    render() {
        return (
            <table>
                <TableHeader/>
                <TableBody/>
            </table>
        )
    }
}

export default Table;
```

## Props (properties)

React handle data through properties, referred to as props, and with state.

### App.jsx

```jsx
import React, {Component} from 'react';
import Table from "./Table";

class App extends Component {
    render() {
        const characters = [
            {
                name: "Charlie",
                job: "Janitor",
            },
            {
                name: "Mac",
                job: "Bounder",
            },
            {
                name: "Dee",
                job: "Aspring actress",
            },
            {
                name: "Dennis",
                job: "Bartender"
            }
        ]

        return (
            <div className="App">
                <h1>Hello, React!</h1>
                <Table characterData = {characters}/>
            </div>
        );
    }
}

export default App;
```

### Table.jsx

```jsx
import React, {Component} from "react";

const TableHeader = () => {
    return (
        <thead>
        <tr>
            <th>Name</th>
            <th>Job</th>
        </tr>
        </thead>
    )
}

const TableBody = (props) =>{
    const rows = props.characterData.map((row, index) => {
        return (
            <tr key = {index}>
                <td>{row.name}</td>
                <td>{row.job}</td>
            </tr>
        )
    })

    return <tbody>{rows}</tbody>
}

class Table extends Component {
    render() {
        // ES6 property shorthand
        const {characterData} = this.props

        return (
            <table>
                <TableHeader/>
                <TableBody characterData={characterData}/>
            </table>
        )
    }
}

export default Table
```

## State

You can think of state as any data that should be saved and modified without necessarily being added to a database.

### App.jsx

```jsx
import React, {Component} from 'react';
import Table from "./Table";

class App extends Component {
    state = {
        characters: [
            {
                name: "Charlie",
                job: "Janitor",
            },
            {
                name: "Mac",
                job: "Bounder",
            },
            {
                name: "Dee",
                job: "Aspring actress",
            },
            {
                name: "Dennis",
                job: "Bartender"
            }
        ],
    }

    removeCharacter = (index) => {
        const {characters} = this.state
        this.setState({
            characters: characters.filter((characters, i) => {
                return i !== index
            })
        })
    }

    render() {
        const {characters} = this.state
        return (
            <div className="App">
                <h1>Hello, React!</h1>
                <Table characterData={characters} removeCharacter={this.removeCharacter} />
            </div>
        );
    }
}

export default App;
```

### Table.jsx

```jsx
import React from "react";

const TableHeader = () => {
    return (
        <thead>
        <tr>
            <th>Name</th>
            <th>Job</th>
            <th>Remove</th>
        </tr>
        </thead>
    )
}

const TableBody = (props) => {
    const rows = props.characterData.map((row, index) => {
        return (
            <tr key={index}>
                <td>{row.name}</td>
                <td>{row.job}</td>
                <td>
                    <button onClick={() => props.removeCharacter(index)}>Delete</button>
                </td>
            </tr>
        )
    })

    return <tbody>{rows}</tbody>
}

const Table = (props) => {
    const {characterData, removeCharacter} = props

    return (
        <table>
            <TableHeader/>
            <TableBody characterData={characterData} removeCharacter={removeCharacter}/>
        </table>
    )
}

export default Table;
```

## Submitting Form Data

### App.jsx

```javascript
import React, {Component} from 'react';
import Table from "./Table";
import Form from "./Form"

class App extends Component {
    state = {
        characters: [],
    }

    removeCharacter = (index) => {
        const {characters} = this.state
        this.setState({
            characters: characters.filter((characters, i) => {
                return i !== index
            })
        })
    }
    handleSubmit = (character) => {
        this.setState({characters: [...this.state.characters, character]})
    }

    render() {
        const {characters} = this.state
        return (
            <div className="App">
                <h1>Hello, React!</h1>
                <Table characterData={characters} removeCharacter={this.removeCharacter} />
                <Form handleSubmit={this.handleSubmit}/>
            </div>
        );
    }
}

export default App;
```

### Form.jsx

```javascript
import React, {Component} from 'react';

class Form extends Component {
    initialState = {
        name: '',
        job: '',
    }

    handleChange = (event) => {
        const {name, value} = event.target

        this.setState({
            [name]: value,
        })
    }

    submitForm = () => {
        this.props.handleSubmit(this.state)
        this.setState(this.initialState)
    }

    state = this.initialState;
    render() {
        const {name, job} = this.state;

        return (
            <form>
                <lable htmlFor="name">Name</lable>
                <input
                    type={"text"}
                    name={"name"}
                    id={"name"}
                    value={name}
                    onChange={this.handleChange}/>
                <input
                    type={"text"}
                    name={"job"}
                    id={"job"}
                    value={job}
                    onChange={this.handleChange}
                    />
                <input type={"button"} value={"Submit"} onClick={this.submitForm}/>
            </form>
        );
    }
}

export default Form;
```

==This is too much for today, I will pause here==
