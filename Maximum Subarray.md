# Maximum Subarray

## Problem Description
Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

### Example:
Input: `nums = [-2,1,-3,4,-1,2,1,-5,4]`  
Output: `6`  
Explanation: `[4,-1,2,1]` has the largest sum = 6.

### Constraints:
- 1 <= nums.length <= 10^5
- -10^4 <= nums[i] <= 10^4

## Solution Approaches

### 1. Dynamic Programming (O(n) Time Complexity)
#### Explanation:
In the dynamic programming approach, we use an array `dp[i]` to store the **maximum subarray sum that ends at index `i`**.

- **State Definition**:
  - `dp[i]` represents the maximum subarray sum ending at index `i`.
- **Transition Formula**:
  - For each index `i`, the maximum subarray sum can be calculated as:
    \[
    dp[i] = \max(nums[i], dp[i-1] + nums[i])
    \]
  - This formula indicates that at each index, we have two choices:
    1. Start a new subarray at `nums[i]`.
    2. Extend the previous subarray by including `nums[i]`.
- **Initialization**:
  - `dp[0]` is initialized to `nums[0]` since the maximum sum ending at the first element is the element itself.

#### Code Implementation:

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        n = len(nums)
        dp = [0] * n  # Create dp array
        dp[0] = nums[0]  # Initialize dp[0] to nums[0]

        max_sum = dp[0]  # Initialize max_sum

        for i in range(1, n):
            dp[i] = max(nums[i], dp[i-1] + nums[i])  # Update dp[i]
            max_sum = max(max_sum, dp[i])  # Update max_sum

        return max_sum

Key Points:

	•	Time Complexity: O(n), as we only pass through the array once.
	•	Space Complexity: O(n), due to the dp array.

Optimization (O(1) Space Complexity):

We can further optimize the space complexity by using two variables instead of a full dp array, since each dp[i] only depends on dp[i-1].

class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        current_sum = nums[0]
        max_sum = nums[0]

        for i in range(1, len(nums)):
            current_sum = max(nums[i], current_sum + nums[i])
            max_sum = max(max_sum, current_sum)

        return max_sum

	•	Time Complexity: O(n)
	•	Space Complexity: O(1)

2. Divide and Conquer (O(n log n) Time Complexity)

The divide and conquer approach divides the array into two halves and recursively finds the maximum subarray sum in the left half, right half, and across the midpoint.

Approach:

	1.	Split the array into two halves.
	2.	Recursively find the maximum subarray sum in the left half and right half.
	3.	Find the maximum subarray sum that crosses the midpoint.
	4.	Return the maximum of the three values.

Code Implementation:

class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        def maxCrossingSum(nums, left, mid, right):
            left_sum = float('-inf')
            current_sum = 0
            for i in range(mid, left - 1, -1):
                current_sum += nums[i]
                left_sum = max(left_sum, current_sum)

            right_sum = float('-inf')
            current_sum = 0
            for i in range(mid + 1, right + 1):
                current_sum += nums[i]
                right_sum = max(right_sum, current_sum)

            return left_sum + right_sum

        def divideAndConquer(nums, left, right):
            if left == right:
                return nums[left]

            mid = (left + right) // 2
            left_max = divideAndConquer(nums, left, mid)
            right_max = divideAndConquer(nums, mid + 1, right)
            cross_max = maxCrossingSum(nums, left, mid, right)

            return max(left_max, right_max, cross_max)

        return divideAndConquer(nums, 0, len(nums) - 1)

Key Points:

	•	Time Complexity: O(n log n), because each level of recursion performs linear work and there are log n levels.
	•	Space Complexity: O(log n), due to the recursion stack.

Summary

	•	The Dynamic Programming approach is faster (O(n)) and uses less space (O(1) in optimized version).
	•	The Divide and Conquer approach is more subtle and runs in O(n log n) time but can be useful in understanding problem-solving patterns like merging results.

