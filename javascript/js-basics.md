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
[Reference video](https://www.youtube.com/watch?v=80KX6aD9R7M)

## Unique Values (using ES6)

* new Set will remove duplicates but will convert Array into an Object
* To Convert back to Array, use the Spread Operator

```javascript
const menu = [
    {
        name: 'pancakes',
        category: 'breakfast',
    },
    {
        name: 'burger',
        category: 'lunch',
    },
    {
        name: 'steak',
        category: 'dinner',
    },
    {
        name: 'bacon',
        category: 'breakfast',
    },
    {
        name: 'eggs',
        category: 'breakfast',
    },
    {
        name: 'pasta',
        category: 'dinner',
    },
];

const uniqueCategories = [...new Set(menu.map(item => item.category))]
// const uniqueCategories = ['all', 'vegetarian', ...new Set(menu.map(item => item.category))]
console.log(uniqueCategories)
```

[Reference video](https://www.youtube.com/watch?v=yxT1lgupUrY)

## Dynamic Object Keys

* Keys can be created using Square Bracker Notation & Dot Operator
* If the key already exist, value will be updated. If not present, the key and value will be created in Object

```javascript
// Dynamic Key using Dot Operator

const person = {
    age: 25
}

person.name = 'vicky'

console.log(person);

// Dynamic Key using Square Bracket Notation

const keyName = 'city'

const student = {
    [keyName]: 'chennai'
}

student['pincode'] = 610001

console.log(student);
```

[Reference Video](https://www.youtube.com/watch?v=_qxCYtWm0tw)

## Filter

* Filter returns new Array based on Condition & the size of resultant array may be different that given input Array
* Returns Empty Array, if none matches the condition
* If we return an object or value instead of TRUE/FALSE, the return will be considered as True
* If we return ZERO from filter, the item will be ignored. All -ve/+ve numbers will be considered as True

```javascript
const people = [
    { name: 'bob', age: 20, position: 'developer' },
    { name: 'peter', age: 25, position: 'designer' },
    { name: 'susy', age: 30, position: 'the boss' },
    { name: 'anna', age: 35, position: 'intern' },
];

youngPeopleArray = people.filter(person => person.age < 30)
console.log(youngPeopleArray);

const people = [
    { name: 'bob', age: 20, position: 'developer' },
    { name: 'peter', age: 25, position: 'designer' },
    { name: 'susy', age: 30, position: 'the boss' },
    { name: 'anna', age: 35, position: 'intern' },
];

youngPeopleArray = people.filter(person => {return 0})
console.log(youngPeopleArray); // Returns Empty List

youngPeopleArray = people.filter(person => {return person.age-30})
console.log(youngPeopleArray); // Returns List with persons whose age is not 30
```

[Reference Video](https://www.youtube.com/watch?v=KeYxsev737s)

## Find

## Reduce

### Reduce to Number

### Reduce to Object

