# Best Time to Buy and Sell Stock

## Problem

Given an array `prices`, where `prices[i]` is the stock price on day `i`, find the maximum profit from **one buy and one sell**.

The buy day must come **before** the sell day.

If no profit is possible, return `0`.

## Approach

Use a **single pass** through the array.

Maintain:

* `minPrice` → minimum price seen so far
* `maxProfit` → maximum profit found so far

For every price:

1. Update the minimum buying price.
2. Calculate profit if we sell today.
3. Update `maxProfit`.

```cpp
minPrice = min(minPrice, prices[i]);
maxProfit = max(maxProfit, prices[i] - minPrice);
```

## Code

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {

        int minPrice = prices[0];
        int maxProfit = 0;

        for(int i = 1; i < prices.size(); i++) {

            minPrice = min(minPrice, prices[i]);

            int profit = prices[i] - minPrice;

            maxProfit = max(maxProfit, profit);
        }

        return maxProfit;
    }
};
```

## Example

```text
prices = [7,1,5,3,6,4]

Minimum price = 1
Best selling price after it = 6

Profit = 6 - 1 = 5
```

## Complexity

* **Time:** `O(n)`
* **Space:** `O(1)`

## Revision Shortcut

**Minimum price → Current profit → Maximum profit**

Remember:

```text
minPrice = cheapest price seen so far
profit = current price - minPrice
```

### Important

We scan **left to right**, so the minimum price is always from a previous day.

```text
BUY → SELL
```

Never:

```text
SELL → BUY
```
