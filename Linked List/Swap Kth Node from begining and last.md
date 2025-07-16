

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
    

`if (k > n || 2 * k - 1 == n) return head;`