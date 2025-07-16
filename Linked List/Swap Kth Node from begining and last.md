

## 🚩 Problem Statement

Given a **singly linked list** and an integer `k`, swap the `k-th` node from the **beginning** and the `k-th` node from the **end** of the list.

✅ You must swap the **nodes by changing links**, not their data.

---

## 💡 Intuition

In a singly linked list:

- Each node points only to the **next** node.
- You **cannot go backward**, so if you want to reconnect a node, you must keep track of its **previous node**.
- Swapping two nodes (say `A` and `B`) requires:
  - Connecting `prevA.next` to `B`
  - Connecting `prevB.next` to `A`
  - Swapping `A.next` and `B.next`

---

## 🔍 Why Previous Pointers (`prev1` and `prev2`) Are Needed?

If you're swapping two nodes in a singly linked list:

... → prev1 → A → ... → prev2 → B → ...



To swap A and B:

- You must update the `.next` of `prev1` and `prev2`
- You also need to swap `A.next` and `B.next` to maintain correct list structure

---

## 🧠 Step-by-Step Approach

---

### ✅ Step 1: Count the total number of nodes (n)


Node temp = head;
int n = 0;
while (temp != null) {
    n++;
    temp = temp.next;
}

### ✅ Step 2: Handle Edge Cases

- If `k > n`, return head as it is.
    
- If both nodes are the same (i.e., `2k - 1 == n`), no need to swap.
    
if (k > n || 2 * k - 1 == n) return head;`

✅ Step 3: Find `k-th` node from beginning (`first`) and its previous (`prev1`)
Node prev1 = null, first = head;
for (int i = 1; i < k; i++) {
    prev1 = first;
    first = first.next;
}

### ✅ Step 4: Find `k-th` node from end (`last`) and its previous (`prev2`)

`Node prev2 = null, 
last = head; 
for (int i = 1; i < n - k + 1; i++) {     prev2 = last;     last = last.next; }`

---

### ✅ Step 5: Reconnect Previous Pointers

java

CopyEdit

`if (prev1 != null) prev1.next = last; else head = last;  // if first was head  if (prev2 != null) prev2.next = first; else head = first;  // if last was head`

---

### ✅ Step 6: Swap `.next` Pointers of `first` and `last`

java

CopyEdit

`Node tempNext = first.next; first.next = last.next; last.next = tempNext;`

---

### ✅ Step 7: Return Updated Head

java

CopyEdit

`return head;`

---

## ✅ Final Java Code

java

CopyEdit