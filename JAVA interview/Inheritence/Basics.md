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

