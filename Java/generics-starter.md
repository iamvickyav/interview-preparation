# Java Generics

Java Generics enable types to be parameters when defining classes, interfaces and methods.

It helps achieve & avoid **ClassCastException**

```java

// Example taken from https://docs.oracle.com/javase/tutorial/java/generics/types.html

public class Box<T> {
    // T stands for "Type"
    private T t;

    public void set(T t) { this.t = t; }
    public T get() { return t; }
}
```

- T stands for the "Type"
- Type can be class/interface
- Type can't be primitive. E.g. int can't be generic but Integer can
- T in Foo<T> is a type parameter & String in Foo<String> f is a type argument
- Assigning RawType to Parametertised type will give warning
