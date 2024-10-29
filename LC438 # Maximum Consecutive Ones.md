# Maximum Consecutive Ones

## Problem Description
Given a binary array `nums`, find the **maximum number of consecutive 1's** in the array.

### Example
```plaintext
Input: nums = [1,1,0,1,1,1]
Output: 3
Explanation: The longest sequence of consecutive 1's is [1, 1, 1], with a length of 3.

Solution Approach: Sliding Window / Simple Counter

Key Concepts

	•	Sliding window logic can be used to find the longest sequence of consecutive 1s.
	•	Alternatively, a simple counter approach can be used, as we only need to count continuous 1s, resetting the count when encountering a 0.

Implementation

class Solution:
    def findMaxConsecutiveOnes(self, nums: list[int]) -> int:
        max_len = 0
        current_len = 0

        for num in nums:
            if num == 1:
                current_len += 1
                max_len = max(max_len, current_len)
            else:
                current_len = 0

        return max_len

Detailed Steps

	1.	Initialize variables:
	•	max_len: Keeps track of the maximum number of consecutive 1s found so far. Initialize to 0.
	•	current_len: Tracks the current sequence length of consecutive 1s. Initialize to 0.
	2.	Iterate through the array:
	•	For each element in nums:
	•	If the element is 1, increment current_len and update max_len if current_len is greater than max_len.
	•	If the element is 0, reset current_len to 0.
	3.	Return the result:
	•	After the loop, return max_len, which represents the longest sequence of consecutive 1s.

Complexity Analysis

	•	Time Complexity: O(n), where n is the length of nums.
	•	We traverse the array once, making it linear time complexity.
	•	Space Complexity: O(1), as only a constant amount of extra space is used for variables (max_len and current_len).

Edge Cases

	•	Empty array: If nums is empty, the function should return 0 since there are no elements to consider.
	•	All 1’s: If nums contains only 1s, the entire array is the longest sequence.
	•	All 0’s: If nums contains only 0s, the result should be 0 as there are no 1s.

Summary

	•	This problem is a straightforward application of counting elements and updating a maximum.
	•	The use of a simple counter makes it very efficient with minimal logic.
	•	It serves as an excellent introduction to sliding window concepts, as well as basic iteration and condition checking.

