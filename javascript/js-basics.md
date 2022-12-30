# Javascript Basics

## Map Function

* Doesn't change size of the Array
* Returns new array
* Usually used to convert Array of Something into Array of Something else. E.g. Array of Persons to Array of Person's name alone

```javascript
const people = [
    {
        name: 'bob',
        age: 20,
        position: 'developer',
    },
    {
        name: 'anna',
        age: 25,
        position: 'designer',
    },
    {
        name: 'susy',
        age: 30,
        position: 'the boss',
    },
    {
        name: 'john',
        age: 26,
        position: 'intern',
    },
];

positions = people.map((person) => {
    return {
        name: person.name
    }
})
console.log(positions)

// output
// [{name:'bob'},{name:'anna'},{name:'susy'},{name:'john'}]
```


## Unique Values



## Dynamic Object Keys

## Filter & Find

## Reduce

### Reduce to Number

### Reduce to Object

