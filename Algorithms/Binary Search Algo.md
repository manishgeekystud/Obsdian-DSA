**Binary Search** is an efficient algorithm for finding an item from a sorted list of elements by repeatedly dividing the search interval in half.

The most commonly used methods in Java to perform Binary Search are:

- Arrays.binarySearch()
- Collections.binarySearch()****
-
### ✅ Prerequisite:

- **The array must be sorted** (either ascending or descending).
### 🧠 Intuition:

- Pick the middle element.
- If it matches the target → done.
- If the target is smaller → search in the left half.
- If the target is greater → search in the right half.
### ⏱️ Time Complexity:

- **Best Case:** `O(1)` (when the element is in the middle)
- **Average Case:** `O(log n)`
- **Worst Case:** `O(log n)`

![[Pasted image 20250518225240.png]]


```java
public static int binarySearch(int[] arr, int target) {
    int low = 0;
    int high = arr.length - 1;

    while (low <= high) {
        int mid = low + (high - low) / 2;

        if (arr[mid] == target)
            return mid; // Target found at mid
        else if (arr[mid] < target)
            low = mid + 1; // Discard left half
        else
            high = mid - 1; // Discard right half
    }

    return -1; // Target not found
}

```

📌 Recursive Version:
```java
public static int binarySearchRecursive(int[] arr, int low, int high, int target) {
    if (low > high)
        return -1;

    int mid = low + (high - low) / 2;

    if (arr[mid] == target)
        return mid;
    else if (arr[mid] > target)
        return binarySearchRecursive(arr, low, mid - 1, target);
    else
        return binarySearchRecursive(arr, mid + 1, high, target);
}

```
### 🔍 Use Cases:

- Search in sorted arrays
- Efficient searching in large datasets
- Problems like:
    - First/Last occurrence of element
    - Count of occurrences
    - Peak element in mountain array
    - Binary Search on answer (optimization problems)
