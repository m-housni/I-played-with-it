# Pairwise

Given an array arr, find element pairs whose sum equal the second argument arg and return the sum of their indices.

You may use multiple pairs that have the same numeric elements but different indices. Each pair should use the lowest possible available indices. Once an element has been used it cannot be reused to pair with another element. For instance, pairwise([1, 1, 2], 3) creates a pair [2, 1] using the 1 at index 0 rather than the 1 at index 1, because 0+2 < 1+2.

For example pairwise([7, 9, 11, 13, 15], 20) returns 6. The pairs that sum to 20 are [7, 13] and [9, 11]. We can then write out the array with their indices and values.

Index	0	1	2	3	4

Value	7	9	11	13	15

Below we'll take their corresponding indices and add them.

7 + 13 = 20 → Indices 0 + 3 = 3

9 + 11 = 20 → Indices 1 + 2 = 3

3 + 3 = 6 → Return 6

# My Solution O(n2)
``` javascript
function pairwise(arr, arg) {
  let sum = 0;
  let used = new Set();
  
  for (let i = 0; i < arr.length - 1; i++) {
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[i] + arr[j] === arg && !used.has(i) && !used.has(j)) {
        sum = sum + i + j;
        used.add(i);
        used.add(j);
      }
    }
  }
  
  return sum;
}

console.log(pairwise([1, 1, 1], 2)); // Example usage
```

### Time Complexity Analysis

1. **Outer Loop (Index `i`)**:
   - This loop runs from `0` to `arr.length - 1`.
   - In the worst case, it executes `n-1` times, where `n` is the length of the array.

2. **Inner Loop (Index `j`)**:
   - This loop runs from `i + 1` to `arr.length`.
   - For each value of `i`, the inner loop runs approximately `n-i-1` times.

3. **Condition Checks**:
   - The condition `arr[i] + arr[j] === arg` is a constant-time check, i.e., `O(1)`.
   - The condition `!used.has(i) && !used.has(j)` involves checking if `i` and `j` are in the `used` set.
   - Each `has` check in a `Set` is `O(1)`, so `!used.has(i) && !used.has(j)` is `O(1)`.

4. **Add Operation**:
   - `used.add(i)` and `used.add(j)` are `O(1)` operations because `Set` operations like `add` and `has` have average time complexity of `O(1)`.

### Combining the Time Complexities

- **Outer Loop**: `O(n)`
- **Inner Loop**: Each iteration of the outer loop runs the inner loop `n-i-1` times.
  - The combined complexity of the nested loops is \( O(n) \times O(n) = O(n^2) \).

- **Condition Checks**: Each condition check inside the inner loop is `O(1)`.

### Overall Time Complexity

The overall time complexity is determined by the nested loops since the condition checks and `Set` operations are all `O(1)`:

\[ O(n) \times O(n) = O(n^2) \]

Therefore, the time complexity of the provided `pairwise` function is **O(n^2)**. This is significantly better than the previous implementation with the `includes` method, which had a time complexity of **O(n^3)** due to the linear search in the `used` array.

