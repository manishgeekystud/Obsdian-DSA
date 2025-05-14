Given an array ****arr[]**** and an integer ****k****, the task is to reverse every subarray formed by consecutive ****K**** elements.

****Examples:**** 

> ****Input:**** arr[] = [1, 2, 3, 4, 5, 6, 7, 8, 9], k = 3   
> ****Output:**** 3, 2, 1, 6, 5, 4, 9, 8, 7
> 
> ****Input:**** arr[] = [1, 2, 3, 4, 5, 6, 7, 8], k = 5   
> ****Output:**** 5, 4, 3, 2, 1, 8, 7, 6
> 
> ****Input:**** arr[] = [1, 2, 3, 4, 5, 6], k = 1   
> ****Output:**** 1, 2, 3, 4, 5, 6
> 
> ****Input:**** arr[] = [1, 2, 3, 4, 5, 6, 7, 8], k = 10   
> ****Output:**** 8, 7, 6, 5, 4, 3, 2, 1

Solution

 The problem can be solved based on the following idea:

> Consider every sub-array of size ****k**** starting from the beginning of the array and reverse it. We need to handle some special cases. 
> 
> - If ****k**** is not a multiple of n where n is the size of the array, for the last group we will have less than k elements left, we need to reverse all remaining elements. 
> - If k ****= 1****, the array should remain unchanged. If k >= n, we reverse all elements present in the array.
> 
> To reverse a subarray, maintain two pointers: left and right. Now, swap the elements at left and right pointers and increment left by 1 and decrement right by 1. Repeat till left and right pointers don't cross each other.!![[Pasted image 20250506212138.png]]

![[Pasted image 20250506212046.png]]
![[Pasted image 20250506212159.png]]![[Pasted image 20250506212332.png]]

```java
//Function to reverse every sub-array of size k
    static void reverseInGroups(int[] arr, int k) {
        int n = arr.length; 

        for (int i = 0; i < n; i += k) {
            int left = i;
            int right = Math.min(i + k - 1, n - 1); 

            // Reverse the sub-array
            while (left < right) {
                int temp = arr[left];
                arr[left] = arr[right];
                arr[right] = temp;
                left++;
                right--;
            }
        }
    }
```