# Find Peak Element: Why Use `while left < right`

## User's Question
> Why do we use `while left < right` instead of `while left <= right` in the "Find Peak Element" problem?

## Explanation

### 1. **Why Use `while left < right`?**
- In this problem, we are looking for the **index of a peak element**.
- Using `while left < right` ensures that the search stops as soon as `left` and `right` point to the **same index**, which is a peak.
- Once `left` equals `right`, the peak index is found, and the loop ends. The value of `left` will be the peak index.
- If we use `while left <= right`, it may cause an **extra iteration** when `left` equals `right`, resulting in unnecessary computations.

### 2. **Characteristics of `while left < right`**
- This condition ensures that the search interval keeps shrinking until `left` and `right` converge to a single index.
- The loop stops when `left` and `right` meet, guaranteeing that the element at this index is a peak.
- In each iteration:
  - If `nums[mid] > nums[mid + 1]`, it indicates a peak is on the **left side or at `mid`**, so we set `right = mid`.
  - If `nums[mid] < nums[mid + 1]`, it indicates a peak is on the **right side**, so we set `left = mid + 1`.

### 3. **Example**
Consider the array `nums = [1, 2, 3, 1]`:

1. **Initial state**: `left = 0`, `right = 3`.
2. **First iteration**:
   - `mid = (0 + 3) // 2 = 1`, `nums[mid] = 2`, `nums[mid + 1] = 3`.
   - Since `2 < 3`, update `left = mid + 1 = 2`.
3. **Second iteration**:
   - `left = 2`, `right = 3`, `mid = (2 + 3) // 2 = 2`, `nums[mid] = 3`, `nums[mid + 1] = 1`.
   - Since `3 > 1`, update `right = mid = 2`.

The loop ends with `left = right = 2`, indicating that the peak element is at index 2.

### 4. **Why `while left <= right` Is Not Suitable**
- Using `while left <= right` would require additional checks to avoid unnecessary iterations.
- When `left` equals `right`, we have already found the peak, making it redundant to continue further.

### Summary
- The condition `while left < right` is more appropriate for finding a peak index because it stops once `left` and `right` meet, simplifying the logic and avoiding extra computations.
- It ensures a more **efficient and concise implementation** of the binary search for this problem.