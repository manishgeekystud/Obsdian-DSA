## 📘 What is Infix, Postfix & Prefix?

### ✅ Infix:

- Operator is **between operands**
    
- Example: `A + B`
    

### ✅ Postfix (also called Reverse Polish Notation):

- Operator is **after operands**
    
- Example: `A B +`
    

### ✅ Prefix:

- Operator is **before operands**
    
- Example: `+ A B`
    

---

## ❓ Why Convert Infix to Postfix?

Infix expressions (like `A + B * C`) need **parentheses and precedence rules** to be evaluated correctly.  
Postfix removes this ambiguity – you can evaluate it **left to right** using a **stack** with **no parentheses**.

---

## 🔧 Goal

Given an infix expression like:
`A + B * C`  

Convert it to postfix:
`A B C * +`

---

## 🔢 Operator Precedence and Associativity

|Operator|Precedence|Associativity|
|---|---|---|
|`^`|3|Right|
|`*` `/` `%`|2|Left|
|`+` `-`|1|Left|

---

## 🧠 Key Observations

- **Operands** (A, B, 1, 2...) go directly to the result.
    
- **Operators** go to the stack.
    
- **Higher precedence operators** are popped before pushing lower precedence.
    
- **Parentheses** control where the expression starts and ends.
    

---

## ✅ Algorithm (Step-by-step)

1. Initialize an empty **stack** and **result string**.
    
2. For each **character** in the infix expression:
    
    - If it’s an **operand**: append it to result.
        
    - If it’s `'('`: push to stack.
        
    - If it’s `')'`: pop from stack to result until `'('` is found.
        
    - If it’s an **operator**:
        
        - While the stack is **not empty** and precedence of top operator is **greater or equal**, pop from stack to result.
            
        - Push the current operator.
            
3. After the loop ends, pop **all remaining operators** from the stack to result.
    

---

## ✅ Java Code

java

CopyEdit

`import java.util.*;  public class InfixToPostfix {      // Function to return precedence of operators     static int precedence(char ch) {         switch (ch) {             case '+': case '-': return 1;             case '*': case '/': return 2;`