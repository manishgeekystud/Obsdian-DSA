Difficulty: **Easy**  Expected Complexity- **O(logn)**  Amazon

Given a sorted array **arr[]** and an integer **x**, find the index (0-based) of the largest element in arr[] that is less than or equal to x. This element is called the **floor** of x. If such an element does not exist, return -1.

**Note:** In case of multiple occurrences of ceil of x, return the index of the last occurrence.

**Examples**

**Input:** arr[] = [1, 2, 8, 10, 10, 12, 19], x = 5
**Output:** 1
**Explanation:** Largest number less than or equal to 5 is 2, whose index is 1.

**Input:** arr[] = [1, 2, 8, 10, 10, 12, 19], x = 11
**Output:** 4
**Explanation:** Largest Number less than or equal to 11 is 10, whose indices are 3 and 4. The index of last occurrence is 4.  

**Input:** arr[] = [1, 2, 8, 10, 10, 12, 19], x = 0  
**Output:** -1
**Explanation:** No element less than or equal to 0 is found. So, output is -1.

Code

O(n )
```java
 static int findFloor(long arr[], int n, long x)
    {
        
        // Naive
        for(int i=0;i < n; i++){
            
            if(arr[i] == x)
                return i;
            else if(arr[i] > x)
                return i-1;
            
        }
        
        return n-1;
        
    }
```

Expected Approach
```java
// Function to find the floor of a number x in a sorted array.
// Floor = greatest element in the array which is <= x.
// Returns the index of the floor element, or -1 if no such element exists.
static int findFloor(int[] arr, int x) {
    int low = 0, high = arr.length - 1;

    // This will store the index of the potential floor value
    int res = -1;

    while (low <= high) {
        int mid = (low + high) / 2; // Find the middle index

        if (arr[mid] <= x) {
            // arr[mid] is a valid floor candidate
            res = mid;

            // Try to find a larger value that is still <= x
            low = mid + 1;
        } else {
            // arr[mid] is too large, look on the left side
            high = mid - 1;
        }
    }

    // If found, returns index of floor; else returns -1
    return res;
}

```