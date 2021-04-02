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
```
import React from "react";

const Hello = () => <h1>Vicky here</h1>
export default Hello;

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
