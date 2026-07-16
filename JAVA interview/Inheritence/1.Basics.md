# What is Inheritance?

**Definition:**

> **Inheritance is a mechanism in Java where one class acquires the properties (fields) and behaviors (methods) of another class.**

It allows a class to **reuse existing code** instead of writing it again.

Java uses the **`extends`** keyword for class inheritance.

---

# Real-Life Example

Think of a **Parent and Child**.

```
Parent
 ├── House
 ├── Car
 ├── Money

        ↓

Child inherits all these properties
```

Similarly in Java,

```
Animal
 ├── eat()
 ├── sleep()

        ↓

Dog
 ├── bark()
```

The `Dog` class automatically gets `eat()` and `sleep()` from `Animal`.

---

# Syntax

```
class Parent {

}

class Child extends Parent {

}
```

Here,

- `Parent` → Superclass / Base Class
- `Child` → Subclass / Derived Class

---

# Example 1

```
class Animal {

    void eat() {
        System.out.println("Animal is eating");
    }
}

class Dog extends Animal {

    void bark() {
        System.out.println("Dog is barking");
    }
}

public class Main {

    public static void main(String[] args) {

        Dog d = new Dog();

        d.eat();   // inherited
        d.bark();  // own method
    }
}
```

### Output

```
Animal is eating
Dog is barking
```

---

# Memory Representation

```
            Animal
          +---------+
          | eat()   |
          +---------+
               ▲
               |
        extends|
               |
            Dog
          +---------+
          | bark()  |
          +---------+
```

The `Dog` object can access both:

- `eat()`
- `bark()`

---

# Why Do We Need Inheritance?

Without inheritance:

```
class Dog {

    void eat() { }

    void sleep() { }
}

class Cat {

    void eat() { }

    void sleep() { }
}
```

Code is duplicated.

With inheritance:

```
class Animal {

    void eat() { }

    void sleep() { }
}

class Dog extends Animal {

}

class Cat extends Animal {

}
```

One copy of common code is shared.

---

# Advantages

### 1. Code Reusability

Write common code once.

```
class Employee {

    void login() { }
}
```

All employee types can reuse it.

---

### 2. Reduces Code Duplication

Common methods stay in the parent.

---

### 3. Easier Maintenance

If you change the parent method,

```
class Animal {

    void eat() { }
}
```

every child automatically gets the updated behavior.

---

### 4. Supports Method Overriding

Child classes can provide specialized implementations.

# Types of Inheritance in Java

> **Interview Frequency:** ⭐⭐⭐⭐⭐ (Very Frequently Asked)

Inheritance defines how one class acquires the properties and methods of another class.

Java supports **5 types of inheritance conceptually**, but only **3 are directly supported using classes**.

---

# Types of Inheritance

|Type|Supported in Java (Classes)?|
|---|---|
|Single Inheritance|✅ Yes|
|Multilevel Inheritance|✅ Yes|
|Hierarchical Inheritance|✅ Yes|
|Multiple Inheritance|❌ No (with classes)|
|Hybrid Inheritance|❌ Not with classes (possible using interfaces)|

---

# 1. Single Inheritance

## Definition

One child class inherits from one parent class.

```
        Animal
           ▲
           │
          Dog
```

- `Animal` → Parent class
- `Dog` → Child class

---

## Java Example

```
class Animal {

    void eat() {
        System.out.println("Animal is eating");
    }
}

class Dog extends Animal {

    void bark() {
        System.out.println("Dog is barking");
    }
}

public class Main {

    public static void main(String[] args) {

        Dog d = new Dog();

        d.eat();   // Inherited method
        d.bark();  // Own method
    }
}
```

### Output

```
Animal is eating
Dog is barking
```

---

## Memory Diagram

```
           Animal
        +-----------+
        | eat()     |
        +-----------+
              ▲
              │ extends
              │
            Dog
        +-----------+
        | bark()    |
        +-----------+
```

---

## Real-Life Example

```
Vehicle
   ▲
   │
 Car
```

A **Car is a Vehicle**.

---

# 2. Multilevel Inheritance

## Definition

A child class becomes the parent of another class.

```
        Animal
           ▲
           │
          Dog
           ▲
           │
         Puppy
```

`Puppy` inherits from `Dog`, and `Dog` inherits from `Animal`.

---

## Java Example

```
class Animal {

    void eat() {
        System.out.println("Eating");
    }
}

class Dog extends Animal {

    void bark() {
        System.out.println("Barking");
    }
}

class Puppy extends Dog {

    void weep() {
        System.out.println("Weeping");
    }
}

public class Main {

    public static void main(String[] args) {

        Puppy p = new Puppy();

        p.eat();
        p.bark();
        p.weep();
    }
}
```

### Output

```
Eating
Barking
Weeping
```

---

## Memory Diagram

```
          Animal
             ▲
             │
            Dog
             ▲
             │
           Puppy
```

`Puppy` can access methods from both `Dog` and `Animal`.

---

## Constructor Execution

