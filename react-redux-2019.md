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
* Providing props from parent to child:
```
<CommentDetail author="Sam />
```
* Props are provided by the first argument in the component:
```
const CommentDetail = (props) => {
```
* Component Reuse: modular component pieces to build larger ones, separate a comment card into CommentDetail and ApprovalCard
* You can pass one component as the child of another:
```
<ApprovalCard>
  <CommentDetail
    author="Big"
    timeAgo="Today at 4:20AM"
    content="Nice blog post"
    avatar={faker.image.avatar()}
  />
</ApprovalCard>
```
* When passing in `CommentDetail` as a prop of `ApprovalCard` it is held in props under `children`
* We can then show this child component in our return, such as:
```
<div className="content">
  {props.children}
</div>
```
* Component is now reusable, and you can pass other things into the component tags:
```
<ApprovalCard>
 <h4>Warning!</h4>
 Are you sure you want to do this?
</ApprovalCard>
```

### Structuring Apps with Class-Based Components
* Functional components: good for simple content without a lot of logic behind it
* Class components: good for just about anything else - complex logic, responding to user inputs, network requests
* Benefits of class components:
  * Easier code organization
  * Can use 'state' (another React system), easier to handle user input
  * Understands lifecycle events, easier to do things when the app first starts
* Simple example application: check user's location and time of year, shows if it's cold or hot
* Automatically set GPS location: In Chrome dev tools, `esc > ... > sensors > geolocation` overrides your location to the selection
* To make location sharing selectable again on browser, `i > location > ask(default)`
* Make a request to geolocation, with callbacks for success and failure:
```
window.navigator.geolocation.getCurrentPosition(
  (position) => console.log(position),
  (err) => console.log(err)
);
```
* Application timeline:
  * JS file loaded by browser
  * App component gets created
  * We call geolocation service
  * App returns JSX, gets rendered to page as HTML
  * ...
  * We get result of geolocation!
* Getting geolocation result back takes some time
* We see content appear on the screen far sooner than when we get a result from the geolocation API
* Want to tell component to rerender itself with new information
* Rules of Class-based Components:
  * Must be a Javascript Class
  * Must extend (subclass) React.Component
  * Must define a 'render' method that returns some amount of JSX
```
class App extends React.Component {
  render() {
    return <div>Latirude: </div>
  }
}
```

### State in React Components
* Rules of State:
  * Only usable with class-based components
  * `State` is a JS object that contains data relevant to a component
  * Updating `State` on a component casues the component ot (almost) instantly rerender
  * State must be initialized when a component is created
  * State can _only_ be updated using the function `setState`
* `constructor(props)` function specific to JS, will be the first thing called any time an instance of a class is created
*  Must call `super(props);` first, as `React.Component` has a constructor function of its own that we're overriding, but we want to ensure the parent constructor function gets called
```
constructor(props) {
  super(props);
  this.state = { lat: null, errorMessage: '' };
  
  window.navigator.geolocation.getCurrentPosition(
    position => {
      this.setState({ lat: position.coords.latitude });
    },
    err => {
      this.setState({ errorMessage: err.message });
    }
  );
}

render() {
  return (
    <div>
      Latitude: {this.state.lat}
      Error: {this.state.errorMessage}
    </div>
  );
}
```
* NEVER want to do a direct assignment of the State object outside of the initial creation in the constructor
* JS callbacks mean setState calls in constructor may not occur until some time after
* Setting state is an additive process; don't need to specify every state variable, only the ones you're changing
* Can conditionally render content based on the current state, such as checking for an error
```
if (this.state.errorMessage && !this.state.lat) { return <div>stuff</div>; }
```

### Understanding Lifecycle Methods
* Component Lifecycle Method: function we can optionally define inside our class-based components, will be automatically called by react in certain point in the component's lifecycle (technically constructor/render count)
* `componentDidMount()` is called directly after our component is rendered onto the screen, good place to do data loading
* Any time we call `setState`, the component will update itself, and will automatically call `componentDidUpdate()` after calling render
* If we stop showing a component on the screen, the `componentWillUnmount()` method will be called, good for cleanup
* Other rare methods: `shouldComponentUpdate`, `getDerivedStateFromProps`, `getSnapshotBeforeUpdate`
* Refactor: move the `window.navigator..` code into `componentDidMount()`
* Alternate state initialization, can simply write the following instead of defining the constructor function:
```
state = { lat: null, errorMessage: '' };
```
* Can use the babel live interpreter to see how the line above compiles into the same code as with the constructor
* Passing State as Props: can render a component and pass the current component's state variable to props:
```
return <SeasonDisplay lat={this.state.lat} />
```
* Ternary Expressions in JSX: can put any JS expression in braces `{}`:
```
<div><h1>{season === 'winter' ? 'Burr, it's chilly' : 'Lets hit the beach'}</h1></div>
```
* Divisive in community if you should put this much logic inside your embedded JS, could also make a helper var
* Configuration objects: create a nested hash holding all the relevant text/icons/etc to switch between:
```
const seasonConfig = {
  summer: {
    text: "Let's hit the beach!",
    iconName: 'sun'
  },
  winter: {
    text: 'Burr it is cold!',
    iconName: 'snowflake'
  }
};
```
* With this, we can replace duplicate ternary expressions with a simple `seasonConfig[season]`, and all information now only exists in one place
* If a css file is meant only to modify a certain component or js file, name it the same for association, then import into main file
* Loading animations can be used when waiting on asynchronous requests
* Separate functional component `Spinner` that can be reused anywhere, import in `index.js`, set as fallback until something else is displayed
* Specifying default props: on the component itself, you can specify:
```
Spinner.defaultProps = {
  message: 'Loading...'
};

export default Spinner;
```
* If you have conditionals in your component's render function but always want something included, you'd need to put it in each conditional! Bad!
* Create helper function `renderContent()` and call that in the render method with the universal things applied:
```
return (
  <div className="border red">
    {this.renderContent()}
  </div>
);
```
* Traditionally, the config objects and helper functions are on top, with the component at the bottom

