# React Notes

## To start working

```sh
npx create-react-app kee
cd kee
npm start
```

## Function Component

```js

import React from 'react';
import Hello from './component/Hello';

class App extends React.Component {
  render() {
    return (
     <Hello></Hello>
    );
  }
}
export default App;
```

### As normal function

```js
import React from "react";

function Hello(){
    return <h1>Vicky</h1>
}
export defailt Hello
```

### As arrow function

```js
import React from "react";

const Hello = () => <h1>Vicky here</h1>
export default Hello;
```

## Class Component

```js

import React from 'react';
import Welcome from './component/Welcome'

class App extends React.Component {
  render() {
    return (
     <div>
      <Welcome></Welcome>
     </div>
    );
  }
}
export default App;
```

```js
import React from 'react'

const Welcome = (props) => {
        return <div>
            <h1>Welcome Vicky</h1>
        </div>
}

export default Welcome
```

## With Props

### Function with props

```js

import React from 'react';
import Welcome from './component/Welcome'

class App extends React.Component {
  render() {
    return (
     <Welcome name="vicky"></Welcome>
     </div>
    );
  }
}
export default App;


import React from 'react'

const Welcome = (props) => {
        return <div>
            <h1>Welcome {props.name}</h1>
        </div>
}

export default Welcome
```

### Class with props

```js

import React from 'react';
import Hello from './component/Hello';

class App extends React.Component {
  render() {
    return (
     <div>Hello World
     <Hello helloName="kee"></Hello>
     </div>
    );
  }
}
export default App;

import React from 'react';

class Hello extends Component {
    render() {
        return(
            <h1>{this.props.helloName}</h1>    
        );
    }
}

export default Hello
```

## Dynamic content passing in props

```js
import React from 'react';
import Welcome from './component/Welcome'

class App extends React.Component {
  render() {
    return (
     <div>
     <Welcome name="vicky">
       <button>Click me</button>
     </Welcome>
     </div>
    );
  }
}
export default App;

import React from 'react'

const Welcome = (props) => {
        return (
        <div>
            <h1>Welcome {props.name}</h1>
            {props.children}
        </div>
        )
}

export default Welcome
```

## props vs state

| props  |  state |
|----------------------|---------------------------|
|  passed to component |  managed by the component |
| function param       | variabled declared in function|
| immutable            | mutable |
| props in functional & this.props in class | useState hook in functional and this.state in class |

## state in class

```js
import React from 'react'
import StateWelcome from './component/StateWelcome'

class App extends React.Component {
  render() {
    return (
     <div>
       <StateWelcome></StateWelcome>
     </div>
    );
  }
}
export default App;

import React, { Component } from 'react'

class StateWelcome extends Component {

    constructor() {
        super()
        this.state = {
            msg : 'Welcome Kee'
        }
    }   

    render() {
        return <h1>{this.state.msg}</h1>
    }
}

export default StateWelcome
```
### Button click event

```js
import React, { Component } from 'react'

class StateChangeWelcome extends Component {

    constructor(){
        super()
        this.state = {
            msg : "Click on Agree button to accept the terms"
        }
    }
    agree() {
        this.setState ({
            msg : "Thank you for accepting the terms !"
        })
    }
    render() {
        return (
            <div>
                <h1> {this.state.msg} </h1>
                <button onClick= {() => this.agree()}>Agree</button>
            </div>
        )
    }
}

export default StateChangeWelcome
```

## Destructing Components

```js
import React from 'react';
import NameComponent from './component/NameComponent'

class App extends React.Component {
  render() {
    return (
     <div>
       <NameComponent firstName="Vicky" lastName="Arumugam"></NameComponent>
     </div>
    );
  }
}
export default App;


import React from 'react'

const NameComponent = ({firstName, lastName}) => {
    return (
        <div>
            <h1>{firstName}</h1>
            <h1>{lastName}</h1>
        </div>
    )
}
export default NameComponent
```

```js
import React from 'react';
import NameComponent from './component/NameComponent'

class App extends React.Component {
  render() {
    return (
     <div>
       <NameComponent firstName="Vicky" lastName="Arumugam"></NameComponent>
     </div>
    );
  }
}
export default App;

import React from 'react'

const NameComponent = (props) => {
    const {firstName, lastName} = props
    return (
        <div>
            <h1>{firstName}</h1>
            <h1>{lastName}</h1>
        </div>
    )
}
export default NameComponent
```

## Button Click in Functional & Class Components

```js
import React from 'react'

function ClickFunction() {

    function click() {
        console.log("Click !!")
    }

    return (
        <div>
            <button onClick={click}>Click me</button>
        </div>
    )
}

export default ClickFunction
```

```js
import React, { Component } from 'react'

class ClickClassFunction extends Component {

    click() {
        console.log("helo")
    }

    render() {
        return (
            <div>
                <button onClick={this.click}>Click me</button>
            </div>
        )
    }
}

export default ClickClassFunction
```

## React Event Binding

### Approach 1 - Binding in button

```js
import React, { Component } from 'react'

class EventBinding extends Component {

    constructor(props) {
        super(props)
    
        this.state = {
             msg : 'hello'
        }
    }

    clickHandler() {
        this.setState ({
            msg : 'thank you'
        })
    }
    
    render() {
        return (
            <div>
                {this.state.msg}
                <button onClick={this.clickHandler.bind(this)}>Click</button>
            </div>
        )
    }
}

export default EventBinding
```

### Bind using Arrow function

```js
import React, { Component } from 'react'

class EventBinding extends Component {

    constructor(props) {
        super(props)
    
        this.state = {
             msg : 'hello'
        }
    }

    clickHandler() {
        this.setState ({
            msg : 'thank you'
        })
    }
    
    render() {
        return (
            <div>
                {this.state.msg}
                <button onClick={() => this.clickHandler()}>Click</button>
            </div>
        )
    }
}

export default EventBinding
```

### Binding in constructor

```js
import React, { Component } from 'react'

class EventBinding extends Component {

    constructor(props) {
        super(props)
    
        this.state = {
             msg : 'hello'
        }
        this.clickHandler = this.clickHandler.bind(this)
    }

    clickHandler() {
        this.setState ({
            msg : 'thank you'
        })
    }
    
    render() {
        return (
            <div>
                {this.state.msg}
                <button onClick={this.clickHandler}>Click</button>
            </div>
        )
    }
}

export default EventBinding
```

### Create Function with arrow button

```js
import React, { Component } from 'react'

class EventBinding extends Component {

    constructor(props) {
        super(props)
    
        this.state = {
             msg : 'hello'
        }
    }

    clickHandler = () => {
        this.setState ({
            msg : 'thank you 2'
        })
    }
    
    render() {
        return (
            <div>
                {this.state.msg}
                <button onClick={this.clickHandler}>Click</button>
            </div>
        )
    }
}

export default EventBinding
```

