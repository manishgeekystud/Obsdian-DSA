Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

**Example 1:**

**Input:** s = "()"

**Output:** true

**Example 2:**

**Input:** s = "()[]{}"

**Output:** true

**Example 3:**

**Input:** s = "(]"

**Output:** false

**Example 4:**

**Input:** s = "([])"

**Output:** true

---------------------------------------------------------------
### ✅ 1. **Stack-Based Approach** (Standard, Most Efficient)

#### ✅ Time Complexity: O(n)

#### ✅ Space Complexity: O(n)

```java
public boolean isValid(String s) {
    Stack<Character> stack = new Stack<>();

    for (char ch : s.toCharArray()) {
        if (ch == '(' || ch == '[' || ch == '{') {
            stack.push(ch);
        } else {
            if (stack.isEmpty()) return false;
            char top = stack.pop();
            if ((ch == ')' && top != '(') ||
                (ch == ']' && top != '[') ||
                (ch == '}' && top != '{')) {
                return false;
            }
        }
    }
    return stack.isEmpty();
}

```

> __The idea is to put all the opening brackets in the stack. Whenever you hit a closing bracket, search if the top of the stack is the opening bracket of the same nature. If this holds then pop the stack and continue the iteration, in the end if the stack is empty, it means all brackets are well-formed . Otherwise, they are not balanced.__

****Illustration:****   
Below is the illustration of the above approach.

![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20190626134001/ForBalancedParanthesisInanExoression1.png)

Follow the steps mentioned below to implement the idea:

- Declare a character [stack](https://www.geeksforgeeks.org/stack-data-structure/) (say ****temp****).
- Now traverse the string exp. 
    - If the current character is a starting bracket ( ****‘(‘ or ‘{‘  or ‘[‘**** ) then push it to stack.
    - If the current character is a closing bracket ( ****‘)’ or ‘}’ or ‘]’**** ) then pop from stack and if the popped character is the matching starting bracket then fine.
    - Else brackets are ****Not Balanced****.
- After complete traversal, if there is some starting bracket left in stack then ****Not balanced****, else ****Balanced****.