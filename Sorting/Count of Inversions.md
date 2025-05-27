## 🔍 **What is an Inversion?**

Given an array `arr[]` of `n` integers, an **inversion** is a pair of indices `(i, j)` such that:

- `i < j`, and
    
- `arr[i] > arr[j]`
    

This means the two elements are **out of order** in the array and violate the condition of being sorted.

---

## 🧠 **Why Count Inversions?**

Counting inversions is a way to **measure how far an array is from being sorted**.

- **Sorted array:** 0 inversions
    
- **Reverse sorted array:** Maximum number of inversions = `n(n-1)/2`
    

---

## ✅ **Example**

Let’s say:
`arr = {2, 4, 1, 3, 5}`

### Find all pairs `(i, j)` where `i < j` and `arr[i] > arr[j]`:

- `(0, 2)` → (2, 1)
    
- `(1, 2)` → (4, 1)
    
- `(1, 3)` → (4, 3)
    

👉 Total Inversions = 3

---

## ⛔ Naive Approach — O(n²)

### Logic:

- Compare every pair of elements in nested loops.
```java
int countInversions(int[] arr) {
    int n = arr.length;
    int count = 0;
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {
            if (arr[i] > arr[j]) {
                count++;
            }
        }
    }
    return count;
}

```