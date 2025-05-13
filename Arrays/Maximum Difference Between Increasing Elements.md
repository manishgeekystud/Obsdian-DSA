Given a **0-indexed** integer array `nums` of size `n`, find the **maximum difference** between `nums[i]` and `nums[j]` (i.e., `nums[j] - nums[i]`), such that `0 <= i < j < n` and `nums[i] < nums[j]`.

Return _the **maximum difference**._ If no such `i` and `j` exists, return `-1`.

**Example 1:**

**Input:** nums = [7,1,5,4]
**Output:** 4
**Explanation:**
The maximum difference occurs with i = 1 and j = 2, nums[j] - nums[i] = 5 - 1 = 4.
Note that with i = 1 and j = 0, the difference nums[j] - nums[i] = 7 - 1 = 6, but i > j, so it is not valid.

**Example 2:**

**Input:** nums = [9,4,3,2]
**Output:** -1
**Explanation:**
There is no i and j such that i < j and nums[i] < nums[j].

**Example 3:**

**Input:** nums = [**1**,5,2,**10**]
**Output:** 9
**Explanation:**
The maximum difference occurs with i = 0 and j = 3, nums[j] - nums[i] = 10 - 1 = 9.



## 🛠️ Brute Force Approach

### 🔍 Idea:

Check **every possible pair** `(i, j)` where `j > i`, and:

- If `nums[j] > nums[i]`, calculate `diff = nums[j] - nums[i]`
- Track the **maximum difference** found.

class Solution {
    public int maximumDifference(int[] nums) {
        int maxDiff=-1;
        int diff=Integer.MIN_VALUE;
        int n=nums.length;
        for(int i=0;i<n;i++)
        {
            for(int j=i+1;j<n;j++)
            {
                if(nums[j]>nums[i])
                   diff=nums[j]-nums[i];

                maxDiff=Math.max(maxDiff,diff);
            }
        }
        return maxDiff;
    }
}

Efficient Solution-Remember this problem and solution is similar to Stock Buy and Sell

## ✅ Efficient (Optimized) Approach — One Pass

### 🔍 Core Idea:

Instead of checking all pairs like brute force, keep track of the **minimum value seen so far** (`min`). For each element `nums[i]`, compute the difference from `min`. If the current number is greater than `min`, it's a valid candidate.

```
class Solution {
    public int maximumDifference(int[] nums) {
        int n = nums.length;
        int min = nums[0];         // Minimum seen so far (nums[i])
        int maxDiff = -1;
        int diff = Integer.MIN_VALUE;

        for (int i = 1; i < n; i++) {
            min = Math.min(min, nums[i]);

            if (nums[i] > min) {
                diff = nums[i] - min;
                maxDiff = Math.max(diff, maxDiff);
            }
        }

        return maxDiff;
    }
}

```

**clean**

public int maximumDifference(int[] nums) {
    int min = nums[0], maxDiff = -1;

    for (int i = 1; i < nums.length; i++) {
        if (nums[i] > min) {
            maxDiff = Math.max(maxDiff, nums[i] - min);
        } else {
            min = nums[i]; // update min if current is smaller
        }
    }

    return maxDiff;
}
