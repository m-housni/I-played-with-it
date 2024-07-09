# Implement Quick Sort
Here we will move on to an intermediate sorting algorithm: quick sort. Quick sort is an efficient, recursive divide-and-conquer approach to sorting an array. In this method, a pivot value is chosen in the original array. The array is then partitioned into two subarrays of values less than and greater than the pivot value. We then combine the result of recursively calling the quick sort algorithm on both sub-arrays. This continues until the base case of an empty or single-item array is reached, which we return. The unwinding of the recursive calls return us the sorted array.

Quick sort is a very efficient sorting method, providing O(nlog(n)) performance on average. It is also relatively easy to implement. These attributes make it a popular and useful sorting method.

# Solution (nlogn)

```javascript
function quickSort(array) {
  if (array.length < 2) {
    return array;
  }

  let pivotIndex = Math.floor(array.length / 2);
  let pivot = array[pivotIndex];
  let left = [];
  let right = [];

  for (let i = 0; i < array.length; i++) {
    if (i !== pivotIndex) {
      if (array[i] < pivot) {
        left.push(array[i]);
      } else {
        right.push(array[i]);
      }
    }
  }

  return [...quickSort(left), pivot, ...quickSort(right)];
}

// Example usage:
let array = [12, 11, 13, 5, 6];
console.log(quickSort(array)); // Output: [5, 6, 11, 12, 13]
```

### Explanation

1. **Pivot Selection**: Instead of always picking the first element as the pivot, we choose the middle element. This helps in cases where the array is already sorted or nearly sorted, improving performance.
2. **Single Pass for Partitioning**: Instead of filtering the array three times, we use a single loop to partition the array into left and right sub-arrays based on the pivot.
3. **Avoiding Extra Filters for Pivot Occurrences**: By choosing a unique pivot element and ensuring that the pivot itself is not included in the left or right sub-arrays, we avoid the need for extra filtering to handle multiple occurrences of the pivot.

### Time Complexity

The time complexity of quicksort is:

1. **Best Case**: \(O(n \log n)\)
   - This occurs when the pivot divides the array into two nearly equal halves, leading to balanced partitions.

2. **Average Case**: \(O(n \log n)\)
   - On average, quicksort performs well, dividing the array into reasonably balanced partitions.

3. **Worst Case**: \(O(n^2)\)
   - This occurs when the pivot selection results in highly unbalanced partitions, such as when the smallest or largest element is consistently chosen as the pivot. This can be mitigated by choosing a good pivot strategy (like picking the median).

### Space Complexity

Quicksort has a space complexity of \(O(\log n)\) due to the recursion stack depth. However, the use of additional arrays for left and right sub-arrays increases the space complexity to \(O(n)\) in practice.

By optimizing the pivot selection and partitioning strategy, this quicksort implementation should perform efficiently for a wide range of input arrays.
