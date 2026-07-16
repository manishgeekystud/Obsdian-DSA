
# IS-A Relationship in Java

> **Interview Frequency:** ⭐⭐⭐⭐⭐ (Very Frequently Asked)

The **IS-A relationship** is the fundamental concept behind **Inheritance**.

It answers the question:

> **"Can one object be considered another object?"**

If the answer is **Yes**, then inheritance is appropriate.

---

# Definition

An **IS-A relationship** means that a **child class is a specialized type of the parent class**.

The child class inherits the properties and methods of the parent class.

In Java, the **`extends`** keyword represents an **IS-A relationship**.

---

# Syntax

```
class Parent {

}

class Child extends Parent {

}
```

Here,

```
Child IS-A Parent
```

---

# Example 1

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

public class Main {

    public static void main(String[] args) {

        Dog dog = new Dog();

        dog.eat();   // Inherited
        dog.bark();  // Own method
    }
}
```

### Output

```
Eating
Barking
```

---

# Relationship

```
Animal
   ▲
   │
 Dog
```

We say:

```
Dog IS-A Animal
```

because every Dog is an Animal.

---

# More Examples

|Child Class|Parent Class|IS-A Relationship|
|---|---|---|
|Dog|Animal|Dog IS-A Animal|
|Cat|Animal|Cat IS-A Animal|
|Car|Vehicle|Car IS-A Vehicle|
|Student|Person|Student IS-A Person|
|Manager|Employee|Manager IS-A Employee|

---

# Memory Diagram

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

A `Dog` object contains:

- `eat()` (Inherited)
- `bark()` (Own method)

---

# Why IS-A Relationship is Important?

It enables **code reuse**.

Instead of writing common methods in every class,

```
class Animal {

    void eat() {
        System.out.println("Eating");
    }

    void sleep() {
        System.out.println("Sleeping");
    }
}

class Dog extends Animal {

}

class Cat extends Animal {

}
```

Both `Dog` and `Cat` automatically inherit `eat()` and `sleep()`.

---

# IS-A Enables Polymorphism

```
Animal a = new Dog();
```

Why is this valid?

Because:

```
Dog IS-A Animal
```

A `Dog` object can be referenced using an `Animal` reference.

Example:

```
class Animal {

    void sound() {
        System.out.println("Animal Sound");
    }
}

class Dog extends Animal {

    @Override
    void sound() {
        System.out.println("Bark");
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
Bark
```

This is **Runtime Polymorphism (Method Overriding)**.

---

# Invalid IS-A Relationship

Consider:

```
class Engine {

}

class Car extends Engine {

}
```

This is **incorrect**.

Ask yourself:

> **Is a Car an Engine?**

Answer:

```
No
```

A car **has** an engine, but it **is not** an engine.

So inheritance is not appropriate here.

---

# Common Interview Trick

Which is correct?

```
Dog IS-A Animal
```

✅ Correct

```
Animal IS-A Dog
```

❌ Incorrect

Every Dog is an Animal, but not every Animal is a Dog.

---

# Difference Between IS-A and HAS-A
# Comparison Table

| Feature                    | IS-A                  | HAS-A                          |
| -------------------------- | --------------------- | ------------------------------ |
| Meaning                    | Inheritance           | Composition                    |
| Keyword                    | `extends`             | Object Reference               |
| Relationship               | Child is a Parent     | Object contains another Object |
| Code Reuse                 | Through inheritance   | Through object composition     |
| Coupling                   | Tighter               | Looser                         |
| Flexibility                | Less                  | More                           |
| Supports Polymorphism      | ✅ Yes                 | Indirectly                     |
| Preferred in Modern Design | Only when appropriate | ✅ Often preferred              |
### HAS-A Example

```
class Engine {

    void start() {
        System.out.println("Engine Started");
    }
}

class Car {

    Engine engine = new Engine();

    void drive() {
        engine.start();
        System.out.println("Car is moving");
    }
}
```

Relationship:

```
Car HAS-A Engine
```

---

# How to Decide?

Ask yourself:

### Question

> **Can I say "X is a Y"?**

If **Yes**

↓

Use **Inheritance**.

Example:

```
Dog IS-A Animal
```

If **No**

↓

Use **Composition (HAS-A)**.

Example:

```
Car HAS-A Engine
```

---

# Interview Questions

### 1. What is an IS-A relationship?

An IS-A relationship represents **inheritance**, where a child class is a specialized form of the parent class and inherits its properties and methods.

---

### 2. How is IS-A implemented in Java?

Using the `extends` keyword for classes (or `implements` for interfaces).

---

### 3. Why is `Animal a = new Dog();` valid?

Because **Dog IS-A Animal**, so a `Dog` object can be assigned to an `Animal` reference.

---

### 4. Give an example where inheritance should not be used.

`Car` and `Engine`.

A car is **not** an engine; it **has** an engine.

This is a **HAS-A** relationship, so composition should be used.

---

# Interview Tip ⭐⭐⭐⭐⭐

Whenever you're deciding between **Inheritance** and **Composition**, ask this simple question:

```
Can I naturally say:

Child IS-A Parent ?
```

- ✅ **Dog IS-A Animal** → Use **Inheritance**
- ✅ **Manager IS-A Employee** → Use **Inheritance**
- ❌ **Car IS-A Engine** → Wrong → Use **Composition (HAS-A)**

**Rule to Remember:**

> **IS-A → Inheritance (`extends`)**  
> **HAS-A → Composition (object/member variable)**