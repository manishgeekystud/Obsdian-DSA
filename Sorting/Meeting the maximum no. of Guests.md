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
```
// Java Program to find maximum guest 
// at any time in a party
import java.util.*;

class GFG {

    static void findMaxGuests(int arrl[], int exit[],
                                          int n)    
    {   
    // Sort arrival and exit arrays
    Arrays.sort(arrl);
    Arrays.sort(exit);

    // guests_in indicates number of guests at a time
    int guests_in = 1, max_guests = 1, time = arrl[0];
    int i = 1, j = 0;

    // Similar to merge in merge sort to process
    // all events in sorted order
    while (i < n && j < n)
    {
        // If next event in sorted order is arrival,
        // increment count of guests
        if (arrl[i] <= exit[j])
        {
            guests_in++;

            // Update max_guests if needed
            if (guests_in > max_guests)
            {
                max_guests = guests_in;
                time = arrl[i];
            }
            i++; //increment index of arrival array
        }
        else // If event is exit, decrement count
        { // of guests.
            guests_in--;
            j++;
        }
    }

    System.out.println("Maximum Number of Guests = "+
                    max_guests + " at time " + time);
    }

    // Driver program to test above function
    public static void main(String[] args)
    {
        int arrl[] = {1, 2, 10, 5, 5};
        int exit[] = {4, 5, 12, 9, 12};
        int n = arrl.length;
        findMaxGuests(arrl, exit, n);
    }
}
// This code is contributed by Prerna Saini
```