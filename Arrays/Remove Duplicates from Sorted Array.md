Given a sorted array, the task is to remove the duplicate elements from the array.

****Examples:**** 

Input  : arr[] = {2, 2, 2, 2, 2}  
Output : arr[] = {2}  
         new size = 1  
  
Input  : arr[] = {1, 2, 2, 3, 4, 4, 4, 5, 5}  
Output : arr[] = {1, 2, 3, 4, 5}  
         new size = 5

Solution:-

# Intuition:

The Intuition is to use two pointers, `i` and `j`, to iterate through the array. The variable `j` is used to keep track of the current index where a unique element should be placed. The initial value of `j` is 1 since the first element in the array is always unique and doesn't need to be changed.

# Explanation:

The code starts iterating from `i = 1` because we need to compare each element with its previous element to check for duplicates.

The main logic is inside the `for` loop:

1. If the current element `nums[i]` is not equal to the previous element `nums[i - 1]`, it means we have encountered a new unique element.
2. In that case, we update `nums[j]` with the value of the unique element at `nums[i]`, and then increment `j` by 1 to mark the next position for a new unique element.
3. By doing this, we effectively overwrite any duplicates in the array and only keep the unique elements.

Once the loop finishes, the value of `j` represents the length of the resulting array with duplicates removed.

Finally, we return `j` as the desired result.

soln:
```java
class Solution {
    public int removeDuplicates(int[] nums) {
        int j = 1;
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] != nums[i - 1]) {
                nums[j] = nums[i];
                j++;
            }
        }
        return j;
    }
}
```

