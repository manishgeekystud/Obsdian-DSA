You are given a **pointer/reference to a node (`del_node`)** in a **singly linked list** (NOT the head), and you must:

- **Delete that node**, so that:
    
    - The value is no longer present in the list.
        
    - The list contains one less node.
        
    - The **order of other nodes remains the same**.
        
- ❗ You are **guaranteed**:
    
    - The node exists.
        
    - It is **not the last node** in the list.
        
    - You are given **only that node**, not the head.
**Input:** Linked List = 1 -> 2, del_node = 1
**Output:** 2
**Explanation:** After deleting 1 from the linked list, we have remaining nodes as 2.  
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700161/Web/Other/blobid0_1724435615.png) 

**Input:** Linked List = 10 -> 20 -> 4 -> 30, del_node = 20
**Output:** 10->4->30
**Explanation:** After deleting 20 from the linked list, we have remaining nodes as 10, 4, 30.  
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700161/Web/Other/blobid1_1724435635.png)  

Solution

## ✅ Idea / Intuition

You **cannot** delete the node in the traditional way (i.e., by updating the previous node’s `.next`) because you don’t have access to the **previous node** or the **head**.

> Instead, you can copy the data from the **next node** into the current node, and delete the next node.

This way, the given node's value gets replaced, and we delete the following node — thus achieving the effect of deleting the current node.

---

## ✅ Code (Java)

```java
class Node {
    int data;
    Node next;
    
    Node(int data) {
        this.data = data;
    }
}

public class Solution {
    public void deleteNode(Node del_node) {

        // Step 1: Copy data from next node
        del_node.data = del_node.next.data;

        // Step 2: Remove next node
        del_node.next = del_node.next.next;
    }
}

```

## 🔍 Dry Run

### Input:


`List: 1 → 2 → 3 → 4 → 5 Given: del_node = 3`

### Process:

- Copy `4` into `3` → list becomes: `1 → 2 → 4 → 4 → 5`
    
- Skip the next `4` → list becomes: `1 → 2 → 4 → 5`
    

✅ Done! Node `3` is effectively removed.