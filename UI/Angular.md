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

### How to read Path Variable

**app-routing.module.ts**
```typescript
const routes: Routes = [
  { path: '', component: WelcomeComponent },
  { path: 'display/:productId', component: ItemDisplayComponent },
];
```

**ItemDisplayComponent.ts**
```typescript
import { Component, OnInit } from '@angular/core';
import { ActivatedRoute } from '@angular/router';

@Component({
  selector: 'app-item-display',
  templateUrl: './item-display.component.html',
  styleUrls: ['./item-display.component.css'],
})
export class ItemDisplayComponent implements OnInit {

  constructor(private route: ActivatedRoute) {
  }

  ngOnInit(): void {
    console.log(this.route.snapshot.params['productId']);
  }
}
```

### Make HTTP Calls

**Import HTTP Module in app.module.ts**

```typescript
@NgModule({
  declarations: [
    AppComponent,
    HeaderComponent,
    ItemDisplayComponent,
    HomeComponent,
  ],
  imports: [BrowserModule, AppRoutingModule, HttpClientModule],
  providers: [],
  bootstrap: [AppComponent],
})
```

**Import HttpClient in Service**

```typescript
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';

@Injectable({
  providedIn: 'root',
})
export class HomesuggestionService {
  constructor(private http: HttpClient) {}

  getNewArrivals() {
    return this.http.get('http://localhost:8080/location/test');
  }
}
```

***Calling service from a Component***
```typescript
@Component({
  selector: 'app-home',
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.css'],
})
export class HomeComponent implements OnInit {
  constructor(private service: HomesuggestionService) {}

  ngOnInit(): void {
    this.service.getNewArrivals().subscribe(
      (response) => this.processResponse(response),
      (error) => this.processErrorResponse(error)
    );
    this.service.getBestSellers();
  }

  processResponse(response) {
    console.log(response);
  }

  processErrorResponse(error) {
    console.log(error.error);
  }
}
```
