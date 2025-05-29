You are given an array of integers **arr[]**. You need to print the count of non-repeated elements in the array.

**Example 1:**

**Input:** arr[] = [1, 1, 2, 2, 3, 3, 4, 5, 6, 7]
**Output:** 4
**Explanation:** 4, 5, 6 and 7 are the elements with frequency 1 and rest elements are repeated so the number of non-repeated elements are 4.

**Input:** arr[] = [10, 20, 30, 40, 10]
**Output:** 3
**Explanation:** 20, 30, 40 are the elements with the frequency 1 and 10 is the repeated element to number of non-repeated elements are 3.

----------------------------------------------------------------------
```java
 static int countNonRepeated(int arr[]) {
        // add your code
        HashMap<Integer,Integer> hm=new HashMap<>();
        for(int n:arr)
        {
            if(hm.containsKey(n))
              hm.put(n,hm.get(n)+1);
            else
              hm.put(n,1);
        }
        int count=0;
        for(int n:hm.values())
        {
            if(n==1)
            count++;
        }
        return count;
    }
```