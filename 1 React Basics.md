# React Basics

React creates a VIRTUAL DOM in memory, and only changes what needs to be changed.
 
## 1 Getting Started

### 1. Prerequisites

In order to use React in production, you need `npm` and Node.js installed.

- Step 1: Go to [Node.js](https://nodejs.org) and install the latest version.
- Step 2: Open the terminal and type `npm -v` and `node -v` to check the version.

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

```js
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

```js
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

```js
import React from 'react';
import ReactDOM from 'react-dom/client';

const myFirstElement = <h1>Hello World!</h1>

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(myFirstElement);
```

## 2 Render HTML

React uses the `ReactDOM.render()` function to render HTML.

The `ReactDOM.render()` function takes two arguments, HTML code and an HTML element, to display the specified HTML code inside the specified HTML element.

```js
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

```js
const myElement = <h1>I Love JSX!</h1>;

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(myElement);
```

Same code without JSX:

```js
const myElement = React.createElement('h1', {}, 'I do not use JSX!');

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(myElement);
```

### 2. Expressions in JSX

With JSX you can write expressions inside curly braces { }:

```js
const myElement = <h1>React is {5 + 5} times better with JSX</h1>;
```

### 3. Inserting a Large Block of HTML

To write HTML on multiple lines, put the HTML inside parentheses:

```js
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

```js
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

```js
// Close empty elements with />
const myElement = <input type="text" />;
```

>JSX will throw an error if the HTML is not properly closed.

### 6. Attribute `class` = `className`

The `class` attribute is a much used attribute in HTML, but since JSX is rendered as JavaScript, and the `class` keyword is a reserved word in JavaScript, you are not allowed to use it in JSX.

Use attribute `className` instead. When JSX is rendered, it translates `className` attributes into `class` attributes.

```js
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

```js
class Car extends React.Component {
  render() {
    return <h2>Hi, I am a Car!</h2>;
  }
}
```

Create a Function component:

```js
function Car() {
  return <h2>Hi, I am a Car!</h2>;
}
```

### 2. Rendering a Component

Now your React application has a component called Car, which returns an `<h2>` element.

To use this component in your application, use similar syntax as normal HTML: `<Car />`

```js
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Car />);
```

### 3. Components in Components
We can refer to components inside other components:

```js
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

```js
function Car() {
  return <h2>Hi, I am a Car!</h2>;
}

export default Car;
```

To be able to use the Car component, you have to `import` the file in your application.

```js
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

```js
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

```js
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

```js
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

```js
<button onClick={shoot}>Take a Shot!</button>
```

HTML:

```js
<button onclick="shoot()">Take a Shot!</button>
```

### 2. Passing Arguments

To pass an argument to an event handler, use an arrow function.

```js
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

```js
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

```js
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

```js
function Goal(props) {
  const isGoal = props.isGoal;
  if (isGoal) {
    return <MadeGoal/>;
  }
  return <MissedGoal/>;
}

const root = ReactDOM.createRoot(document.getElementById('root'));
// Will render "Missed!"
root.render(<Goal isGoal={false} />);
```

#### Ternary Operator
Another way to conditionally render elements is by using a ternary operator.

```js
function Goal(props) {
  const isGoal = props.isGoal;
  return (
    <>
      { isGoal ? <MadeGoal/> : <MissedGoal/> }
    </>
  );
  
const root = ReactDOM.createRoot(document.getElementById('root'));
// Will render "GOAL!!!"
root.render(<Goal isGoal={true} />);
```

#### Logical `&&` Operator

Another way to conditionally render a React component is by using the `&&` operator.

```js
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

```js
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

```js
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

>Note: forms will be introduced after React Hooks.

## 8 Router

`create-react-app` doesn't include page routing.

React Router is the most popular solution.

### 1. Add React Router 

To add the latest version of React Router in your application, run this in the terminal from the root directory of the application: `npm i -D react-router-dom@latest`.

### 2. Folder Structure

To create an application with multiple page routes, let's first start with the file structure.

Within the `src` folder, we'll create a folder named `pages` with several files:

`src\pages\`:

- `Layout.js`
- `Home.js`
- `Blogs.js`
- `Contact.js`
- `NoPage.js`

Each file will contain a very basic React component.

### 3. Usage

Now we will use React Router to route to pages based on URL:

```js
// index.js

import ReactDOM from "react-dom/client";
import { BrowserRouter, Routes, Route } from "react-router-dom";
import Layout from "./pages/Layout";
import Home from "./pages/Home";
import Blogs from "./pages/Blogs";
import Contact from "./pages/Contact";
import NoPage from "./pages/NoPage";

export default function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Layout />}>
          <Route index element={<Home />} />
          <Route path="blogs" element={<Blogs />} />
          <Route path="contact" element={<Contact />} />
          <Route path="*" element={<NoPage />} />
        </Route>
      </Routes>
    </BrowserRouter>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);
