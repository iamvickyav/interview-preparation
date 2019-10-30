## Volatile

Indicate to JVM that Thread should not cache value of this variable and always read it from main memory

- Can be used only with variable
- After Java 5, write to any volatile variable happens before any read into the volatile variable
- Helps in achieving "happens-before" relationship in Java Memory model

### Usage

- Double & Long are 64 bits hence platform dependence. Write may happen in two 32 bit write steps. Hence chance of missing one write by another. Hence use volatile
- In achieving 
- Singleton

## Program for Interfaces

 “Program to an interface, not an implementation“, which leads to polymorphism

**Reference** : https://javarevisited.blogspot.com/2011/06/volatile-keyword-java-example-tutorial.html