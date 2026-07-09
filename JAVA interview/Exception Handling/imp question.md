## 
**1.What is an Exception?**

An **Exception** is an **event (or object)** that occurs during the execution of a program and disrupts the normal flow of instructions.

In Java, an exception is represented as an **object** created by the JVM or explicitly by the programmer. All exceptions inherit from the `Throwable` class.

> **Interview Definition (30 seconds):**
> 
> "An exception is an object that represents an abnormal condition occurring during program execution. When an exception occurs, Java interrupts the normal execution flow and transfers control to an appropriate exception handler (`catch` block). If no handler is found, the program terminates and the JVM prints the stack trace."

**2.Exception Heirarchy**

The Java Exception Hierarchy is built around the **`Throwable`** class.
```
                    Object
                       |
                 Throwable
                /          \
             Error       Exception
                            |
                    RuntimeException
                            |
         ------------------------------------
         |         |         |             |
NullPointer  Arithmetic  ArrayIndex   IllegalArgument
Exception    Exception   OutOfBounds  Exception
                          Exception
```
```
// A more detailed hierarchy:
java.lang.Object
        |
        +-- java.lang.Throwable
                |
                +-- java.lang.Error
                |      |
                |      +-- VirtualMachineError
                |      |      +-- OutOfMemoryError
                |      |      +-- StackOverflowError
                |      |
                |      +-- LinkageError
                |      +-- AssertionError
                |
                +-- java.lang.Exception
                       |
                       +-- IOException
                       |      |
                       |      +-- FileNotFoundException
                       |      +-- EOFException
                       |
                       +-- SQLException
                       |
                       +-- ClassNotFoundException
                       |
                       +-- InterruptedException
                       |
                       +-- ParseException
                       |
                       +-- RuntimeException
                              |
                              +-- NullPointerException
                              +-- ArithmeticException
                              +-- ArrayIndexOutOfBoundsException
                              +-- StringIndexOutOfBoundsException
                              +-- NumberFormatException
                              +-- IllegalArgumentException
                              +-- IllegalStateException
                              +-- ClassCastException
                              +-- UnsupportedOperationException
```
Errors indicate **serious problems** in the JVM.

They are **not intended to be handled** by application code.

Examples:

- OutOfMemoryError
- StackOverflowError
- VirtualMachineError
- LinkageError

3. **checked vs unchecked exception?**

Java exceptions are divided into two categories:

```
Throwable
    |
    +-- Exception
            |
            +-- Checked Exceptions
            |       |
            |       +-- IOException
            |       +-- SQLException
            |       +-- ClassNotFoundException
            |       +-- InterruptedException
            |
            +-- RuntimeException (Unchecked)
                    |
                    +-- NullPointerException
                    +-- ArithmeticException
                    +-- ArrayIndexOutOfBoundsException
                    +-- NumberFormatException
                    +-- IllegalArgumentException
```
# What is a Checked Exception?

A **Checked Exception** is an exception that the **Java compiler checks at compile time**.

If code can throw a checked exception, you **must** either:

- Handle it using `try-catch`, or
- Declare it using the `throws` keyword.

Otherwise, the program will not compile
```java
import java.io.FileReader;

public class Demo {
    public static void main(String[] args) {
        FileReader fr = new FileReader("data.txt");
    }
}


o/p:-Unhandled exception type FileNotFoundException
```
# Handling a Checked Exception

### Using try-catch
```java
import java.io.*;

public class Demo {
    public static void main(String[] args) {

        try {
            FileReader fr = new FileReader("data.txt");
        } catch (FileNotFoundException e) {
            System.out.println("File not found.");
        }

    }
}
```
**Using throws**
```java
import java.io.*;

public class Demo {

    public static void readFile() throws IOException {
        FileReader fr = new FileReader("data.txt");
    }

}
```
Here, the responsibility of handling the exception is transferred to the caller.
# Common Checked Exceptions

| Exception                | When It Occurs               |
| ------------------------ | ---------------------------- |
| `IOException`            | Input/output operations fail |
| `FileNotFoundException`  | File does not exist          |
| `SQLException`           | Database-related errors      |
| `ClassNotFoundException` | Class cannot be located      |
| `InterruptedException`   | Thread interruption          |
| `ParseException`         | Parsing invalid input        |
==**What is an Unchecked Exception?**==

An **Unchecked Exception** is an exception that the compiler **does not check** during compilation.

These exceptions occur **at runtime**.
The compiler does **not** force you to handle them.
They are subclasses of `RuntimeException`.


