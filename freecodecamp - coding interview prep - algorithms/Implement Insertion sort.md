# Implement Insertion Sort
The next sorting method we'll look at is insertion sort. This method works by building up a sorted array at the beginning of the list. It begins the sorted array with the first element. Then it inspects the next element and swaps it backwards into the sorted array until it is in sorted position. It continues iterating through the list and swapping new items backwards into the sorted portion until it reaches the end. This algorithm has quadratic time complexity in the average and worst cases.

Instructions: Write a function insertionSort which takes an array of integers as input and returns an array of these integers in sorted order from least to greatest.

# Solution O(n2)

```javascript
function insertionSort(array) {
  for (let i = 1; i < array.length; i++) {
    let key = array[i];
    let j = i - 1;

    // Move elements of array[0..i-1], that are greater than key,
    // to one position ahead of their current position
    while (j >= 0 && array[j] > key) {
      array[j + 1] = array[j];
      j = j - 1;
    }
    array[j + 1] = key;
  }
  return array;
}

// Example usage:
let array = [12, 11, 13, 5, 6];
console.log(insertionSort(array)); // Output: [5, 6, 11, 12, 13]
```

### Time Complexity

Insertion sort is an algorithm with a straightforward approach to sorting. Here's an analysis of its time complexity:

1. **Best Case**: \(O(n)\)
   - This occurs when the array is already sorted. The inner loop does not need to make any swaps, so each of the \(n\) elements is processed in constant time.

2. **Average Case**: \(O(n^2)\)
   - On average, the elements in the array are in a random order, so the inner loop will run multiple times for each element.

3. **Worst Case**: \(O(n^2)\)
   - This occurs when the array is sorted in reverse order. In this scenario, the inner loop has to move each element all the way to the beginning of the array, resulting in a quadratic number of comparisons and swaps.

### Space Complexity

Insertion sort is an **in-place sorting algorithm**, which means it does not require any additional storage proportional to the input size:
- **Space Complexity**: \(O(1)\)

### Detailed Walkthrough

Let's consider an example array: `[12, 11, 13, 5, 6]`.

1. **Iteration 1 (i=1)**: `key = 11`
   - Compare `11` with `12`. Since `11` is smaller, swap them. Result: `[11, 12, 13, 5, 6]`.

2. **Iteration 2 (i=2)**: `key = 13`
   - Compare `13` with `12`. Since `13` is larger, it remains in place. Result: `[11, 12, 13, 5, 6]`.

3. **Iteration 3 (i=3)**: `key = 5`
   - Compare `5` with `13`. Swap them. Result: `[11, 12, 5, 13, 6]`.
   - Compare `5` with `12`. Swap them. Result: `[11, 5, 12, 13, 6]`.
   - Compare `5` with `11`. Swap them. Result: `[5, 11, 12, 13, 6]`.

4. **Iteration 4 (i=4)**: `key = 6`
   - Compare `6` with `13`. Swap them. Result: `[5, 11, 12, 6, 13]`.
   - Compare `6` with `12`. Swap them. Result: `[5, 11, 6, 12, 13]`.
   - Compare `6` with `11`. Swap them. Result: `[5, 6, 11, 12, 13]`.

### Summary

Insertion sort is particularly efficient for small arrays or arrays that are already partially sorted. Its simplicity and low overhead make it a useful choice for certain applications, despite its \(O(n^2)\) time complexity for average and worst-case scenarios.
