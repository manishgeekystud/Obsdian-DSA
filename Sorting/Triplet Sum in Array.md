Given an array **`arr[]`** and an integer **`target`**, determine if there exists a triplet in the array whose sum equals the given `target`.

Return `true` if such a triplet exists, otherwise, return `false`.

**Examples  
**

**Input**: `arr[] = [1, 4, 45, 6, 10, 8]`, `target = 13`   
**Output**: true   
**Explanation**: The triplet {1, 4, 8} sums up to 13

**Input**: `arr[] = [1, 2, 4, 3, 6, 7]`, `target = 10`   
**Output**: true   
**Explanation**: The triplets {1, 3, 6} and {1, 2, 7} both sum to 10. 

**Input**: `arr[] = [40, 20, 10, 3, 6, 7]`, `target = 24`   
**Output**: false   
**Explanation**: No triplet in the array sums to 24

----------------------------------------------------------------------
## 🪜 Brute Force Approach

### 🔧 Idea:

Try every combination of three numbers using three nested loops. Return true if any triplet adds up to the target.

### 🧑‍💻 Java Code:
```java
public boolean hasTripletBruteForce(int[] arr, int target) {
    int n = arr.length;
    for (int i = 0; i < n - 2; i++) {
        for (int j = i + 1; j < n - 1; j++) {
            for (int k = j + 1; k < n; k++) {
                if (arr[i] + arr[j] + arr[k] == target) {
                    return true;
                }
            }
        }
    }
    return false;
}

```


### ⏱ Time: `O(n³)`

### 📦 Space: `O(1)`

🟥 **Too slow for large inputs**

---

## ⚡ Efficient Approach: Two Pointers after Sorting

### 🔧 Idea:

1. **Sort** the array.
    
2. Loop through each element `i` and apply **two-pointer** approach to the subarray `arr[i+1 ... n-1]` to find if there is a pair that sums up to `target - arr[i]`.

```
import java.util.Arrays;

public class TripletSum {

    /**
     * Checks if any triplet in the array adds up to the target.
     */
    public static boolean hasTripletWithSum(int[] arr, int target) {
        // Step 1: Sort the array
        Arrays.sort(arr);

        // Step 2: Fix the first element one by one
        for (int i = 0; i < arr.length - 2; i++) {
            int left = i + 1;                  // Second pointer
            int right = arr.length - 1;        // Third pointer

            // Step 3: Use two pointers to find a pair with sum = target - arr[i]
            while (left < right) {
                int sum = arr[i] + arr[left] + arr[right];

                if (sum == target) {
                    return true; // Triplet found
                } else if (sum < target) {
                    left++; // Increase sum
                } else {
                    right--; // Decrease sum
                }
            }
        }

        // No triplet found that sums to target
        return false;
    }

    // Example Usage
    public static void main(String[] args) {
        System.out.println(hasTripletWithSum(new int[]{1, 4, 45, 6, 10, 8}, 13)); // true
        System.out.println(hasTripletWithSum(new int[]{1, 2, 4, 3, 6, 7}, 10));   // true
        System.out.println(hasTripletWithSum(new int[]{40, 20, 10, 3, 6, 7}, 24)); // false
    }
}

```