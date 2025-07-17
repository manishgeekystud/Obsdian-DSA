Given a singly linked list. The task is to remove duplicates (nodes with duplicate values) from the given list (if it exists).  
**Note:** Try not to use extra space. The nodes are arranged in a **sorted** way.

**Examples:**

**Input:**
LinkedList: 2->2->4->5
**Output:** 2 -> 4 -> 5  
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700196/Web/Other/blobid0_1723610760.png)
**Explanation:** In the given linked list 2 -> 2 -> 4 -> 5, only 2 occurs more than 1 time. So we need to remove it once.

**Input:**
LinkedList: 2->2->2->2->2
**Output:** 2  
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700196/Web/Other/blobid1_1723610768.png)
**Explanation:** In the given linked list  2 -> 2 -> 2 -> 2, 2 is the only element and is repeated 5 times. So we need to remove any four 2.

**Expected Time Complexity** : O(n)  
**Expected Space** **Complexity**: O(1)

## 🧠 Intuition

In a **sorted list**, duplicates are always **consecutive**. So, while traversing, we can simply check:

- If `current.data == current.next.data` → duplicate found → **skip it**
- Else → move to the next node

This way, we can remove all duplicates **in a single pass** using **O(1)** space.

---

## ✅ Approach

### Steps:
1. Initialize a pointer `curr` to the head of the list.
2. Loop until `curr.next == null`:
   - If `curr.data == curr.next.data`, remove the duplicate by:
     ```java
     curr.next = curr.next.next;
     ```
   - Else, move `curr` forward:
     ```java
     curr = curr.next;
     ```
3. Return the updated head.

---

## ✅ Java Code with Comments


// Function to remove duplicates from sorted linked list
Node removeDuplicates(Node head) {
    // Start from the head node
    Node curr = head;

    // Traverse until the end of the list
    while (curr != null && curr.next != null) {

        // If current and next node have the same data, skip the next node
        if (curr.data == curr.next.data) {
            curr.next = curr.next.next;  // duplicate removed
        } else {
            curr = curr.next;  // move forward
        }
    }

    return head;  // return the updated list
}
