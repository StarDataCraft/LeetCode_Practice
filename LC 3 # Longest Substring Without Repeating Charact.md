LC 3 # Longest Substring Without Repeating Characters

## Problem Description
Given a string `s`, find the length of the **longest substring** without repeating characters.

### Example
```plaintext
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.

Solution Approach: Sliding Window

Explanation

The goal is to find the longest substring without repeating characters. The most effective way to solve this problem is by using a sliding window technique.

Key Concepts

	1.	Sliding Window:
	•	Imagine the window as a section of the string that contains only unique characters.
	•	We use two pointers, left and right, to define the boundaries of this window.
	•	The right pointer is used to expand the window, while the left pointer helps in contracting the window when a repeating character is found.
	2.	HashMap for Character Index Tracking:
	•	A dictionary (char_map) is used to store the last seen index of each character.
	•	This helps to efficiently check if a character is within the current window and adjust the window size accordingly.

Code Implementation

class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        char_map = {}
        left = 0
        max_len = 0

        for right, char in enumerate(s):
            # If character is already in the current window, move left pointer
            if char in char_map and char_map[char] >= left:
                left = char_map[char] + 1

            # Update the character's latest index in char_map
            char_map[char] = right

            # Update the maximum length of the substring found
            max_len = max(max_len, right - left + 1)

        return max_len

Detailed Steps

	1.	Initialize Variables:
	•	char_map: To store the last index of each character.
	•	left: Start of the sliding window, initially set to 0.
	•	max_len: To keep track of the longest substring found so far.
	2.	Iterate Through the String:
	•	For each character in the string, check if it is within the current window.
	•	If it is, update the left pointer to char_map[char] + 1 to exclude the duplicate character from the current window.
	3.	Update Maximum Length:
	•	After adjusting the window, update the max_len to be the maximum of the current max_len and the length of the current window (right - left + 1).

Important Points

	•	Why use char_map[char] + 1?
	•	This ensures that the window starts from the character immediately after the last occurrence of the repeating character.
	•	It effectively removes the repeated character from the window, allowing us to continue finding longer substrings.
	•	When to update max_len?
	•	Update max_len at every step since we want to ensure that we capture the longest possible substring at any given moment.

Complexity Analysis

	•	Time Complexity: O(n), where n is the length of the string s.
	•	Each character is processed at most twice (once by the right pointer and once by the left pointer).
	•	Space Complexity: O(min(n, m)), where n is the length of the string, and m is the size of the character set (e.g., 26 for lowercase letters, 128 for ASCII).

Common Pitfalls

	•	Forgetting to update left only when the character is within the current window.
	•	Not updating char_map[char] to the current index, which can lead to incorrect results.

Summary

	•	Use a sliding window to expand and contract based on character repetition.
	•	Track characters’ indices using a hash map for efficient window adjustment.
	•	The solution efficiently finds the longest substring without repeating characters in linear time.

