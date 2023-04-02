# React Hooks

Hooks allow function components to have access to state and other React features. Because of this, class components are generally no longer needed.

## 1 Introduction

### 1. What is a Hook?

Hooks allow us to "hook" into React features such as state and lifecycle methods.

You must `import` Hooks from `react`.

State generally refers to application data or properties that need to be tracked.

#### Example

```j
import React, { useState } from "react";
import ReactDOM from "react-dom/client";

function FavoriteColor() {
  const [color, setColor] = useState("red");

  return (
    <>
      <h1>My favorite color is {color}!</h1>
      <button
        type="button"
        onClick={() => setColor("blue")}
      >Blue</button>
      <button
        type="button"
        onClick={() => setColor("red")}
      >Red</button>
      <button
        type="button"
        onClick={() => setColor("pink")}
      >Pink</button>
      <button
        type="button"
        onClick={() => setColor("green")}
      >Green</button>
    </>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<FavoriteColor />);
```

### 2. Hook Rules
There are 3 rules for hooks:

- Hooks can only be called inside React function components.
- Hooks can only be called at the top level of a component.
- Hooks cannot be conditional.

## 2 The `useState` Hook

The React `useState` Hook allows us to track state in a function component.

State generally refers to data or properties that need to be tracking in an application.

### 1. Import `useState`

To use the `useState` Hook, we first need to `import` it into our component.

```j
import { useState } from "react";
```

### 2. Initialize `useState`

We initialize our state by calling `useState` in our function component.

`useState` accepts an initial state and returns two values:

- The current state.
- A function that updates the state.

```js
import { useState } from "react";

function FavoriteColor() {
  const [color, setColor] = useState("");
}
```

##### Explained

The first value, `color`, is our current state.

The second value, `setColor`, is the function that is used to update our state.

Lastly, we set the initial state to an empty string: `useState("")`.

### 3. Read State

We can use the state variable in the rendered component.

```j
import { useState } from "react";
import ReactDOM from "react-dom/client";

function FavoriteColor() {
  const [color, setColor] = useState("red");

  return <h1>My favorite color is {color}!</h1>
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<FavoriteColor />);
```

```j

```

```j

```

```j

``` 


```j

```
