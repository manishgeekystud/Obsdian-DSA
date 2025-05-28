##Input: arrl[] = {1, 2, 9, 5, 5}
       exit[] = {4, 5, 12, 9, 12}
First guest in array arrives at 1 and leaves at 4, 
second guest arrives at 2 and leaves at 5, and so on.

Output: 5
There are maximum 3 guests at time 5.

🧠 Problem Statement

You are given two arrays:

- `arr[]`: arrival times of guests
    
- `dep[]`: departure times of guests
    

Each guest stays at a party from `arr[i]` to `dep[i]` (inclusive or exclusive based on the variation). Your task is to find the **maximum number of guests present at the party at the same time**.

---

## ✅ Example

`arr[] = {1, 3, 5} dep[] = {2, 6, 10}`

Explanation:

- Guest 1: 1 to 2
    
- Guest 2: 3 to 6
    
- Guest 3: 5 to 10
    

At time 5, both Guest 2 and Guest 3 are present ⇒ max = **2**

---

## 🧮 Efficient Approach (Two Pointers + Sorting)

### Steps:

1. Sort both `arr[]` and `dep[]`.
    
2. Use two pointers (`i` for arrival, `j` for departure).
    
3. Traverse using the following logic:
    
    - If `arr[i] <= dep[j]`: a new guest has arrived before the earliest departure ⇒ increment count.
        
    - Else: a guest has left ⇒ decrement count.
        
4. Track the maximum value of guests present at any point.
    

---

### 🧑‍💻 Java Code
```java
import java.util.Arrays;

public class GuestMax {

    // Function to find the maximum number of guests present at the same time
    public static int findMaxGuests(int[] arr, int[] dep) {
        // Step 1: Sort both arrival and departure times
        Arrays.sort(arr);
        Arrays.sort(dep);
        
        int n = arr.length;
        int i = 0;      // Pointer for arrival
        int j = 0;      // Pointer for departure
        int guests = 0; // Current number of guests present
        int maxGuests = 0; // Track the maximum guests at any time

        // Step 2: Traverse both arrays
        while (i < n && j < n) {
            // If a guest arrives before or at the same time as the next departure
            if (arr[i] <= dep[j]) {
                guests++; // One more guest has arrived
                maxGuests = Math.max(maxGuests, guests); // Update max if needed
                i++; // Move to the next arrival
            } else {
                guests--; // One guest has departed
                j++; // Move to the next departure
            }
        }

        return maxGuests; // Return the maximum number of guests present at the same time
    }
}

```