```
new Puppy();
```

Execution order:

```
Animal()
↓

Dog()
↓

Puppy()
```

Parent constructors execute before child constructors.

---

# 3. Hierarchical Inheritance

## Definition

Multiple child classes inherit from one parent class.

```
             Animal
          /     |     \
        Dog    Cat    Cow
```

---

## Java Example

```
class Animal {

    void eat() {
        System.out.println("Eating");
    }
}

class Dog extends Animal {

    void bark() {
        System.out.println("Bark");
    }
}

class Cat extends Animal {

    void meow() {
        System.out.println("Meow");
    }
}

class Cow extends Animal {

    void moo() {
        System.out.println("Moo");
    }
}

public class Main {

    public static void main(String[] args) {

        Dog d = new Dog();
        Cat c = new Cat();
        Cow cw = new Cow();

        d.eat();
        d.bark();

        c.eat();
        c.meow();

        cw.eat();
        cw.moo();
    }
}
```

### Output

```
Eating
Bark
Eating
Meow
Eating
Moo
```

---

## Memory Diagram

```
                 Animal
             +-----------+
             | eat()     |
             +-----------+
              ▲    ▲    ▲
              │    │    │
            Dog   Cat  Cow
```

All child classes reuse the `eat()` method.

---

# 4. Multiple Inheritance (Not Supported with Classes)

## Definition

One child class inherits from more than one parent class.

```
        A
      /   \
     B     C
      \   /
        D
```

This is **not allowed** with Java classes.

---

## Invalid Java Code

```
class A {

}

class B {

}

class C extends A, B {

}
```

### Result

```
Compilation Error
```

---

## Why is Multiple Inheritance Not Supported?

Because of the **Diamond Problem**.

Suppose:

```
class A {

    void show() {
        System.out.println("A");
    }
}

class B extends A {

    @Override
    void show() {
        System.out.println("B");
    }
}

class C extends A {

    @Override
    void show() {
        System.out.println("C");
    }
}
```

If Java allowed:

```
class D extends B, C {

}
```

Then:

```
D d = new D();
d.show();
```

Which `show()` should execute?

- `B.show()`?
- `C.show()`?

The compiler cannot decide.

This ambiguity is called the **Diamond Problem**.

Java avoids it by disallowing multiple inheritance with classes.

---

# 5. Hybrid Inheritance

## Definition

A combination of two or more inheritance types.

Example:

```
            A
          /   \
         B     C
          \
           D
```

This combines:

- Hierarchical inheritance
- Multiple inheritance

---

## Supported?

- ❌ Not with classes.
- ✅ Possible using interfaces.

Example:

```
interface A {
    void display();
}

interface B {
    void print();
}

class C implements A, B {

    public void display() {
        System.out.println("Display");
    }

    public void print() {
        System.out.println("Print");
    }
}
```

Here, `C` implements multiple interfaces without ambiguity.

---

# Comparison Table

|Type|Structure|Java Classes|Example|
|---|---|---|---|
|Single|A → B|✅|`Dog extends Animal`|
|Multilevel|A → B → C|✅|`Puppy extends Dog`|
|Hierarchical|A → B, C, D|✅|`Dog`, `Cat`, `Cow` extend `Animal`|
|Multiple|A & B → C|❌|Not allowed|
|Hybrid|Combination|❌ (classes) / ✅ (interfaces)|Multiple interfaces|

---

# Interview Questions

### 1. How many types of inheritance are there in Java?

Conceptually, there are **5 types**:

- Single
- Multilevel
- Hierarchical
- Multiple
- Hybrid

Using **classes**, Java supports only:

- Single
- Multilevel
- Hierarchical

---

### 2. Why is Multiple Inheritance not supported?

To avoid the **Diamond Problem**, where the compiler cannot determine which parent class implementation should be inherited.

---

### 3. Can Java achieve Multiple Inheritance?

Yes, using **interfaces**.

Example:

```
interface Camera {
    void click();
}

interface MusicPlayer {
    void playMusic();
}

class SmartPhone implements Camera, MusicPlayer {

    public void click() {
        System.out.println("Photo clicked");
    }

    public void playMusic() {
        System.out.println("Playing music");
    }
}
```

---

### 4. Which inheritance type is most commonly used?

**Single Inheritance** is the most common because it is simple, avoids ambiguity, and models straightforward **is-a** relationships.

---

### 5. Which inheritance type is used in frameworks?

Frameworks such as Spring and Hibernate often use:

- **Single inheritance** for extending base classes.
- **Interfaces** for achieving flexibility similar to multiple inheritance.

---

# Interview Tip

A very common interview question is:

> **Why does Java support multiple inheritance through interfaces but not through classes?**

**Answer:**

- A class can inherit implementation from only one parent class to avoid the Diamond Problem.
- Interfaces mainly define contracts (method declarations), so a class can safely implement multiple interfaces. If two interfaces provide the same default method, Java requires the implementing class to explicitly override it, removing ambiguity.