

Given the head of a linked list that may contain a loop.  A loop means that the last node of the linked list is connected back to a node in the same list. The task is to remove the loop from the linked list (if it exists).

**Custom Input format:**

A **head** of a singly linked list and a **pos** (1-based index) which denotes the position of the node to which the last node points to. If **pos = 0**, it means the last node points to null, indicating there is no loop.

The generated output will be **true** if there is no loop in list and other nodes in the list remain unchanged, otherwise, **false**.

**Examples:**

**Input:** head = 1 -> 3 -> 4, pos = 2
**Output:** true
**Explanation:** The linked list looks like  
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700332/Web/Other/blobid0_1718609709.png)  
A loop is present in the list, and it is removed.

**Input:** head = 1 -> 8 -> 3 -> 4, pos = 0
**Output:** true
**Explanation:** **![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700332/Web/Other/blobid0_1718609876.png)  
**The Linked list does not contains any loop. 

**Input:** head = 1 -> 2 -> 3 -> 4, pos = 1
**Output:** true
**Explanation:** The linked list looks like   
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700332/Web/Other/blobid2_1718609744.png)  
A loop is present in the list, and it is removed.

**SOLUTION**

Given the ****head**** of a linked list that may contain a loop.  A loop means that the ****last node**** of the linked list is connected back to a node in the same list. The task is to ****remove**** the loop from the linked list (if it exists).

****Example:****

> ****Input:**** 
> 
> ![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700332/Web/Other/blobid0_1718609709.png)
> 
> ****Output:**** 1 -> 3 -> 4  
> ****Explanation:**** The Loop is removed from the above example.

## 🚀 Approach: Floyd’s Cycle Detection (Tortoise & Hare)

- Use **two pointers**: `slow` and `fast`
- Detect the loop using Floyd's algorithm
- Once detected:
  - If the loop starts at the `head`, handle that as a **special case**
  - Otherwise, move both pointers until they meet at the **node just before the loop start**
- Break the loop by setting `fast.next = null`

---

## ✅ Clean Java Code with Comments


```java
// Function to remove a loop in the linked list
public static void removeLoop(Node head) {
    // Step 1: Initialize two pointers
    Node slow = head;
    Node fast = head;

    // Step 2: Detect loop using Floyd’s algorithm
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;

        // Loop detected
        if (fast == slow)
            break;
    }

    // Step 3: No loop found — exit
    if (fast == null || fast.next == null)
        return;

    // Step 4: Reset slow to head to find the start of the loop
    slow = head;

    // 🔄 Special Case: Loop starts at head
    if (slow == fast) {
        // Move fast until it reaches the last node in the loop
        while (fast.next != slow) {
            fast = fast.next;
        }
        // Break the loop
        fast.next = null;
        return;
    }

    // 🔁 General Case: Loop starts somewhere after head
    while (slow.next != fast.next) {
        slow = slow.next;
        fast = fast.next;
    }

    // Break the loop
    fast.next = null;
}
```

## 🧠 Intuition Behind Logic

- **Meeting Point** in Floyd’s algorithm is guaranteed inside the loop if one exists.
    
- By moving `slow` back to the head and then shifting both `slow` and `fast` one step at a time, they will meet **just before** the loop's starting node.
    
- For the **special case** where the loop starts at the head itself, `slow == fast` right after detection.  
    So, to find the **last node in the loop**, we move `fast` until `fast.next == slow`.
    

---

## 📊 Time & Space Complexity

|Metric|Value|
|---|---|
|Time Complexity|O(n)|
|Space Complexity|O(1)|
|Extra Data Structures|❌ None used|

---

## ✅ Edge Cases Handled

- Loop starts at the head
    
- Loop starts in the middle
    
- No loop exists
    
- List has only one node