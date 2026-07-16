# Method Overloading

## Definition

**Method Overloading** means **having multiple methods with the same name in the same class but with different parameter lists.**

The compiler decides **which method to call** based on the method signature.

---

## Rules

Methods must differ by at least one of the following:

- Number of parameters
- Type of parameters
- Order of parameters

The following **do not** create overloading by themselves:

- Return type only
- Access modifier only
- `throws` clause only

---

## Example 1: Different Number of Parameters

```
class Calculator {

    int add(int a, int b) {
        return a + b;
    }

    int add(int a, int b, int c) {
        return a + b + c;
    }
}
```

---

## Example 2: Different Data Types

```
class Calculator {

    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
    }
}
```

---

## Example 3: Different Parameter Order

```
class Demo {

    void show(int a, String b) {
        System.out.println("Method 1");
    }

    void show(String b, int a) {
        System.out.println("Method 2");
    }
}
```

---

## Invalid Overloading

Changing only the return type is **not allowed**.

```
class Demo {

    int add(int a, int b) {
        return a + b;
    }

    // Compilation Error
    double add(int a, int b) {
        return a + b;
    }
}
```

### Why?

Because the compiler identifies methods using:

```
Method Name + Parameter List
```

The return type is **not** part of the method signature.

---

## Memory Representation

```
Calculator
│
├── add(int,int)
│
├── add(int,int,int)
│
└── add(double,double)
```

The compiler chooses the correct method during compilation.

---

# Method Overriding

## Definition

**Method Overriding** occurs when a child class provides its **own implementation** of a method already defined in the parent class.

The decision is made **at runtime** based on the actual object.

---

## Rules

- Parent and child classes are required.
- Method name must be the same.
- Parameters must be the same.
- Return type must be the same or covariant.
- Access modifier cannot be more restrictive.
- `final`, `private`, and `static` methods cannot be overridden (`static` methods are hidden, not overridden).

---

## Example

```
class Animal {

    void sound() {
        System.out.println("Animal Sound");
    }
}

class Dog extends Animal {

    @Override
    void sound() {
        System.out.println("Dog Barks");
    }
}

public class Main {

    public static void main(String[] args) {

        Animal a = new Dog();

        a.sound();
    }
}
```

### Output

```
Dog Barks
```

---

## Runtime Memory Representation

```
Reference Type      Object Created

Animal  --------->  Dog Object
                        │
                        ▼
                 sound() -> Dog's version
```

Although the reference is `Animal`, the actual object is `Dog`, so the overridden method executes.

---

# Why Overriding?

Suppose all animals make different sounds.

Instead of writing different method names:

```
dogSound();
catSound();
cowSound();
```

we use one common method:

```
sound();
```

Each child class provides its own implementation.

---

## Another Example

```
class Shape {

    void draw() {
        System.out.println("Drawing Shape");
    }
}

class Circle extends Shape {

    @Override
    void draw() {
        System.out.println("Drawing Circle");
    }
}

class Rectangle extends Shape {

    @Override
    void draw() {
        System.out.println("Drawing Rectangle");
    }
}
```

Now:

```
Shape s = new Circle();
s.draw();
```

Output:

```
Drawing Circle
```

---

# Difference Between Overloading and Overriding

|Feature|Method Overloading|Method Overriding|
|---|---|---|
|Definition|Same method name with different parameter list|Child class provides a new implementation of the parent's method|
|Polymorphism|Compile-time (Static)|Runtime (Dynamic)|
|Decision Made|By compiler|By JVM at runtime|
|Inheritance Required|❌ No|✅ Yes|
|Method Name|Same|Same|
|Parameters|Must be different|Must be the same|
|Return Type|Can differ, but not **only** by return type|Same or covariant|
|Access Modifier|Any|Cannot be more restrictive than parent|
|`static` Methods|Can be overloaded|Cannot be overridden (hidden instead)|
|`final` Methods|Can be overloaded|Cannot be overridden|
|`private` Methods|Can be overloaded within the same class|Cannot be overridden|
|Annotation|Not required|`@Override` is recommended|
|Binding|Early Binding|Late Binding|

---

# Quick Comparison

### Overloading

```
class Demo {

    void show() { }

    void show(int x) { }

    void show(String s) { }
}
```

Compiler decides which `show()` to call.

---

### Overriding

