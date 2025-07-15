[2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/02/addtwonumber1.jpg)

**Input:** l1 = [2,4,3], l2 = [5,6,4]
**Output:** [7,0,8]
**Explanation:** 342 + 465 = 807.

**Example 2:**

**Input:** l1 = [0], l2 = [0]
**Output:** [0]

**Example 3:**

**Input:** l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
**Output:** [8,9,9,9,0,0,0,1]

## Java Solution (Your Code)

```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode dummyHead = new ListNode(0);
        ListNode currNode = dummyHead;
        int carry = 0;

        while (l1 != null || l2 != null || carry != 0) {
            int x = (l1 != null) ? l1.val : 0;
            int y = (l2 != null) ? l2.val : 0;

            int sum = carry + x + y;
            carry = sum / 10;

            currNode.next = new ListNode(sum % 10);
            currNode = currNode.next;

            if (l1 != null) l1 = l1.next;
            if (l2 != null) l2 = l2.next;
        }

        return dummyHead.next;
    }
}
```

---

## Dry Run:

### Input:

```
l1 = 2 -> 4 -> 3
l2 = 5 -> 6 -> 4
```

### Iteration-wise Breakdown:

|Iteration|l1.val|l2.val|carry|sum = l1 + l2 + carry|new digit|new carry|List so far|
|---|---|---|---|---|---|---|---|
|1|2|5|0|2 + 5 + 0 = 7|7|0|7|
|2|4|6|0|4 + 6 + 0 = 10|0|1|7 -> 0|
|3|3|4|1|3 + 4 + 1 = 8|8|0|7 -> 0 -> 8|

### Final Output:

```
7 -> 0 -> 8 (represents 807)
```

---

## Explanation:

- A dummy head node is used to simplify handling the head pointer.
    
- We loop while either list is not null or there is a carry.
    
- Each iteration adds corresponding digits and any carry.
    
- A new node is created for the digit `sum % 10`, and carry is updated as `sum / 10`.
    
- Handles different lengths and final carry automatically.
    

---

## Edge Cases Handled:

- Different length lists.
    
- Carry overflow after final digit.
    
- Lists with `0` values.
    

---

## Time and Space Complexity:

- **Time Complexity:** O(max(N, M)) — where N and M are lengths of the two lists.
    
- **Space Complexity:** O(max(N, M)) — for the output list.
    

---

## Alternate Approaches:

### 1. **Convert to Integer (Not Recommended)**

- Convert lists to integers, add them, and convert back to a linked list.
    
- ❌ Unsafe for large values (integer overflow).
    

### 2. **Recursive Approach**

```java
public ListNode addTwoNumbers(ListNode l1, ListNode l2, int carry) {
    if (l1 == null && l2 == null && carry == 0) return null;
    int sum = carry;
    if (l1 != null) sum += l1.val;
    if (l2 != null) sum += l2.val;

    ListNode node = new ListNode(sum % 10);
    node.next = addTwoNumbers(
        l1 != null ? l1.next : null,
        l2 != null ? l2.next : null,
        sum / 10
    );
    return node;
}
```

### 3. **Using Stack (for forward order lists)**

- Push digits onto stacks, pop and add.
    
- Useful if numbers are stored in forward order.