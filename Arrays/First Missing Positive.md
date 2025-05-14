
### Overview

**Input:** arr[] = [2, -3, 4, 1, 1, 7]
**Output:** 3
**Explanation:** Smallest positive missing number is 3.

The task is to find the smallest positive integer that is not present in `nums`.

Note that positive integers are greater than zero.

Let's discuss the two main cases:

**1. No Missing Integer in `nums`:**

| 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |

`nums` contains `9` elements. The smallest missing positive integer is `10`.

For an array of length `n`, if the array contains all of the integers in the range `1` to `n`, the smallest missing positive integer is `n + 1`.

**2. Missing Integer in `nums`:**

|-10|1|2|2|3|4|6|6|8|
|---|---|---|---|---|---|---|---|---|

`nums` contains `9` elements. The smallest missing positive integer is `5`.

For an array of length `n`, if the array does not contain all of the integers in the range `1` to `n`, the smallest missing positive integer is the first integer missing from that range.

Let's also discuss the constraints:

> You must implement an algorithm that runs in O(n) time and uses O(1) auxiliary space.

**1. Time Complexity:**

Hint number three reminds us that O(2n)=O(n). While we know that one does not equal two, O notation describes an algorithm's limiting behavior as the input size grows toward infinity.

**2. Space Complexity:**

The optimized approaches in this article use in-place solutions. Does in-place mean a constant space complexity? By [definition](https://en.wikipedia.org/wiki/In-place_algorithm), an in-place algorithm transforms the input using no auxiliary data structures proportional to the input size. An in-place algorithm does not necessarily mean constant space complexity; for example, an in-place recursive algorithm uses the recursion stack, so the space is not constant.

The problem specifically asks us to use constant _auxiliary_ space, so in-place solutions meet this criterion.

---

### Approach 1: Boolean Array

#### Intuition

We can solve the problem by iterating through the numbers `1` to `n`, and use linear search to determine whether each number is in the array. The first number we cannot find is the smallest missing integer. This approach would result in a quadratic time complexity.

We need to determine whether an element is in the array in constant time. Array indexing provides constant lookup time. We need to check the existence of a relatively small range of values, positive numbers between `1` and `n`, so we can use an array like a hash table by using the index as a key and the value as a presence indicator. The default value is `false`, which represents a missing number, and we set the value to `true` for keys that exist in `nums`. Numbers not in the range `1` to `n` are not relevant in the search for the first missing positive, so we do not mark them in the `seen` array.

To solve the problem, we can create an array of size `n + 1`. For each positive number less than `n` in `nums`, we set `seen[num]` to `true`. Then, we iterate through the integers `1` to `n` and return the first number that is not marked as seen in the array. If the array contains all of the elements `1` to `n`, we return `n + 1`.

> **Note:** This approach does not meet the problem constraint of solving the problem using constant auxiliary space. It is included to make the solution accessible, and it can provide valuable background for solving the problem within the space constraints. Other approaches that do not meet the time and/or space constraints are not included as they are less relevant to understanding the following approaches.

#### Algorithm

1. Initialize a variable `n` to the length of `nums`.
    
2. Initialize an array `seen` to size `n + 1`.
    
3. Mark the elements in `nums` as seen in the array `seen`.
    
    - For each `num` in `nums`, if `num` is greater than `0` and less than or equal to `n`, set `seen[num]` to `true`.
4. Find the smallest missing positive number:
    
    - For `i` from `1` to `n`, If `seen[i]` is not `true`, return `i`, the smallest missing integer.
5. If `seen` contains all elements `1` to `n`, return `n + 1` as the smallest missing positive number.
    

#### Implementation
```
 public int firstMissingPositive(int[] nums) {
        int n = nums.length;
        boolean[] seen = new boolean[n + 1]; // Array for lookup

        // Mark the elements from nums in the lookup array
        for (int num : nums) {
            if (num > 0 && num <= n) {
                seen[num] = true;
            }
        }

        // Iterate through integers 1 to n
        // return smallest missing positive integer
        for (int i = 1; i <= n; i++) {
            if (!seen[i]) {
                return i;
            }
        }

        // If seen contains all elements 1 to n
        // the smallest missing positive number is n + 1
        return n + 1;
    }
```

TC- O(n)  SC - O(n)

**Approach 2**

```java
public int missingNumber(int[] arr) {
        // Your code here
        int n = arr.length;
        int res=1;
        Arrays.sort(arr);
        for(int i=0;i<n;i++)
        {
            if(arr[i]==res)
              res++;
              
            else if(arr[i]>res)
               break;
        }
        
        return res;
    }
```

**Approach 3**
### ****[Expected Approach] Using Cycle Sort - O(n) Time and O(1) Space****

> The idea is similar to [Cycle Sort](https://www.geeksforgeeks.org/cycle-sort/) and move each element in the array to its correct position based on its value. So for each number, say ****x,**** such that 1 <= x <= n, is placed at the (x - 1)th index.
> 
> Finally, iterate through the array and check if the numbers are in the expected indexes or not. The first place where the number doesn’t match its index gives us the first missing positive number. If all the numbers from 1 to n, are at their correct indexes, then the next number i.e., ****n + 1****, is the smallest missing positive number.

![[Pasted image 20250512230408.png]]

![[Pasted image 20250512230432.png]]
![[Pasted image 20250512230452.png]]
![[Pasted image 20250512230508.png]]
![[Pasted image 20250512230518.png]]
![[Pasted image 20250512230530.png]]
![[Pasted image 20250512230543.png]]
![[Pasted image 20250512230554.png]]
![[Pasted image 20250512230603.png]]
![[Pasted image 20250512230617.png]]

**Code**
```
    // Function for finding the first missing positive number
    static int missingNumber(int[] arr) {
        int n = arr.length;
        for (int i = 0; i < n; i++) {

            // if arr[i] is within the range [1, n] and arr[i]
            // is not placed at (arr[i]-1)th index in arr
            while (arr[i] >= 1 && arr[i] <= n
                   && arr[i] != arr[arr[i] - 1]) {

                // then swap arr[i] and arr[arr[i]-1] to
                // place arr[i] to its corresponding index
                int temp = arr[i];
                arr[i] = arr[arr[i] - 1];
                arr[temp - 1] = temp;
            }
        }

        // If any number is not at its corresponding index 
        // then it is the missing number
        for (int i = 1; i <= n; i++) {
            if (i != arr[i - 1]) {
                return i;
            }
        }

        // If all number from 1 to n are present then n+1 
        // is smallest missing number
        return n + 1;
    }

```





