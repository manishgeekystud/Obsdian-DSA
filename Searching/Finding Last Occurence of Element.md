- **Goal:** Return the index of the **last occurrence** of a number `x` in a **sorted array**.
    
- **Why Binary Search?** Since the array is sorted, binary search provides an efficient **O(log n)** solution.
    
- **Key Trick:** If you find `x`, you **don’t stop** — instead, move to the **right** to check for a later occurrence.

✅ **Java Code**
```java
// Function to find the index of the last occurrence of x in a sorted array
static int findLastOccurrence(int[] arr, int x) {
    int low = 0;
    int high = arr.length - 1;
    int result = -1; // Will store the index of last occurrence

    while (low <= high) {
        int mid = low + (high - low) / 2; // Safer mid calculation

        if (arr[mid] == x) {
            result = mid;       // Potential answer found
            low = mid + 1;      // Move right to find later occurrence
        } else if (arr[mid] > x) {
            high = mid - 1;     // Discard right half
        } else {
            low = mid + 1;      // Discard left half
        }
    }

    return result; // Returns -1 if x not found
}

```

Dry Run
```
arr = {1, 2, 2, 2, 3, 4}, x = 2

Initial: low = 0, high = 5
Step 1: mid = 2 → arr[mid] = 2 → result = 2 → low = 3
Step 2: mid = 4 → arr[mid] = 3 → high = 3
Step 3: mid = 3 → arr[mid] = 2 → result = 3 → low = 4

Return result = 3

```