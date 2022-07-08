# React Basics

## `setState()`

- `setSate`: schedules an update to a component’s state object; when state changes, the component responds by re-rendering.

```jsx
setState({ stateName: updatedStateValue})
// Or
setState((prevState) => ({ 
   stateName: prevState.stateName + 1 
}))
```

## `setState()` and secondary callback

Consider the following code

```jsx
class App extends Component {

    constructor(props) {
        super(props);
        this.state = {
            name: "Sirui",
            school: "NYU"
        }
    }

    render() {
        return (
            <div className="App">
                <header className="App-header">
                    <img src={logo} className="App-logo" alt="logo" />
                    <p>Hi {this.state.name}, I study at {this.state.school}</p>
                    <button onClick={() => {
                        this.setState({name: "Zhang"});
                        console.log(this.state);
                    }}>Change name</button>
                </header>
            </div>
        );
    }
}
```

After click the `button`, however, the console output:

```jsx
{name: 'Sirui', school: 'NYU'}
```

The name shown in page get updated, but the state passed to console is not up to date.
That is because `setState()` is asynchronous call, by the time we log state the console, which is a synchronous call, the state might not be updated.

To avoid such problem, we can pass `setState()` a function and a call back.
`setState(()=>{}, ()=>{})`

The ==first== function return the object used to shaw merge with `this.state`.
In this way, we can also pass `state` and `props` to the function and based on that to update our `state`.

(optional) The ==second== function we pass to `setState()` is a call back function, which will run after the first function is finished.

Therefore, we can write our code in this way:

```jsx
<button onClick={() => {
    this.setState(()=>{
        return {name: "Zhang"};
    },
    ()=>{
        console.log(this.state);
    });
}}>Change name</button>
```

The console will output the desired value

```jsx
{name: 'Zhang', school: 'NYU'}
```

## Mapping Array to Elements

Before we start talking about arrays, we first take a look at the `App.js` file

```jsx
import './App.css';
import {Component} from "react";

class App extends Component {

    render() {
        return (
            <div className="App">

            </div>
        );
    }
}


export default App;
```

The `render()` method inside `App` class will usually contains all the components we used in this app, and it is considered one of the best practice to write React code.

### to map array to elements

```jsx
class App extends Component {

    constructor(props) {
        super(props);
        this.state = {
            monsters: [
                {name: 'Linda'},
                {name: 'Frank'},
                {name: 'Andrei'},
                {name: 'Jacky'},
            ],
        }
    }

    render() {
        return (
            <div className="App">
                {this.state.monsters.map(monster => {
                    return <h1 key={monster.name}>{monster.name}</h1>
                })}
            </div>
        );
    }
}

```

each element returned my `map` must have a unique `key` value: react use `key` to different different elements.

## Single Page Application

### React Lifecycle

[React lifecycle diagram](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)

Each component in React has a lifecycle which you can monitor and manipulate during its three main phases

- `Mounting`
- `Updating`
- `Unmounting`

#### `Mounting` Stage

Mounting means putting elements into DOM

When mounting a component, the following method is called in order:

- `constructor()`
- `getDerivedStateFromProps()`
- `render()`
- `componentDidMount()`

##### `constructor()`

Called before anything else, when the component is initiated, and it is the natural place to set up the initial `state` and other initial values.

The `constructor()` is called with `props`, as arguments, and you should always start by calling the `super(props)` before anything else, this will initiates the parent's constructor method and allows the component to inherit methods from its parent `React.Component`

##### `getDerivedStateFromProps`

Called right before rendering the element(s) in the DOM.

The natural place to set the `state` object based on the initial `props`.

It takes `state` as an argument, and returns an object with changes to `state`.

==example==

```jsx
lass Header extends React.Component {
  constructor(props) {
    super(props);
    this.state = {favoritecolor: "red"};
  }
  static getDerivedStateFromProps(props, state) {
    return {favoritecolor: props.favcol };
  }
  render() {
    return (
      <h1>My Favorite Color is {this.state.favoritecolor}</h1>
    );
  }
}
```

the initial `favoritecolor` is `red`, `getDerivedStateFromPros` change it to new `favcol` attribute

##### `render`

The required method to outputs the DOM to the HTML

##### `componentDidMount`

Called after the component is rendered.

This is where you run statements that requires that the component is already placed in the DOM.

#### Updating, Unmounting

...

### `componentDidMount()` in detail

The `componentDidMount()` method allows us to execute the React code when the component is already placed in the DOM. This method is called during the Mounting phase of the React Life-cycle i.e after the component is rendered.

All the AJAX requests and the DOM or state updation should be coded in the componentDidMount()

In practice, `componentDidMount` is the best place to put calls to fetch data, for two reasons:

1. Using `didMount` makes it clear that data won't be loaded until _after_ the initial render. This reminds you to set up initial `state` properly, so you don't end up with undefined state that causes errors.
2. If you ever need to render your app on the server, `componentDidMount` will ensure that data is only fetched from the client where it should be.

## Understanding Components

[React.Component](https://reactjs.org/docs/react-component.html)

## Understanding Props (properties)

[Components and Props](https://reactjs.org/docs/components-and-props.html)

To use props with class component

```jsx
import React, {Component} from 'react';

class CardList extends Component {

    render() {
        const {monsters} = this.props;
        return (
            <div>
                {monsters.map(monster =>
                    <div key={monster.name}><h1>{monster.name}</h1></div>
                )}
            </div>
        );
    }
}

export default CardList;
```

## Rendering and Re-rendering

[Re-rendering Components in ReactJs](https://www.geeksforgeeks.org/re-rendering-components-in-reactjs/)

Re-render can be caused due to any of the three reasons listed:

1. Update in state
2. Update in prop
3. Re-rendering of the parent component
