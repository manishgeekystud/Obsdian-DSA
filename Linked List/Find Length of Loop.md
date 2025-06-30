Given the head of a linked list, determine whether the list contains a loop. If a loop is present, **return the number of nodes** in the loop, otherwise **return 0**.

**Note: '**c**'** is the position of the node which is the next pointer of the last node of the linkedlist. If c is 0, then there is no loop.

**Examples:**

**Input:** head: 1 → 2 → 3 → 4 → 5, c = 2
**Output:** 4
**Explanation:** There exists a loop in the linked list and the length of the loop is 4.  
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/893387/Web/Other/blobid0_1745983361.jpg)  

**Input:** head: 25 → 14 → 19 → 33 → 10 → 21 → 39 → 90 → 58 → 45, c = 4
**Output:** 7
**Explanation:** The loop is from 33 to 45. So length of loop is 33 → _10_ → 21 → 39 → 90 → 58 → _45_ = 7.  
The number 33 is connected to the last node of the linkedlist to form the loop because according to the input the 4th node from the beginning(1 based indexing)   
will be connected to the last node in the LinkedList.  
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/893387/Web/Other/blobid0_1745659828.jpg)  

**Input:** head: 0 → 1 → 2 → 3, c = 0
**Output:** 0
**Explanation:** There is no loop.

## ✅ **1. What’s the problem?**

Given the head of a linked list, detect if a **loop/cycle** exists.  
If a loop is present, **return the number of nodes in the loop**.

---

## ✅ **2. What’s the approach?**

We use **Floyd’s Cycle Detection Algorithm (Tortoise and Hare)**:

1. **Detect the loop** using two pointers moving at different speeds.
    
2. **Find the meeting point** inside the loop.
    
3. From the meeting point, **count the number of nodes to come back to the same point.**
    

---

## ✅ **3. Step-by-Step Method**

### 🟢 **Step 1: Detect the Loop**

- Use two pointers:
    
    - `slow` moves **1 step**
        
    - `fast` moves **2 steps**
        
- Traverse:
    
    - If `fast == null` or `fast.next == null`: **No loop**
        
    - If `slow == fast`: **Loop detected**
        

---

### 🟢 **Step 2: Count the Length**

- Keep `slow` fixed at meeting point.
    
- Initialize `count = 1`.
    
- Move another pointer (`temp = slow.next`) one step at a time:
    
    - Increment `count` each step.
        
    - Stop when `temp == slow`.
        
- The final `count` is the **length of the loop**.
    

---

## ✅ **4. Visual Example**
```java
1 -> 2 -> 3 -> 4 -> 5
           ^        |
           |________|
- Loop: `3 -> 4 -> 5 -> 3`
    
- Length = 3 nodes.
```
CODE