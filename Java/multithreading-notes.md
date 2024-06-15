# Java MultiThreading

Notes from Lecture - https://www.linkedin.com/learning/learning-java-threads/what-is-a-thread?u=2154233 by Peggy Fisher

## Thread in Java

* Default thread is main
* Thread - Independent path of code execution
* Thread executes the Runnable objects
* Each thread gets its own private Stack - To store local variables, track methods calls
* Default priority is 5

> **Interesting Read** - Relationship between Java thread and OS threads. Whenever we create an object of type Thread, that object, among other things, contains the code that needs to execute and the start method. When we run that start method, we ask the OS to create and start a new OS thread belonging to our application's process, and ask the JVM to allocate a fixed-size stack space to store the thread's local variables from that point on. The OS is fully responsible for scheduling and running the thread on the CPU, just like any other thread. (Reference: https://dev.to/elayachiabdelmajid/java-21-virtual-threads-1h5b). Java thread maps to OS threads in one to one fashion

## Creating Thread

* java.lang.Thread interface
* java.lang.Runnable interface

## Thread Type

### Daemon

* Doesn't stop JVM from exiting
* setDaemon(true)
E.g. Java Garbage Collector

### Non Daemon
* Default thread type
* Blocks JVM from exiting
* Program ends when all Daemon threads complete

E.g. main thread is non daemon

### Thread Lifecycle

* At beginning, Thread will be in **New state**
* `start()` will change Thread to **Runnable state**
* Code in `run()` methods get executed and Thread is **Running state**
* Can switch to **Waiting state** for other Thread to complete the task. Done using `wait()`
* notify() method to continue execution
* sometimes wait can be timed like Sleep for 1000ms
* Dead state when execution is complete

### Thread State

* name, alive/dead, execution state, priority, daemon or non daemon
* Execution State - NEW, RUNNABLE, BLOCKED, WAITING, TIMED_WAITING, TERMINATED

### Synchronization

* solves race condition 
* ensure thread safely update shared variable
* Syncronized code is called Critical section

#### How Synchronization works 

* JVM supports Synchronization via Monitors. Every job object is associated with a monitor. 
* Monitor is a mutual exclusion construct that prevents multiple threads from concurrently entering critical section
* Before thread enters critical section, it must get a lock from monitor
* If monitor is already locked, Thread will go to BLOCKED state
* When thread gets access to critical section, shared variables are copied to thread's working memory & will be written back to main memory once thread complete exection


* When syncronized keyword added to static method, lock is on java.lang.Class object


### Thread Notify

* notifyAll() - notifies all threads that are in waiting state. Uses object condition queue
