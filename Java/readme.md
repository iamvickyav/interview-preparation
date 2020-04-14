# Java last minute Revision Guide

  * [OOP concepts in Java](#oop-concepts-in-java)
  * [Class](#class)
  * [Object](#object)
  * [Encapsulation](#encapsulation)
  * [Abstraction](#abstraction)
  * [Polymorphism](#polymorphism)
    + [Method Overloading &amp; Overriding in Java](#method-overloading--amp--overriding-in-java)
      - [Overloading](#overloading)
      - [Overriding](#overriding)
    + [Rule for overriding](#rule-for-overriding)
    + [Covariant return type](#covariant-return-type)
- [Java Bean/POJO](#java-bean-pojo)
- [Constructor](#constructor)
- [Abstract Class](#abstract-class)
- [Interface](#interface)
  * [Marker Interface](#marker-interface)
- [Inheritance](#inheritance)
  * [Types of Inheritance](#types-of-inheritance)
    + [How multiple inheritance indirectly achieved in Java?](#how-multiple-inheritance-indirectly-achieved-in-java-)
- [Keywords in Java](#keywords-in-java)
  * [Final in Java](#final-in-java)
  * [Static in Java](#static-in-java)
  * [Super in Java](#super-in-java)
- [Packages](#packages)
- [Exception Handling in Java](#exception-handling-in-java)
  * [Error](#error)
  * [Exception](#exception)
  * [Exception Types](#exception-types)
    + [Checked Exception](#checked-exception)
    + [Unchecked Exception](#unchecked-exception)
  * [Exception Handling](#exception-handling)
- [Multi-Threading in Java](#multi-threading-in-java)
  * [By extending Thread class](#by-extending-thread-class)
  * [By implementing Runnable interface](#by-implementing-runnable-interface)
  * [Synchronization](#synchronization)
  * [Inter process communication](#inter-process-communication)
- [String](#string)
  * [Methods in String](#methods-in-string)
  * [String Pool](#string-pool)
- [Array](#array)
- [Wrapper class in Java](#wrapper-class-in-java)
  * [Auto boxing and Unboxing](#auto-boxing-and-unboxing)
- [Collection](#collection)
  * [Story behind Collection](#story-behind-collection)
  * [Java 1.2 and Collection rebirth](#java-12-and-collection-rebirth)
  * [List Data structure](#list-data-structure)
    + [ArrayList](#arraylist)
    + [LinkedList](#linkedlist)
  * [Set Data structure](#set-data-structure)
    + [HashSet](#hashset)
    + [TreeSet](#treeset)
    + [LinkedHashSet](#linkedhashset)
  * [Map Data structure](#map-data-structure)
    + [Map is not part of collection why?](#map-is-not-part-of-collection-why-)
  * [Collections class](#collections-class)

## OOP concepts in Java
## Class

Collection of similar properties of object. Class is user defined data type which contains properties and methods

## Object

Example/Instance of a class. It exist in real world.

How to create an object instance?

**Syntax** : **new** constructor\_method

**E.g.** new Student()

## Encapsulation

Binds together the data and functions &amp; provide security

**Achieved using POJO class** (declare all variable as private &amp; create public getter, setter methods)

## Abstraction

Hide certain details and only show the essential features of the object.

**Achieved using Interface &amp; Abstract Class**

## Polymorphism

Poly - Many Forms. Same name can be used for different operations

Achieved using **Method Overloading &amp; Method Overriding**.

### Method Overloading &amp; Overriding in Java

#### Overloading

Methods have same names but different number or type or order of parameters. Overloading is determined at the compile time. It&#39;s otherwise called static or compile time polymorphism

E.g.

display(String name)

display(String name, int number)

display(int number, String name)

Method won&#39;t be considered overloaded, if the return type is the only difference between two methods.

#### Overriding

A child class implements the method with same signature as a method in a parent class.

In method overriding both the super &amp; sub class have same method signature, compile doesn&#39;t figure out which method to call at compile-time. In this case, JVM decides which method to call at runtime that&#39;s why it&#39;s called dynamic polymorphism.

### Rule for overriding

| **Overridden Method (Super class method)** | **Overriding Method (Sub class method)** |
| --- | --- |
| If public | should be public |
| If protected | should be protected or public |
| If default (no access specifier) | should be protected or public or default |
| If private | can&#39;t be overridden |
| If static | can&#39;t be overridden |

### Covariant return type

Generally when we override a method, the signature has to be same for both methods. But there is a privilege to change the return type of the overriding method.

The return type we change should be the subtype of the return type of overridden method.

```
class Student {

}

class BE_Student extends Student {

	public Student getStudent() {
		return new Student();
	}
}

class ME_Student extends BE_Student {

	public BE_Student getStudent() {
		return new Student();
	}
}
```

In above case, we are trying to override the getStudent() method in BE\_Student class in ME\_Student class. In order to override, the signature should be same in both super and sub class.

In the above case, super class getStudent() method returns Student object. Subclass getStudent() method returns the BE\_Student object. Still it is a legal overriding. Because BE\_Student is sub class of Student object.

# Java Bean/POJO

```
class Student {

 private member variables  //class variable

 public getters() 
 public setters()  //to access private variable

}
```

# Constructor

When you create a new instance of the class, Constructor will be called automatically.

This can be used to initialize values in the class

**Restrictions**

- Same name as Class Name
- Only one Default Constructor
- Constructor Overloading is possible
- When we use Parameterized Constructor, Default Constructor is mandatory

# Abstract Class

Abstract class is class which may or may not contains abstract methods. The child extends Abstract class, it should give define the abstract methods.

Abstract Class can have

- Abstract methods and normal methods
- Static, final &amp; normal variables

We cannot create object for abstract class

# Interface

An interface is a reference type, similar to a class &amp; it&#39;s used to achieve 100 % abstraction

Interface can have

- Only abstract methods, and by default all methods are public
- Only  public static final variables //constants
- Cannot have static or final methods in interface

Class which extends Interface should give implementation for all methods in interface

If the class which extends interface is an abstract class, it need not give definition for all interface methods instead class which extends the abstract class has to define the undefined methods in interface

## Marker Interface

An interface with no methods is called Marker Interface

E.g. Serializable, Clonnable are marker interfaces

These interfaces are used to indicate something to compiler or JVM that the class implementing any of these interface have some special behaviour

# Inheritance

Inheriting the parent properties / behaviour. Represents the **IS A relationship** in real world. Achieved using **extends** keyword

Possible inheritance hierarchy

- One Interface can extend another interface
- One class can implements any number of interface
- One abstract class can implements any number of interface

## Types of Inheritance

**Single Inheritance**

When a class extends another class

```
class A {

}

class B extends A {

}
```

**Multilevel Inheritance**

One class which inherits property of another class which itself inherited class from another super class is called Multilevel inheritance

```
class A {

}

class B extends A {

}

class C extends B {

}
```

**Multiple Inheritance**

Java doesnot support multiple inheritance directly. In general, multiple inheritance means one class extends property from more than one super class.

**Why multiple inheritance not supported in Java?**

When a class inherit from two or more classes, there is a chance two methods with same signature exist in both the super classes. So compiler will face ambiguity situation on choosing between the two method implementation. So in Java, multiple inheritance is not supported by default.

```
class A {

}

class B {

}

class C extends A,B {

// Error not possible

}
```

### How multiple inheritance indirectly achieved in Java?

In Java, multiple inheritance is indirectly implemented using Interface. So a class can implement more than one interface at time.

If two interfaces have methods with same signature, Java will take the implementation given in the class for both the interface methods.

# Keywords in Java

Reserved words with special meaning which is already defined in the Java language.

Keywords can&#39;t be used as name for variables, methods or classes. Keywords usually will be in lower case

**E.g.** public, return, final, static

## Final in Java

final keyword serves different purpose depends upon the place it&#39;s been used

**In methods:** final methods cannot be overridden

**In variables (Fields):** final variables will be treated as constants

**In class:** final class can&#39;t be inherited further

E.g. String, all wrapper classes (Integer, Float) are final classes in Java

## Static in Java

static keyword serves different functionality depends on the place it&#39;s been used

**In methods:** When a method is declared as static, it can be accesses using the class name even without creating an object for the class. These methods are called as class methods.

**In variables (Fields):** When number of objects are created from the same class, they each have their own distinct copies all variables. If we have to create variables that are common to all objects, we should declare them as static. Fields that have the static modifier in their declaration are called static fields or class variables. They are associated with the class, rather than with any object

**In class:** Only nested class (A class declared inside another class) can be declared as static in Java. Normal classes can&#39;t be declared as static

## Super in Java

The super keyword in java is generally used to refer immediate parent class object

super is used to refer immediate parent class variable &amp; methods

super() is used to invoke immediate parent class constructor

Whenever we call the overridden method, we can only call the sub class implementation of the method. If we want to call super class implementation, use super keyword

# Packages

A package is a namespace that organizes a set of related classes and interfaces. Conceptually you can think of packages as being similar to different folders on your computer

Default imported package in all Java class is java.lang.\*

To use a package, we use the keyword **import**.

# Exception Handling in Java

## Error

Unexpected situation, occurs during program execution where further execution is impossible

## Exception

Unexpected situation, occurs during program execution where further execution is possible

By default, JRE will handle the exception &amp; exit the program execution safely. User can also handle exception manually using try/catch/throw/finally mechanism

## Exception Types

### Checked Exception

Checked exceptions are checked at compile-time

If a method is throwing a checked exception then it should handle the exception using either try-catch block or it should declare the exception using throws keyword

E.g. FileNotFoundException, IOException

### Unchecked Exception

Unchecked exceptions are not checked at compile-time rather they are checked at runtime

All unchecked exception extends RuntimeException class

E.g. ArithmeticException, NullPointerException, ArrayIndexOutOfBoundsException

## Exception Handling

Exception handling is done using try/catch/finally mechanism or using throws keyword

**try**		- contains a block of program statements within which an exception might occur. try can be followed by either one or more catch block or finally block or both

**catch**	- each catch block is an exception handler that handles the type of exception indicated by its argument

**finally**	- finally block will be called, irrespective of exception occurred or not. Usually resource cleanup operations are performed here

```
try {

} catch (IndexOutOfBoundsException e) {

    System.out.println(&quot;IndexOutOfBoundsException: &quot; + e.getMessage());

} catch (IOException e) {

    System.out.println(&quot;Caught IOException: &quot; + e.getMessage());

}
```

**throws**         - throws keyword used to declare an exception (usually checked exception) in method signature. throws keyword propagate the exception (if occurred) to the caller method. If we use throws keyword, we can skip the try/catch mechanism.

E.g. void display() throws IOException {

}

**throw**         - throw keyword is used to explicitly throw an exception.

E.g. throw new ArithmeticException()

# Multi-Threading in Java

Multithreading in java is a process of executing multiple threads simultaneously. Usually used in games.

There are two ways of creating a Thread.

## By extending Thread class

```
class MultiClass extends Thread {

	public void run() {
		System.out.println(&quot;thread method started…&quot;);
	}

	public static void main(String args[]) {
		MultiClass t1=new MultiClass ();
		t1.start();
	}
}
```

## By implementing Runnable interface

```
class MultiClass implements Runnable {

	public void run() {
		System.out.println(&quot;Thread is running...&quot;);
	}

	public static void main(String args[]) {
		MultiClass mc1=new MultiClass ();
		Thread t1 =new Thread(mc1);
		t1.start();
	}
}
```

## Synchronization

In multi-threaded environment, if we need to make a resource available to one thread at a time, we use synchronization. The synchronization keyword in java creates a block of code called critical section (which can be used by only one thread at a time using lock).

## Inter process communication

Two or more threads can interact with each other using three methods such as

- wait()   (Release the lock &amp; make the thread suspended)
- notify()  (Release the lock &amp; Resumes a thread which is suspended)
- notifyAll()  (Release the lock &amp; Resumes all thread which are suspended)

# String

String is an object that represents sequence of char values. String is immutable in Java

Example:

**Method 1: (Using String literal)**

```
char[] ch={&#39;i&#39;,&#39;t&#39;,&#39;e&#39;,&#39;c&#39;,&#39;h&#39;};

String s=new String(ch);
```

**Method 2: (Using new keyword)**
```
String s=new String(&quot;itech&quot;);
```

## Methods in String

concat(), split(), length(), substring()

## String Pool

String is special class in java. String Pool in java is a pool of Strings stored in Java Heap Memory. We can create String object using new operator as well as providing values in double quotes.

```
String s1 = &quot;iTech&quot;;

String s2 = &quot;iTech &quot;;

if(s1 == s2)

System.out.println(&quot;equal&quot;); //Prints equal.

String s3 = new String(&quot;iTech&quot;);

String s4 = new String(&quot;iTech&quot;);

if(s3 == s4)

System.out.println(&quot;equal&quot;); //Prints not equal
```

# Array

Array is a collection of similar data type of elements. They are stored in continuous memory space. In Java, Array is treated as Object.

To access elements in Array, we use the index of the element. Array uses the [] brackets to define the size of array.

Array index always starts with Zero. There are two ways to define the array.

**Array defining Method 1**

```
int a[]=new int[2];

a[0]=10;

a[1]=20;
```

**Array defining Method 2**

```
int a[]={33,3,4,5};
```

# Wrapper class in Java

Java platform provides wrapper classes for each of the primitive data types. These classes &quot;wrap&quot; the primitive in an object.

Byte, Integer, Float, Short, Float, Long, Double are the wrapper classes in Java.

## Auto boxing and Unboxing

**Auto boxing** is converting primitive to wrapper automatically by Java compiler.

```
Integer n = new Integer(100);

Instead use Integer n = 100;
```

Java compiler will convert primitive 100 into Integer object automatically.

**Unboxing** is converting wrapper to primitive automatically by Java compiler.

```
Integer n = 3;

int n1 = n;
```

Here even though n is object, it will be converted to primitive int automatically.

# Collection

Its just a short introduction about Java collection.

## Story behind Collection

Handling large number of objects situation is not new in Java. Even when Java first introduced we have Vector, HastTable classes to work with Collection of objects.

But on that time importance were given to multi-threading than efficiency.

So by default HastTable and Vector classes are synchronized and are thread safe. In order to achieve thread safe they compromised in performance. Later they figured performance matters than thread safety in Collection.

## Java 1.2 and Collection rebirth

So a complete new set of classes and interfaces were introduced in Java 1.2 to redefine the way Java deals with collection.

On top of it we have a number of interfaces developed for collection.

Collection interface is the primary interface (with add, addAll, iterator methods) which declares basic definition to work with any collection.

Java introduced 4 important data structures to deal with collection of objects such as List, Set, Map, Queue (though the first three are widely used).

List, Set, Queue are interfaces extending collection interface but map interface doesnot extends collection interface.

## List Data structure

List is ordered and will allow duplicates

**List implementation classes**

### ArrayList

Uses Java Array in back end. It stores data in insertion order. Best if we are going to perform more read operation. For accessing any element in the ArrayList irrespective of the position, ArrayList consumes same time.

### LinkedList

Uses Linked concept in back end. (Second data have pointer to first and third elements a and so on). Stores data in insertion order. Best if we have more insertion and deletion operation.

## Set Data structure

Set wont allow duplicates

**Set implementation classes**

### HashSet

Stores data in a random order (unpredictable). HashSet uses Hashing algorithm in back end. It can only store unique elements. Best for addition.

### TreeSet

Stores data in sorted order (ascending).

Uses Red Black Tree algorithm in back end. Stores only unique elements. Best for frequent read/write operation.

### LinkedHashSet

Uses LinkedList and HashSet in back end. Stores unique elements but in insertion order.

## Map Data structure

Everything is stored as key value pair (both key and value are Objects). Keys are unique. One key mapped to one value.

Important Map methods: put(), get(), keySet(), entrySet()

**Concrete implementation classes**

Map provides three implementation classes such as HashMap, TreeMap, LinkedHashMap. Character of all the three classes are same as HashSet, TreeSet, LinkedHashSet.

**HashMap** - Keys are stored in Random order

**TreeMap** - Keys are sorted in natural order

**LinkedHashSet** - Keys are stored in insertion order.

### Map is not part of collection why?

It is part of the collection framework but it doesn&#39;t implement the java.util.Collection interface. The Collection interface is implemented by (is the root of) List-like Collections while Map is implemented by (is the root of) the KEY-VALUE-like collections

## Collections class

Collections class is a utility class which has number of static methods to help developers operate on Collection data structure in easier way. Few methods available with Collections class are as follow

sort(), max(), min(), reverseOrder(), shuffle()
