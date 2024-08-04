# Design Patterns

## Types

* Creational - How objects can be created
* Structural - Assemble objects and classes into larger structures
* Behavioral - How objects interact with each other

### Creational

**Strategy Design Pattern**

> Strategy is a behavioral design pattern that lets you define a family of algorithms, put each of them into a separate class, and make their objects interchangeable.

> Reference: https://refactoring.guru/design-patterns/strategy

E.g. Map with different navigation logic for Walk, Drive, Train etc

**Decarator Design Pattern**

Used to achieve Open To Extension but close to modification solid principle

> Decorator is a structural design pattern that lets you attach new behaviors to objects by placing these objects inside special wrapper objects that contain the behaviors.

> Reference: https://refactoring.guru/design-patterns/decorator

Aspect Oriented Programming uses Decarator & Proxy Design Patterns under the good

**Observer Pattern**

When we want to notify interested parties when something happens

**Singleton Pattern**

Only one instance of object

**Facade Pattern**

When you want to use an 3rd party library, instead of initiatizing and using it everywhere, we can use a Facade class which interact with that library & our application will only interact with the facade layer. So maintenance is easy & not all features of 3rd party library are exposed via Facade 

## Reference

* [https://www.youtube.com/watch?v=YMAwgRwjEOQ&ab_channel=AlexHyett](5 Design Patterns)
