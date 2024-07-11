# Implement Binary Search
Binary search is an O(log(n)) efficiency algorithm for searching a sorted array to find an element. It operates using the following steps:

Find the middle value of a sorted array. If value == target return true (The value has been found and the search is complete).
If middle value < target, search right half of array in next compare.
If middle value > target, search left half of array in next compare.
If after searching the whole array the value is not present, return false (The array has been searched and the value is not in the array).
As you can see, you are successively halving an array, which gives you the log(n) efficiency. For this challenge, we want you to show your work - how you got to the target value... the path you took!

Write a function binarySearch that implements the binary search algorithm on an array, returning the path you took (each middle value comparison) to find the target in an array.

The function takes a sorted array of integers and a target value as input. It returns an array containing (in-order) the middle value you found at each halving of the original array until you found the target value. The target value should be the last element of the returned array. If the value is not found, return the string Value Not Found.

For example, binarySearch([1,2,3,4,5,6,7], 5) would return [4,6,5].

For this challenge, when halving, you MUST use Math.floor() when doing division: Math.floor(x/2). This will give a consistent, testable path.

Note: The following array will be used in tests:

# Solution O(logn)
``` javascript
function binarySearch(searchList, value) {
  let arrayPath = [];

  let minIndex = 0
  let maxIndex = searchList.length-1
  let mid
  while( minIndex <= maxIndex ) {
    mid = Math.floor((minIndex+maxIndex)/2)
    arrayPath.push(searchList[mid])
    if( value < searchList[mid] ) {
      maxIndex = mid - 1
    } else if( value > searchList[mid] ) {
      minIndex = mid + 1
    } else {
      console.log(arrayPath)
      return arrayPath; 
    }
  }
  return "Value Not Found"
  
}

binarySearch([0, 1, 2, 3, 4, 5, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22,
  23, 49, 70],1)
```


The given `binarySearch` function searches for a value in a sorted list and logs the path taken during the search. Here's a detailed analysis of its time complexity:

### Function Explanation

1. **Initialization:**
    - `arrayPath` is initialized to store the path of elements checked during the search.
    - `minIndex` and `maxIndex` are initialized to the start and end of the list, respectively.

2. **Binary Search Loop:**
    - The loop continues as long as `minIndex` is less than or equal to `maxIndex`.
    - `mid` is calculated as the midpoint of the current search range.
    - The element at `mid` is added to `arrayPath`.
    - If the value at `mid` is greater than the target, update `maxIndex` to `mid - 1` to search in the left half.
    - If the value at `mid` is less than the target, update `minIndex` to `mid + 1` to search in the right half.
    - If the value at `mid` is equal to the target, print and return `arrayPath`.

3. **Return Value:**
    - If the loop ends without finding the target, return "Value Not Found".

### Time Complexity Analysis

The time complexity of the binary search function is determined by the number of iterations of the while loop.

1. **Loop Iterations:**
    - The loop halves the search space each time.
    - In each iteration, the size of the search range is reduced by approximately half.
    - The number of iterations required to reduce the search space to one element (or to determine the element is not present) is \(\log_2 n\), where \(n\) is the number of elements in the list.

2. **Operations per Iteration:**
    - Calculating the midpoint (`mid = Math.floor((minIndex + maxIndex) / 2)`) is \(O(1)\).
    - Comparing the value at `mid` with the target is \(O(1)\).
    - Updating `minIndex` or `maxIndex` is \(O(1)\).
    - Adding an element to `arrayPath` is \(O(1)\).

Therefore, each iteration of the while loop performs a constant amount of work, and the number of iterations is \(\log_2 n\).

### Overall Time Complexity

Combining these observations, the time complexity of the binary search function is:
\[ T(n) = O(\log n) \]

### Space Complexity Analysis

1. **Auxiliary Space:**
    - The `arrayPath` array stores the elements checked during the search.
    - In the worst case, `arrayPath` will store all elements checked, which is at most \(\log_2 n\) elements.

Therefore, the space complexity is:
\[ S(n) = O(\log n) \]

### Summary

- **Time Complexity:** \(O(\log n)\)
- **Space Complexity:** \(O(\log n)\)

The binary search function is efficient both in terms of time and space, making it suitable for searching in large sorted lists.
