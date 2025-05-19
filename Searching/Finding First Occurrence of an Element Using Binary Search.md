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
            high = mid - 1;      // Move left to find earlier occurrence as it might
        } else if (arr[mid] > x) {
            high = mid - 1;      // Discard right half
        } else {
            low = mid + 1;       // Discard left half
        }
    }

    return result; // Returns -1 if not found, else index
}
```
### 🔁 **Dry Run Example**

```java
arr = {1, 2, 2, 2, 3, 4}, x = 2

Initial: low = 0, high = 5
Step 1: mid = 2 → arr[mid] = 2 → result = 2 → high = 1
Step 2: mid = 0 → arr[mid] = 1 → low = 1
Step 3: mid = 1 → arr[mid] = 2 → result = 1 → high = 0

Return result = 1

```
### 🧠 **Recap Points**

- Use a variable `result` to store potential answer.
- On finding `x`, don’t stop. Update `result` and move `high = mid - 1` to go left.
- This ensures we get the **first position** where `x` occurs.
- Useful in problems like counting occurrences, finding range etc.