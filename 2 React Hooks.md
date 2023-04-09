# React Hooks

Hooks allow function components to have access to state and other React features. Because of this, class components are generally no longer needed.

## 1 Introduction

### 1. What is a Hook?

Hooks allow us to "hook" into React features such as state and lifecycle methods.

You must `import` Hooks from `react`.

State generally refers to application data or properties that need to be tracked.

#### Example

```js
import React, { useState } from "react"
import ReactDOM from "react-dom/client"

function FavoriteColor() {
  const [color, setColor] = useState("red")

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
  )
}

const root = ReactDOM.createRoot(document.getElementById('root'))
root.render(<FavoriteColor />)
```

### 2. Hook Rules
There are 3 rules for hooks:

- Hooks can only be called inside React function components.
- Hooks can only be called at the top level of a component.
- Hooks cannot be conditional.

## 2 The `useState` Hook

The React `useState` Hook allows us to track state in a function component.

State generally refers to data or properties that need to be tracking in an application.

### 1. Importing `useState`

To use `useState`, we first need to `import` it into our component.

```js
import { useState } from "react"
```

### 2. Initializing `useState`

We initialize our state by calling `useState` in our function component.

`useState` accepts an initial state and returns two values:

- The current state.
- A function that updates the state.

#### Syntax

```js
function FavoriteColor() {
  const [color, setColor] = useState("")
}
```

The first value, `color`, is our current state.

The second value, `setColor`, is the function that is used to update our state.

Lastly, we set the initial state to an empty string: `useState("")`.

### 3. Reading State

We can use the state variable in the rendered component.

```js
function FavoriteColor() {
  const [color, setColor] = useState("red")

  return <h1>My favorite color is {color}!</h1>
}
```

### 4. Updating State

To update our state, we use our state update function.

```js
function FavoriteColor() {
  const [color, setColor] = useState("red")

  return (
    <>
      <h1>My favorite color is {color}!</h1>
      <button
        type="button" onClick={() => setColor("blue")}>Blue</button>
    </>
  )
}
```

### 5. What Can State Hold
`useState` can be used to keep track of strings, numbers, booleans, arrays, objects, and any combination of these!

We could create multiple state Hooks to track individual values:

```js
function Car() {
  const [brand, setBrand] = useState("Ford")
  const [model, setModel] = useState("Mustang")
  const [year, setYear] = useState("1964")
  const [color, setColor] = useState("red")

  return (
    <>
      <h1>My {brand}</h1>
      <p>
        It is a {color} {model} from {year}.
      </p>
    </>
  )
}
```

Or, we can just use one state and include an object instead!

```js
function Car() {
  const [car, setCar] = useState({
    brand: "Ford",
    model: "Mustang",
    year: "1964",
    color: "red"
  })

  return (
    <>
      <h1>My {car.brand}</h1>
      <p>
        It is a {car.color} {car.model} from {car.year}.
      </p>
    </>
  )
}
``` 

### 6. Updating Objects and Arrays in State

When state is updated, the entire state gets overwritten.

What if we only want to update the color of our car?

If we only called `setCar({color: "blue"})`, this would remove the `brand`, `model`, and `year` from our state.

We can use the JavaScript spread operator to help us:

```js
  const updateColor = () => {
    setCar(previousState => {
      return { ...previousState, color: "blue" }
    })
  }
```

#### Example

```js
import React, { useState } from "react"
import ReactDOM from "react-dom/client"

function Car() {
  const [car, setCar] = useState({
    brand: "Ford",
    model: "Mustang",
    year: "1964",
    color: "red"
  })

  const updateColor = () => {
    setCar(previousState => {
      return { ...previousState, color: "blue" }
    })
  }

  return (
    <>
      <h1>My {car.brand}</h1>
      <p>
        It is a {car.color} {car.model} from {car.year}.
      </p>
      <button type="button" onClick={updateColor}>Blue</button>
    </>
  )
}

const root = ReactDOM.createRoot(document.getElementById('root'))
root.render(<Car />)
```

