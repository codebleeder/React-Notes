# React Notes
* creates an HTML element
```javascript
const element = document.createElemen(tagName)
```
* sets the background-color to blue:
```javascript
element.style = "background-color: blue"
``` 
* sets the class of the element to: container
```javascript  
element.className = "container" 
```
* multiple classes can be set by separating them with a space character: 
```javascript
element.className = "container center"
```

* A React Element is the smallest building block.
* It's a representation of a small piece of your UI.
* React.createElement returns a React Element
```javascript
React.createElement(type, options, children)
React.createElement("h1", {className: "center", style: "color: red"}, 'heading');
```
* Install ReactDOM with: 
```
npm install react-dom
```
* Import ReactDOM's render method with 
```
import {render} from "react-dom"
```
* ReactDOM weighs 119KB when imported.
* The root element is where ReactDOM will render your UI
* The signature of render is: 
```
render(element, root)
```

```javascript
import {render} from "react-dom";

const root = document.querySelector("#root");
render(React.createElement("p", {}, "Hello World"), root);
```
## Root Element
* The root element is completely managed by ReactDOM
* You should not change/update the content of the root element
* Apps built with React have a single root element (Most common use case)
* Existing Apps that integrate React to make a feature interactive, could have more than 1 root.

## JSX
* JSX is a special syntax for React that makes it easier to represent your UI
* JSX looks similar to HTML but it is not HTML
* JSX code you write gets transformed into React.createElement
* JSX is not part of your browser. You need a tool to transform it to valid JavaScript.
* JSX requires React to be in scope.
```javascript
import React from "react";
import {render} from "react-dom";

const root = document.querySelector("#react-root");
render(<h1>Hello World</h1>, root);
```
## Adding Attributes to JSX
* Attributes in JSX get passed as the 2nd argument of React.createElement(...)
* <div className="active"></div> is how you would give the class active to this element.
* You need quotes around attribute values that are strings.
```javascript
const title = <h1 id="brand-title" className="primary-color">Supermarket</h1>;
```
## Working with JSX
* A JSX element is an object
* you can treat a JSX element like an object
* you can assign a JSX element to a variable
* you can return a JSX element from a function
```javascript
const title = <h1 className="title">Supermarket</h1>;

function getTitle(is_open) {
    if (is_open) {
        return <h1 className="title">Supermarket</h1>
    } else {
        return <h1 className="title">Supermarket (closed)</h1> 
    }
}
```
## JSX Expressions
example:
```javascript
const title = <h1>You have {2 + 3} notifications</h1>;

const user = {
    id: 1,
    name: "Sam"
};

const element = <p className="user-info">Welcome {user.name}!</p>
```
function calls:
```javascript
function capitalise(word) {
    return word[0].toUpperCase() + word.substring(1).toLowerCase();
}
const name = "brendan";

const element = <p className="user-info">Welcome {capitalise(name)}</p>
```
* An expression is any valid JavaScript code that resolves to a value
* Expressions in JSX need to be wrapped inside curly braces: {expression}
* \<h1 className="title">You have {2 + 3} notifications</h1> is an example of JSX with an expression.
## Attribute expressions
example:
```javascript
const count = 5;

const element = <input tabIndex={count} />;
```
Number and boolean attribute values should be passed as an expression:
```javascript
<input tabIndex={2} disabled={true} className="textbox" />
```
* If the value of the attribute is a string, then wrap it with quotes
* If the value of the attribute is an expression, then wrap it with curly braces {}
* Number and boolean attribute values should be passed as an expression
## JSX Children
Always wrap your JSX elements with () when written after a return. So the code becomes:
```javascript
const getList = () => {
    return (
        <ul>
            <li>First Item</li>
            <li>Second Item</li>
        </ul>
    );
}
```
## Self-closing tags
* Use self-closing syntax for self-closing elements in JSX
```javascript
const image = <img src="image.png" />
```
## JSX Fragments
* You can only return 1 element in JSX
* Wrap multiple elements with React.Fragment
* The short syntax is <> that can be closed with </>
* The original syntax is: <React.Fragment> and </React.Fragment>
So if you want to return the below HTML from a function:
```html
<h1>Grocery delivered to your door</h1>
<h2>Free delivery</h2>
<p>Get started now!</p>
```
You will have to use a Fragment that wraps these 3 elements:
```javascript
function getHeroBanner() {
    return (
        <>
            <h1>Grocery delivered to your door</h1>
            <h2>Free delivery</h2>
            <p>Get started now!</p>
        </>
    );
}
```
## Intro to Components
* A React Component is a function that returns one React  Element describing a section of the UI.
* Components defined with a function are called function components.
* React Components promote code reuse and are easier to debug.
* A React Component's name has to start with an uppercase.
* Use UpperCamelCase when naming React Components
## Components under the hood
* The first part of a JSX tag determines the type of the React element.
* Capitalized types indicate that the JSX tag is referring to a React component.
* A React Component is a function that returns a React Element.

## One Component per file
Footer.js:
```javascript
//Footer.js
import React from "react";

export default function Footer() {
    return (
        <>
             <h3>Footer</h3>
             <p>All rights reserved</p>
        </>
    );
}
```
index.js:
```javascript
//index.js
import React from "react";
import {render} from "react-dom";
import Footer from "./Footer.js";

function App() {
    return (<>
         <Footer />
         <Footer />
    </>);
}

const root = document.querySelector("#root");

render(<App />, root);
```
* Define one component per file for easier maintenance.
* Make the name of the file match the name of the Component.
* To be able to use a Component that you defined, you need to export it.
* To be able to use a Component defined in another file, you need to import it
## Props
```html
<GreetUser user="Sam" id="2" />
```
```javascript
import React from "react";

export default function GreetUser(props){
    return <div>Welcome {props.user}</div>;
}
```
* Props is short for properties
* Props is an object received as the first argument of a Component
* Attributes on Components get converted into an object called Props
* Props make components more reusable
## Children props
```javascript
import React from "react";

function Navbar(props){
    return <div className="navbar">{props.children}</div>;
}

const element = <Navbar>
    <HeroTitle>Welcome!</HeroTitle>
    <div>Some content</div>
    <p>Another content</p>
</Navbar>;
```
## Destructuring
* destructuring in ES6:
```javascript
const person = {
    first_name: "Jennifer",
    last_name: "Doe",
    age: 24,
};

const {first_name, last_name} = person;
```
### destructuring props in react:
* before destructuring:
```javascript
import React from "react";

function WelcomeUser(props) {
    const username = props.username;
    const notifications = props.notifications;

    return <div>Welcome {username}! You've got {notifications} unread notifications.</div>;
}
```
* After destructuring:
```javascript
import React from "react";

function WelcomeUser(props) {
    const {username, notifications} = props;

    return <div>Welcome {username}! You've got {notifications} unread notifications.</div>;
}
```
* Destructuring in the argument:
```javascript
import React from "react";

function WelcomeUser({username, notifications}) {
    return <div>Welcome {username}! You've got {notifications} unread notifications.</div>;
}
```
* example 2:
```javascript
import React from "react";
import {render} from "react-dom";

function Button(props){
    const {className, children} = props;
    return <button className={className}>{children}</button>;
}

const root = document.querySelector("#react-root");

render(<Button className="primary">Login</Button>, root);
```