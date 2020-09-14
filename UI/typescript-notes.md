# TypeScript Notes

* `var` keyword will have scope equal to the nearest declared function. Hence use `let` keyword

## Types

```typescript
let a: number;
let b: boolean;
lec c: string;
let d: any;
let e: number[] = [2,3,4];
let f: any[] = [1, true, 'vicky']

const red = 0;
const blue = 1;

enum Color {RED, BLUE}
let bgColor = Color.RED;
```

## Type assertion

```typescript
let message;
message = 'vicky';
let result = (<string>message).endsWith('y');
let result2 = (message as string).endsWith('y');
```

## Arrow functions

```typescript
let log = function(message){
  console.log(message);
}

let log2 = (message) => {
  console.log(message);
}

let log3 = message => console.log(message);

let log4 = () => console.log('hi');
```

## Interfaces

### Inline annotations

```typescript
let draw = (point: {x:number, y:number}) => {};

draw({
    x:1,
    y:2
})
```

### Interface

```typescript
interface Point {
  x: number;
  y: number;
}

let draw = (point: Point) => {};

draw({
  x: 1,
  y: 2,
});
```

## Class & Object

```typescript
class Point {
  x: number;
  y: number;

  constructor(x: number, y: number) {
    this.x = x;
    this.y = y;
  }

  draw() {
    console.log("X:" + this.x + ",Y:" + this.y);
  }

  drawWithPoint(point: Point) {}
}

//let p: Point = new Point();
let p = new Point(2, 2);
p.draw();
```

* Construct param can be made optional by putting a ?. Remember once a param is optional, all following property has to be optional 

```typescript
constructor(x?: number, y?: number) {
    this.x = x;
    this.y = y;
}

let p = new Point();
```

```typescript
class Point {
  x: number;
  y: number;

  constructor(x: number, y: number) {
    this.x = x;
    this.y = y;
  }
}

// Equiavalent to below

class Point {
  constructor(private x: number, private y: number) {
  }
}
```

## Access modifiers
* Public (default access specifier)
* Private
* Protected

## Module in Typescript

```typescript
## point.ts

class Point {
  x: number;
  y: number;

  constructor(x: number, y: number) {
    this.x = x;
    this.y = y;
  }

  draw() {
    console.log("X:" + this.x + ",Y:" + this.y);
    console.log(`X: ${this.x}, Y${this.y}`);
  }
}
```

```typescript
import {Point} from './point';

let point = new Point(2,2);
point.draw();
```

* If we fail in compilation `tsc *.ts --target ES5`