## 2.5 Forms

Just like in HTML, React uses forms to allow users to interact with the web page.

### 1. Adding Forms

You add a form with React like any other element.

#### Example

Add a form that allows users to enter their name:

```js
function MyForm() {
  return (
    <form>
      <label>Enter your name:
        <input type="text" />
      </label>
    </form>
  )
}
```

This will work as normal, the form will submit and the page will refresh.

But this is generally not what we want to happen in React.

We want to prevent this default behavior and let React control the form.

### 2. Handling Forms

Handling forms is about how you handle the data when it changes value or gets submitted.

| In HTML| In React
|---|---|
Form data is usually handled by the DOM.| Form data is usually handled by the components.

When the data is handled by the components, all the data is stored in the component state.

You can control changes by adding event handlers in the `onChange` attribute.

We can use `useState` to keep track of each inputs value and provide a "single source of truth" for the entire application.

#### Example

Use `useState` to manage the input when users enter their name:

```js
function MyForm() {
  const [name, setName] = useState("")

  return (
    <form>
      <label>Enter your name:
        <input type="text" value={name}
          onChange={(event) => setName(event.target.value)}
        />
      </label>
    </form>
  )
}
```

### 3. Submitting Forms

You can control the submit action by adding an event handler in the `onSubmit` attribute and a submit button:

```js
function MyForm() {
  const [name, setName] = useState("")

  const handleSubmit = (event) => {
    event.preventDefault()
    alert(`Your name is ${name}`)
  }

  return (
    <form onSubmit={handleSubmit}>
      <label>Enter your name:
        <input type="text" value={name}
          onChange={(event) => setName(event.target.value)}
        />
      </label>
      <input type="submit" />
    </form>
  )
}
```

### 4. Multiple Input Fields

You can control the values of more than one input field by adding a `name` attribute to each element.

We will initialize our state with an empty object.

To access the fields in the event handler use the `event.target.name` and `event.target.value` syntax.

To update the state, use square brackets [bracket notation] around the property name.

#### Example

Write a form with two input fields, `name` and `age`: 

```js
import React, { useState } from 'react'
import ReactDOM from 'react-dom/client'

function MyForm() {
  const [inputs, setInputs] = useState({})

  const handleChange = (event) => {
    setInputs(values => ({...values, [event.target.name]: event.target.value}))
  }

  const handleSubmit = (event) => {
    event.preventDefault()
    alert(inputs)
  }

  return (
    <form onSubmit={handleSubmit}>
      <label>Enter your name:
      <input type="text" name="name" value={inputs.name || ""} 
        onChange={handleChange}
      />
      </label>
      <label>Enter your age:
        <input 
          type="number" 
          name="age" 
          value={inputs.age || ""} 
          onChange={handleChange}
        />
        </label>
        <input type="submit" />
    </form>
  )
}

const root = ReactDOM.createRoot(document.getElementById('root'))
root.render(<MyForm />)
```

### 5. Textarea

The textarea element in React is slightly different from ordinary HTML.

In HTML the value of a textarea was the text between the start tag `<textarea>` and the end tag `</textarea>`.

```html
<textarea>
  Content of the textarea.
</textarea>
```

In React the value of a textarea is placed in a `value` attribute. We'll use `useState` to mange the value of the textarea:

```js
import React, { useState } from 'react'
import ReactDOM from 'react-dom/client'

function MyForm() {
  const [textarea, setTextarea] = useState(
    "The content of a textarea goes in the value attribute."
  )

  const handleChange = (event) => {
    setTextarea(event.target.value)
  }

  return (
    <form>
      <textarea value={textarea} onChange={handleChange} />
    </form>
  )
}

const root = ReactDOM.createRoot(document.getElementById('root'))
root.render(<MyForm />)
```

### 6. Select

