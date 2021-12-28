# Node.js

## Notes from Crash Course

Commands to start with

```sh
# Create Empty Node Project with package.json

> npm init

# Install dependency as dev dependencies

> npm install --save-dev nodemon
(or)
> npm install -D nodemon
```

### Modules

**Exporting Module**
```js
const person = {
    name  : 'John',
    age   : 30,
}

module.exports = person; 
```

**Use Exported Module**

```js
const person = require("./person")

console.log(person)
```

**Exporting ES6 class as Module**
```js
class People {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }

    greetings() {
        console.log(`Hello Mr. ${this.name}`)
    }
}

module.exports = People;
```
**Use Imported ES6 class Module**
```js
const People = require("./personclass")

const people = new People("John", 30);
console.log(people.greetings())
```

**Module Behind the scence**

From Documentation

> Before a module's code is executed, Node.js will wrap it with a function wrapper that looks like the following:

```js
(function(exports, require, module, __filename, __dirname) { 
    // Module code actually lives in here 
});
```
