- **Goal:** Return the index of the first occurrence of a number `x` in a sorted array.
    
- **Why Binary Search?** Since the array is sorted, binary search helps reduce time complexity to **O(log n)**.
    
- **Key Trick:** Even if we find the element, we continue searching **to the left** (lower half) to ensure it’s the first occurrence.
    

---

### ✅ **Java Code**

```java
// Function to find the index of the first occurrence of x in a sorted array
static int findFirstOccurrence(int[] arr, int x) {
    int low = 0;
    int high = arr.length - 1;
    int result = -1; // Stores the index of first occurrence

    while (low <= high) {
        int mid = low + (high - low) / 2; // Prevents overflow

        if (arr[mid] == x) {
            result = mid;        // Possible answer found
            high = mid - 1;      // Move left to find earlier occurrence
        } else if (arr[mid] > x) {
            high = mid - 1;      // Discard right half
        } else {
            low = mid + 1;       // Discard left half
        }
    }

    return result; // Returns -1 if not found, else index
}

```