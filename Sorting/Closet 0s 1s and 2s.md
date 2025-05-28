Given an array of 0s, 1s, and 2s. Arrange the array elements such that all 0s come first, followed by all the 1s and then, all the 2s.

**Note:** Do not use the inbuilt sort function.  
 

**Example 1:**

**Input**: N = 5, arr[] = {0, 2, 1, 2, 0}
**Output**: 0 0 1 2 2

**Example 2:**

**Input**: N = 3, arr[] = {0, 1, 0}
**Output**: 0 0 1

======================================================

```java
public static void segragate012(int arr[], int N) {
    int c0 = 0, c1 = 0, c2 = 0;  // Counters for 0s, 1s, and 2s
    int i = 0;

    // Count the number of 0s, 1s, and 2s
    for (int n : arr) {
        if (n == 0)
            c0++;
        else if (n == 1)
            c1++;
        else
            c2++;
    }

    // Overwrite array with 0s
    while (c0 > 0) {
        arr[i] = 0;
        c0--;
        i++;
    }

    // Overwrite array with 1s
    while (c1 > 0) {
        arr[i] = 1;
        c1--;
        i++;
    }

    // Overwrite array with 2s
    while (c2 > 0) {
        arr[i] = 2;
        c2--;
        i++;
    }
}

```