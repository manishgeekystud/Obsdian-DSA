**Examples  
**

**Input**: arr[] = [1, 3, 2, 4]
**Output**: [3, 4, 4, -1]
**Explanation**: The next larger element to 1 is 3, 3 is 4, 2 is 4 and for 4, since it doesn't exist, it is -1.

**Input**: arr[] = [6, 8, 0, 1, 3]
**Output**: [8, -1, 1, 3, -1]
**Explanation**: The next larger element to 6 is 8, for 8 there is no larger elements hence it is -1, for 0 it is 1 , for 1 it is 3 and then for 3 there is no larger element on right and hence -1.

**Input**: arr[] = [10, 20, 30, 50]
**Output**: [20, 30, 50, -1]
**Explanation**: For a sorted array, the next element is next greater element also except for the last element.

-----------------------------------------------------------------------
## 🛠️ **Brute-Force Approach**

### 🔸 Idea:

For each element, scan all elements to its right until a greater element is found.

### 🔁 Code (O(n²)):

```java
public ArrayList<Integer> nextGreaterBrute(int[] arr) {
    ArrayList<Integer> result = new ArrayList<>();
    int n = arr.length;

    for (int i = 0; i < n; i++) {
        int next = -1;
        for (int j = i + 1; j < n; j++) {
            if (arr[j] > arr[i]) {
                next = arr[j];
                break;
            }
        }
        result.add(next);
    }

    return result;
}

```

### ⏱️ Time Complexity:

- **O(n²)** — Nested loop for each element
    

### 📦 Space Complexity:

- **O(n)** — Output list
    

---

## ✅ **Optimized Stack-Based Approach** 

### 🔸 Idea:

We process elements **from right to left**, keeping a stack of "potential next greater elements".

> For each element, we pop smaller/equal elements from the stack.  
> The top of the stack (if any) is the **next greater element**.

---

### 🔁 Your Code (O(n)):

```java
public ArrayList<Integer> nextLargerElement(int[] arr) {
    ArrayList<Integer> nextG = new ArrayList<>();
    Stack<Integer> st = new Stack<>();
    int n = arr.length;

    nextG.add(-1);            // Last element has no next greater
    st.push(arr[n - 1]);      // Start from the end

    for (int i = n - 2; i >= 0; i--) {
        while (!st.isEmpty() && st.peek() <= arr[i]) {
            st.pop();         // Remove smaller/equal elements
        }

        int ans = st.isEmpty() ? -1 : st.peek();  // Top of stack is next greater
        nextG.add(ans);
        st.push(arr[i]);      // Add current element to stack
    }

    Collections.reverse(nextG);  // Because we filled it in reverse
    return nextG;
}

```

## 🔍 Dry Run Example: `arr = [4, 5, 2, 25]`

Processing from right to left:

|i|arr[i]|Stack before|Stack after|nextG added|
|---|---|---|---|---|
|3|25|[]|[25]|-1|
|2|2|[25]|[25, 2]|25|
|1|5|[25, 2] → pop 2|[25, 5]|25|
|0|4|[25, 5]|[25, 5, 4]|5|

Reverse nextG → [5, 25, 25, -1]

---

## ⏱️ Time & Space Complexity

|Metric|Value|
|---|---|
|Time Complexity|**O(n)**|
|Space Complexity|**O(n)** (stack + result)|