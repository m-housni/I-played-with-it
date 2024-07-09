# Implement Quick Sort
Here we will move on to an intermediate sorting algorithm: quick sort. Quick sort is an efficient, recursive divide-and-conquer approach to sorting an array. In this method, a pivot value is chosen in the original array. The array is then partitioned into two subarrays of values less than and greater than the pivot value. We then combine the result of recursively calling the quick sort algorithm on both sub-arrays. This continues until the base case of an empty or single-item array is reached, which we return. The unwinding of the recursive calls return us the sorted array.

Quick sort is a very efficient sorting method, providing O(nlog(n)) performance on average. It is also relatively easy to implement. These attributes make it a popular and useful sorting method.

# Solution (nlogn)

```javascript
function quickSort(array) {
  if (array.length < 2) {
    return array;
  }

  let pivot = array[0];
  let pivotOccurences = array.filter(e => e === pivot);
  let left = array.filter(e => e < pivot);
  let right = array.filter(e => e > pivot);

  return [...quickSort(left), ...pivotOccurences, ...quickSort(right)];
}

```

### Time Complexity Analysis

1. **Pivot Selection**:
   - The pivot is selected as the first element of the array. This takes constant time, \(O(1)\).

2. **Partitioning**:
   - The partitioning is done using the `filter` method, which iterates through the entire array three times:
     - `array.filter(e => e === pivot)`
     - `array.filter(e => e < pivot)`
     - `array.filter(e => e > pivot)`
   - Each of these operations takes \(O(n)\) time, where \(n\) is the length of the array. Thus, the partitioning step takes \(O(n) + O(n) + O(n) = O(3n) = O(n)\) time.

3. **Recursion**:
   - The recursive calls are made on the left and right sub-arrays. In the average and best cases, the pivot divides the array into two equal parts, leading to balanced recursion. In the worst case, one sub-array is empty, and the other contains the rest of the elements, leading to unbalanced recursion.

### Overall Time Complexity

- **Best and Average Case**: 
  - When the pivot splits the array into two equal (or nearly equal) parts, each partitioning step takes \(O(n)\), and there are \(O(\log n)\) levels of recursion. Thus, the overall time complexity is \(O(n \log n)\).

- **Worst Case**: 
  - When the pivot results in highly unbalanced splits (e.g., when the array is already sorted in ascending or descending order), one partition is empty, and the other has \(n - 1\) elements. This leads to \(n\) levels of recursion, with each level taking \(O(n)\) time. Thus, the overall time complexity is \(O(n^2)\).

### Space Complexity

- The space complexity is influenced by:
  - **Recursion Stack**: In the worst case, the recursion stack can go as deep as \(n\) levels, leading to \(O(n)\) space complexity.
  - **Additional Arrays**: The use of `filter` creates new arrays for `left`, `right`, and `pivotOccurences`, which require additional space proportional to the input size \(O(n)\).

### Summary

- **Best Case Time Complexity**: \(O(n \log n)\)
- **Average Case Time Complexity**: \(O(n \log n)\)
- **Worst Case Time Complexity**: \(O(n^2)\)
- **Space Complexity**: \(O(n)\)

The function performs well on average but can degrade to quadratic time complexity in the worst case due to poor pivot selection. Optimizing the pivot selection (e.g., using the median-of-three method) can help mitigate the worst-case scenario.
