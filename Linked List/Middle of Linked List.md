# 🔗 Finding the Middle of a Singly Linked List

---

## 🧠 Problem Statement

Given the head of a singly linked list, return the **middle node**. If the list has an even number of nodes, return the **second middle node**.

---

## ✅ Example

### Input:
List: 1 → 2 → 3 → 4 → 5
### Output:
Middle Node = 3

shell
Copy
Edit

### Input:
List: 1 → 2 → 3 → 4 → 5 → 6

shell
Copy
Edit

### Output:
Middle Node = 4 (2nd middle in even case)

yaml
Copy
Edit

---

## 🥇 Approach 1: **Count & Traverse Again**

### 👉 Idea:
1. Traverse to count total number of nodes `n`.
2. Traverse again to `n / 2` to reach middle.

### 💡 Time: O(n) + O(n/2) → O(n)  
### 💡 Space: O(1)

### ✅ Code (Java):
```java
Node findMiddle(Node head) {
    int count = 0;
    Node temp = head;

    // Count total nodes
    while (temp != null) {
        count++;
        temp = temp.next;
    }

    // Go to middle node
    int mid = count / 2;
    temp = head;
    for (int i = 0; i < mid; i++) {
        temp = temp.next;
    }

    return temp;
}
🥈 Approach 2: Slow and Fast Pointer (Tortoise Method) ✅ Most Optimal
👉 Idea:
Use two pointers: slow moves one step, fast moves two.

When fast reaches end, slow will be at the middle.

💡 Time: O(n)
💡 Space: O(1)
✅ Code (Java):
java
Copy
Edit
Node findMiddle(Node head) {
    Node slow = head;
    Node fast = head;

    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }

    return slow;  // slow now points to middle
}
🔍 Dry Run (Odd-Length List)
Input:
Copy
Edit
1 → 2 → 3 → 4 → 5
Step	slow	fast
0	1	1
1	2	3
2	3	5
3	-	null

✅ Output: slow = 3