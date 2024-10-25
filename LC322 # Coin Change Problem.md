# Coin Change Problem

The **Coin Change** problem is a classic dynamic programming challenge that requires finding the **minimum number of coins** needed to make up a given amount using a set of coin denominations. This problem tests your understanding of dynamic programming, specifically how to solve the **unbounded knapsack problem**.

## Problem Description

Given:
- A list of **coin denominations** (`coins`), where each coin can be used an unlimited number of times.
- A **target amount** (`amount`).

Goal:
- Find the **minimum number of coins** needed to make up the given amount.
- If it is **not possible** to make up the amount, return `-1`.

## Dynamic Programming Approach

### 1. **Define the State**
   - Let **`dp[i]`** represent the **minimum number of coins** required to make up the amount `i`.
   - The size of the `dp` array is `amount + 1` because it needs to store solutions for amounts from `0` to `amount`.

### 2. **Initialization**
   - Set `dp[0] = 0` because **0 coins** are needed to make up the amount of **0**.
   - Initialize the rest of the `dp` array with a large value, such as `float('inf')`, to indicate that the amount is initially unreachable.

### 3. **State Transition**
   - For each coin denomination in `coins` and each amount from `1` to `amount`, update the `dp` array:
     - If `i >= coin`, use the recurrence relation:
       \[
       dp[i] = \min(dp[i], dp[i - coin] + 1)
       \]
     - This means that to make up amount `i`, you can either:
       - **Not use the coin**, so `dp[i]` remains the same.
       - **Use the coin**, in which case you add `1` to the number of coins needed to make up amount `i - coin`.

### 4. **Final Result**
   - If `dp[amount]` is still `float('inf')`, it means that the amount cannot be formed with the given coin denominations, so return `-1`.
   - Otherwise, return `dp[amount]`, which gives the **minimum number of coins needed**.

## Python Code Implementation

```python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        dp = [float('inf')] * (amount + 1)  # Step 2: Initialize dp array
        dp[0] = 0  # Step 2: Base case for amount 0
        
        # Step 3: Update dp array based on state transition
        for coin in coins:
            for i in range(coin, amount + 1):
                dp[i] = min(dp[i], dp[i - coin] + 1)
        
        # Step 4: Final result
        return dp[amount] if dp[amount] != float('inf') else -1