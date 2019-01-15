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

