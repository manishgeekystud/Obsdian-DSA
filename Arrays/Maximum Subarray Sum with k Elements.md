****Examples :**** 

****Input  :**** arr[] = {100, 200, 300, 400}  
         k = 2  
****Output :**** 700  
  
****Input  :**** arr[] = {1, 4, 2, 10, 23, 3, 1, 0, 20}  
         k = 4   
****Output :**** 39  
We get maximum sum by adding subarray {4, 2, 10, 23}  
of size 4.  
  
****Input  :**** arr[] = {2, 3}  
         k = 3  
****Output :**** Invalid  
There is no subarray of size 3 as size of whole  
array is 2.

**Naive**
```java
    static int maxSum(int arr[], int n, int k)
    {
        // Initialize result
        int max_sum = Integer.MIN_VALUE;

        // Consider all blocks starting with i.
        for (int i = 0; i < n - k + 1; i++) {
            int current_sum = 0;
            for (int j = 0; j < k; j++)
                current_sum = current_sum + arr[i + j];

            // Update result if required.
            max_sum = Math.max(current_sum, max_sum);
        }

        return max_sum;
    }
```
 


    

**Efficient Approach**

The below representation will make it clear how the window slides over the array.

> Consider an array ****arr[]**** = {5, 2, -1, 0, 3} and value of ****k**** = 3 and ****n**** = 5
> 
> This is the initial phase where we have calculated the initial window sum starting from index 0 . At this stage the window sum is 6. Now, we set the maximum_sum as current_window i.e 6.   
>  
> 
> ![](https://media.geeksforgeeks.org/wp-content/uploads/sliding-window1.png)
> 
> Now, we slide our window by a unit index. Therefore, now it discards 5 from the window and adds 0 to the window. Hence, we will get our new window sum by subtracting 5 and then adding 0 to it. So, our window sum now becomes 1. Now, we will compare this window sum with the maximum_sum. As it is smaller, we won't change the maximum_sum.   
>  
> 
> ![](https://media.geeksforgeeks.org/wp-content/uploads/sliding-window2.png)
> 
>   
> Similarly, now once again we slide our window by a unit index and obtain the new window sum to be 2. Again we check if this current window sum is greater than the maximum_sum till now. Once, again it is smaller so we don't change the maximum_sum.  
> Therefore, for the above array our maximum_sum is 6.
> 
> ![](https://media.geeksforgeeks.org/wp-content/uploads/sliding-window3.png)

```java
static int maxSum(int arr[], int n, int k)
    {
        // n must be greater
        if (n <= k) {
            System.out.println("Invalid");
            return -1;
        }

        // Compute sum of first window of size k
        int max_sum = 0;
        for (int i = 0; i < k; i++)
            max_sum += arr[i];

        // Compute sums of remaining windows by
        // removing first element of previous
        // window and adding last element of
        // current window.
        int window_sum = max_sum;
        for (int i = k; i < n; i++) {
            window_sum += arr[i] - arr[i - k];
            max_sum = Math.max(max_sum, window_sum);
        }

        return max_sum;
    }
```