A drop down list, or a select box, in React is also a bit different from HTML.

In HTML, the selected value in the drop down list was defined with the `selected` attribute:

#### Example

The default selection is "Volvo":

```html
<select>
  <option value="Ford">Ford</option>
  <option value="Volvo" selected>Volvo</option>
  <option value="Fiat">Fiat</option>
</select>
```

In React, the selected value is defined with a `value` attribute on the `select` tag:

#### Example

The selected value "Volvo" is initialized in `useState`:

```js
function MyForm() {
  const [myCar, setMyCar] = useState("Volvo")

  const handleChange = (event) => {
    setMyCar(event.target.value)
  }

  return (
    <form>
      <select value={myCar} onChange={handleChange}>
        <option value="Ford">Ford</option>
        <option value="Volvo">Volvo</option>
        <option value="Fiat">Fiat</option>
      </select>
    </form>
  )
}
```

By making these slight changes to `<textarea>` and `<select>`, React is able to handle all input elements in the same way.

## 3 The `useEffect` Hooks

The `useEffect` Hook allows you to perform side effects in your components, for instance: fetching data, directly updating the DOM, and timers.

### 1. Syntax

`useEffect` accepts two arguments: 
- A render function that gets executed on every render.
- Dependencies, which are all variables that will get the function executed when any one of them changes.

Let's explain using a timer as an example.

```js
import React, { useState, useEffect } from "react"
import ReactDOM from "react-dom/client"

function Timer() {
  const [count, setCount] = useState(0)

  useEffect(() => {
    setTimeout(() => { setCount((count) => count + 1) }, 1000)
  })

  return <h1>I've rendered {count} {(count === 0 || count === 1) ? "time" : "times"}!</h1>
}

const root = ReactDOM.createRoot(document.getElementById('root'))
root.render(<Timer />)
```

Here we use `setTimeout()` to count 1 second after the initial render.

But wait! It keeps counting even though it should only count once!

That's because `useEffect` runs on every render. That means that every second, when `count` changes, a render happens and triggers the function again.

To prevent this from happening, we can pass an empty array as the second argument.

#### Example

No dependencies is passed:

```js
 useEffect(() => {
  // Runs on every render
})
```

An empty array is passed:

```js
useEffect(() => {
  // Runs only on the first render
}, [])
```

You can pass props or state values as dependencies:

```js
useEffect(() => {
  // Runs on the first render
  // And any time any dependency value changes
}, [prop, state])
```

So, to fix this issue, let's only run this effect on the initial render.

```js
  useEffect(() => {
    setTimeout(() => { setCount((count) => count + 1) }, 1000)
  }, []) // <- add empty brackets as a dependency
```

### 2. Effect Cleanup
Some effects require cleanup to reduce memory leaks.

Timeouts, subscriptions, event listeners, and other effects that are no longer needed should be disposed.

We do this by including a return function at the end of `useEffect`.

#### Example

Clean up the `timer` function at the end of `useEffect`:

>In order to clean up the function you have to name it.

```js
import React, { useState, useEffect } from "react"
import ReactDOM from 'react-dom/client'

function Timer() {
  const [count, setCount] = useState(0)

  useEffect(() => {
    let timer = setTimeout(() => { setCount((count) => count + 1) }, 1000)
    return () => clearTimeout(timer)
  }, [])

  return <h1>I've rendered {count} {(count === 0 || count === 1) ? "time" : "times"}!</h1>
}

const root = ReactDOM.createRoot(document.getElementById('root'))
root.render(<Timer />)
```

## 4 The `useContext` Hook

### 1. React Context

React Context is a way to manage state globally.

It can be used together with `useState` to share state between deeply nested components more easily than using `useState` alone.

### 2. The Problem

State should be held by the highest parent component in the stack that requires access to the state.

To illustrate, we have many nested components. Only the component at the top and bottom of the stack need access to the state.

To do this without Context, we will need to pass the state as "props" through each nested component. This is called "prop drilling".


