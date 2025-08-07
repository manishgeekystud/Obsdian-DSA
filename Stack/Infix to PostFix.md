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

```java
import java.util.*;

public class InfixToPostfix {

    // Function to return precedence of operators
    static int precedence(char ch) {
        switch (ch) {
            case '+': case '-': return 1;
            case '*': case '/': return 2;
            case '^': return 3;
        }
        return -1;
    }

    // Main function to convert infix to postfix
    public static String convert(String infix) {
        StringBuilder result = new StringBuilder();
        Stack<Character> stack = new Stack<>();

        for (int i = 0; i < infix.length(); i++) {
            char ch = infix.charAt(i);

            // 1. If operand, add to result
            if (Character.isLetterOrDigit(ch)) {
                result.append(ch);
            }

            // 2. If '(', push to stack
            else if (ch == '(') {
                stack.push(ch);
            }

            // 3. If ')', pop till '('
            else if (ch == ')') {
                while (!stack.isEmpty() && stack.peek() != '(') {
                    result.append(stack.pop());
                }
                if (!stack.isEmpty()) stack.pop(); // pop '('
            }

            // 4. If operator
            else {
                while (!stack.isEmpty() && precedence(ch) <= precedence(stack.peek())) {
                    result.append(stack.pop());
                }
                stack.push(ch);
            }
        }

        // Pop any remaining operators
        while (!stack.isEmpty()) {
            result.append(stack.pop());
        }

        return result.toString();
    }

    public static void main(String[] args) {
        String infix = "A+(B*C-(D/E^F)*G)*H";
        String postfix = convert(infix);
        System.out.println("Postfix: " + postfix);
    }
}

```

## 🧪 Example Walkthrough

### Infix:

`A + B * C`

### Steps:

1. `A` → operand → result: `A`
    
2. `+` → operator → stack: `+`
    
3. `B` → operand → result: `AB`
    
4. `*` → operator with higher precedence than `+` → stack: `+ *`
    
5. `C` → operand → result: `ABC`
    
6. End → pop stack: `*`, `+` → result: `ABC*+`
    

### ✅ Final Postfix:

`ABC*+`

---

## 📦 Time & Space Complexity

- **Time:** O(n)
    
- **Space:** O(n) (for stack and result)
    

---

## 🔁 Related Interview Questions

- Convert Infix to Prefix
    
- Evaluate Postfix Expression
    
- Balanced Parentheses using Stack
    

---