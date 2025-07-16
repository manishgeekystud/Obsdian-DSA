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

