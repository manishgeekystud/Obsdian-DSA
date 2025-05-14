Given an array of **positive** integers. Your task is to rearrange the array elements alternatively i.e. first element should be the max value, the second should be the min value, the third should be the second max, the fourth should be the second min, and so on.  
**Note:** Modify the original array itself. Do it without using any extra space. You do not have to return anything.

**Examples:**

**Input:** arr[] = [1, 2, 3, 4, 5, 6]
**Output:** [6, 1, 5, 2, 4, 3]
**Explanation:** Max element = 6, min = 1, second max = 5, second min = 2, and so on... The modified array is: [6, 1, 5, 2, 4, 3]

**Input:** arr[]= [10, 20, 30, 40, 50, 60, 70, 80, 90, 100, 110]
**Output:** [110, 10, 100, 20, 90, 30, 80, 40, 70, 50, 60]
**Explanation:** Max element = 110, min = 10, second max = 100, second min = 20, and so on... Modified array is : [110, 10, 100, 20, 90, 30, 80, 40, 70, 50, 60]

**Input:** arr[]= [1]
**Output:** [1]

**Brute force O(n)**

```java
import java.util.*;

public class Solution {
    public static void rearrangeBruteForce(int[] arr) {
        int n = arr.length;
        int[] temp = new int[n];
        
        int start = 0;          // pointer to smallest
        int end = n - 1;        // pointer to largest
        boolean flag = true;    // to alternate between max and min
        Arrays.sort(arr);
        
        for (int i = 0; i < n; i++) {
            if (flag) {
                temp[i] = arr[end--]; // place largest
            } else {
                temp[i] = arr[start++]; // place smallest
            }
            flag = !flag;
        }

        // Copy back to original array
        for (int i = 0; i < n; i++) {
            arr[i] = temp[i];
        }
    }
}

```

**Efficient**
✅ Problem Recap
Goal: Rearrange the array so that it becomes:
[Max, Min, 2nd Max, 2nd Min, ...]
📌 Constraints:

Do it in-place — i.e., no extra array allowed

Use O(1) extra space

Only rearrange, don’t sort or return a new array

🔧 Trick to Solve In-place
We use the idea of encoding two numbers into one slot (Desi jugaad style!) — very similar to the arr[i] = old + new × multiplier trick used in other in-place problems.

🎩 Encoding Strategy:
Let:

max_idx = index of current max element (starting from end)
min_idx = index of current min element (starting from start)
max_elem = some number greater than the maximum element in the array (for encoding)

We use:
**arr[i] = arr[i] + (value_to_store % max_elem) * max_elem;**
And to decode:
**arr[i] = arr[i] / max_elem;**


```java
public class Solution {
    public static void rearrange(long arr[], int n) {
        int max_idx = n - 1;
        int min_idx = 0;
        long max_elem = arr[n - 1] + 1; // +1 to ensure it's > all elements
        Arrays.sort(arr);

        for (int i = 0; i < n; i++) {
            // Place max at even indexes, min at odd
            if (i % 2 == 0) {
                arr[i] = arr[i] + (arr[max_idx] % max_elem) * max_elem;
                max_idx--;
            } else {
                arr[i] = arr[i] + (arr[min_idx] % max_elem) * max_elem;
                min_idx++;
            }
        }

        // Decode actual values
        for (int i = 0; i < n; i++) {
            arr[i] = arr[i] / max_elem;
        }
    }
}


```
## 🧠 Desi Tip to Remember

> “Jab jagah kam ho, toh ek dabbe mein do cheezein chipka do!  
> Pehle value chhupa do encoding se, baad mein nikaal lo division se.” 😄