## 🧠 What is a Postfix Expression?

Postfix (also called **Reverse Polish Notation**) is a way of writing mathematical expressions **without using parentheses**.

### ✅ Infix vs Postfix:

|Infix|Postfix|
|---|---|
|`2 + 3`|`2 3 +`|
|`2 + 3 * 4`|`2 3 4 * +`|
|`(2 + 3) * 4`|`2 3 + 4 *`|

In postfix:

- **Operands** come first.
    
- **Operators** come after their operands.
    

---

## 🎯 Goal:

Given a postfix expression, **evaluate its result** using a **stack**.

---

## 🧪 Example:

### Expression:

`"231*+9-"`  
Breakdown:  
`2 + (3 * 1) - 9` → `5 - 9` → `-4`

---

## 🛠️ Key Idea (Using Stack):

1. Traverse expression from **left to right**.
    
2. **If operand**, push to stack.
    
3. **If operator**, pop **two** operands from stack:
    
    - Apply operator → `a op b` (important: **second popped is b**, first is a).
        
    - Push result back to stack.
        
4. Final result will be on top of stack.
    

---

## ✅ Java Code:

