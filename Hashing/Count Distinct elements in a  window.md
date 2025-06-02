Given an array of size n and an integer k, return the count of distinct numbers in all windows of size k. 

**Example:** 

**Input:** arr[] = {1, 2, 1, 3, 4, 2, 3};
       k = 4
**Output:** 3 4 4 3

**Explanation**:
First window is {1, 2, 1, 3}, count of distinct numbers is 3
Second window is {2, 1, 3, 4} count of distinct numbers is 4
Third window is {1, 3, 4, 2} count of distinct numbers is 4
Fourth window is {3, 4, 2, 3} count of distinct numbers is 3

**Input**: arr[] = {1, 2, 4, 4};
       k = 2
**Output**: 2 2 1

**Explanation**:
First window is {1, 2}, count of distinct numbers is 2
First window is {2, 4}, count of distinct numbers is 2
First window is {4, 4}, count of distinct numbers is 1
 

  
**Naive Approach:** The naive solution is to traverse the given array considering every window in it and keeping a count on the distinct elements of the window. 

**Algorithm:** 

1. For every index i from 0 to len_array(n) - k, i.e _n - k_, traverse the array from _i_ to _i + k_. This is the window
2. Traverse the window, from _i_ to that index and check if the element is present or not.
3. If the element is not present in the prefix of the array, i.e no duplicate element is present from _i_ to _index-1_, then increase the count.
4. Print the count.

Below is the implementation of the above approach:
```java
// Simple Java program to count distinct elements in every
// window of size k

import java.util.Arrays;

class Test {
    // Counts distinct elements in window of size k
    static int countWindowDistinct(int win[], int k)
    {
        int dist_count = 0;

        // Traverse the window
        for (int i = 0; i < k; i++) {
            // Check if element arr[i] exists in arr[0..i-1]
            int j;
            for (j = 0; j < i; j++)
                if (win[i] == win[j])
                    break;
            if (j == i)
                dist_count++;
        }
        return dist_count;
    }

    // Counts distinct elements in all windows of size k
    static void countDistinct(int arr[], int n, int k)
    {
        // Traverse through every window
        for (int i = 0; i <= n - k; i++)
            System.out.println(countWindowDistinct(Arrays.copyOfRange(arr, i, arr.length), k));
    }

    // Driver method
    public static void main(String args[])
    {
        int arr[] = { 1, 2, 1, 3, 4, 2, 3 }, k = 4;

        countDistinct(arr, arr.length, k);
    }
}
```

**Efficient** **Approach**

![[Pasted image 20250602232830.png]]
