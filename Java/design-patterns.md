# Gang of Four (GoF) Design Patterns


- Erich Gamma
- Richard Helm
- Ralph Johnson
- John Vlissides

## Categories
### Creational Patterns 
- Deals with ways of object creation
### Structural Patterns
- Deals with relationship between objects
### Behavioral Patterns 
- Deals with interaction between objects

## Creational Pattern

### Singleton - Ensures only one instance of an object is created

Only one object instance per JVM of a class. Singleton in Spring means single instance of of a class per container

- E.g. **DBConnection** in app

#### How to achieve singleton ?

- Make constructor private
- Create a static method to return the instance

```
// Eager Initialization

public class Singleton {

    private static final Singleton instance = new Singleton();

    private Singleton(){
    }

    static Singleton getInstance() {
       return instance;
    }
}
```
```
// Lazy Initialization

public class Singleton {

    private static Singleton instance;

    private Singleton(){

    }

    static Singleton getInstance() {
        if(instance==null)
            instance = new Singleton();
        return instance;
    }
}
```
```
// For multi threaded environment (Double checked Locking Mechanism)

- Add synchronized keyword for getInstance() method
- Write to a volatile field will happen before any read operation

public class Singleton {

    private volatile static Singleton instance;

    private Singleton(){
    }

    static Singleton getInstance() {
       if(instance == null) {
           synchronized (Singleton.class) {
               if(instance == null) {
                   instance = new Singleton();
               }
           }
       }
       return instance;
    }
}
```

### Prototype - Creates a new object from an existing object

Used when the Object creation is a costly and requires a lot of time and resources and you have a similar object already existing. Prototype pattern provides a mechanism to copy the original object to a new object and then modify it according to our needs

An object that supports cloning is called a prototype

**Cloneable interface **
- to mark objects that permit cloning
- Marker interface hence no need to override any method
- if not added Cloneable, CloneNotSupportedException will be thrown
- A call to super.clone() performs a shallow copy

Shallow Copy - If field is a primitive, copy the value. If field is reference, then copy the reference

If object contains only primitive or immutable fields - Go for Shallow Copy. Otherwise override clone() method for deep copy

### Builder - Creates create complex objects

Building complex object can be achieved using overloaded constructor. This type of design is called telescopic constructor pattern which is an anti pattern. Setter doesn't guarantee all values to be set (also the order). So go for Builder

Enforce a step-by-step process to construct a complex object  

In short abstract factory is concerned with what is made, while the builder with how it is made

- Builder class as static inner class
- No Setter method & Builder class is used in constructor
- Achieved Immutability
- java.lang.StringBuilder#append() [Unsynchronized class]
- java.lang.StringBuffer#append() [Synchronized class]

```
public class User 
{
    //All final attributes
    private final String firstName; // required
    private final String lastName; // required
    private final int age; // optional
    private final String phone; // optional
    private final String address; // optional
 
    private User(UserBuilder builder) {
        this.firstName = builder.firstName;
        this.lastName = builder.lastName;
        this.age = builder.age;
        this.phone = builder.phone;
        this.address = builder.address;
    }
 
    //All getter, and NO setter to provde immutability
    public String getFirstName() {
        return firstName;
    }
    public String getLastName() {
        return lastName;
    }
    public int getAge() {
        return age;
    }
    public String getPhone() {
        return phone;
    }
    public String getAddress() {
        return address;
    }
 
    @Override
    public String toString() {
        // SOME CODE
    }
 
    public static class UserBuilder 
    {
        private final String firstName;
        private final String lastName;
        private int age;
        private String phone;
        private String address;
 
        public UserBuilder(String firstName, String lastName) {
            this.firstName = firstName;
            this.lastName = lastName;
        }
        public UserBuilder age(int age) {
            this.age = age;
            return this;
        }
        public UserBuilder phone(String phone) {
            this.phone = phone;
            return this;
        }
        public UserBuilder address(String address) {
            this.address = address;
            return this;
        }
        //Return the finally consrcuted User object
        public User build() {
            User user =  new User(this);
            validateUserObject(user);
            return user;
        }
        private void validateUserObject(User user) {
            //Do some basic validations to check 
            //if user object does not break any assumption of system
        }
    }
}
// https://howtodoinjava.com/design-patterns/creational/builder-pattern-in-java/

```

## Factory Method

This pattern favors method invocation instead of making direct constructor calls to create objects.

- helps encapsulate object creation code from client code
- decouples client code from the concrete classes
- centralized location for object creation code

## Adapter Design Pattern

https://springframework.guru/gang-of-four-design-patterns/adapter-pattern/



## Reference

- https://springframework.guru/gang-of-four-design-patterns/
- https://springframework.guru/gang-of-four-design-patterns/prototype-pattern/ 
- https://www.geeksforgeeks.org/prototype-design-pattern/
- https://www.journaldev.com/1440/prototype-design-pattern-in-java
- https://github.com/in28minutes/interview-guide


