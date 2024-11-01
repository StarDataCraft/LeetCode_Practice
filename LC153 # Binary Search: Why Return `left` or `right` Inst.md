# Binary Search: Why Return `left` or `right` Instead of `mid`

## Key Question
> Why is the final return value in binary search-based problems usually `left` or `right` instead of `mid`?

## Explanation

### 1. **Purpose of `mid` in Binary Search**
- The `mid` variable is used **only as a comparison tool** within each iteration of the binary search loop.
- It helps decide whether to update `left` or `right` based on the problem’s conditions:
  - If a condition is met, `left` or `right` is adjusted accordingly.
  - `mid` itself does not represent the final answer but rather guides us toward it by narrowing down the search range.

### 2. **Loop Termination and Final Return Value**
- Binary search typically uses either `while left <= right` or `while left < right` as the loop condition:
  - **`while left <= right`**: The loop stops when `left > right`.
  - **`while left < right`**: The loop stops when `left == right`.
- In both cases:
  - The final iteration will not update or re-compute `mid` because the loop has already exited.
  - **Therefore, `mid` is not available for the final return value**, as the last comparison has already been completed.
  
### 3. **Why `left` or `right` Points to the Answer**
- The binary search loop narrows down the range, and **`left` and `right` eventually converge on the target value** (such as a peak, minimum, or boundary).
- Once `left` and `right` converge, they directly indicate the position of the desired value.
- **Final return of `left` or `right`** ensures accuracy, as both point to the answer once the loop completes.

### Example: Finding Minimum in a Rotated Sorted Array
In the problem of finding the minimum in a rotated sorted array, we use `while left < right` to continually shrink the search range until `left` and `right` converge on the minimum value:

1. We start with `left = 0` and `right = len(nums) - 1`.
2. At each step:
   - Calculate `mid`, then compare `nums[mid]` with `nums[right]`.
   - Adjust `left` or `right` based on the comparison.
3. Once the loop ends, `left == right`, and **this position is the minimum element**.

In this case, `mid` only guides the search but is not part of the final result.

### Key Takeaways
- **`mid` is used for comparisons** within each loop iteration but is not re-evaluated after the loop ends.
- The final return value in binary search is typically `left` or `right` because:
  - They converge on the target position, indicating the answer.
  - Using `left` or `right` provides a precise and efficient result.
- This logic is common in binary search-based problems, where the answer is reached through `left` and `right` convergence.