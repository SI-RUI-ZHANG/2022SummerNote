# Components

## Setting Up the Project

### import bootstrap

==terminal==

```bash
npm i bootstrap
```

==index.js==

```jsx
import 'bootstrap/dist/css/bootstrap.css';
```

## First React Component

### `components/counter.jsx`

```jsx
import React, {Component} from 'react';

class Counter extends Component {
    render() {
        return (
            <h1>Hello World</h1>
        );
    }
}

export default Counter;
```

### `index.js`

```jsx
import Counter from "./components/counter";

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
    <Counter/>
);
reportWebVitals();
```

## Specifying Children

To return multiple lines of JSX, we must wrap it into one `div` or use `<React.Fragment>`

### use `div`

```jsx
import React, {Component} from 'react';

class Counter extends Component {
    render() {
        return (
            <div>
                <h1>Hello World</h1>
                <button>Increment</button>
            </div>
        );
    }
}

export default Counter;
```

### use `React.Fragment`

```jsx
import React, {Component} from 'react';

class Counter extends Component {
    render() {
        return (
            <React.Fragment>
                <h1>Hello World</h1>
                <button>Increment</button>
            </React.Fragment>
        );
    }
}

export default Counter;
```

## Embedding Expressions

- `{}`: allows us to insert value dynamically in JSX expressions
- `state`: an instance of React Component Class that holds some information that may change over the lifetime of the component.

### counter.jsx

```jsx
import React, {Component} from 'react';

class Counter extends Component {
    // here we store data in state instance of Counter class
    state = {
        count: 0,
    };

    render() {
        return (
            <div>
            // we can write any javascript expression inside the {} 
                <span>{this.formatCount()}</span>
                <button>Increment</button>
            </div>
        );
    }

    formatCount() {
        // use javascript object deconstructing
        const {count} = this.state
        // JSX just behaves like any other basic components of javascript 
        return count === 0 ? <h1>Zero</h1> : <h1>{count}</h1>;
    }
}

export default Counter;
```

## Setting Attributes

we can set attribute of JSX element through `{}`

- `style={}`: when setting styles for JSX element, we must pass a javaScript object
  - inline style: `style={{color: "red"}}`

```jsx
import React, {Component} from 'react';

class Counter extends Component {
    state = {
        count: 0,
    };

    styles = {
        fontSize: '1em',
        fontWeight: 'bold'
    }

    render() {
        return (
            <div>
                <span style={this.styles} className={"badge badge-primary m-2"}>{this.formatCount()}</span>
                <span style={{fontSize: "2em", color: "red"}} className={"badge badge-primary m-2"}>{this.formatCount()}</span>
                <button className={"btn btn-secondary btn-sm"}>Increment</button>
            </div>
        );
    }

    formatCount() {
        const {count} = this.state
        return count === 0 ? "Zero" : {count};
    }
}

export default Counter;
```

## Rendering Classes Dynamically

Notice that we should keep the render method as clean as possible

```jsx
import React, {Component} from 'react';

class Counter extends Component {
    state = {
        count: 1,
    };

    render() {
        return (
            <div>
                <span className={this.getBadgeClasses()}>{this.formatCount()}</span>
                <button className={"btn btn-secondary btn-sm"}>Increment</button>
            </div>
        );
    }

    // extract getBadgeClasses from render method
    getBadgeClasses() {
        let classes = "badge m-2 badge-";
        classes += this.state.count === 0 ? "warning" : "primary";
        return classes;
    }

    ......
    ......

}

export default Counter;
```

## Rendering Lists

When rendering lists, we use `Array.prototype.map()` to generate a list of items
Notice that each list item must have a unique `key` value

```jsx
import React, {Component} from 'react';

class Counter extends Component {
    state = {
        count: 1,
        tags: ['tag1', 'tag2', 'tag3']
    };

    render() {
        return (
            <div>
                <span className={this.getBadgeClasses()}>{this.formatCount()}</span>
                <button className={"btn btn-secondary btn-sm"}>Increment</button>
                <ul> {this.state.tags.map(tag => <li key={tag}>{tag}</li>)} </ul>
            </div>
        );
    }

    ......
    ......

}

export default Counter;
```

