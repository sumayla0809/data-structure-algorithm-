# Best Time to Buy and Sell Stock II

## Approach

Here, we can make **multiple transactions**.

So whenever today's price is greater than yesterday's price, we take that profit.

```cpp
prices[i] - prices[i - 1]
```

If the difference is positive, add it to `profit`.

### Example

```text
[7, 1, 5, 3, 6, 4]

1 → 5 = +4
3 → 6 = +3

Total = 7
```

We don't need to explicitly decide when to buy and sell. Adding every positive difference gives the maximum profit.

## Code

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {

        int profit = 0;

        for(int i = 1; i < prices.size(); i++) {

            if(prices[i] > prices[i - 1]) {
                profit += prices[i] - prices[i - 1];
            }
        }

        return profit;
    }
};
```

## Complexity

* **Time:** `O(n)`
* **Space:** `O(1)`

## Revision Shortcut

**Multiple transactions → Add every positive difference**

```cpp
if(prices[i] > prices[i - 1])
    profit += prices[i] - prices[i - 1];
```

### Remember

**Price increases → take profit**

**Price decreases → ignore**

```text
7 → 1  ❌
1 → 5  +4
5 → 3  ❌
3 → 6  +3

Answer = 7
```
