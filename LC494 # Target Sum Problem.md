# Target Sum Problem

The **Target Sum** problem is a classic dynamic programming problem that requires converting a given array into a subset sum problem to find the number of ways to reach a target sum by adding or subtracting the elements of the array.

## Problem Description

Given:
- An array of integers, `nums`.
- An integer, `target`.

Goal:
- Count the number of ways to assign `+` and `-` signs to elements in `nums` such that the total sum equals `target`.

## Dynamic Programming Solution

### 1. **Key Idea: Convert to Subset Sum Problem**
   - First, calculate the total sum of `nums`, denoted as `total_sum`.
   - Define a new variable `P`, which represents the subset sum:
     \[
     P = \frac{\text{target} + \text{total\_sum}}{2}
     \]
   - The problem then becomes finding the number of subsets in `nums` that sum up to `P`.

### 2. **Conditions for Valid `P`**
   - The conversion to subset sum only makes sense if:
     1. `(target + total_sum) % 2 == 0` (to ensure `P` is an integer).
     2. `target <= total_sum` (to ensure `P` is achievable).
     3. `(target + total_sum) >= 0` (to ensure `P` is non-negative).

### 3. **Dynamic Programming Array Definition**
   - Use a 1D DP array, `dp`, where `dp[i]` represents the number of ways to get a sum of `i` using elements in `nums`.
   - Initialize `dp[0] = 1` because there is exactly one way to achieve a sum of 0 (by using the empty set).

### 4. **Dynamic Programming Update**
   - For each element in `nums`, iterate backward through the DP array from `P` to the element's value:
     ```python
     for num in nums:
         for i in range(P, num - 1, -1):
             dp[i] += dp[i - num]
     ```
   - The backward iteration ensures that each element is only counted once in each subset, avoiding over-counting.

### 5. **Final Result**
   - Return `dp[P]`, which represents the number of ways to form the sum `P` using subsets of `nums`.

## Python Code Implementation

```python
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        total_sum = sum(nums)

        # Check if the target sum can be converted to a valid subset sum problem
        if (target + total_sum) % 2 != 0 or target > total_sum or (target + total_sum) < 0:
            return 0

        P = (target + total_sum) // 2

        # Initialize the dp array
        dp = [0] * (P + 1)
        dp[0] = 1

        # Update dp array for each num in nums
        for num in nums:
            for i in range(P, num - 1, -1):
                dp[i] += dp[i - num]

        return dp[P]