```js
import React, { useState } from "react"
import ReactDOM from "react-dom/client"

function Component1() {
  const [user, setUser] = useState("Jac Cris")

  return (
    <>
      <h1>Hello {user}</h1>
      <Component2 user={user} />
    </>
  )
}

function Component2({ user }) {
  return (
    <>
      <h1>Component 2</h1>
      <Component3 user={user} />
    </>
  )
}

function Component3({ user }) {
  return (
    <>
      <h1>Component 3</h1>
      <Component4 user={user} />
    </>
  )
}

function Component4({ user }) {
  return (
    <>
      <h1>Component 4</h1>
      <Component5 user={user} />
    </>
  )
}

function Component5({ user }) {
  return (
    <>
      <h1>Component 5</h1>
      <h2>Hello {user} again!</h2>
    </>
  )
}

const root = ReactDOM.createRoot(document.getElementById('root'))
root.render(<Component1 />)
```

Even though component 2-4 did not need the `user` state, they had to pass the state along so that it could reach component 5.

The solution is to create context.

### 3. Creating Context

To create context, you must import `createContext` and initialize it:

```js
import React, { useState, createContext } from "react"
import ReactDOM from "react-dom/client"

const UserContext = createContext()
```

Next we'll use the Context Provider to wrap the tree of components that need the state Context.

### 4. Context Provider

Wrap child components in the Context Provider and supply the state value.

```js
function Component1() {
  const [user, setUser] = useState("Jac Cris")

  return (
    <UserContext.Provider value={user}>
      <h1>Hello {user}!</h1>
      <Component2 user={user} />
    </UserContext.Provider>
  )
}
```

Now, all components in this tree will have access to the user Context.

### 5. Using `useContext`

In order to use the Context in a child component, we need to access it using the `useContext` Hook.

First, include `useContext` in the import statement:

```js
import React, { useState, createContext, useContext } from "react"
```

Then you can access the `user` Context in all components:

```js
function Component5() {
  const userAgain = useContext(UserContext)
  return (
    <>
      <h1>Component 5</h1>
      <h2>Hello {userAgain} again!</h2>
    </>
  )
}
```

#### Example 

```js
import React, { useState, createContext, useContext } from "react"
import ReactDOM from "react-dom/client"

const UserContext = createContext()

function Component1() {
  const [user, setUser] = useState("Jac Cris")

  return (
    <UserContext.Provider value={user}>
      <h1>Hello {user}!</h1>
      <Component2 />
    </UserContext.Provider>
  )
}

function Component2() {
  return (
    <>
      <h1>Component 2</h1>
      <Component3 />
    </>
  )
}

function Component3() {
  return (
    <>
      <h1>Component 3</h1>
      <Component4 />
    </>
  )
}

function Component4() {
  return (
    <>
      <h1>Component 4</h1>
      <Component5 />
    </>
  )
}

function Component5() {
  const userAgain = useContext(UserContext)
  return (
    <>
      <h1>Component 5</h1>
      <h2>Hello {userAgain} again!</h2>
    </>
  )
}

const root = ReactDOM.createRoot(document.getElementById('root'))
root.render(<Component1 />)
```

## 5 The `useRef` Hook

The `useRef` Hook can be used to:

- Store a mutable value that does not cause re-renders when updated.
- Access a DOM element directly.
- Persist values between renders.

### 1. Does Not Cause Re-renders

We can use a `useRef` Hook to count how many times our application renders:

```js
import React, { useState, useEffect, useRef } from "react"
import ReactDOM from "react-dom/client"

function App() {
  const [inputValue, setInputValue] = useState("")
  const count = useRef(0)

  useEffect(() => { ++count.current })

  return (
    <>
      <input type="text" value={inputValue}
        onChange={(event) => setInputValue(event.target.value)}/>
      <h1>Render Count: {count.current}</h1>
    </>
  )
}

const root = ReactDOM.createRoot(document.getElementById('root'))
root.render(<App />)
```

