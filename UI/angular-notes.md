# Angular Notes

## Components

* Create a component
* Regsiter the component in app.module.ts
* Refer the component in UI using the selector specified in Component

## Creating First Component

```typescript
// courses.component.ts
import {Component} from '@angular/core';

@Component({
  selector : 'courses',
  template : '<h2>Hello</h2>'
})
export class CourseComponent {
}
```

## Adding Bootstrap

Following command will save bootstrap and it will also put entry in `package.json`

```sh
npm install bootstrap --save
```

Advantage of adding in package.json, it will add dependencies in `node_modules` which we don't need to checkin in Git

In style.css

```
@import "~bootstrap/dist/css/bootstrap.css"
```

## Class Binding

Enables adding a class to element based on the boolean value

```typescript
// courses.component.ts
import {Component} from '@angular/core';

@Component({
  selector : 'courses',
  template : '<button class="btn" [class.active]="isActive">submit</button>'
})
export class CourseComponent {

  isActive = false; 
}
```

## Style Binding

Bind style (Refer DOM Style properties) based on boolean condition

```typescript
// courses.component.ts
import {Component} from '@angular/core';

@Component({
  selector : 'courses',
  template : "<button [style.backgroundColor]="isActive : 'blue' : 'green'">submit</button>'
})
export class CourseComponent {

  isActive = false; 
}
```

## Event Binding

Use parathesis for binding instead of square bracket

```typescript
// courses.component.ts
import {Component} from '@angular/core';

@Component({
  selector : 'courses',
  template : '<button (click)="onSave($event)"></button>'
})
export class CourseComponent {
    
    onSave($event){
      console.log("button clicked", $event);
    }
}
```

