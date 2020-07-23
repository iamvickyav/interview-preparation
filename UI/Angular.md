# AngularJS

## Installation

```
> npm install -g @angular/cli@7.0.3
```

## Angular CLI Commands

```
// To generate a new Angular Project
> ng new todo

// To start the application
> ng serve

// Coding standard check
// Ruled defined in tslint.js
> ng lint

// To build application & generate the artifacts in dist
> ng build

// To run test cases called spec
// File name is *.spec.ts
> ng test

// To run integration test using Selenium
> ng e2e
```

## Angular Folder structure

src/app - Where Angular Code resides

src/assets - For images

src/environment - For multi environment support

tsconfig.json - For converting TS to JS

package.json - External frameworks and tools

node_modeules - where the dependencies specified in package.json get downloaded

src/main.ts & src/index.html - Default files which get loaded on ng serve command

src/polyfills.ts - For browser compatibility issues

## Angular Concepts

### Angular Components

Pages are divided into component. Each component is responsible for view, style & code to react to user actions like click on button

Files are

.component.html
.component.css
.component.ts
.component.spec.ts

### How to create Component

Using Decarator (Like annotations) called @Component

```
@Component({
    selector : 'app-root',
    templateUrl : './app.component.html',
    styleUrls : ['./app.component.css']
})
```

selector - tag name for the component

To access member varaible (interpolation) = {{ var_name }}

```
> ng generate component welcome
```

app.module.ts - gets updates 
