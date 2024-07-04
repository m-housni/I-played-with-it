Heap's Algorithm is an efficient method for generating all possible permutations of a given set. It was introduced by B. R. Heap in 1963. The algorithm generates the permutations by systematically swapping elements. It's particularly well-suited for computer implementations due to its simple recursive nature and in-place generation of permutations.

### Understanding Heap's Algorithm

Heap's Algorithm works by producing permutations through a series of element swaps. The algorithm operates as follows:

1. **Initialization:** Start with the original array.
2. **Recursion and Swapping:** Recursively generate permutations by swapping elements.
3. **Base Case:** When the recursion depth reaches 1, it means a permutation is complete, and it's added to the list of permutations.

Here's a step-by-step description:

1. **Generate permutations for n elements by generating permutations for n-1 elements, and then rotating the n-th element through the positions of the first n-1 elements.**
2. **Swap elements based on whether n is even or odd:**
   - If n is even, swap the i-th element with the n-th element.
   - If n is odd, swap the first element with the n-th element.
3. **Repeat the process until all permutations are generated.**

### Example with a Step-by-Step Breakdown

Let's generate all permutations for the array [1, 2, 3].

```javascript
function heapPermute(n, arr, results) {
  if (n === 1) {
    results.push(arr.slice());
  } else {
    for (let i = 0; i < n - 1; i++) {
      heapPermute(n - 1, arr, results);
      if (n % 2 === 0) {
        [arr[i], arr[n - 1]] = [arr[n - 1], arr[i]]; // Swap for even n
      } else {
        [arr[0], arr[n - 1]] = [arr[n - 1], arr[0]]; // Swap for odd n
      }
    }
    heapPermute(n - 1, arr, results);
  }
}

function generatePermutations(arr) {
  const results = [];
  heapPermute(arr.length, arr, results);
  return results;
}

// Example usage
const permutations = generatePermutations([1, 2, 3]);
console.log(permutations);
```

### Step-by-Step Breakdown of Example [1, 2, 3]

1. **Initial call:** `heapPermute(3, [1, 2, 3], [])`
2. **Recursive call 1:** `heapPermute(2, [1, 2, 3], [])`
   - Recursive call 1.1: `heapPermute(1, [1, 2, 3], [])` -> Add [1, 2, 3]
   - Swap elements since n is even: [1, 2, 3] -> [2, 1, 3]
   - Recursive call 1.2: `heapPermute(1, [2, 1, 3], [])` -> Add [2, 1, 3]
   - Restore order: [2, 1, 3] -> [1, 2, 3]
3. **Swap first element with last:** [1, 2, 3] -> [3, 2, 1]
4. **Recursive call 2:** `heapPermute(2, [3, 2, 1], [])`
   - Recursive call 2.1: `heapPermute(1, [3, 2, 1], [])` -> Add [3, 2, 1]
   - Swap elements since n is even: [3, 2, 1] -> [2, 3, 1]
   - Recursive call 2.2: `heapPermute(1, [2, 3, 1], [])` -> Add [2, 3, 1]
   - Restore order: [2, 3, 1] -> [3, 2, 1]
5. **Restore order:** [3, 2, 1] -> [1, 2, 3]

The permutations generated are:
- [1, 2, 3]
- [2, 1, 3]
- [3, 1, 2]
- [1, 3, 2]
- [2, 3, 1]
- [3, 2, 1]

### Summary

Heap's Algorithm efficiently generates all permutations of an array by using a systematic approach to swapping elements. The algorithm's recursive nature makes it well-suited for computer implementations, and it can handle permutations in-place without requiring additional memory for intermediate results. By understanding and implementing Heap's Algorithm, you can efficiently tackle problems that require generating all permutations of a given set.
