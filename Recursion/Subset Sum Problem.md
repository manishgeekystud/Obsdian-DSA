

## Problem Statement

You have a collection of non-negative values, representing available options, and a non-negative target value. Your task is to determine whether there exists a subset within the collection whose sum equals the given target value.

### Example

**Example1:**

```
Input: arr = [1, 2, 3], target_sum = 3
Output: True
Explanation: There is a subset (1, 2) with sum 3.
```

![subsets of the given set](https://www.scaler.com/topics/images/subsets-of-the-given-set.webp) 

**Example2:**

```
Input: arr = {10, 20, 30, 40, 50}, sum = 25
Output: False
Explanation: There is no subset whose sum will be equal to 25.
```

## Approach 1: Using Recursion

We can approach the Subset Sum Problem recursively by considering two cases for each element in the set:

1. **Case 1:** Include the current element in the subset. In this case, reduce the target sum by the value of the current element, and consider the remaining elements in the set.
2. **Case 2:** Exclude the current element from the subset. In this case, keep the target sum unchanged and consider the remaining elements in the set.

The recursion continues until we either find a subset that satisfies the target sum or exhaust all elements in the set.

Following is the recursion tree: 

![Recurrence Tree](https://www.scaler.com/topics/images/recurrence-tree.webp)

**Algorithm:**

1. Define a recursive function that takes the current index of the set and the remaining sum to be achieved.
2. For each index, check the base cases:
    - If the remaining sum is zero, return true (subset found).
    - If there are no elements left to consider (index becomes zero) and the remaining sum is still positive, return false (no subset found).
3. Recur by considering two cases:
    - Case 1: Include the current element and reduce the remaining sum by the value of the current element.
    - Case 2: Exclude the current element and keep the remaining sum unchanged.
4. If any of the recursive calls return true, then there exists a subset that satisfies the target sum; otherwise, no such subset exists.

### Code Implementation
````
// Java implementation of subset-sum using recursion 
class Solution {
  
    // This recursive function returns true if there exists a sum, else false
    static boolean SubsetSum(int set_1[], int N, int target_sum){
        // Base Case 1 if target sum reaches 0, we have found a subset sum equal to targetsum
        if (target_sum == 0)
            return true;
        // Base Case 2, if we reach the 0 index without finding the subset sum
        if (N == 0)
            return false;
  
        // if we find a element larger then the target we just don't include it in the subset
        if (set_1[N - 1] > target_sum)
            // we recurr without changing the sum and decrementing the index
            return SubsetSum(set_1, N - 1, target_sum);
  
        //  if the number is not greater than target_sum we call the both recurrance relations
        // if any of the below gives true, we have found the case.
        return SubsetSum(set_1, N - 1, target_sum) || SubsetSum(set_1, N - 1, target_sum - set_1[N - 1]);
    }
  
    // Driver code 
    
public static void main(String args[]){
    // given set of elements are:
    int set_1[] = {2, 3, 1, 1};
    
    // given target sum is :
    int target_sum = 4;
    // length of the set array 
    int N = set_1.length;
    // Calling the SubsetSum to check whether subset sum equals target sum in the given set of elements
    if (SubsetSum(set_1, N, target_sum))
        // if exists return true
        System.out.println("True");
    else
        // if not return false
        System.out.println("False");
    }
}
```

**Output:**

```
True
````