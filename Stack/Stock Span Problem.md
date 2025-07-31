Given `N` days of stock prices `price[0...N-1]`, compute an array `span[0...N-1]`, where:

- `span[i] = max consecutive days before and including day i where price[j] ≤ price[i]`
****Examples:****

> ****Input:**** N = 7, price[] = [100 80 60 70 60 75 85]  
> ****Output:**** 1 1 1 2 1 4 6  
> ****Explanation:**** Traversing the given input span for 100 will be 1, 80 is smaller than 100 so the span is 1, 60 is smaller than 80 so the span is 1, 70 is greater than 60 so the span is 2 and so on. Hence the output will be 1 1 1 2 1 4 6.
> 
> ****Input:**** N = 6, price[] = [10 4 5 90 120 80]  
> ****Output:****1 1 2 4 5 1  
> ****Explanation:**** Traversing the given input span for 10 will be 1, 4 is smaller than 10 so the span will be 1, 5 is greater than 4 so the span will be 2 and so on. Hence, the output will be 1 1 2 4 5 1.

![[Pasted image 20250731225407.png]]
-------------------------------------------------------------------------------------------------
