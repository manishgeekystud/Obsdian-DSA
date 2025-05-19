
---

Given a sorted array arr[] and a number x, write a function that counts the occurrences of x in arr[]. Expected time complexity is O(Logn) 

**Examples:** 

  **Input:** arr[] = {1, 1, 2, 2, 2, 2, 3,},   x = 2
  **Output:** 4 // x (or 2) occurs 4 times in arr[]

 ** Input:** arr[] = {1, 1, 2, 2, 2, 2, 3,},   x = 3
  **Output:** 1 

  **Input:** arr[] = {1, 1, 2, 2, 2, 2, 3,},   x = 1
  **Output:** 2 

 ** Input:** arr[] = {1, 1, 2, 2, 2, 2, 3,},   x = 4
 ** Output:** -1 // 4 doesn't occur in arr[] 
-------------------------------------------------------------------------------------------------------
To **count the number of occurrences of a given number** (say `x`) in a **sorted array**, you can use **binary search** to:

1. Find the **first occurrence** of `x`.
    
2. Find the **last occurrence** of `x`.
    
3. The count is then:
    count=(last index−first index)+1
    
**Method: Binary Search**
```java
public class OccurrenceCounter {

    // Function to count occurrences of x in sorted array arr[]
    public static int countOccurrences(int[] arr, int x) {
        int first = firstOccurrence(arr, x);
        int last = lastOccurrence(arr, x);

        // If x is not found in the array
        if (first == -1) return 0;

        // Count = last - first + 1
        return last - first + 1;
    }

    // Binary search to find first occurrence of x
    public static int firstOccurrence(int[] arr, int x) {
        int low = 0, high = arr.length - 1;
        int res = -1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (arr[mid] == x) {
                res = mid;        // Record index
                high = mid - 1;   // Move left to find earlier occurrence
            } else if (arr[mid] < x) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }

        return res;
    }

    // Binary search to find last occurrence of x
    public static int lastOccurrence(int[] arr, int x) {
        int low = 0, high = arr.length - 1;
        int res = -1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (arr[mid] == x) {
                res = mid;        // Record index
                low = mid + 1;    // Move right to find later occurrence
            } else if (arr[mid] < x) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }

        return res;
    }

    // Test
    public static void main(String[] args) {
        int[] arr = {1, 2, 2, 2, 3, 4, 5};
        int x = 2;
        int count = countOccurrences(arr, x);
        System.out.println("Number of occurrences of " + x + " is: " + count);
    }
}


```