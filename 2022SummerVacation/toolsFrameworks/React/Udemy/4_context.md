# Context

[official documentation](https://reactjs.org/docs/context.html)

> context provides a way to pass data through the component tree without having to pass props down manually at every level

## When to use context

> Context is designed to share data that can be considered "global" for a tree of React
> components

## API

### `React.createContext`

```jsx
const MyContext = React.createContext(defaultValue);
```

Creates a `Context` object.
When React renders a component that subscribes to this Context object it will read the current context value from the closest matching `Provider` above it in the tree.

The `defaultValue` argument is **only** used when a component does not have a matching `Provider` above it in the tree.

### `Context.Provider`

```jsx
<MyContext.Provider value={/* some value */}>
```

Every `Context` object comes with a `Provider` React component that allows consuming components to subscribe to context changes.

- `Provider` accepts a `value` prop to be passed to consuming components that are descendants of this `Provider`
- One `Provider` can be connected to many consumers
- `Provider` can be nested to override values deeper within the tree
- consumers that are descendants of a Provider will re-render whenever the Provider's `value` prop changes
- changes are determined by comparing the new and old values

### `useContext`

```jsx
const value = useContext(MyContext);
```

Accepts a context object (the value returned from `React.createContext`) and returns the current context value for that context.
The current context value is determined by the `value` prop of the nearest `<MyContext.Provider>` above the calling component in the tree.

When the nearest `<MyContext.Provider>` above the component updates, this Hook will trigger a rerender with the latest context `value` passed to that `MyContext` provider.

**NOTICE**: A component calling `useContext` will always re-render when the context value changes.

Example:

```jsx
const themes = {
    light: {
        foreground: "#000000",
        background: "#eeeeee"
    },
    dark: {
        foreground: "#ffffff",
        background: "#222222"
    }
};

const ThemeContext = React.createContext(themes.light);

function App() {
    return (
        <ThemeContext.Provider value={themes.dark}>
            <Toolbar/>
        </ThemeContext.Provider>
    );
}

function Toolbar(props) {
    return (
        <div>
            <ThemedButton />
        </div>
    )
}

function ThemedButton() {
    const theme = useContext(ThemeContext);
    return (
        <button style={{background: theme.background, color: theme.foreground}}>
            I am styled by theme context!
        </button>
    )
}
```
