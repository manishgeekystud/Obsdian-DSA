# `super` Keyword in Java (Interview Notes)

> **Interview Frequency:** ⭐⭐⭐⭐⭐ (Very Frequently Asked)

The **`super`** keyword is a reference variable that refers to the **immediate parent class object**.

It is mainly used to:

1. Access the parent class variable.
2. Call the parent class method.
3. Invoke the parent class constructor.

---

# Why Do We Need `super`?

Suppose both parent and child classes have the same variable or method name.

```
Parent
   |
 Child
```

Without `super`, Java accesses the child class member.

Using `super`, we can explicitly access the parent class member.

---

# Syntax

```
super.variableName;

super.methodName();

super();
```

---

# Uses of `super`

|Use|Purpose|
|---|---|
|`super.variable`|Access parent class variable|
|`super.method()`|Call parent class method|
|`super()`|Call parent class constructor|

---

# 1. Access Parent Class Variable

## Example

```
class Animal {

    String color = "White";
}

class Dog extends Animal {

    String color = "Black";

    void printColor() {

        System.out.println(color);        // Child variable
        System.out.println(super.color);  // Parent variable
    }
}

public class Main {

    public static void main(String[] args) {

        Dog d = new Dog();

        d.printColor();
    }
}
```

### Output

```
Black
White
```

---

# Memory Diagram

```
        Animal
       color = White
            ▲
            │
          Dog
       color = Black
```

```
color
```

↓

```
Black
```

```
super.color
```

↓

```
White
```

---

# 2. Call Parent Class Method

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
        System.out.println("Dog Bark");
    }

    void display() {

        sound();        // Child method
        super.sound();  // Parent method
    }
}
```

### Output

```
Dog Bark
Animal Sound
```

---

# Method Call Flow

```
display()

│

├── sound()

│       ↓

│   Dog.sound()

│

└── super.sound()

        ↓

    Animal.sound()
```

---

# 3. Call Parent Constructor

## Example

```
class Animal {

    Animal() {
        System.out.println("Animal Constructor");
    }
}

class Dog extends Animal {

    Dog() {

        super();

        System.out.println("Dog Constructor");
    }
}

public class Main {

    public static void main(String[] args) {

        new Dog();
    }
}
```

### Output

```
Animal Constructor
Dog Constructor
```

---

# Constructor Execution Order

```
new Dog()

↓

super()

↓

Animal()

↓

Dog()
```

The parent constructor always executes **before** the child constructor.

---

# Is `super()` Mandatory?

No.

If you don't write it explicitly, Java inserts it automatically.

Example:

```
class Dog extends Animal {

    Dog() {

        System.out.println("Dog");
    }
}
```

Compiler changes it internally to:

```
class Dog extends Animal {

    Dog() {

        super();

        System.out.println("Dog");
    }
}
```

---

# When Must We Write `super(...)`?

If the parent class **does not have a no-argument constructor**, you must explicitly call one of its constructors.

Example:

```
class Animal {

    Animal(String name) {
        System.out.println(name);
    }
}

class Dog extends Animal {

    Dog() {
        super("Tommy");
    }
}
```

If you omit `super("Tommy")`, the compiler tries to insert `super()`, which does not exist, causing a compilation error.

---

# Rules of `super()`

### Rule 1

`super()` must be the **first statement** in a constructor.

Correct:

```
Dog() {

    super();

    System.out.println("Dog");
}
```

Incorrect:

```
Dog() {

    System.out.println("Dog");

    super(); // Compilation Error
}
```

---

### Rule 2

`super()` can only be used inside a constructor.

---

### Rule 3

You cannot use both `this()` and `super()` in the same constructor.

Incorrect:

```
Dog() {

    this();

    super(); // Compilation Error
}
```

Reason: both must be the first statement.

---

# `this` vs `super`

|`this`|`super`|
|---|---|
|Refers to current class object|Refers to immediate parent class object|
|Access current class members|Access parent class members|
|Calls current class constructor (`this()`)|Calls parent class constructor (`super()`)|
|Used within the same class|Used to interact with the parent class|

---

# Common Interview Questions

### 1. What is the `super` keyword?

`super` is a reference to the **immediate parent class**. It is used to access parent variables, parent methods, and parent constructors.

---

### 2. Can we use `super` in a static method?

❌ No.

`super` is associated with an object, while static methods belong to the class and do not have access to an instance.

---

### 3. Is `super()` mandatory?

No.

If omitted, the compiler automatically inserts `super()` **only if the parent has a no-argument constructor**.

---

### 4. Why must `super()` be the first statement?

Because the parent part of an object must be initialized before the child part.

Object creation order:

```
Parent Object

↓

Child Object
```

---

### 5. Can `super` access private members of the parent?

❌ No.

Private members are not accessible outside the parent class, even through `super`.

---

### 6. Can `super` call a grandparent's constructor directly?

❌ No.

`super()` always refers to the **immediate parent**. The parent constructor is responsible for calling its own parent, forming a constructor chain.

---

# Best Practices

- Use `super.method()` only when you need the parent implementation in addition to the child's.
- Use `super.variable` when a child field hides a parent field.
- Avoid unnecessary use of `super`; if there is no ambiguity, direct access is usually clearer.
- Always ensure `super(...)` is the first statement in a constructor when explicitly calling a parent constructor.

---

# Interview Tip ⭐⭐⭐⭐⭐

Remember the **3 uses of `super`**:

```
super.variable
        ↓
Access Parent Variable

super.method()
        ↓
Call Parent Method

super()
        ↓
Call Parent Constructor
```

**Easy Memory Trick:**

> **`super` = Parent**

- `super.variable` → Parent Variable
- `super.method()` → Parent Method
- `super()` → Parent Constructor