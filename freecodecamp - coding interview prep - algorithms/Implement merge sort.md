# Implement Merge Sort
Another common intermediate sorting algorithm is merge sort. Like quick sort, merge sort also uses a divide-and-conquer, recursive methodology to sort an array. It takes advantage of the fact that it is relatively easy to sort two arrays as long as each is sorted in the first place. But we'll start with only one array as input, so how do we get to two sorted arrays from that? Well, we can recursively divide the original input in two until we reach the base case of an array with one item. A single-item array is naturally sorted, so then we can start combining. This combination will unwind the recursive calls that split the original array, eventually producing a final sorted array of all the elements. The steps of merge sort, then, are:

1) Recursively split the input array in half until a sub-array with only one element is produced.

2) Merge each sorted sub-array together to produce the final sorted array.

Merge sort is an efficient sorting method, with time complexity of O(nlog(n)). This algorithm is popular because it is performant and relatively easy to implement.

As an aside, this will be the last sorting algorithm we cover here. However, later in the section on tree data structures we will describe heap sort, another efficient sorting method that requires a binary heap in its implementation.

Instructions: Write a function mergeSort which takes an array of integers as input and returns an array of these integers in sorted order from least to greatest. A good way to implement this is to write one function, for instance merge, which is responsible for merging two sorted arrays, and another function, for instance mergeSort, which is responsible for the recursion that produces single-item arrays to feed into merge. Good luck!

# Solution O(nlogn)

``` javascript
function mergeSort(array) {
  // merge two sorted arrays
  const merge = (s1,s2) => {
    let [i,j] = [0,0]
    let s = []
    while(i<s1.length && j<s2.length) {
      if(s1[i]<s2[j]) {
        s.push(s1[i])
        i++
      } else {
        s.push(s2[j])
        j++
      }
    }

    while(i<s1.length) {
      s.push(s1[i])
      i++
    }

    while(j<s2.length) {
      s.push(s2[j])
      j++
    }

    return s
  }

  if(array.length <= 1)
    return array

  const middle = Math.floor(array.length/2)
  const left = array.slice(0,middle)
  const right = array.slice(middle)

  return merge( mergeSort(left), mergeSort(right) )

  
}

console.log(mergeSort([1,4,2,8,345,123,43,32,5643,63,123,43,2,55,1,234,92]))
```



# Time Complexity Analysis

1. **Base Case:**
    - If the array length is 1 or less, the function returns immediately. This operation is \(O(1)\).

2. **Recursive Case:**
    - The array is split into two halves: `left` and `right`.
    - This splitting operation takes \(O(n)\) time because of the `slice` function, which creates subarrays.

3. **Recursive Calls:**
    - The function calls itself recursively on the left and right subarrays. This divides the problem into two subproblems of size \(n/2\).

4. **Merge Function:**
    - The `merge` function takes two sorted subarrays and merges them into a single sorted array.
    - Merging two sorted arrays of total length \(n\) takes \(O(n)\) time.

### Recurrence Relation

The time complexity \(T(n)\) can be expressed as:
\[ T(n) = 2T\left(\frac{n}{2}\right) + O(n) \]

Here:
- \(2T\left(\frac{n}{2}\right)\) is the time complexity for the two recursive calls on subarrays of size \(n/2\).
- \(O(n)\) is the time complexity for merging the two subarrays.

### Solving the Recurrence Relation

The recurrence relation \(T(n) = 2T\left(\frac{n}{2}\right) + n\) can be solved using the Master Theorem for divide-and-conquer recurrences of the form:
\[ T(n) = aT\left(\frac{n}{b}\right) + f(n) \]

In this case:
- \(a = 2\)
- \(b = 2\)
- \(f(n) = n\)

According to the Master Theorem, we compare \(f(n)\) with \(n^{\log_b a}\):

\[ \log_b a = \log_2 2 = 1 \]

Thus, \(f(n) = O(n)\) matches \(n^{\log_b a}\). Therefore, by the Master Theorem, we have:

\[ T(n) = O(n \log n) \]

### Conclusion

The time complexity of the given `mergeSort` function is:

\[ T(n) = O(n \log n) \]

### Example Execution

```javascript
console.log(mergeSort([1, 4, 2, 8, 345, 123, 43, 32, 5643, 63, 123, 43, 2, 55, 1, 234, 92]));
```

This will output the sorted array:

\[ [1, 1, 2, 2, 4, 8, 32, 43, 43, 55, 63, 92, 123, 123, 234, 345, 5643] \]

Thus, the merge sort function operates with a time complexity of \(O(n \log n)\), making it efficient for sorting large arrays.
