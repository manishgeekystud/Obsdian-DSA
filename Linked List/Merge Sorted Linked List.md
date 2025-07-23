# 🔗 Merge Two Sorted Linked Lists — Iterative Approach

---

## ✅ Problem Statement

Given two **sorted** singly linked lists `head1` and `head2`, merge them into a single sorted linked list in **ascending order**.

- The merged list should maintain **sorted order**.
- Return the **head** of the new linked list.
- The input lists are already sorted individually.

**Examples:**

**Input:** head1 = 5 -> 10 -> 15 -> 40, head2 = 2 -> 3 -> 20
**Output:** 2 -> 3 -> 5 -> 10 -> 15 -> 20 -> 40
**Explanation:  
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700176/Web/Other/blobid1_1722768650.png)**

**Input**: head1 = 1 -> 1, head2 = 2 -> 4
**Output:** 1 -> 1 -> 2 -> 4
**Explanation:  
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700176/Web/Other/blobid3_1722768742.png)**

**Constraints:**  
1 <= no. of nodes<= 103  
0 <= node->data <= 105



## 🧠 Intuition

Since both lists are sorted, we can merge them by:
- Traversing both lists in parallel
- Picking the **smaller node** at each step
- Moving that node to the result list

We continue until one list ends, and then append the remaining nodes of the other list.

---

## 📘 Algorithm

1. Create two pointers: `head` and `tail` to track the result list.
2. Compare the first elements of `head1` and `head2`:
   - The smaller one becomes the **starting node** (`head`) of the merged list.
3. Loop through both lists until one becomes `null`:
   - Compare `head1.data` and `head2.data`
   - Append the smaller node to `tail.next` and move `tail`
4. After the loop:
   - Attach the non-null remaining list to `tail.next`
5. Return the `head` of the merged list.

---

## ✅ Java Code with Comments

```java
Node sortedMerge(Node head1, Node head2) {
    Node head = null;
    Node tail = null;

    // Step 1: Initialize the head of the merged list
    if (head1.data <= head2.data) {
        head = head1;
        tail = head1;
        head1 = head1.next;
    } else {
        head = head2;
        tail = head2;
        head2 = head2.next;
    }

    // Step 2: Traverse both lists and merge
    while (head1 != null && head2 != null) {
        if (head1.data <= head2.data) {
            tail.next = head1;   // Attach smaller node
            tail = head1;        // Move tail
            head1 = head1.next;  // Move input pointer
        } else {
            tail.next = head2;
            tail = head2;
            head2 = head2.next;
        }
    }

    // Step 3: Attach remaining nodes
    if (head1 == null) {
        tail.next = head2;
    } else {
        tail.next = head1;
    }

    // Step 4: Return the new head
    return head;
}```

## 🔁 Dry Run Example

### Input:

ini

CopyEdit

`head1 = 1 → 3 → 5 head2 = 2 → 4 → 6`

### Step-by-Step:

1. Start:
    
    - `head = 1` (head1 smaller)
        
    - `tail = 1`
        
2. Compare: 3 vs 2 → pick 2 → `1 → 2`
    
3. Compare: 3 vs 4 → pick 3 → `1 → 2 → 3`
    
4. Compare: 5 vs 4 → pick 4 → `1 → 2 → 3 → 4`
    
5. Compare: 5 vs 6 → pick 5 → `1 → 2 → 3 → 4 → 5`
    
6. head1 is null → attach remaining head2 (6)
    

**Output:** `1 → 2 → 3 → 4 → 5 → 6`

---

## ⏱ Time and Space Complexity

|Metric|Value|
|---|---|
|Time Complexity|O(n + m)|
|Space Complexity|O(1)|
```