`useRef()` returns an Object called `current`.

When we initialize `useRef` we set the initial value for `current`: `useRef(0)`.

>It's like doing this: `const count = {current: 0}`. We can access the count by using `count.current`.

#### Example

Same example from before, without using `useRef`. Here we replace the `count` `useRef` Hook with the `count` `useState` Hook:

```js
import React, { useState } from "react"
import ReactDOM from "react-dom/client"

function App() {
  const [inputValue, setInputValue] = useState("")
  const [count, setCount] = useState(0)

  return (
    <>
      <input type="text" value={inputValue}
        onChange={(event) => {
          setCount((count) => ++count)
          return setInputValue(event.target.value)
        }}
      />
      <h1>Render Count: {count}</h1>
    </>
  )
}

const root = ReactDOM.createRoot(document.getElementById("root"))
root.render(<App />)
```

### 2. Accessing DOM Elements

In general, we want to let React handles all DOM manipulation.

But there are some instances where `useRef` can be used without causing issues.

We can add a `ref` attribute to an element to access it directly in the DOM.

```js
import React, { useRef } from "react"
import ReactDOM from "react-dom/client"

function App() {
  const inputElement = useRef()

  const focusOnInput = () => {
    inputElement.current.focus()
  }

  return (
    <>
      <input type="text" ref={inputElement} />
      <button onClick={focusOnInput}>Focus on Input</button>
    </>
  )
}

const root = ReactDOM.createRoot(document.getElementById('root'))
root.render(<App />)
```

### 3. Tracking State Changes

`useRef` can also be used to keep track of previous state values.

This is because we are able to persist `useRef` values between renders.

```js
import React, { useState, useEffect, useRef } from "react"
import ReactDOM from "react-dom/client"

function App() {
  const [inputValue, setInputValue] = useState("")
  const previousInputValue = useRef("")

  // previousInputValue.current is updated each time the inputValue is updated
  useEffect(() => { previousInputValue.current = inputValue }, [inputValue])

  return (
    <>
      <input type="text" value={inputValue}
        {/* The inputValue is updated when we enter text into the input field */}
        onChange={(event) => setInputValue(event.target.value)}
      />
      <h2>Current Value: {inputValue}</h2>
      <h2>Previous Value: {previousInputValue.current}</h2>
    </>
  )
}

const root = ReactDOM.createRoot(document.getElementById('root'))
root.render(<App />)
```

## 6 The `useReducer` Hook

The `useReducer` Hook is similar to the `useState` Hook.

It allows for custom state logic.

If you find yourself keeping track of multiple pieces of state that rely on complex logic, `useReducer` may be useful.

### 1. Syntax

`useReducer` accepts two arguments:

- A reducer function to contain your custom state logic.
- An initial state, generally an object.

`useReducer` returns the current `state` and a `dispatch` method.

#### Example

The example below creates the logic to keep track of the todo app `finished` status.

All of the logic to add, delete, and snooze a todo could be contained within a single `useReducer` Hook by adding more actions.

```js
import React, { useReducer } from "react"
import ReactDOM from "react-dom/client"

const initialTodos = [
  {
    id: 1,
    title: "Buy milk",
    finished: false,
  },
  {
    id: 2,
    title: "Create a responsive web",
    finished: false,
  },
  {
    id: 3,
    title: "Learn React",
    finished: false,
	}
]

const finishedLogic = (state, checkedTodo) => {
  return state.map((todo) => {
    if (todo.id === checkedTodo.id) {
      return {...todo, finished: !todo.finished}
    }
    return todo
  })
}

function Todos() {
  const [todos, dispatch] = useReducer(finishedLogic, initialTodos)

  return (
    <>
      {todos.map((todo) => (
        <div key={todo.id}>
          <label>
            {/* There is a checked attribute here */}
            <input type="checkbox" checked={todo.finished}
              onChange={() => dispatch(todo)}
            />
            {todo.title}
          </label>
        </div>
      ))}
    </>
  )
}

const root = ReactDOM.createRoot(document.getElementById('root'))
root.render(<Todos />)
```

