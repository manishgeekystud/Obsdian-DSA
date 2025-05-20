Given a positive integer **n,** find the square root of n. If **n** is not a perfect square, then return the floor value.

> Floor value of any number is the greatest Integer which is less than or equal to that number

**Examples:**

**Input:** n = 4
**Output:** 2
**Explanation:** Since, 4 is a perfect square, so its square root is 2.  

**Input:** n = 11
**Output:** 3
**Explanation:** Since, 11 is not a perfect square, floor of square root of 11 is 3.

**Input:** n = 1
**Output:** 1

**Constraints:**  
1 ≤ n ≤  3 x 104

![[Pasted image 20250521011046.png]]
![[Pasted image 20250521011108.png]]
![[Pasted image 20250521011122.png]]
![[Pasted image 20250521011134.png]]
![[Pasted image 20250521011144.png]]
![[Pasted image 20250521011153.png]]
![[Pasted image 20250521011207.png]]
![[Pasted image 20250521011215.png]]

code
```java
// Java program to find the square root of given integer
// using binary search

class GfG {
  
    static int floorSqrt(int n) {
  
        // Initial search space
        int lo = 1, hi = n;
        int res = 1;
        
        while (lo <= hi) {
            int mid = lo + (hi - lo) / 2;
            
            // If square of mid is less than or equal to n 
            // update the result and search in upper half
            if (mid * mid <= n) {
                res = mid;
                lo = mid + 1;
            }
            
            // If square of mid exceeds n, 
            // search in the lower half
            else {
                hi = mid - 1;
            }
        }
        
        return res;
    }
```