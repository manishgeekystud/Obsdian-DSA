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

## ⚡ Efficient Approach — O(n log n) Using Modified Merge Sort

This is a clever technique where you count inversions **during the merge step** of merge sort.

### Why does it work?

When two sorted subarrays are merged:

- If `left[i] ≤ right[j]`: no inversion.
    
- If `left[i] > right[j]`: then all elements from `left[i]` to `left[end]` will form inversions with `right[j]`.
    

### Steps:

1. Recursively split the array.
    
2. While merging, count the number of inversions using the rule above.
    
3. Sum all inversion counts from left, right, and merged parts.
    

---

### Full Java Code:
```java
import java.util.Arrays;

public class InversionCounter {

    public static int mergeAndCount(int[] arr, int left, int mid, int right) {
        int[] leftArr = Arrays.copyOfRange(arr, left, mid + 1);
        int[] rightArr = Arrays.copyOfRange(arr, mid + 1, right + 1);

        int i = 0, j = 0, k = left, swaps = 0;

        while (i < leftArr.length && j < rightArr.length) {
            if (leftArr[i] <= rightArr[j]) {
                arr[k++] = leftArr[i++];
            } else {
                arr[k++] = rightArr[j++];
                swaps += (leftArr.length - i); // Inversions found!
            }
        }

        // Copy any remaining elements
        while (i < leftArr.length) arr[k++] = leftArr[i++];
        while (j < rightArr.length) arr[k++] = rightArr[j++];

        return swaps;
    }

    public static int mergeSortAndCount(int[] arr, int left, int right) {
        int count = 0;
        if (left < right) {
            int mid = (left + right) / 2;

            count += mergeSortAndCount(arr, left, mid);
            count += mergeSortAndCount(arr, mid + 1, right);
            count += mergeAndCount(arr, left, mid, right);
        }
        return count;
    }

    public static void main(String[] args) {
        int[] arr = {2, 4, 1, 3, 5};
        int count = mergeSortAndCount(arr, 0, arr.length - 1);
        System.out.println("Number of inversions: " + count);
    }
}

```