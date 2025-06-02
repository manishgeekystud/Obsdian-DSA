Given an array of size n and an integer k, return the count of distinct numbers in all windows of size k. 

**Example:** 

**Input:** arr[] = {1, 2, 1, 3, 4, 2, 3};
       k = 4
**Output:** 3 4 4 3

**Explanation**:
First window is {1, 2, 1, 3}, count of distinct numbers is 3
Second window is {2, 1, 3, 4} count of distinct numbers is 4
Third window is {1, 3, 4, 2} count of distinct numbers is 4
Fourth window is {3, 4, 2, 3} count of distinct numbers is 3

**Input**: arr[] = {1, 2, 4, 4};
       k = 2
**Output**: 2 2 1

**Explanation**:
First window is {1, 2}, count of distinct numbers is 2
First window is {2, 4}, count of distinct numbers is 2
First window is {4, 4}, count of distinct numbers is 1
 

  
**Naive Approach:** The naive solution is to traverse the given array considering every window in it and keeping a count on the distinct elements of the window. 

**Algorithm:** 

1. For every index i from 0 to len_array(n) - k, i.e _n - k_, traverse the array from _i_ to _i + k_. This is the window
2. Traverse the window, from _i_ to that index and check if the element is present or not.
3. If the element is not present in the prefix of the array, i.e no duplicate element is present from _i_ to _index-1_, then increase the count.
4. Print the count.

Below is the implementation of the above approach:
