# Why Use `left = mid + 1` in Binary Search?

## User's Question
> Why do we update `left` to `mid + 1` instead of just setting it to `mid`?

## Explanation
In binary search, we update `left = mid + 1` to **exclude the already checked middle element** (`mid`) from the next search interval. This is a crucial part of the binary search logic, ensuring the search continues in the correct half of the array.

### Detailed Explanation

1. **Mid Element is Already Checked**:
   - In each iteration of binary search, the middle element (`mid`) is compared with the target.
   - If `nums[mid] < target`, it means the target is definitely in the right half of the array, beyond `mid`.
   - Therefore, we need to update `left` to `mid + 1`, which ensures the new search interval starts immediately to the right of `mid`.

2. **Avoiding Infinite Loops**:
   - If we were to update `left = mid` instead of `left = mid + 1`, the `mid` element would still be included in the next search interval.
   - This can lead to an **infinite loop**, as `left` and `right` may not move closer to each other, preventing the search interval from shrinking.

### Example
Consider the array `nums = [1, 2, 3, 4, 5, 6]` and the target value `target = 5`:

1. **Initial state**:
   - `left = 0`, `right = 5`, `mid = 2`, `nums[mid] = 3`.
   - Since `3 < 5`, update `left = mid + 1 = 3`.

2. **Next iteration**:
   - `left = 3`, `right = 5`, `mid = 4`, `nums[mid] = 5`.
   - Now `nums[mid] == target`, so return `mid = 4`.

If we had updated `left = mid` instead of `left = mid + 1` in the first iteration, `left` would remain at `2`, resulting in a potential **infinite loop**.

### Summary
- **`left = mid + 1`** ensures that the already checked middle element is excluded from the next search interval.
- It allows the search to progress correctly in the right half of the array when `nums[mid] < target`.
- This step is critical for the efficiency of binary search, maintaining its **O(log n)** time complexity.

By excluding `mid` from the next search interval, binary search avoids potential infinite loops and continues to halve the search space in each iteration.