### Handling User Input with Forms and Events
* Generate new react application with `create-react-app pics`, start it up with `npm start`
* Project structure: make a separate components folder to store components
* When we pass a method as a prop to another component, we do not put `()` at the end as that will evaluate the function when we pass it
```
<input type="text" onChange={this.onInputChange} />
```
* `onClick`, `onChange`, and `onSubmit` are callback functions that are automatically invoked in inputs/forms/etc, dependent on the element type
* Naming convention with event handlers is "on" + "element type" + "event type", "handle" is also popular
* Single line functions are often condensed in the return statement:
```
<input type="text" onChange={e => console.log(e.target.value)} />
```
* Controlled element search bar flow:
  * User types in input
  * Callback gets invoked
  * We call setState with the new value
  * Component rerenders
  * Input is told what its value is (coming from state)
```
<input type="text"
  value={this.state.term}
  onChange={e => this.setState({ term: e.target.value })}
/>
```
* Before refactoring controlled, the only way to find the input value right now was reaching into the DOM and pulling the value from the `input` element
* After refactoring, we can just refer to the current state, never need to look into the DOM
* With the controlled method, we can also apply changes to the user input in real time, ie:
```
this.setState({ term: e.target.value.toUpperCase() })
```
* Form submittal: make an `onFormSubmit(event)` method and pass that into the form's `onSubmit` attribute
* To stop the form submitting from automatically refreshing the page, use `event.preventDefault()`
* The following code results in `TypeError: Cannot read property 'state' of undefined`:
```
onFormSubmit(event) {
  event.preventDefault();
  console.log(this.state.term);
}
...
<form onSubmit={this.onFormSubmit} ... >
```
* `this` is a reference back to the instance of the class itself, which we can use to get reference to state, render, onFormSubmit, etc
* To determine what `this` in a function refers to, look to where it's called, and look what's left of the `.`, don't look at the function, look at where the function gets called
```
class Car {
  setDriveSound(sound) {
    this.sound = sound;
  }

  drive() {
    return this.sound;
  }
}

const car = new Car();
car.setDriveSound('vroom');

const drive = car.drive;
drive();
```
* The code above will result in `Cannot read property 'sound' of undefined`, because we pulled it off of its `this` reference. This is exactly what happens in react!
* One way to fix this is adding a constructor function to our Car class, binding and overwriting the function :
```
constructor() {
  this.drive = this.drive.bind(this);
}
```
* Can also replace our function declaration with an arrow function:
```
onFormSubmit = (event) => {...};
```
* Can also pass an arrow function directly into the onChange prop:
```
<form onSubmit={(event) => this.onFormSubmit(event)} ... >
```
* When we use the arrow function here, it only gets called when the action occurs, so we have to now invoke the onFormSubmit function
* Communicating from child to parent: define `onSearchSubmit(term)` in parent component, and pass as a prop into the `SearchBar` component. This way, the `App` component knows when the user searches, and can execute a new function in response
* In a class-based component, we reference the props object with `this.props`

### Making API Requests with React
* When user enters a search, we want to make an `Ajax`, or network request to the Unsplash API
* Axios: standalone 3rd party package that can be installed with npm
* Fetch: singular function built into modern browsers, far more basic and lower
* By convention, put imports for third party packages and dependencies above imports for files you've created
* With `axios.get`, enter arguments for the request url and the special configurations to pass in
```
axios.get('https://api.unsplash.com/search/photos', {
  params: { query: term },
  headers: {
    Authorization: '...',    
  }
});
```
* To view results for your request, can go to  Network > All > Preview, where the returned json/xml can be viewed
* Network requests are asynchronous, takes some time to get a response, after we've already exited the method that called it
* Whenever we make a request with Axios, it returns an object called a promise, giving a notification when something is completed. Use a `.then()` function chained onto `axios.get()` that is called after the response is returned
```
axios
  .get('...', {
    ...
  })
  .then(response => {
    console.log(response.data.results);
  });
}
```
* Alternate method: mark a function as async, allows us to use await:
```
async onSearchSubmit(term) {
  const response = await axios
    .get('...', {...});
}
console.log(response.data.results);
```
* With await, whatever gets returned by the axios request is assigned to a variable that we can use later on
* If you call `this.props.onSubmit()`, the value of `this` in the onSubmit method will be referring to `props`, not the component that called it! Need to call `this.props.onSubmit.bind(this)` or one of the other 2 solutions listed above
* Creating custom clients: make a separate file that has the preconfigured settings:
```
import axios from 'axios';
export default axios.create({
  baseURL: 'https://api.unsplash.com',
  headers: {
    Authorization: 'Client-ID ...'
  }
});
```
* Now can just `import unsplash from '../api/unsplash'` and make a request to `unsplash.get()`

