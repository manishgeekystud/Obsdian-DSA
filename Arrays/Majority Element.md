Given an array `nums` of size `n`, return _the majority element_.

The majority element is the element that appears more than `⌊n / 2⌋` times. You may assume that the majority element always exists in the array.

**Example 1:**

**Input:** nums = [3,2,3]
**Output:** 3

**Example 2:**

**Input:** nums = [2,2,1,1,1,2,2]
**Output:** 2

Solution

__The basic solution is to have two loops and keep track of the__ _****maximum****_ __count for all different elements. If the maximum count becomes greater than__ _****n/2****_ __then break the loops and return the element having the maximum count. If the maximum count doesn’t become more than n/2 then the majority element__  doesnt exist

Follow the steps below to solve the given problem:

- Create a variable to store the max count, __count = 0__
- Traverse through the array from start to end.
- For every element in the array run another loop to find the count of similar elements in the given array.
- If the count is greater than the max count update the max count and store the index in another variable.
- If the maximum count is greater than half the size of the array, print the element. Else print there is no majority element.

Code
```java
// Java program to find Majority
// element in an array

import java.io.*;

class GFG {

	// Function to find Majority element
	// in an array
	static void findMajority(int arr[], int n)
	{
		int maxCount = 0;
		int index = -1; // sentinels
		for (int i = 0; i < n; i++) {
			int count = 0;
			for (int j = 0; j < n; j++) {
				if (arr[i] == arr[j])
					count++;
			}

			// update maxCount if count of
			// current element is greater
			if (count > maxCount) {
				maxCount = count;
				index = i;
			}
		}

		// if maxCount is greater than n/2
		// return the corresponding element
		if (maxCount > n / 2)
			System.out.println(arr[index]);

		else
			System.out.println("No Majority Element");
	}

```

but this n2 solution we nee