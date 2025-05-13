Given an integer array `nums`, move all `0`'s to the end of it while maintaining the relative order of the non-zero elements.

**Note** that you must do this in-place without making a copy of the array.

**Example 1:**

**Input:** nums = [0,1,0,3,12]
**Output:** [1,3,12,0,0]

**Example 2:**

**Input:** nums = [0]
**Output:** [0]

**Brute force** 

requires Extra space
```class Solution {
    public void moveZeroes(int[] nums) {
        int n = nums.length;
        int temp[] = new int[n];
        int m = n - 1;
        for (int i = 0; i < n; i++) {
            if (nums[i] == 0) {
                temp[m] = 0;
                m--;
            }
        }
        m = 0;
        for (int i = 0; i < n; i++) {
            if (nums[i] != 0) {
                temp[m] = nums[i];
                m++;
            }
        }

        for (int i = 0; i < n; i++) {
            nums[i] = temp[i];
        }

    }
}
```

==efficient==

**Goal:**  
Move all zeros in the array to the end **in-place**, keeping the order of non-zero elements unchanged.

**Approach (Two-pointer technique):**

- Use a pointer `count` to track the position for the next non-zero element.
    
- Traverse the array:
    
    - If `nums[i] != 0`, swap `nums[i]` with `nums[count]`, then increment `count`.
        
- This way, all non-zero elements are pushed to the front, and zeros are moved to the end.
    

**Time Complexity:** `O(n)`  
**Space Complexity:** `O(1)` (in-place)

**Example Dry Run:**  
Input: `[0, 1, 0, 3, 12]`  
Output: `[1, 3, 12, 0, 0]`
```java
  public void moveZeroes(int[] nums) {
        int count=0;
        for(int i =0;  i<nums.length;i++)
        {    
            //move all non zeros to front 
            if(nums[i]!=0)
            {   int temp=nums[count];
                nums[count]=nums[i];
                nums[i]=temp;
            count++;
            }
        }
        
    }
```
