Given a **sorted** array **arr[]** of distinct integers. Sort the array into a wave-like array(In Place). In other words, arrange the elements into a sequence such that arr[1] >= arr[2] <= arr[3] >= arr[4] <= arr[5].....  
If there are multiple solutions, find the lexicographically smallest one.

**Note:** The given array is sorted in ascending order, and you don't need to return anything to change the original array.

**Examples:**

**Input:** arr[] = [1, 2, 3, 4, 5]
**Output: [**2, 1, 4, 3, 5]
**Explanation:** Array elements after sorting it in the waveform are 2, 1, 4, 3, 5.

**Input:** arr[] = [2, 4, 7, 8, 9, 10]
**Output: [**4, 2, 8, 7, 10, 9]
**Explanation:** Array elements after sorting it in the waveform are 4, 2, 8, 7, 10, 9.  
  
Input: arr[] = [1]  
Output: [1]

must do in O(n) time and O(1) space

solution

```java
 public static void swap(int arr[], int from, int to){
        int temp = arr[from];
        arr[from] = arr[to];
        arr[to] = temp;
    }
    public static void convertToWave(int arr[], int n){
        
        // Your code here
        if(n%2!=0) n--;
        
        for(int i=0; i<n; i+=2){
            swap(arr, i, i+1);
        }
    }
```