
Difficulty: **Easy**
Given a binary sorted non-increasing array of 1s and 0s**.** You need to print the **count of 1s** in the binary array.

**Example 1:**

**Input:**
N = 8
arr[] = {1,1,1,1,1,0,0,0}
**Output:** 5
**Explanation:** Number of 1's in given 
binary array : 1 1 1 1 1 0 0 0 is 5.

**Example 2:**

**Input:**
N = 8
arr[] = {1,1,0,0,0,0,0,0}
**Output:** 2
**Explanation:** Number of 1's in given 
binary array : 1 1 0 0 0 0 0 0 is 2.

**Your Task:**  
The task is to complete the function **countOne**() which takes the array arr[] and its size N as inputs and returns the count of 1s in the input array.

------------------------------------------------------
## Expected Approach:

### Intuition

The intuition is to reduce our searching area. We can think of using binary search. Since given binary array is sorted and non increasing, so we can use the binary search approach here. and with the help of binary search check the starting position of 0, once the index of first 0 is found then return index as the total number of 1 present in the given array.

### Example:

> **array=[1,1,1,1,0,0,0]**
> 
> - **l=0, r=6**
>     - mid=3, array[3]=1  
>         now we will check if mid+1 is also 1 as we cannot skip count for any of the 1.
>     - but here mid+1 is 0,so the 1 at the mid is the last 1
>     - hence mid+1 that is **4 is the answer**.

### Implementation

- initialize variables low=0, high=N-1;
- iterate over the array while low <= high
    - initialize variable **mid** as  mid = (low+high)/2
    - check if mid element is equal to 1 and (mid + 1)th element is also equal to 1 then update low = mid + 1
    - if mid element is 0, then iterate for lower half, i.e., update high = mid-1, since the array is sorted reversely hence 1 must be present at right side of this mid only.
    - if mid == N-1 or mid element is equal to 1 and mid +1 th element is equal to 0 then return mid+1 as the total number of 1 present in the array.

### Complexity

**Time Complexity: O(log N)**, binary search approach takes O(log N)  
**Auxiliary Space: O(1)**, there is no required any extra space for binary

**Code**
```
//Back-end complete function Template for Java

class Solution{
    
    public static int countOnes(int arr[], int n){
        
        int low = 0, high = n-1;
        
        int mid = (low+high)/2;
        
        // Binary Search
        while(low <= high){
            
            mid = (low + high)/2;
            
            // if mid is 1, then check for upper half
            if(arr[mid] == 1 && mid+1 < n && arr[mid+1] == 1){
                low = mid+1;
            }
            
            // if mid is 0, then iterate for upper half
            else if(arr[mid] == 0){
                high = mid-1;
            }
            
            // else, iterate for lower half
        else if(arr[mid] == 1 && ((mid+1 < n && arr[mid+1] == 0) || (mid == n-1))){
                return mid+1;
            }
            
        }
        return 0;
    }
    
}
```