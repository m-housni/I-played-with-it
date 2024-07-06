# Implement Bubble Sort

This is the first of several challenges on sorting algorithms. Given an array of unsorted items, we want to be able to return a sorted array. We will see several different methods to do this and learn some tradeoffs between these different approaches. While most modern languages have built-in sorting methods for operations like this, it is still important to understand some of the common basic approaches and learn how they can be implemented.

Here we will see bubble sort. The bubble sort method starts at the beginning of an unsorted array and 'bubbles up' unsorted values towards the end, iterating through the array until it is completely sorted. It does this by comparing adjacent items and swapping them if they are out of order. The method continues looping through the array until no swaps occur at which point the array is sorted.

This method requires multiple iterations through the array and for average and worst cases has quadratic time complexity. While simple, it is usually impractical in most situations.

Instructions: Write a function bubbleSort which takes an array of integers as input and returns an array of these integers in sorted order from least to greatest.

# My Solution
``` javascript
function bubbleSort(array) {

  let numSwaps = 0

  do {
    numSwaps = 0
    for ( let i = 0; i < array.length -1; i++ ) {
      if( array[i] > array[i+1] ) {
        [ array[i] , array[i+1] ] = [ array[i+1] , array[i] ]
        numSwaps++
      }
    }
  } while ( numSwaps !== 0 )

  return array;

}
```

### Time Complexity Analysis

Bubble Sort works by repeatedly swapping adjacent elements if they are in the wrong order. The key points to consider are the two nested loops: the inner loop and the outer loop.

1. **Outer Loop (`do...while` loop)**:
   - This loop continues as long as there are swaps made in the inner loop (`numSwaps !== 0`).
   - In the worst case, the outer loop runs for each element in the array, i.e., `n` times.

2. **Inner Loop (`for` loop)**:
   - For each iteration of the outer loop, the inner loop compares adjacent elements and performs swaps if necessary.
   - The inner loop runs `n-1` times for an array of length `n`.

### Worst-Case Scenario

In the worst-case scenario, the array is in reverse order, requiring the maximum number of swaps. In this case:

- On the first pass, the largest element moves to the end.
- On the second pass, the second-largest element moves to the second-to-last position, and so on.

The total number of comparisons and swaps can be approximated as the sum of the first `n` natural numbers:

\[ \sum_{i=1}^{n-1} i = \frac{(n-1)n}{2} \]

### Combining the Complexity

The outer loop runs `n` times, and for each iteration, the inner loop runs `n-1` times in the worst case. Thus, the combined complexity is:

\[ O(n) \times O(n-1) = O(n) \times O(n) = O(n^2) \]

### Best-Case Scenario

In the best-case scenario, the array is already sorted:

- The inner loop still runs `n-1` times, but no swaps are needed.
- The outer loop runs only once as `numSwaps` will be `0` after the first pass.

However, the time complexity in Big-O notation is still considered \(O(n^2)\) because Bubble Sort does not know the array is sorted until it completes one full pass without swaps.

### Conclusion

The time complexity of the provided Bubble Sort function is:

- **Worst-case time complexity**: \(O(n^2)\)
- **Average-case time complexity**: \(O(n^2)\)
- **Best-case time complexity**: \(O(n)\) (if the algorithm is optimized to detect the sorted array, which is not shown in this implementation)

Bubble Sort is generally inefficient for large datasets due to its quadratic time complexity.
