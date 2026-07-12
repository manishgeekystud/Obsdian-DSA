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

```java
public class Demo {

    public static void main(String[] args) {

        String name = null;

        System.out.println(name.length());

    }

}
```
Compilation succeeds.

At runtime:

```java
Exception in thread "main"
java.lang.NullPointerException
```

# Comparison Table

| Feature                           | Checked Exception   | Unchecked Exception |
| --------------------------------- | ------------------- | ------------------- |
| Compiler Checks                   | ✅ Yes               | ❌ No                |
| Detected                          | Compile time        | Runtime             |
| Must Handle                       | ✅ Yes               | ❌ No                |
| Parent Class                      | `Exception`         | `RuntimeException`  |
| Program Compiles Without Handling | ❌ No                | ✅ Yes               |
| Represents                        | External conditions | Programming bugs    |
| Recovery Expected                 | Usually             | Sometimes           |
### 1. Can we have a try block without catch?

**Yes**, if there is a `finally`.

```
try {
    System.out.println("Hello");
}
finally {
    System.out.println("Cleanup");
}
```

---

### 2. Can we have a catch without try?

**No.** A `catch` block must always follow a `try` block.

---

### 3. Can we have multiple catch blocks?

**Yes.**

```
try {

}
catch(IOException e){

}
catch(SQLException e){

}
```

---

### 4. Can we have multiple finally blocks?

**No.** Only one `finally` block can be associated with a `try`.

---

### 5. Does finally always execute?

**Almost always.** It executes whether an exception occurs or not, except in situations like `System.exit(0)`, JVM crashes, or forced process termination.

---

### 6. What happens if an exception occurs inside the catch block?

It propagates unless it is handled by another surrounding `try-catch`.

Example:

```
try {
    int x = 10 / 0;
}
catch (ArithmeticException e) {
    String s = null;
    System.out.println(s.length()); // New NullPointerException
}
```

The new `NullPointerException` is **not** handled by the same `catch`; it propagates unless there is an outer handler.

---

### 7. Can we return from try, catch, and finally?

Yes, but returning from `finally` is discouraged because it overrides returns from `try` or `catch` and can even suppress exceptions.

---

# One-Minute Interview Revision

| Block     | Purpose                     | Executes When                                              |
| --------- | --------------------------- | ---------------------------------------------------------- |
| `try`     | Contains risky code         | Always entered first                                       |
| `catch`   | Handles matching exceptions | Only if a matching exception occurs                        |
| `finally` | Cleanup code                | Almost always, regardless of whether an exception occurred |

### Execution Order

```
try
 ↓
Exception?
 ↓
catch (if matched)
 ↓
finally
 ↓
Program continues (or exception propagates if unhandled)
```

### Interview Tip

If asked, **"Which block is guaranteed to execute?"**, answer:

> **`finally` is designed to execute regardless of whether an exception occurs or is caught, making it the preferred place for cleanup logic. The main exceptions are when the JVM exits abruptly (for example, via `System.exit(0)`) or crashes.**

==**Throw vs Throws?**==

# Throw vs Throws in Java (Complete Interview Guide)

One of the most common Java interview questions is:

> **What is the difference between `throw` and `throws`?**

Although their names are similar, they serve **completely different purposes**.

- **`throw`** is used to **explicitly create and throw an exception object**.
- **`throws`** is used in a **method declaration** to indicate that the method may pass an exception to its caller.

---

# Quick Comparison

|Feature|`throw`|`throws`|
|---|---|---|
|Purpose|Explicitly throws an exception|Declares possible exceptions|
|Used In|Method body|Method signature|
|Followed By|Exception object|Exception class(es)|
|Number Allowed|One exception object at a time|Multiple exception classes|
|Used With|Checked & Unchecked exceptions|Mainly checked exceptions|
|Responsibility|Creates/throws exception|Passes handling responsibility to caller|

---

# Visual Difference

``
                    Exception Handling

          throw                      throws
             |                          |
    Inside Method Body         Method Declaration
             |                          |
    Throws Exception Object    Declares Exception Types
```

---

# What is `throw`?

The `throw` keyword is used to **manually throw an exception**.

### Syntax

```
throw new ExceptionType("Message");
```

---

## Example 1: Throwing an ArithmeticException

```
public class Demo {

    public static void main(String[] args) {

        throw new ArithmeticException("Division by zero");

    }

}
```

### Output

```
Exception in thread "main"
java.lang.ArithmeticException: Division by zero
```

---

# How JVM Executes `throw`

```
throw new ArithmeticException("Invalid");
```java

### Execution Steps

|Step|Action|
|---|---|
|1|Create `ArithmeticException` object|
|2|Store message inside object|
|3|JVM throws the object|
|4|JVM searches for matching `catch`|
|5|If not found, program terminates|

---

# Memory Representation

```
Stack

main()
   |
throw new ArithmeticException()

           |
           V

Heap
+---------------------------+
| ArithmeticException       |
| Message = "Invalid"       |
+---------------------------+
```

The exception object is created on the **heap**, and the reference is thrown.

---

# Example 2: Throw with try-catch

```
public class Demo {

    public static void main(String[] args) {

        try {

            throw new ArithmeticException("Invalid Division");

        }

        catch (ArithmeticException e) {

            System.out.println(e.getMessage());

        }

    }

}
```

### Output

```
Invalid Division
```

---

# Throwing a Custom Exception

```
public class Demo {

    static void validateAge(int age) {

        if(age < 18) {

            throw new IllegalArgumentException("Not Eligible");

        }

        System.out.println("Eligible");

    }

