Given an array of integers ****arr[]**** of size ****N**** and an integer, the task is to rotate the array elements to the ****left**** by ****d**** positions.

****Examples:****  

> _****Input:****_   
> __arr[] = {1, 2, 3, 4, 5, 6, 7}, d = 2__  
> _****Output:****_ __3 4 5 6 7 1 2__
> 
> _****Input:****_ __arr[] = {3, 4, 5, 6, 7, 1, 2}, d=2__  
> _****Output:****_ __5 6 7 1 2 3 4__

_****Naive:****_

idea is to Rotate the Array by one position in lRotateOne which is easier to do
now run a loop for same method for D times

`class GFG {
    static void lRotateOne(int arr[], int n) {
        int temp = arr[0];
        for (int i = 1; i < n; i++) {
            arr[i - 1] = arr[i];
        }
        arr[n - 1] = temp;
    }

    static void leftRotate(int arr[], int d, int n) {
        for (int i = 0; i < d; i++) {
            lRotateOne(arr, n);
        }
    }
     
****Efficient Approach:****

```
  static void leftRotate(int arr[], int d, int n)
    {
    	int temp[] = new int[d];

    	for(int i = 0; i  < d; i++)
    	{
    		temp[i] = arr[i];
    	}

    	for(int i = d; i  < n; i++)
    	{
    		arr[i - d] = arr[i];
    	}

    	for(int i = 0; i  < d; i++)
    	{
    		arr[n - d + i] = temp[i];
    	}	
    }
```