## Conditional Rendering

### with helper function

```jsx
import React, {Component} from 'react';

class CounterTemp extends Component {
    state = {
        count: 1,
        tags: ['tag1', 'tag2', 'tag3']
    };

    renderTags() {
        if (this.state.tags.length === 0) return <p>There are no tags!</p>;
        return <ul> {this.state.tags.map(tag => <li key={tag}>{tag}</li>)} </ul>
    }

    render() {
        return (
            <div>
                {this.renderTags()}
            </div>
        );
    }
}

export default CounterTemp;
```

### use `&&` operator

In javascript, if we evaluates two truthy values with `&&`, the javascript engine will return the second value

```javascript
console.log( true && "Hello World" )
// Hello World
```

```jsx
import React, {Component} from 'react';

class CounterTemp extends Component {
    state = {
        count: 1,
        tags: ['tag1', 'tag2', 'tag3']
    };

    render() {
        return (
            <div>
                {this.state.tags.length === 0 && "please create a new tag"}
                {this.state.tags.map(tag => <li key={tag}>{tag}</li>)}
            </div>
        );
    }
}

export default CounterTemp;
```

## Handling Events

```jsx
    render() {
        return (
            <div>
                <span className={this.getBadgeClasses()}>{this.formatCount()}</span>
                <button onClick={this.handleIncrement} className={"btn btn-secondary btn-sm"}>Increment</button>
            </div>
        );
    }
```

## Binding Event Handlers

### use `bind`

add a constructor for our class and in that constructor, bind function's `this` to the class object

```jsx
import React, {Component} from 'react';

class Counter extends Component {

    ......
    ......

    constructor(props) {
        super(props);
        this.handleIncrement = this.handleIncrement.bind(this);
    }

    render() {
        return (
            <div>
                <span className={this.getBadgeClasses()}>{this.formatCount()}</span>
                <button onClick={this.handleIncrement} className={"btn btn-secondary btn-sm"}>Increment</button>
            </div>
        );
    }

    handleIncrement() {
        console.log("Increment Clicked", this);
    }

    ......
    ......
}

export default Counter;
```

### use arrow function

```jsx
import React, {Component} from 'react';

class Counter extends Component {

    ......
    ......

    render() {
        return (
            <div>
                <span className={this.getBadgeClasses()}>{this.formatCount()}</span>
                <button onClick={this.handleIncrement} className={"btn btn-secondary btn-sm"}>Increment</button>
            </div>
        );
    }

    handleIncrement = () => {
        console.log("Increment Clicked", this);
    }

    ......
    ......
}

export default Counter;
```

## Updating the State

in React, we use `setState()` to update value in `state`
we need to pass a javascript object to `setState()` method

```jsx
import React, {Component} from 'react';

class Counter extends Component {
    state = {
        count: 0,
    };

    render() {
        return (
            <div>
                <span className={this.getBadgeClasses()}>{this.formatCount()}</span>
                <button onClick={this.handleIncrement} className={"btn btn-secondary btn-sm"}>Increment</button>
            </div>
        );
    }

    handleIncrement = () => {
        console.log("Increment Clicked", this);
        this.setState({count: this.state.count + 1})
    }
    ......
    ......
}

export default Counter;
```

## Passing Event Arguments

when we need to pass event arguments, we can rewrite function reference in render into a inline arrow function

```jsx
import React, {Component} from 'react';

class Counter extends Component {
    ......
    ......
    render() {
        return (
            <div>
                <span className={this.getBadgeClasses()}>{this.formatCount()}</span>
                <button onClick={() => this.handleIncrement("product")} className={"btn btn-secondary btn-sm"}>Increment</button>
            </div>
        );
    }

    handleIncrement = product => {
        console.log(product)
        this.setState({count: this.state.count + 1})
    };
    ......
    ......
}

export default Counter;
```

