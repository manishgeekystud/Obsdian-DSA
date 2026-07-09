## What is an Exception?

An **Exception** is an **event (or object)** that occurs during the execution of a program and disrupts the normal flow of instructions.

In Java, an exception is represented as an **object** created by the JVM or explicitly by the programmer. All exceptions inherit from the `Throwable` class.

> **Interview Definition (30 seconds):**
> 
> "An exception is an object that represents an abnormal condition occurring during program execution. When an exception occurs, Java interrupts the normal execution flow and transfers control to an appropriate exception handler (`catch` block). If no handler is found, the program terminates and the JVM prints the stack trace."