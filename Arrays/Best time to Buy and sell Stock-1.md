ou are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

You want to maximize your profit by choosing a **single day** to buy one stock and choosing a **different day in the future** to sell that stock.

Return _the maximum profit you can achieve from this transaction_. If you cannot achieve any profit, return `0`.

**Example 1:**

**Input:** prices = [7,1,5,3,6,4]
**Output:** 5
**Explanation:** Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.

**Example 2:**

**Input:** prices = [7,6,4,3,1]
**Output:** 0
**Explanation:** In this case, no transactions are done and the max profit = 0.


solution

**Brute Force**

  public static int maxProfit(int[] prices) {
        int maxProfit = 0;
        int n = prices.length;

        for (int i = 0; i < n - 1; i++) {
            for (int j = i + 1; j < n; j++) {
                int profit = prices[j] - prices[i];
                maxProfit = Math.max(maxProfit, profit);
            }
        }

        return maxProfit;
    }

**Efficient**

```
public int maxProfit(int[] prices) {
        int min = Integer.MAX_VALUE;
        int profit = Integer.MIN_VALUE;
        
        for (int i = 0; i < prices.length; i++) {
            min = Math.min(prices[i],min);
            profit = Math.max(profit, prices[i] - min);
        }
        return profit;
    }

```