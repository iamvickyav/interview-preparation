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