Below is the same example, without using `useReducer`. Notice that the biggest difference is the `checked` attribute.

I don't even know any example for the main usage of `useReducer` at this point. W3Schools refuse to elaborate further. 

¯\\\_(ツ)_/¯ Enjoy!

```js
import React from "react"
import ReactDOM from "react-dom/client"

const initialTodos = [
  {
    id: 1,
    title: "Buy milk",
    finished: false,
  },
  {
    id: 2,
    title: "Create a responsive web",
    finished: false,
  },
  {
    id: 3,
    title: "Learn React",
    finished: false,
  }
]

const finishedLogic = (todo) => {
  todo.finished = !todo.finished
}

function Todos() {
  return (
    <>
      {initialTodos.map((todo) => (
        <div key={todo.id}>
          <label>
            {/* There is no checked attribute here */}
            <input type="checkbox" 
              onChange={() => finishedLogic(todo)}
            />
            {todo.title}
          </label>
        </div>
      ))}
    </>
  )
}

const root = ReactDOM.createRoot(document.getElementById('root'))
root.render(<Todos />)
```

## 6.5 `memo`

Using `memo` will cause React to skip rendering a component if its props have not changed.

This can improve performance.

### 1. Problem

In this example, the `Todos` component re-renders even when the todos have not changed.

```js
// Todos.js

const Todos = ({ todos }) => {
  console.log("child render")
  return (
    <>
      <h2>My Todos</h2>
      {todos.map((todo, index) => {
        return <p key={index}>{todo}</p>
      })}
    </>
  )
}

export default Todos
```

```js
// index.js

import React, { useState } from "react"
import ReactDOM from "react-dom/client"
import Todos from "./Todos"

const App = () => {
  const [count, setCount] = useState(0)
  const [todos, setTodos] = useState(["Todo 1", "Todo 2"])

  const increment = () => {
    setCount((count) => ++count)
  }

  return (
    <>
      <Todos todos={todos} />
      <hr />
      <div>
        Count: {count}
        {/* Will console.log when the increment button is clicked, 
        which is undesired */}
        <button onClick={increment}>+</button>
      </div>
    </>
  )
}

const root = ReactDOM.createRoot(document.getElementById('root'))
root.render(<App />)
```

When you click the increment button, the `Todos` component also re-renders.

If this component was complex, it could cause performance issues.

### 2. Solution

To fix this, we can use `memo`.

Use `memo` to keep the `Todos` component from needlessly re-rendering.

```js
// Todos.js

import { memo } from "react"

const Todos = ({ todos }) => {
  console.log("child render")
  return (
    <>
      <h2>My Todos</h2>
      {todos.map((todo, index) => {
        return <p key={index}>{todo}</p>
      })}
    </>
  )
}

export default memo(Todos)
```

Now the `Todos` component only re-renders when the `todos` that are passed to it through props are updated.

## 7 The `useCallback` Hook

>**Tl;dr:** `memo` only works if your components do not use a `useState` Hook. Include `useCallback` when your components use a `useState` Hook.
>`useCallback` = `memo` + `useState`

The `useCallback` Hook returns a *memoized* callback function.

>Think of memoization as caching a value so that it does not need to be recalculated.

This can improve performance by isolating resource intensive functions so that they will not automatically run on every render.

The `useCallback` Hook only runs when one of its dependencies update.

### 1. Problem

One reason to use `useCallback` is to prevent a component from re-rendering unless its props have changed.

In this example, you might think that the `Todos` component will not re-render unless the `todos` change, since it uses `memo`:

