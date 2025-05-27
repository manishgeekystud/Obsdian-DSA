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

import java.util.*;

public class tUf {

    private static int merge(int[] arr, int low, int mid, int high) {
        ArrayList<Integer> temp = new ArrayList<>(); // temporary array
        int left = low;      // starting index of left half of arr
        int right = mid + 1;   // starting index of right half of arr

        //Modification 1: cnt variable to count the pairs:
        int cnt = 0;

        //storing elements in the temporary array in a sorted manner//

        while (left <= mid && right <= high) {
            if (arr[left] <= arr[right]) {
                temp.add(arr[left]);
                left++;
            } else {
                temp.add(arr[right]);
                cnt += (mid - left + 1); //Modification 2
                right++;
            }
        }

        // if elements on the left half are still left //

        while (left <= mid) {
            temp.add(arr[left]);
            left++;
        }

        //  if elements on the right half are still left //
        while (right <= high) {
            temp.add(arr[right]);
            right++;
        }

        // transfering all elements from temporary to arr //
        for (int i = low; i <= high; i++) {
            arr[i] = temp.get(i - low);
        }
        return cnt; // Modification 3
    }

    public static int mergeSort(int[] arr, int low, int high) {
        int cnt = 0;
        if (low >= high) return cnt;
        int mid = (low + high) / 2 ;
        cnt += mergeSort(arr, low, mid);  // left half
        cnt += mergeSort(arr, mid + 1, high); // right half
        cnt += merge(arr, low, mid, high);  // merging sorted halves
        return cnt;
    }

    public static int numberOfInversions(int[] a, int n) {
        // Count the number of pairs:
        return mergeSort(a, 0, n - 1);
    }


    public static void main(String[] args) {
        int[] a = {5, 4, 3, 2, 1};
        int n = 5;
        int cnt = numberOfInversions(a, n);
        System.out.println("The number of inversions are: " + cnt);
    }
}



```

### 🔢 Time and Space Complexity

|Approach|Time Complexity|Space Complexity|
|---|---|---|
|Naive|O(n²)|O(1)|
|Merge|O(n log n)|O(n)|

---

### ✅ Applications

- **Sorting evaluation** – how close is a sequence to being sorted?
    
- **Kendall Tau distance** – used in ranking and recommendation systems.
    
- **Comparing arrays or permutations**.