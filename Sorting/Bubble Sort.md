## 🔍 What is Bubble Sort?

Bubble Sort is a **simple comparison-based sorting algorithm** that repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. This process is repeated until the array is sorted.

---

## ⚙️ Algorithm Explanation

- Repeatedly swap adjacent elements if they are in the wrong order.
    
- In each pass, the largest unsorted element "bubbles" to the end of the list.
    
- After every iteration, one less element (from the end) needs to be checked.
    

---

## 🧠 Pseudocode

```java
for (int i = 0; i < n - 1; i++) {
    for (int j = 0; j < n - i - 1; j++) {
        if (arr[j] > arr[j + 1]) {
            // swap arr[j] and arr[j+1]
        }
    }
}

```