```js
// Todos.js

import { memo } from "react"

const Todos = ({ todos, addTodo }) => {
  console.log("child render")
  return (
    <>
      <h2>My Todos</h2>
      {todos.map((todo, index) => {
        return <p key={index}>{todo}</p>
      })}
      <button onClick={addTodo}>Add Todo</button>
    </>
  )
}

export default memo(Todos)
```

```js
// index.js

import React, { useState } from "react"
import ReactDOM from "react-dom/client"
import Todos from "./Todos"

const App = () => {
  const [count, setCount] = useState(0)
  const [todos, setTodos] = useState([])

  const increment = () => {
    setCount((count) => ++count)
  }
  // No useCallback
  const addTodo = () => {
    setTodos((todos) => [...todos, "New Todo"])
  }

  return (
    <>
      {/* Should only console.log when the addTodo button is clicked */}
      <Todos todos={todos} addTodo={addTodo} />
      <hr />
      <div>
        Count: {count}
        {/* But also console.log when the increment button is clicked */}
        <button onClick={increment}>+</button>
      </div>
    </>
  )
}

const root = ReactDOM.createRoot(document.getElementById('root'))
root.render(<App />)
```

Try running this and click the count increment button.

You will notice that the `Todos` component re-renders even when the `todos` do not change.

Why does this not work? We are using `memo`, so the `Todos` component should not re-render since neither the `todos` state nor the `addTodo` function changes when the count is incremented.

This is because of something called "referential equality". It means that, every time a component re-renders, its functions get recreated. Because of this, the `addTodo` function has actually changed.

### 2. Solution

To fix this, we can use the `useCallback` hook to prevent the function from being recreated unless necessary.

The `useCallback` Hook accepts a second parameter to declare dependencies. The `addTodo` function will only run when its dependencies have changed.

```js
const App = () => {
  const [count, setCount] = useState(0)
  const [todos, setTodos] = useState([])

  const increment = () => {
    setCount((count) => ++count)
  }
  // Yes useCallback
  const addTodo = useCallback(() => {
    setTodos((todos) => [...todos, "New Todo"])
  }, [todos])

  return (
    <>
      {/* Now only console.log when the addTodo button is clicked */}
      <Todos todos={todos} addTodo={addTodo} />
      <hr />
      <div>
        Count: {count}
        {/* No longer console.log when the increment button is clicked */}
        <button onClick={increment}>+</button>
      </div>
    </>
  )
}
```

Now the `Todos` component will only re-render when the `todos` prop changes.

## 8 The `useMemo` Hook

>**Tl;dr:** `memo` only works if your components do not use a `useState` Hook. Include `useMemo` when your components use a `useState` Hook.
>`useMemo` = `memo` + `useState`

The `useMemo` Hook returns a memoized value.

The `useMemo` Hook only runs when one of its dependencies update,  and this can improve performance.

>The main difference between `useMemo` and `useCallback` is that `useMemo` returns a memoized **value** and `useCallback` returns a memoized **function**.

### 1. Problem

The `useMemo` Hook can be used to keep expensive, resource intensive functions from needlessly running.

In this example, we have a poor performing function that runs on every render.

When changing the `count` or adding a `todo`, you will notice a delay in execution.

```js
import React, { useState } from "react"
import ReactDOM from "react-dom/client"

const expensiveCalculation = (num) => {
  console.log("Calculating...")
  for (let i = 0 i < 10000 i++) {
    ++num
  }
  return num
}

const App = () => {
  const [count, setCount] = useState(0)
  const [todos, setTodos] = useState([])
  // No useMemo
  const calculation = expensiveCalculation(count)

  const increment = () => {
    setCount((count) => ++count)
  }
  const addTodo = () => {
    setTodos((todos) => [...todos, "New Todo"])
  }

  return (
    <div>
      <div>
        <h2>My Todos</h2>
        {todos.map((todo, index) => {
          return <p key={index}>{todo}</p>
        })}
        {/* Also console.log when the addTodo button is clicked */}
        <button onClick={addTodo}>Add Todo</button>
      </div>
      <hr />
      <div>
        Count: {count}
        {/* Should only console.log when the increment button is clicked */}
        <button onClick={increment}>+</button>
        <h2>Expensive Calculation</h2>
        {calculation}
      </div>
    </div>
  )
}

const root = ReactDOM.createRoot(document.getElementById('root'))
root.render(<App />)
```

