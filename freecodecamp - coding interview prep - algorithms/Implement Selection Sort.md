# Implement Selection Sort

Here we will implement selection sort. Selection sort works by selecting the minimum value in a list and swapping it with the first value in the list. It then starts at the second position, selects the smallest value in the remaining list, and swaps it with the second element. It continues iterating through the list and swapping elements until it reaches the end of the list. Now the list is sorted. Selection sort has quadratic time complexity in all cases.

Instructions: Write a function selectionSort which takes an array of integers as input and returns an array of these integers in sorted order from least to greatest.

# Solution O(n2)

``` javascript
function selectionSort(array) {
  for (let i = 0; i < array.length - 1; i++) {
    let minIndex = i;
    for (let j = i + 1; j < array.length; j++) {
      if (array[j] < array[minIndex]) {
        minIndex = j;
      }
    }
    if (minIndex !== i) {
      [array[i], array[minIndex]] = [array[minIndex], array[i]];
    }
  }
  return array;
}
```

### Time Complexity Analysis

1. **Outer Loop (Index `i`)**:
   - This loop runs from `0` to `array.length - 1`.
   - In the worst case, it executes `n-1` times, where `n` is the length of the array.

2. **Inner Loop (Index `j`)**:
   - This loop runs from `i + 1` to `array.length`.
   - For each value of `i`, the inner loop runs approximately `n-i-1` times.

3. **Condition Check and Assignment**:
   - The condition `array[j] < array[minIndex]` is a constant-time check, i.e., `O(1)`.
   - The assignment `minIndex = j` is also `O(1)`.

4. **Swap Operation**:
   - The swap operation `[array[i], array[minIndex]] = [array[minIndex], array[i]]` is `O(1)`.

### Combining the Time Complexities

- **Outer Loop**: `O(n)`
- **Inner Loop**: For each iteration of the outer loop, the inner loop runs `n-i-1` times.
  - The total number of comparisons is the sum of the first `n-1` natural numbers:
    \[
    \sum_{i=1}^{n-1} (n-i) = \sum_{i=1}^{n-1} i = \frac{(n-1)n}{2}
    \]
  - This simplifies to \( O(n^2) \).

### Overall Time Complexity

The overall time complexity is determined by the nested loops, both running in a manner that results in quadratic complexity:

\[ O(n) \times O(n) = O(n^2) \]

Therefore, the time complexity of the provided selection sort function is **O(n^2)**.

### Space Complexity

The space complexity of selection sort is **O(1)** because it only uses a fixed amount of extra space (a few variables) and does not require additional space proportional to the input size.

### Summary

- **Time Complexity**: \(O(n^2)\)
- **Space Complexity**: \(O(1)\)

This time complexity is typical for comparison-based sorting algorithms like selection sort, which is why it's often not used for large datasets, where more efficient algorithms like quicksort or mergesort (with average time complexity of \(O(n \log n)\)) are preferred.