### Building Lists of Records
* JS Map Statements: iterate over an array, modify each value, and return a brand new array
* Can be used to replace this 
```
for (let i = 0; i < numbers.length; i++) {
  newNumbers.push(numbers[i] * 10);
}
```
with this
```
numbers.map((num) => num * 10);
```
* Can use mapping to return a list of components or elements:
```
const images = props.images.map((image) => {
  return <img src={image.urls.regular} />
});

return <div>{images}</div>
```
* Need to add a `key` prop to each element in a list, helps react render lists and updates to lists more performantly 

## Redux
* Redux: state management library, makes creating complex applications easier, not required to create a React app
* Redux cycle: Action Creator > Action > Dispatch > Reducers > State
* Insurance company: Person dropping off the form > the form > for receiver > departments > compiled department data
* Analogy of a central repository of data that different departments can source from and edit
* Action creator example:
```
const createPolicy = (name, amount) => {
  return {
    type: 'CREATE_POLICY',
    payload: {
      name: name,
      amount: amount
    }
  };
};
```
* Reducer example:
```
const policies = (listOfPolicies = [], action) => {
  if (action.type === 'CREATE_POLICY') {
    return [...listOfPolicies, action.payload.name];
  } else if (action.type === 'DELETE_POLICY') {
    return listOfPolicies.filter(name => name !== action.payload.name);
  }
  return oldListOfClaims;
};
```
* Any time we want to change something inside of a reducer, we ALWAYS want to return a NEW object, instead of modifying an existing one
* `...` example:
```
const numbers = [1,2,3]
[...numbers, 4]
> [1,2,3,4]
```
* Creating a Redux store:
```
const {createStore, combineReducers } = Redux;

const ourDepartments = combineReducers({
  accounting: accounting,
  claimsHistory: claimsHistory,
  policies: policies
});

const store = createStore(ourDepartments);
const action = createPolicy('Alex', 20);
store.dispatch(action);
```
* Redux Cycle: to change the state of our app, we call an...
  * Action Creator, which produces an
  * Action, which gets fed to
  * Dispatch, which forwards the action to
  * Reducers, which create a new 
  * State, then we wait until we need to update state again
* Without redux, app complexity will tend to grow exponentially as its size increases
* With redux, initial complexity is higher, but complexity growth is slower and more linear

## More
### Handling Forms with Redux Form
* Form data held inside Redux store, passed down with `mapStateToProps` and fed into the form values, with action creators to update store when form inputs are updated
* Redux form does all of those things for us, as it's so repetitive and can be abstracted away
* Wizard form: information is entered across different pages/series of fields, and is all accumulated into Redux store
```
import { reducer as formReducer } from 'redux-form';

export default combineReducers({
  auth: authReducer,
  form: reducer
});
```
* Exporting with a reduxForm helper adds a ton of props to our redux component for handling things
* `Field` is a react component supplied by reduxForm, that automates the redux store updates
* Field doesn't know anything about what it's rednering, and that must be supplied as the `component` prop, where we put a function that returns an HTML element that's wrapped by the field
* We can use `input {...formProps.input}`, which passes in all the props of the formProps object and assigns them to the input element, such as onChange, value, etc.

```
renderInput({ input, label, meta }) {
  return (
    <div className="field">
      <label>{label}</label>
      <input {...formProps.input} autoComplete="off" />
      <div>{meta.error}</div>
    </div>
  );
}

onSubmit(formValues) {
  console.log(formValues);
}

render() {
  return (
    <form onSubmit={this.props.handleSubmit(this.onSubmit)} className="ui form">
      <Field name="title" label="Enter Title component={this.renderInput} />
      <Field name="description" label="Enter Description" component={this.renderInput} />
    </form>
  );
}
```
* `handleSubmit`: a function we're supposed to call any time a form is submitted, provided by reduxForm
* Form validation: want to check that title and description fields are filled in before submission is possible
* If error, return an object, with each invalid field having a key-value pair with the name of the field and the error message
```
const validate = (formValues)  => {
  const errors = {};
  
  if (!formValues.title) {
    errors.title = 'You must enter a title';
  }
  
  if (!formValues.description) {
    errors.description = 'You must enter a description';
  }
  
  return errors;
};
```
* Validate is called every time the form is initially rendered or the user interacts with it in any way
* If a field name lines up with a key in our errors object, that error message will be passed to the renderInput function
* You can turn off autocompletion on an input element with `autoComplete="off"`
* `meta.touched` attribute is a boolean that indicates if an element has been clicked on and then clicked off, can be used to determine if the error message should be shown after the user clicks off it

