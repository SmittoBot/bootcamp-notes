## Modern React/Redux
### React Intro
* React is a JS library to produce browser content and handle user interactions
* React can work by itself, but can also integrate with many other libraries and packages
* Javascript classes are part of ES 2015
* React components are made of either JS functions or classes
* JSX: looks like HTML and can be placed in JS code, determines the content of a React app
* Can use components to create event handlers, used to detect user interaction and respond to it
* React library knows what a component is and how to make components work together
* ReactDOM knows how to take a component and make it show up in the DOM

### Setup
* Install Node: nodejs.org/en/download, choose the respective installer
* Check that node was successfully installed with `node -v`, may need to restart terminal
* Install create-react-app:
```
npm install -g create-react-app
```
* Node package manager, install a package onto our computer, install globally to run from the terminal, package name
```
create-react-app jsx
```
* create-react-app installed 1700 packages! Why?
* Inside react project are a ton of dependencies, including Babel
* ES5 and ES2015 are references to a version of JS. There are different versions of ES spec every year after 2015 with new features
* Little issue: JS we write has to be executed on the user's browser, certain browsers aren't completely up to date
* ES2016-19 aren't always supported by browsers, users can't always run our code
* Babel: command-line tool that can take any version of JS and spit out a newer version
  * We can write ES2016 code, feed it into Babel, and Babel can spit out ES5 code that can be executed on any browser
  * Babel included any time we generate a react project

### Create-React-App
* src: folder where we put all the source code we write
* public: folder that stores static files, like images
* node_modules: folder that contains all of our project dependencies
* package.json: records our project dependencies and configures our project
* package-lock.json: records the exact version of packages that we install
* Start in terminal with `npm start`, stop with `Control+C`, once started can visit at `localhost:3000`
* Importing a dependency: `import React from 'react'`
* When we use an import statement, it uses a module system called ES2015 Modules, if we use the CommonJS modules, we make use of the require statement such as `const React = require('react')`
* A component is a function or class that produces HTML to show the user, and handle feedback from the user
* ES2015 arrow function: `function() {` can also be `() => {`
* By convention, we take our component and render it inside of the div with id root in the `index.html` file

### Building Content with JSX
* No browser natively understands what JSX is, it first gets converted into equivalent JS code
* Babel homepage: babeljs.io, can look at code converted into ES5 JS, converts returns to `React.createElement` for each element
* When returning JSX with a react component, can't just place opening tag on the next line, must wrap in parentheses:
```
return (
  <div>
  </div>
);
```
* JSX vs HTML
  * Adding custom styling to an element differs: 
    * HTML: `<div style="background-color: red':></div>`
    * JSX: `<div style={{backgroundColor:'red'}}></div>`, represents properties with a JS object
  * With compound property names, remove the dashes and instead use camelCase
  * Adding a class to an element uses different syntax:
    * use className instead of class
    * Ex: `<label className="label">`, avoids collisions with the class keyword from `class App extends React.Component`
    * Note: Objects are not valid as a React child, cannot print JS objects as text
  * JSX can easily reference JS variables:
    * Use `{buttonText}` syntax to reference JS variables inside JSX, can also call functions like `{getButtonText()}`
* Convention: with JSX, use "" whenever you want to indicate a string, but for any non-JSX property make use of ''
* More differences between JSX and HTML that you can find by checking your console for warnings

### Communicating with Props
* Component Nesting: a component can be shown inside of another
* Component Reusabilit: want to make components that can be easily reused throughout application
* Component Configuration: should be able to configure a component when it is created
* Semantic-UI: CSS framework similar to Bootstrap, quick and simple styling for general use
* faker.js: Package for generating fake data, great for new app testing
* To import code from an external package:
```
import faker from 'faker';
```
* Creating a Reusable, Configurable Component:
  * Identify the JSX that appears to be duplicated, tink of a descriptive name for what it does
  * Create a new file to house this new component - it should have the same name as the component
  * Create a new component in the new file, paste the JSX into it
  * Make the new component configurable by using React's `props` system
* React components are traditionally written in upper-case and camel cased, like `CommentDetail`
* The export statement we place in a component file makes is accessible to every other file in the project
```
export default CommentDetail;
```
* Webpack automaticaly tries to find files with `.js` ending when importing, so just need to import from `./CommentDetail`
* If we want to show one component inside of another, we treat it like a JSX tag, `<CommentDetail />`
* Props:
  * System for passing data from a parent component to a child component
  * Goal is to customize or configure a child component
 