    public static void main(String[] args) {

        validateAge(15);

    }

}
```

Output

```
Exception in thread "main"
java.lang.IllegalArgumentException: Not Eligible
```

---

# What is `throws`?

The `throws` keyword is used to **declare** that a method may throw one or more exceptions.

It does **not** throw an exception itself.

### Syntax

```
returnType methodName() throws ExceptionType {

}
```

---

# Example

```
import java.io.*;

public class Demo {

    static void readFile() throws IOException {

        FileReader fr = new FileReader("abc.txt");

    }

}
```

Here:

- `readFile()` may throw `IOException`.
- The caller must handle it or declare it again.

---

# Flow of `throws`

```
readFile()

        |
        V

throws IOException

        |
        V

Caller

Handle?
  /      \
Yes      No
 |         |
Continue  Compilation Error
```

---

# Complete Example

```
import java.io.*;

public class Demo {

    static void readFile() throws IOException {

        FileReader fr = new FileReader("abc.txt");

    }

    public static void main(String[] args) {

        try {

            readFile();

        }

        catch(IOException e){

            System.out.println("Handled");

        }

    }

}
```

Output

```
Handled
```

---

# Multiple Exceptions with `throws`

A method can declare multiple exception types.

```
public void process()
        throws IOException,
               SQLException,
               ClassNotFoundException {

}
```

---

# Can `throw` Throw Checked Exceptions?

Yes.

```
import java.io.IOException;

public class Demo {

    static void test() throws IOException {

        throw new IOException("File Missing");

    }

}
```

Since `IOException` is checked, the method must declare it with `throws` or handle it with `try-catch`.

---

# Can `throw` Throw Runtime Exceptions?

Yes.

```
throw new NullPointerException();
```

No `throws` declaration is required because `NullPointerException` is unchecked.

---

# Dry Run

```
public class Demo {

    static void checkAge(int age) {

        if(age < 18)

            throw new ArithmeticException();

        System.out.println("Eligible");

    }

    public static void main(String[] args) {

        checkAge(15);

    }

}
```

### Execution Table

|Step|Statement|Result|
|---|---|---|
|1|`main()`|Starts|
|2|`checkAge(15)`|Called|
|3|`15 < 18`|True|
|4|`throw new ArithmeticException()`|Exception created|
|5|Search for `catch`|Not found|
|6|Program terminates|Stack trace printed|

---

# `throw` vs `throws` (Side-by-Side)

## `throw`

```
throw new IOException();
```

- Creates an exception object.
- Immediately transfers control to the exception-handling mechanism.

---

## `throws`

```
void read() throws IOException {

}
```

- Declares that the method may throw an exception.
- Shifts handling responsibility to the caller.

---

# Flow Diagram

```
                  Method

         +--------------------+
         |                    |
         | throw Exception    |
         |                    |
         +--------------------+
                   |
              Exception Object
                   |
             Search catch block


         +--------------------+
         |                    |
         | throws IOException |
         |                    |
         +--------------------+
                   |
          Caller Handles Later
```

---

# Common Mistakes

### ❌ Using an exception class with `throw`

Wrong:

```
throw IOException;
```

Correct:

```
throw new IOException();
```

`throw` requires an **exception object**, not a class name.

---

### ❌ Using an object with `throws`

Wrong:

```
public void test() throws new IOException();
```

Correct:

```
public void test() throws IOException {
}
```

`throws` lists **exception classes**, not objects.

---

### ❌ Assuming `throws` actually throws an exception

`throws` only declares a possibility. The exception is thrown only if code inside the method executes a `throw` statement or calls another method that throws an exception.

---

# Best Practices

- Use **`throw`** when validating business rules or method arguments.

```
if (salary < 0) {
    throw new IllegalArgumentException("Salary cannot be negative");
}
```

- Use **`throws`** for checked exceptions that callers are expected to handle.

```
public void readFile() throws IOException {
}
```

- Prefer specific exception types instead of generic `Exception`.

---

# Interview Questions

### 1. What is the difference between `throw` and `throws`?

- `throw` explicitly throws an exception object.
- `throws` declares that a method may throw one or more exceptions.

---

### 2. Can we use `throw` without `throws`?

**Yes**, for unchecked exceptions.

```
throw new NullPointerException();
```

---

### 3. Can we use `throws` without `throw`?

**Yes**.

```
void read() throws IOException {

}
```

The method may call another method that throws the exception, or it may be implemented later.

---

### 4. Can `throws` declare multiple exceptions?

**Yes.**

```
void process()
throws IOException,
       SQLException,
       ParseException {

}
```

---

### 5. Can `throw` throw multiple exceptions at once?

**No.**

Only **one exception object** can be thrown by a single `throw` statement.

---

### 6. Does `throws` create an exception object?

**No.**

It only informs the compiler and the caller about possible exceptions.

---

### 7. Which keyword transfers responsibility to the caller?

**Answer:** `throws`

---

# One-Minute Interview Revision

|`throw`|`throws`|
|---|---|
|Used inside a method|Used in the method declaration|
|Throws an exception object|Declares exception classes|
|Immediate exception generation|Passes responsibility to the caller|
|Followed by `new Exception()`|Followed by exception class names|
|One exception object at a time|Can declare multiple exception types|

### Easy Way to Remember

- **`throw` → Action**: _"I am throwing an exception now."_
- **`throws` → Declaration**: _"This method might throw these exceptions, so the caller should be prepared."_
  
  

Custom Exceptions