### 2. Solution

To fix this performance issue, we can use `useMemo` to memoize the `expensiveCalculation` function. This will cause the function to only run when needed.

The `useMemo` Hook accepts a second parameter to declare dependencies. The `calculation` function will only run when its dependencies have changed.

```js
const App = () => {
  const [count, setCount] = useState(0)
  const [todos, setTodos] = useState([])
  // Yes useMemo
  const calculation = useMemo(() => expensiveCalculation(count), [count])

  const increment = () => {
    setCount((count) => ++count)
  }
  const addTodo = () => {
    setTodos((todos) => [...todos, "New Todo"])
  }

  return (
    <div>
      <div>
        <h2>My Todos</h2>
        {todos.map((todo, index) => {
          return <p key={index}>{todo}</p>
        })}
        {/* No longer console.log when the addTodo button is clicked */}
        <button onClick={addTodo}>Add Todo</button>
      </div>
      <hr />
      <div>
        Count: {count}
        {/* Now only console.log when the increment button is clicked */}
        <button onClick={increment}>+</button>
        <h2>Expensive Calculation</h2>
        {calculation}
      </div>
    </div>
  )
}
``` 

## 9 Custom Hooks

Hooks are reusable functions.

When you have component logic that needs to be used by multiple components, we can extract that logic to a custom Hook.

Custom Hooks start with "use", for example: `useFetch`.

### 1. Build a Hook

In the following code, we are fetching data in our `Home` component and displaying it.

We will use the [JSONPlaceholder](https://jsonplaceholder.typicode.com) service to fetch fake data. This service is great for testing applications when there is no existing data.

#### Example

Use the JSONPlaceholder service to fetch fake "todo" items and display the titles on the page:

```js
// index.js

import React, { useState, useEffect } from "react"
import ReactDOM from "react-dom/client"

const Home = () => {
  const [data, setData] = useState(null)

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/todos")
      .then((res) => res.json())
      .then((data) => setData(data))
 }, [])

  return (
    <>
      {data &&
        data.map((item) => {
          return <p key={item.id}>{item.title}</p>
        })}
    </>
  )
}

const root = ReactDOM.createRoot(document.getElementById('root'))
root.render(<Home />)
```

The fetch logic may be needed in other components as well, so we will extract that into a custom Hook.

#### Example

Move the fetch logic to a new file to be used as a custom Hook:

```js
// useFetch.js

import { useState, useEffect } from "react"

const useFetch = (url) => {
  const [data, setData] = useState(null)

  useEffect(() => {
    fetch(url)
      .then((res) => res.json())
      .then((data) => setData(data))
  }, [url])

  return [data]
}

export default useFetch
```

```js
// index.js

import React from "react"
import ReactDOM from "react-dom/client"
import useFetch from "./useFetch"

const Home = () => {
  const [data] = useFetch("https://jsonplaceholder.typicode.com/todos")

  return (
    <>
      {data &&
        data.map((item) => {
          return <p key={item.id}>{item.title}</p>
        })}
    </>
  )
}

const root = ReactDOM.createRoot(document.getElementById('root'))
root.render(<Home />)
```

We have created a new file called `useFetch.js` containing a function called `useFetch` which contains all of the logic needed to fetch our data.

We removed the hard-coded URL and replaced it with a `url` variable that can be passed to the custom Hook.

Lastly, we return our data from our Hook.

In `index.js`, we import our `useFetch` Hook and use it like any other Hook. This is where we pass in the URL to fetch data from.

Now we can reuse this custom Hook in any component to fetch data from any URL.