```

#### Explained

We wrap our content first with `<BrowserRouter>`.

Then we define our `<Routes>`. An application can have multiple `<Routes>`. Our basic example only uses one.

In `<Routes>` there are many `<Route>`s. `<Route>`s can be nested.

The first `<Route>` has a path of `/` and renders the `Layout` component.

The nested `<Route>`s inherit and add to the parent route. So the blogs path is combined with the parent and becomes `/blogs`.

The `Home` component route does not have a path but has an `index` attribute. That specifies this route as the default route for the parent route, which is `/`.

Setting the `path` to `*` will act as a catch-all for any undefined URLs. This is great for a 404 error page.

### 4. Pages / Components

```js
// Layout.js

// The "layout route" is a shared component
// that will be rendered on all pages.

// The Layout component takes in <Outlet> and <Link> elements.
import { Outlet, Link } from "react-router-dom";

const Layout = () => {
  return (
    <>
      <nav>
        <ul>
          <li>
            // <Link> is used to set the URL.
            // Anytime we link to an internal path, 
            // we will use <Link> instead of <a href="">.
            <Link to="/">Home</Link>
          </li>
          <li>
            <Link to="/blogs">Blogs</Link>
          </li>
          <li>
            <Link to="/contact">Contact</Link>
          </li>
        </ul>
      </nav>

      // <Outlet> renders the current route selected.
      <Outlet />
    </>
  )
};

export default Layout;
```

```js
// Home.js

const Home = () => {
  return <h1>Home</h1>;
};

export default Home;
```

```js
// Blogs.js

const Blogs = () => {
  return <h1>Blog Articles</h1>;
};

export default Blogs;
```

```js
// Contact.js

const Contact = () => {
  return <h1>Contact Me</h1>;
};

export default Contact;
```

```js
// NoPage.js

const NoPage = () => {
  return <h1>Error 404: PAGE NOT FOUND</h1>;
};

export default NoPage;
```

## 8.5 Memo

>Note: memo will be introduced after React Hooks.

## 9 CSS Styling

There are many ways to style React with CSS, here we wukk look at three common ways:

- Inline styling
- CSS stylesheets
- CSS Modules

### 1. Inline Styling

To style an element with the inline style attribute, the value must be a JavaScript object:


```js
const Header = () => {
  return (
    <>
      <h1 style={{color: "red"}}>Hello Style!</h1>
      <p>Add a little style!</p>
    </>
  );
}
```

>In JSX, JavaScript expressions are written inside curly braces, and since JavaScript objects also use curly braces, the styling in the example above is written inside two sets of curly braces `{{}}`.

You can also create an object with styling information, and refer to it in the style attribute:

```js
const Header = () => {
  const myStyle = {
    color: "white",
    backgroundColor: "DodgerBlue",
    padding: "10px",
    fontFamily: "Sans-Serif"
  };
  return (
    <>
      <h1 style={myStyle}>Hello Style!</h1>
      <p>Add a little style!</p>
    </>
  );
}
```

#### camelCased Property Names

Since the inline CSS is written in a JavaScript object, properties with hyphen separators, like `background-color`, must be written with camel case syntax:

```html
// Use backgroundColor instead of background-color
<h1 style={{backgroundColor: "lightblue"}}>Hello Style!</h1>
```

### 2. CSS Stylesheet

You can write your CSS styling in a separate file, just save the file with the `.css` file extension, and import it in your application.

```css
/* style.css */

body {
  background-color: #282c34;
  color: white;
  padding: 40px;
  font-family: Sans-Serif;
  text-align: center;
}
```

Import the stylesheet in your application:

```js
import React from 'react';
import ReactDOM from 'react-dom/client';
import './style.css';

const Header = () => {
  return (
    <>
      <h1>Hello Style!</h1>
      <p>Add a little style!.</p>
    </>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Header />);
```

### 3. Modules

Another way of adding styles to your application is to use CSS Modules.

CSS Modules are convenient for components that are placed in separate files.

Create the CSS module with the `.module.css` extension, example: `my-style.module.css`.

```css
/* my-style.module.css */

.bigblue {
  color: DodgerBlue;
  padding: 40px;
  font-family: Sans-Serif;
  text-align: center;
}
```

Import the stylesheet in your component:

```js
// Car.js

import styles from './my-style.module.css'; 

const Car = () => {
  return <h1 className={styles.bigblue}>Hello Car!</h1>;
}

export default Car;
```

Import the component in your application:

```js
// index.js

import ReactDOM from 'react-dom/client';
import Car from './Car.js';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Car />);
```

## 10 Sass Styling

### 1. What is Sass?

Sass is a CSS pre-processor.

Sass files are executed on the server and sends CSS to the browser.

### 2. Install Sass

If you use the create-react-app in your project, you can easily install Sass by running this command in your terminal: `npm i sass`.

### 3. Create a Sass file

Create a Sass file the same way as you create CSS files, but Sass files have the file extension `.scss`

In Sass files you can use variables and other Sass functions:

```scss
// my-sass.scss 

$myColor: red;

h1 {
  color: $myColor;
}
```

Import the Sass file the same way as you imported a CSS file:

```jss
import React from 'react';
import ReactDOM from 'react-dom/client';
import './my-sass.scss';

const Header = () => {
  return (
    <>
      <h1>Hello Style!</h1>
      <p>Add a little style!.</p>
    </>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Header />);
```
