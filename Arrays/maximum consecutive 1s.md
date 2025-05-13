In a realm where numbers hold secrets, a captivating challenge awaits, which is, **To Find Maximum Consecutive 1s !!!**

**Our Task**: Given a binary array, find the count of the maximum number of consecutive 1's present in the array.

![](https://media.geeksforgeeks.org/wp-content/uploads/20230621200054/Maximum-consicutive-1's.jpg)

**Examples :** 

> **Input:** arr[] = {1, 1, 0, 0, 1, 0, 1, 0, 1, 1, 1, 1}
> **Output:** 4
> 
> **Input:** arr[] = {0, 0, 1, 0, 1, 0, 1, 0, 1, 0, 1}
> **Output:** 1

We have 2 approaches to solve the problem: **Naive Approach** and **Efficient Approach**

### 1) Naive Approach:

In this approach, we use two looks and traverse the array from start to end. At each element, we check if it is 1 or 0. If the element is 1, we increment the count variable and count the number of 1s along with it if any. After each completion of the inner loop, we find the maximum between the current count and the previous count.

**Time Complexity :** O(n2)   
**Auxiliary Space :** O(1)

### **2)  Efficient Approach:**

An efficient solution is to traverse the array from left to right. If we see a 1, we increment the count and compare it with the maximum so far. If we see a 0, we reset the count to 0.

**Time Complexity :** O(n)   
**Auxiliary Space :** O(1)

**Brute**

```
   static int maxConsecutiveOnes(int arr[], int n)
    {
    	int res = 0;

    	for(int i = 0; i < n; i++)
    	{
    		int curr = 0;

    		for(int j = i; j < n; j++)
    		{
    			if(arr[j] == 1) curr++;
    			else break;
    		}

    		res = Math.max(res, curr);
    	}
    	
    	return res;
    }
```
**Efficient**

    static int maxConsecutiveOnes(int arr[], int n)
    {
    	int res = 0, curr = 0;

    	for(int i = 0; i < n; i++)
    	{
    		if(arr[i] == 0)
    			curr = 0;
    		else
    		{
    			curr++;

    			res = Math.max(res, curr);
    		}
    	}
    	
    	return res;
    