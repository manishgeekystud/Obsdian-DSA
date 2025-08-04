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
You’re watching the **stock price of a company** every day.

Let’s say these are the prices over a few days:
`Day     1   2   3   4   5   6   7
 Price      100  80    60  70     60    75   85`

Now, for each day, we want to answer:

> **"How many consecutive days up to today (including today) has the price been less than or equal to today’s price?"**

This is called the **"stock span"**.

### 📊 Breakdown:

Let’s go **day-by-day**:

- **Day 1: Price = 100**
    
    - No previous day. So, span = 1
        
- **Day 2: Price = 80**
    
    - Yesterday was 100 (more), so only today counts → span = 1
        
- **Day 3: Price = 60**
    
    - Yesterday was 80 (more), so only today counts → span = 1
        
- **Day 4: Price = 70**
    
    - Yesterday was 60 (less) ✅ → keep counting back
        
    - Day 2: 80 (more) ❌ → stop
        
    - So span = 2 (Day 4 and 3)
        
- **Day 5: Price = 60**
    
    - Yesterday was 70 (more), so only today counts → span = 1
        
- **Day 6: Price = 75**
    
    - Day 5: 60 ✅
        
    - Day 4: 70 ✅
        
    - Day 2: 80 ❌ → stop
        
    - So span = 4 (Day 6, 5, 4, 3)
        
- **Day 7: Price = 85**
    
    - All prices before are less! ✅
        
    - So span = 6
        

---

### ✅ Final Span Array:


`Day:    1   2  3  4  5  6  7 
Price:       100 80  60 70  60 75  85 
Span:        1     1    1    2  1    4   6


===========================================================
**solution**

**==Brute Force==**

### 🔸 Idea:

For each day `i`:

- Look backwards to count how many consecutive days (including today) the stock price was **less than or equal** to today's price.
    
- Stop when you hit a day with a **higher price**
    

This is a simple **O(n²)** approach.

**CODE**
```java
public ArrayList<Integer> calculateSpan(int[] price) {
    ArrayList<Integer> span = new ArrayList<>();

    for (int i = 0; i < price.length; i++) {
        int count = 1;  // Span always includes current day

        // Look back at previous days
        for (int j = i - 1; j >= 0; j--) {
            if (price[j] <= price[i]) {
                count++;
            } else {
                break;  // Stop if previous price is greater
            }
        }

        span.add(count);
    }

    return span;
}


```
