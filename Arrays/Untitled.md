```java
class Solution {

    public int maxSubarraySumCircular(int[] nums) {

          // Your code here

        int n=nums.length;

        int result=Integer.MIN_VALUE;

        int normalMax= kadaneMax(nums);

        int minSubArraySum=kadaneMin(nums);

        int tSum=0;

        for(int i=0;i<n;i++)

           tSum+=nums[i];

  

        int circularMax=tSum-minSubArraySum;

       return (circularMax == 0) ? normalMax : Math.max(normalMax, circularMax) ;

    }

    public int kadaneMax(int[] nums)

    {

        int maxSum=Integer.MIN_VALUE;

        int sum=0;

        for(int i=0;i<nums.length;i++)

        {

            if(sum<0)

               sum=nums[i];

            else

              sum+=nums[i];

  

            maxSum=Math.max(sum,maxSum);

        }

        return maxSum;

    }

  

   public int kadaneMin(int[] nums) {

    int minSum = Integer.MAX_VALUE;

    int sum = 0;

    for (int i = 0; i < nums.length; i++) {

        if (sum > 0)

            sum = nums[i];     // start new subarray

        else

            sum += nums[i];    // extend previous subarray

  

        minSum = Math.min(sum, minSum);  // update minimum

    }

  

    return minSum;

}

  

}

```