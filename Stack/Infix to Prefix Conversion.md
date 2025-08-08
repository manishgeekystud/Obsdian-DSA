## 1️⃣ What is Infix & Prefix?

|Notation|Definition|Example (A + B) * C|
|---|---|---|
|**Infix**|Operators are **between** operands|`(A + B) * C`|
|**Prefix (Polish)**|Operators are **before** operands|`* + A B C`|
|**Postfix (Reverse Polish)**|Operators are **after** operands|`A B + C *`|

---

## 2️⃣ Why convert Infix → Prefix?

- Computers **don’t naturally understand infix** because precedence and brackets complicate evaluation.
    
- Prefix doesn’t require parentheses — evaluation happens strictly **left to right**.
    
- Useful in expression evaluation without ambiguity.
    

---

## 3️⃣ The Core Difference from Infix → Postfix

When converting **infix to postfix**:

- We scan **left → right**.
    
- Operators go **after** operands.
    

When converting **infix to prefix**:

- The logic is **similar**, but…
    
- We **reverse the input**, swap parentheses, convert to postfix, then reverse again.
    

---

### Why reverse the input?

If we reverse an infix expression and swap `(` with `)`, then run the postfix algorithm, we get the **reversed prefix** expression. Reversing again gives the final prefix.

---

## 4️⃣ Step-by-step Algorithm (Infix → Prefix using stack)

1. **Reverse** the infix expression.
    
    - While reversing, swap `(` with `)`.
        
2. **Apply Infix → Postfix algorithm** on the reversed expression:
    
    - Use a stack to store operators.
        
    - Use precedence rules.
        
    - Append operands directly to result.
        
3. **Reverse** the postfix result to get prefix.
    

---

## 5️⃣ Operator Precedence Table

|Operator|Precedence|Associativity|
|---|---|---|
|`^`|3|Right-to-left|
|`* /`|2|Left-to-right|
|`+ -`|1|Left-to-right|

---

## 6️⃣ Example & Dry Run

Expression:
`(A - B / C) * (A / K - L)`

### Step 1: Reverse and Swap Brackets

Original: `(A - B / C) * (A / K - L)`  
Reverse: `(L - K / A) * (C / B - A)`  
Swap parentheses:

css

CopyEdit

`( L - K / A ) * ( C / B - A )`

→ actually in reversed form:

css

CopyEdit

`) L - K / A ( * ) C / B - A (`

---

### Step 2: Apply Infix → Postfix on reversed string

We use stack rules and precedence to produce:

css

CopyEdit

`L K A / - C B A - / *`

---

### Step 3: Reverse Postfix to get Prefix

Reverse:

css

CopyEdit

`* - L / K A / - C / B A`

---

## 7️⃣ Java Implementation

java

CopyEdit

`import java.util.*;  public class InfixToPrefix {          static int precedence(char ch) {         switch (ch) {             case '+': case '-': return 1;             case '*': case '/': return 2;             case '^': return 3;         }         return -1;     }      static String infixToPrefix(String s) {         // Step 1: Reverse the string and swap brackets         StringBuilder sb = new StringBuilder(s);         sb.reverse();         for (int i = 0; i < sb.length(); i++) {             if (sb.charAt(i) == '(') sb.setCharAt(i, ')');             else if (sb.charAt(i) == ')') sb.setCharAt(i, '(');         }                  // Step 2: Convert reversed expression to postfix         String postfix = infixToPostfix(sb.toString());                  // Step 3: Reverse postfix to get prefix         return new StringBuilder(postfix).reverse().toString();     }      static String infixToPostfix(String s) {         StringBuilder result = new StringBuilder();         Stack<Character> st = new Stack<>();          for (int i = 0; i < s.length(); i++) {             char ch = s.charAt(i);              // Operand             if (Character.isLetterOrDigit(ch)) {                 result.append(ch);             }             // Opening bracket             else if (ch == '(') {                 st.push(ch);             }             // Closing bracket             else if (ch == ')') {                 while (!st.isEmpty() && st.peek() != '(') {                     result.append(st.pop());                 }                 st.pop();             }             // Operator             else {                 while (!st.isEmpty() && precedence(st.peek()) >= precedence(ch)) {                     result.append(st.pop());                 }                 st.push(ch);             }         }         while (!st.isEmpty()) {             result.append(st.pop());         }         return result.toString();     }      public static void main(String[] args) {         String exp = "(A-B/C)*(A/K-L)";         System.out.println("Infix: " + exp);         System.out.println("Prefix: " + infixToPrefix(exp));     } }`

---

## 8️⃣ Key Notes & Differences

|Step|Infix → Postfix|Infix → Prefix|
|---|---|---|
|Scan direction|Left → Right|Reverse, then Left → Right|
|Bracket handling|Normal|Swap `(` and `)` when reversing|
|Final step|Direct output|Reverse final postfix to get prefix|

---

If you want, I can also make a **side-by-side dry run table** comparing **infix → postfix** and **infix → prefix** for the same input so you can visualize the difference clearly.  
Do you want me to prepare that?

Voice chat ended

Ask ChatGPT

### Unlock more with Plus

ChatGPT Plus gives you higher limits, smarter models, and Sora for video.

Get Plus

  

Tools