You are given an integer array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

On each day, you may decide to buy and/or sell the stock. You can only hold **at most one** share of the stock at any time. However, you can buy it then immediately sell it on the **same day**.

Find and return _the **maximum** profit you can achieve_.

**Example 1:**

**Input:** prices = [7,1,5,3,6,4]
**Output:** 7
**Explanation:** Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
Total profit is 4 + 3 = 7.

**Example 2:**

**Input:** prices = [1,2,3,4,5]
**Output:** 4
**Explanation:** Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
Total profit is 4.

**Example 3:**

**Input:** prices = [7,6,4,3,1]
**Output:** 0
**Explanation:** There is no way to make a positive profit, so we never buy the stock to achieve the maximum profit of 0.


### 💡 Brute Force – Idea:

- Try **every possible buy and sell day pair**.
  For every profitable transaction (`prices[j] > prices[i]`):
    
    - Calculate the **current profit**: `prices[j] - prices[i]`.
    - Then look ahead to **simulate future profits** using greedy logic starting from day `j+1`.
- Update and track the **maximum total profit** obtained this way.
    ---

### 🔁 Algorithm Steps:

1. Loop over all possible buy days `i`.
2. For each `i`, loop over all sell days `j > i`.
3. If the transaction is profitable (`prices[j] > prices[i]`):
    - Calculate current profit = `prices[j] - prices[i]`
    - Add future profit from `j+1` onward using a nested loop (greedy).
4. Track the **maximum total profit** across all valid buy-sell pairs

```
    public static int maxProfit(int[] prices) {
        int n = prices.length;
        int maxProfit = 0;

        for (int i = 0; i < n - 1; i++) {
            for (int j = i + 1; j < n; j++) {
                if (prices[j] > prices[i]) {
                    int currentProfit = prices[j] - prices[i];

                    // Simulate future profits after selling at j
                    int futureProfit = 0;
                    for (int k = j + 1; k < n; k++) {
                        if (prices[k] > prices[k - 1]) {
                            futureProfit += prices[k] - prices[k - 1];
                        }
                    }

                    maxProfit = Math.max(maxProfit, currentProfit + futureProfit);
                }
            }
        }

        return maxProfit;
    }
```

### 💡 Greedy Strategy: Efficient

- Whenever the **next day's price is higher than the current day's**, we can consider this as a profitable opportunity.
    
- So, we **buy on day i** and **sell on day i+1** whenever `prices[i+1] > prices[i]`.
    
- This is equivalent to **summing all upward price differences**.
    

---

### ✅ Algorithm Steps:

1. Initialize `maxProfit = 0`.
    
2. Iterate from day 1 to end of prices.
    
3. If `prices[i] > prices[i-1]`, add the difference to `maxProfit`.
    
4. Return `maxProfit` at the end.

```
  public int maxProfit(int[] prices) {
        
        int diff=0;
        int profit=0;

        for(int i=1;i<prices.length;i++)
        {
            diff=prices[i]-prices[i-1];
            if(diff>0)
            profit+=diff;
        }
        return profit;
    }
```