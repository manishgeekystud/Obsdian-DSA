
Given the head of a singly linked list, swap every two adjacent nodes and return its head.  
⚠️ Do **not** change the node values — only modify links between nodes.

**Example 1:**

**Input:** head = [1,2,3,4]

**Output:** [2,1,4,3]

**Explanation:**

![](https://assets.leetcode.com/uploads/2020/10/03/swap_ex1.jpg)

**Example 2:**

**Input:** head = []

**Output:** []

**Example 3:**

**Input:** head = [1]

**Output:** [1]

**Example 4:**

**Input:** head = [1,2,3]

**Output:** [2,1,3]

---------------------------------------------------------------------
Solution
## ✅ Intuition

When you are given a pair of nodes like this:

prev → first → second → next

You want to rearrange it to:

prev → second → first → next

You need:
- A dummy node to easily manage changes at the head.
- A pointer `prev` to keep track of the node before the pair.
- Inside the loop, grab two nodes at a time (`first` and `second`), then perform the swap using 3 pointer updates.

---

## 📘 Algorithm

1. Create a dummy node pointing to the head.
2. Set `prev = dummy`
3. Loop while `prev.next` and `prev.next.next` are not null:
   - Set `first = prev.next`
   - Set `second = prev.next.next`
   - Perform the swap:
     - `first.next = second.next`
     - `second.next = first`
     - `prev.next = second`
   - Move `prev = first` to check the next pair.
4. Return `dummy.next` (new head after all swaps)

---

## ✅ Java Code (with Comments)

```java
public ListNode swapPairs(ListNode head) {
    // Dummy node to handle edge cases like swapping at head
    ListNode dummy = new ListNode(0);
    dummy.next = head;

    // prev tracks the node before the pair
    ListNode prev = dummy;

    // Loop through list in pairs
    while (prev.next != null && prev.next.next != null) {
        // Identify the pair to swap
        ListNode first = prev.next;
        ListNode second = prev.next.next;

        // Swap the nodes
        first.next = second.next;  // First now points to node after second
        second.next = first;       // Second points to first, reversing them
        prev.next = second;        // prev now points to second (new front of pair)

        // Move prev to the end of this swapped pair
        prev = first;
    }

    // Return the new head
    return dummy.next;
}
```
```

🔁 Dry Run Example
Input:
head = [1, 2, 3, 4]
Initial Setup:
dummy → 1 → 2 → 3 → 4
prev = dummy
1st Iteration:
first = 1, second = 2

Swap → prev.next = 2, 
          2.next = 1, 
          1.next = 3

New list: dummy → 2 → 1 → 3 → 4

Move prev = 1

2nd Iteration:
first = 3, second = 4

Swap → prev.next = 4,
          4.next = 3,
          3.next = null

New list: dummy → 2 → 1 → 4 → 3

Final Output:
[2, 1, 4, 3]

⏱️ Time and Space Complexity
Metric	Value
Time Complexity	O(n)
Space Complexity	O(1)

🧠 Summary
We use a dummy node to make swapping at the head easier.

Every pair is swapped using 3 pointer changes.

We never modify the values, only rearrange nodes.







