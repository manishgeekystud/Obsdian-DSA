

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

### 1. [Detect Loop in Linked List using Floyd's Cycle Detection Algorithm](https://www.geeksforgeeks.org/detect-loop-in-a-linked-list/):

- Use two pointers, ****slow**** and ****fast**** and initialize them with the ****head**** of the linked list.
- Move the ****fast**** pointer ****forward**** by two nodes and move the ****slow**** pointer forward by ****one**** node.
- If the ****slow**** and ****fast**** pointer points to the ****same node****, ****loop**** is found.
- Else if the ****fast**** pointer reaches ****NULL****, then ****no loop**** is found.
- Else ****repeat**** the above steps till we reach the ****end**** of the linked list or a ****loop**** is found.

