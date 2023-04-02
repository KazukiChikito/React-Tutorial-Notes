# React Basics

React creates a VIRTUAL DOM in memory, and only changes what needs to be changed.
 
## 1 Getting Started

### 1. Prerequisites

In order to use React in production, you need `npm` and Node.js installed.

- Step 1: Go to [Node.js](https://nodejs.org) and install the latest version.
- Step 2: Open the Command Prompt and type `npm -v` and `node -v` to check the version.

A few checking beforehand: 

- Step 3: Type `npm uninstall -g create-react-app` and uninstall any older version of `create-react-app`.
- Step 4: Type `npm install tar@latest -g` to install the latest version of `tar` globally.
- Step 5: Finally, type `npm install -g npx` to install `npx`.

### 2. Setting up a React Environment

If you have `npx` and Node.js installed, you can create a React application by using `create-react-app`.

Run this command to create a React application named `my-react-app`: `npx create-react-app my-react-app`.

### 3. Run the React Application

Now you are ready to run your first real React application!

Run this command to move to the `my-react-app` directory: `cd my-react-app`.

Run this command to run the React application `my-react-app`: `npm start`.

A new browser window will pop up with your newly created React App! If not, open your browser and type `localhost:3000` in the address bar.

The result will look like this:

![my-react-app](https://www.w3schools.com/react/screenshot_myfirstreact.png)

### 4. Modify the React Application

So far so good, but how do I change the content?

Look in the `my-react-app` directory, and you will find a `src` folder. Inside the `src` folder there is a file called `App.js`, open it and it will look like this:

```j
import logo from './logo.svg';
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}

export default App;
```

Try changing the HTML content and save the file.

#### Example

```j
function App() {
  return (
    <div className="App">
      <p>It's time</p>
      <h1>Hello World!</h1>
    </div>
  );
}

export default App;
```

### 5. What's Next?

Now you have a React Environment on your computer, and you are ready to learn more about React.

If you want to follow the same steps on your computer, start by stripping down the `src` folder to only contain one file: `index.js`. You should also remove any unnecessary code inside the `index.js` file to keep things simple.

```j
import React from 'react';
import ReactDOM from 'react-dom/client';

const myFirstElement = <h1>Hello World!</h1>

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(myFirstElement);
```

## 2 Render HTML

React uses the `ReactDOM.render()` function to render HTML.

The `ReactDOM.render()` function takes two arguments, HTML code and an HTML element, to display the specified HTML code inside the specified HTML element.

```j
ReactDOM.render(<p>Hello World!</p>, document.getElementById('root'));
```

```html
<body>
  <div id="root"></div>
</body>
```

## 3 JSX

JSX stands for JavaScript XML.

JSX allows us to write HTML in React.

### 1. Why use JSX?

JSX allows us to write HTML elements in JavaScript and place them in the DOM without any `createElement()`  and/or `appendChild()` methods.

#### Example

Using JSX:

```j
const myElement = <h1>I Love JSX!</h1>;

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(myElement);
```

Same code without JSX:

```j
const myElement = React.createElement('h1', {}, 'I do not use JSX!');

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(myElement);
```

### 2. Expressions in JSX

With JSX you can write expressions inside curly braces { }:

```j
const myElement = <h1>React is {5 + 5} times better with JSX</h1>;
```

### 3. Inserting a Large Block of HTML

To write HTML on multiple lines, put the HTML inside parentheses:

```j
const myElement = (
  <ul>
    <li>Apples</li>
    <li>Bananas</li>
    <li>Cherries</li>
  </ul>
);
```

### 4. One Top Level Element

The HTML code must be wrapped in one top level element.

So if you like to write two paragraphs, you must put them inside a parent element, like a `div` element.

Alternatively, you can use a "fragment" to wrap multiple lines. This will prevent unnecessarily adding extra nodes to the DOM.

A fragment looks like an empty HTML tag: `<></>`.

```j
const myElement = (
  <>
    <p>I am a paragraph.</p>
    <p>I am a paragraph too.</p>
  </>
);
```

>JSX will throw an error if the HTML is not correct, or if the HTML misses a parent element.

### 5. Elements Must be Closed

JSX follows XML rules, and therefore HTML elements must be properly closed.

```j
// Close empty elements with />
const myElement = <input type="text" />;
```

>JSX will throw an error if the HTML is not properly closed.

### 6. Attribute `class` = `className`

The `class` attribute is a much used attribute in HTML, but since JSX is rendered as JavaScript, and the `class` keyword is a reserved word in JavaScript, you are not allowed to use it in JSX.

Use attribute `className` instead. When JSX is rendered, it translates `className` attributes into `class` attributes.

```j
const myElement = <h1 className="myclass">Hello World</h1>;
```

## 4 Components

Components are like functions that return HTML elements.

Components come in two types:
- Class components.
- Function components.

### 1. Creating a Component

#### Class Component

A class component must include the `extends React.Component` statement and a `render()` method.

#### Function Component

Function components can be written using much less code and are easier to understand than Class components.

#### Example

Create a Class component:

```j
class Car extends React.Component {
  render() {
    return <h2>Hi, I am a Car!</h2>;
  }
}
```

Create a Function component:

```j
function Car() {
  return <h2>Hi, I am a Car!</h2>;
}
```

### 2. Rendering a Component

Now your React application has a component called Car, which returns an `<h2>` element.

To use this component in your application, use similar syntax as normal HTML: `<Car />`

```j
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Car />);
```

### 3. Components in Components
We can refer to components inside other components:

```j
function Car() {
  return <h2>I am a Car!</h2>;
}

function Garage() {
  return (
    <>
      <h1>Who lives in my Garage?</h1>
      // Here the Car component is used inside the Garage component
      <Car />
    </>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Garage />);
```

### 4. Components in Files

React is all about re-using code, and it is recommended to split your components into separate files.

To do that, create a new file with a `.js` file extension and put the code inside it.

The filename must start with an uppercase character.

This is a new file, named "Car.js":

```j
function Car() {
  return <h2>Hi, I am a Car!</h2>;
}

export default Car;
```

To be able to use the Car component, you have to `import` the file in your application.

```j
import React from 'react';
import ReactDOM from 'react-dom/client';
import Car from './Car.js';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Car />);
```

## 5 Props

Props are arguments passed into React components.

Props are passed to components via HTML attributes.

`props` stands for properties.

>React Props are read-only! You will get an error if you try to change their value.

### 1. Usage

Props are how you pass data from one component to another, as parameters:

```j
function Car(props) {
  return <h2>I am a { props.brand }!</h2>;
}

function Garage() {
  return (
    <>
      <h1>Who lives in my garage?</h1>
      <Car brand="Ford" />
    </>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Garage />);
```

If you have a variable to send, and not a string as in the example above, you just put the variable name inside curly brackets:

```j
function Car(props) {
  return <h2>I am a { props.brand }!</h2>;
}

function Garage() {
  const carName = "Ford";
  return (
    <>
      <h1>Who lives in my garage?</h1>
      <Car brand={ carName } />
    </>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Garage />);
```

Or if it was an object:

```j
function Car(props) {
  return <h2>I am a { props.brand.model }!</h2>;
}

function Garage() {
  const carInfo = { name: "Ford", model: "Mustang" };
  return (
    <>
      <h1>Who lives in my garage?</h1>
      <Car brand={ carInfo } />
    </>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Garage />);
```

## 6 Events

Just like HTML DOM events, React can perform actions based on user events.

React has the same events as HTML: click, change, mouseover, etc.

### 1. Adding Events

React events are written in camelCase syntax: `onClick` instead of `onclick`.

React event handlers are written inside curly braces: `onClick={shoot}`  instead of `onClick="shoot()"`.

React: 

```j
<button onClick={shoot}>Take a Shot!</button>
```

HTML:

```j
<button onclick="shoot()">Take a Shot!</button>
```

### 2. Passing Arguments

To pass an argument to an event handler, use an arrow function.

```j
function Football() {
  const shoot = (shot) => {
    alert(shot);
  }

  return (
    <button onClick={() => shoot("Nice Shot!")}>Take a shot!</button>
  );
}
```

### 3. The Event Object

Event handlers have access to the React event that triggered the function.

In our example the event is the "click" event.

```j
function Football() {
  const shoot = (shot, event) => {
    alert(event.type);
    alert(shot);
  }

  return (
    <button onClick={(event) => shoot("Nice Shot!", event)}>Take a shot!</button>
  );
}
```

### 4. Conditionals

React supports `if` statements, but not inside JSX.

If you want to use conditionals in JSX, instead use ternary operators or logical `&&` operators.

#### Example

```j
// We'll use these two components:
function MissedGoal() {
  return <h1>Missed!</h1>;
}
function MadeGoal() {
  return <h1>GOAL!!!</h1>;
}
```

#### `if` Statement

We can use the `if` JavaScript operator to decide which component to render.

```j
function Goal(props) {
  const isGoal = props.isGoal;
  if (isGoal) {
    return <MadeGoal/>;
  }
  return <MissedGoal/>;
}

const root = ReactDOM.createRoot(document.getElementById('root'));
// Will render "Missed"
root.render(<Goal isGoal={false} />);
```

#### Ternary Operator
Another way to conditionally render elements is by using a ternary operator.

```j
function Goal(props) {
  const isGoal = props.isGoal;
  return (
    <>
      { isGoal ? <MadeGoal/> : <MissedGoal/> }
    </>
  );
```

#### Logical `&&` Operator

Another way to conditionally render a React component is by using the `&&` operator.

```j
function Garage(props) {
  const cars = props.cars;
  return (
    <>
      <h1>Garage</h1>
      // If cars.length > 0 is equates to true, 
      // the expression after && will render.
      {cars.length > 0 &&
        <h2>
          You have {cars.length} cars in your garage.
        </h2>
      }
    </>
  );
}

const cars = ['Ford', 'BMW', 'Audi'];
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Garage cars={cars} />);
```

## 7 Lists

### 1. `map()`

In React, you will render lists with some type of loop. The `map()` array method is generally the preferred method.

Let's render all of the cars from our garage:

```j
function Car(props) {
  return <li>I am a { props.brand }</li>;
}

function Garage() {
  const cars = ['Ford', 'BMW', 'Audi'];
  return (
    <>
      <h1>Who lives in my garage?</h1>
      <ul>
        {cars.map((car) => <Car brand={car} />)}
      </ul>
    </>
  );
}
```

When you run this code in your `create-react-app`, it will work but you will receive a warning that there is no "key" provided for the list items.

### 2. Keys

Keys allow React to keep track of elements. This way, if an item is updated or removed, only that item will be re-rendered instead of the entire list.

Keys need to be unique to each sibling. But they can be duplicated globally.

>Generally, the key should be a unique ID assigned to each item. As a last resort, you can use the array index as a key.

Let's refactor our previous example to include keys:

```j
function Car(props) {
  return <li>I am a { props.brand }</li>;
}

function Garage() {
  const cars = [
    {id: 1, brand: 'Ford'},
    {id: 2, brand: 'BMW'},
    {id: 3, brand: 'Audi'}
  ];
  return (
    <>
      <h1>Who lives in my garage?</h1>
      <ul>
        {cars.map((car) => <Car key={car.id} brand={car.brand} />)}
      </ul>
    </>
  );
}
```

## 7.5 Forms

Note: forms will be introduced after React Hooks.

## 8 Router

`create-react-app` doesn't include page routing.

React Router is the most popular solution.





```j

```

```j

```

```j

```

```j

```



## 9



```j

```