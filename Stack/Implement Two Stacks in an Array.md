Your task is to implement  2 stacks in one array efficiently. You need to implement 4 methods.

**twoStacks :** Initialize the data structures and variables to be used to implement  2 stacks in one array.  
**push1** : pushes element into the first stack.  
**push2** : pushes element into the second stack.  
**pop1** : pops an element from the first stack and returns the popped element. If the first stack is empty, it should return -1.  
**pop2** : pops an element from the second stack and returns the popped element. If the second stack is empty, it should return -1.  

**Examples:**

**Input:**
push1(2)
push1(3)
push2(4)
pop1()
pop2()
pop2()
**Output:** [3, 4, -1]
**Explanation:**
push1(2) the stack1 will be {2}
push1(3) the stack1 will be {2,3}
push2(4) the stack2 will be {4}
pop1()   the poped element will be 3 from stack1 and stack1 will be {2}
pop2()   the poped element will be 4 from stack2 and now stack2 is empty
pop2()   the stack2 is now empty hence returned -1.

--------------------------------------------------------------------
## ****Implement two stacks in an array by Dividing the space into two halves:****

### 🔸 **Key Concept**

- Use a **single array** `arr[0 ... n-1]` to hold both stacks.
    
- **Stack 1** grows **left → right** from index `0`.
    
- **Stack 2** grows **right → left** from index `n-1`.
    

---

### 🔸 **Pointers**

- `top1`: Points to the top of Stack 1. Initially `-1`.
    
- `top2`: Points to the top of Stack 2. Initially `n`.
    

---


**CODE**

```java
class TwoStacks {
    int size;
    int top1, top2;
    int[] arr;

    // Constructor: Initialize array and pointers
    public TwoStacks(int n) {
        size = n;
        arr = new int[n];
        top1 = -1;         // Stack1 starts from beginning
        top2 = n;          // Stack2 starts from end
    }

    // Method to push an element to stack1
    public void push1(int x) {
        if (top1 < top2 - 1) {
            top1++;
            arr[top1] = x;
        } else {
            // Stack Overflow, do nothing or handle
        }
    }

    // Method to push an element to stack2
    public void push2(int x) {
        if (top1 < top2 - 1) {
            top2--;
            arr[top2] = x;
        } else {
            // Stack Overflow, do nothing or handle
        }
    }

    // Method to pop an element from stack1
    public int pop1() {
        if (top1 >= 0) {
            int val = arr[top1];
            top1--;
            return val;
        } else {
            return -1; // Stack1 is empty
        }
    }

    // Method to pop an element from stack2
    public int pop2() {
        if (top2 < size) {
            int val = arr[top2];
            top2++;
            return val;
        } else {
            return -1; // Stack2 is empty
        }
    }
}

```