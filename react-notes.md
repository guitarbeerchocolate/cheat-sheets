# React.js Cheat Sheet

This cheat sheet covers important concepts, components, hooks, lifecycle methods, and best practices in React.js.

---

## Table of Contents

- [Installation and Setup](#installation-and-setup)
- [JSX](#jsx)
- [Components](#components)
  - [Functional Components](#functional-components)
  - [Class Components](#class-components)
- [Props](#props)
- [State](#state)
- [Events](#events)
- [Hooks](#hooks)
  - [useState](#usestate)
  - [useEffect](#useeffect)
  - [useContext](#usecontext)
  - [useRef](#useref)
  - [useReducer](#usereducer)
- [Lifecycle Methods (Class Components)](#lifecycle-methods-class-components)
- [Conditional Rendering](#conditional-rendering)
- [Lists and Keys](#lists-and-keys)
- [Forms](#forms)
- [Routing (React Router)](#routing-react-router)
- [Best Practices](#best-practices)

---

## Installation and Setup

To create a new React app, use `create-react-app`:

```bash
npx create-react-app my-app
cd my-app
npm start
```

---

## JSX

- JSX allows you to write HTML inside JavaScript.
- JSX must have one root element, and you can wrap elements in `<>...</>` (React Fragments).

Example:

```jsx
function App() {
  return (
    <>
      <h1>Hello, World!</h1>
      <p>Welcome to React</p>
    </>
  );
}
```

---

## Components

React apps are built using components. There are two types of components:

### Functional Components

Functional components are stateless functions that return JSX.

```jsx
function Greeting() {
  return <h1>Hello, World!</h1>;
}
```

### Class Components

Class components can hold and manage their own state.

```jsx
class Greeting extends React.Component {
  render() {
    return <h1>Hello, World!</h1>;
  }
}
```

---

## Props

- **Props** (short for properties) are used to pass data from a parent component to a child component.

Example:

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}!</h1>;
}

function App() {
  return <Welcome name="Alice" />;
}
```

---

## State

- State is an object that holds data that can change over time.
- You can manage state in functional components using the `useState` hook or within class components using `this.state`.

Example using `useState`:

```jsx
function Counter() {
  const [count, setCount] = React.useState(0);

  return (
    <>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </>
  );
}
```

---

## Events

React handles events similarly to HTML, but with camelCase naming conventions (e.g., `onClick`, `onChange`).

Example:

```jsx
function Button() {
  const handleClick = () => {
    alert("Button clicked!");
  };

  return <button onClick={handleClick}>Click Me</button>;
}
```

---

## Hooks

Hooks are functions that allow you to use state and other React features in functional components.

### `useState`

The `useState` hook is used to manage state in functional components.

```jsx
const [state, setState] = useState(initialState);
```

### `useEffect`

The `useEffect` hook runs side effects (e.g., data fetching, subscriptions) after the component renders.

```jsx
useEffect(() => {
  console.log("Component mounted or updated");

  return () => {
    console.log("Cleanup when the component unmounts");
  };
}, [dependencyArray]); // Optional dependencies to trigger the effect
```

### `useContext`

The `useContext` hook allows you to access context values in a functional component.

```jsx
const theme = useContext(ThemeContext);
```

### `useRef`

The `useRef` hook provides a way to persist values across renders without causing re-renders, or to access DOM elements directly.

```jsx
const inputRef = useRef(null);

useEffect(() => {
  inputRef.current.focus(); // Focus on the input field after render
}, []);
```

### `useReducer`

The `useReducer` hook is an alternative to `useState` for managing more complex state logic.

```jsx
const [state, dispatch] = useReducer(reducer, initialState);
```

---

## Lifecycle Methods (Class Components)

Lifecycle methods are only available in class components and help manage the component lifecycle.

- `componentDidMount`: Invoked after the component is added to the DOM.
- `componentDidUpdate`: Invoked after a state or prop change.
- `componentWillUnmount`: Invoked before the component is removed from the DOM.

Example:

```jsx
class MyComponent extends React.Component {
  componentDidMount() {
    console.log("Component mounted");
  }

  componentDidUpdate(prevProps, prevState) {
    console.log("Component updated");
  }

  componentWillUnmount() {
    console.log("Component will unmount");
  }

  render() {
    return <div>Hello, World!</div>;
  }
}
```

---

## Conditional Rendering

Conditional rendering allows you to display different UI elements based on certain conditions.

Example:

```jsx
function UserGreeting(props) {
  if (props.isLoggedIn) {
    return <h1>Welcome back!</h1>;
  }
  return <h1>Please sign in.</h1>;
}
```

---

## Lists and Keys

Rendering lists in React is done using the `map()` function, and keys are used to identify elements.

Example:

```jsx
const numbers = [1, 2, 3, 4, 5];

function NumberList() {
  return (
    <ul>
      {numbers.map((number) => (
        <li key={number.toString()}>{number}</li>
      ))}
    </ul>
  );
}
```

---

## Forms

Handling forms in React involves managing the state of form inputs.

Example:

```jsx
function Form() {
  const [value, setValue] = React.useState("");

  const handleSubmit = (e) => {
    e.preventDefault();
    alert(`Form submitted with: ${value}`);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        value={value}
        onChange={(e) => setValue(e.target.value)}
      />
      <button type="submit">Submit</button>
    </form>
  );
}
```

---

## Routing (React Router)

To implement routing in React, you can use **React Router**.

Installation:

```bash
npm install react-router-dom
```

Example:

```jsx
import { BrowserRouter as Router, Route, Switch, Link } from "react-router-dom";

function App() {
  return (
    <Router>
      <nav>
        <Link to="/">Home</Link>
        <Link to="/about">About</Link>
      </nav>

      <Switch>
        <Route path="/" exact component={Home} />
        <Route path="/about" component={About} />
      </Switch>
    </Router>
  );
}

function Home() {
  return <h1>Home</h1>;
}

function About() {
  return <h1>About</h1>;
}
```

---

## Best Practices

1. **Keep Components Small**: Break components down into small, reusable pieces.
2. **Use Functional Components**: Prefer functional components with hooks over class components.
3. **State Management**: Use state wisely, and consider using tools like `useReducer` or context for managing complex state.
4. **Keys in Lists**: Always provide unique keys when rendering lists.
5. **Use Prop Types or TypeScript**: Ensure props are typed correctly using PropTypes or TypeScript for better development experience.
6. **Optimize Performance**: Use `React.memo` to prevent unnecessary re-renders, and use the `useCallback` and `useMemo` hooks where appropriate.

---

This cheat sheet provides a quick reference to React.js concepts, hooks, and best practices. It can help you get started or serve as a refresher when working on React projects.