```
class Animal {

    void sound() {
        System.out.println("Animal");
    }
}

class Dog extends Animal {

    @Override
    void sound() {
        System.out.println("Dog");
    }
}
```

JVM decides at runtime which `sound()` to execute.

---

# Common Interview Questions

### 1. Can we overload the `main()` method?

✅ Yes.

```
public static void main(String[] args) { }

public static void main(int x) { }
```

Only `main(String[] args)` is used as the program entry point.

---

### 2. Can constructors be overloaded?

✅ Yes.

```
class Student {

    Student() { }

    Student(int id) { }

    Student(int id, String name) { }
}
```

---

### 3. Can constructors be overridden?

❌ No.

Constructors are **not inherited**, so they cannot be overridden.

---

### 4. Can static methods be overridden?

❌ No.

They are **method hidden**, not overridden.

```
class Parent {

    static void show() {
        System.out.println("Parent");
    }
}

class Child extends Parent {

    static void show() {
        System.out.println("Child");
    }
}
```

The method called depends on the **reference type**, not the object.

---

### 5. Can private methods be overridden?

❌ No.

Private methods are not visible to child classes.

---

### 6. Can we overload static methods?

✅ Yes.

```
class Demo {

    static void display() { }

    static void display(int x) { }
}
```

---

### 7. Can we overload methods by changing only the return type?

❌ No.

```
int add(int a, int b) { }

double add(int a, int b) { } // Compilation Error
```

---

### 8. What is the difference between Early Binding and Late Binding?

- **Early Binding (Compile-time Binding):** The compiler determines which method to call. This happens in **method overloading**.
- **Late Binding (Runtime Binding):** The JVM determines which method to call based on the actual object. This happens in **method overriding**.

---

# Best Practices

- Use **overloading** when methods perform the same logical operation with different kinds or numbers of inputs.
- Use **overriding** when a child class needs specialized behavior while keeping the same method contract.
- Always use the `@Override` annotation when overriding—it helps the compiler catch mistakes.
- Avoid overloading methods with signatures that are too similar, as it can make code harder to read.

---

# Interview Tip ⭐⭐⭐⭐⭐

A simple way to remember the difference:

|If you hear...|Think...|
|---|---|
|**Same class, different parameters**|**Method Overloading**|
|**Parent and Child, same method implementation changed**|**Method Overriding**|
# What is Runtime Polymorphism?

Runtime polymorphism happens when a **parent reference** points to a **child object**, and the JVM decides **at runtime** which overridden method to execute.

Example:

```
Animal a = new Dog();

a.sound();
```

Output

```
Dog Barks
```

Why?

Because at runtime the JVM sees that:

```
Reference → Animal

Object → Dog
```

So it executes

```
Dog.sound()
```

This behavior is **Runtime Polymorphism**.

---

# Visual Diagram

```
          Animal
             ▲
             │
            Dog

Animal a = new Dog();

        │
        ▼
JVM checks actual object

Dog

↓

Calls Dog.sound()
```

---

# Interview Question

### Is this Runtime Polymorphism?

```
Dog d = new Dog();

d.sound();
```

**Answer:**

❌ **No.**

Although `sound()` is overridden, there is **no polymorphism** here because both the **reference type** and **object type** are `Dog`.

The compiler already knows which method will be called.

---

### Is this Runtime Polymorphism?

```
Animal a = new Dog();

a.sound();
```

**Answer:**

✅ **Yes.**

The reference is `Animal`, but the object is `Dog`.

The JVM decides at runtime which method to execute.

---

# Comparison

|Method Overriding|Runtime Polymorphism|
|---|---|
|A programming technique|A runtime behavior|
|Child redefines parent's method|JVM chooses overridden method at runtime|
|Happens while writing the class|Happens when the program runs|
|Required for runtime polymorphism|Achieved because of method overriding|

---

# Interview Answer (Best Answer)

> **Method Overriding and Runtime Polymorphism are closely related but not identical. Method Overriding is the mechanism where a child class provides its own implementation of a parent method. Runtime Polymorphism is the behavior where the JVM selects the appropriate overridden method at runtime based on the actual object. In other words, method overriding enables runtime polymorphism.**

---

## Easy Memory Trick ⭐⭐⭐⭐⭐

```
Method Overriding
        ↓
Creates
        ↓
Runtime Polymorphism
```

Remember:

- **Overriding = Code you write**
- **Runtime Polymorphism = Behavior the JVM performs**