# No Repeats Please
Return the number of total permutations of the provided string that don't have repeated consecutive letters. Assume that all characters in the provided string are each unique.

For example, aab should return 2 because it has 6 total permutations (aab, aab, aba, aba, baa, baa), but only 2 of them (aba and aba) don't have the same letter (in this case a) repeating.

# Solution
``` javascript
function permAlone(str) {

  const permutations = str => {
      const results = [];
    
      function swap(arr, i, j) {
          const temp = arr[i];
          arr[i] = arr[j];
          arr[j] = temp;
      }
    
      function generate(n, arr) {
          if (n === 1) {
              results.push(arr.slice());
          } else {
              for (let i = 0; i < n - 1; i++) {
                  generate(n - 1, arr);
                  swap(arr, n % 2 === 0 ? i : 0, n - 1);
              }
              generate(n - 1, arr);
          }
      }
    
      generate(str.length, str.split(''));
      return results.map(arr => arr.join(''));
  }

  const isNoRepeat = str => { 
    let strArr = str.split('')
    for ( let i = 0; i < strArr.length - 1; i++ ) {
      if(strArr[i] === strArr[i+1]) 
        return false
    }
    return true;
  }

  let perms = permutations(str)
  let ctr = 0;
  for ( let i = 0; i < perms.length; i++ ) {
    if( isNoRepeat(perms[i]) ){
      console.log(perms[i])
      ctr++
    }
  }
  console.log(ctr)
  return ctr;
}

// Test cases
console.log(permAlone("abc")); // 6
console.log(permAlone("aab")); // 2
console.log(permAlone("aaa")); // 0
console.log(permAlone("aabb")); // 8
console.log(permAlone("abcd")); // 24
console.log(permAlone("")); // 1
console.log(permAlone("a")); // 1
console.log(permAlone("aabbcc")); // 120

```

# Analysis

The `permAlone` function calculates the number of permutations of a given string that do not have any repeating consecutive characters. Here's a detailed explanation of the function and its components:

### Function Breakdown

1. **Permutations Generator (`permutations` function):**
   - **Purpose:** Generate all possible permutations of the input string.
   - **Process:**
     - Initialize an empty array `results` to store the permutations.
     - Define a helper function `swap` to swap elements in an array.
     - Define a recursive function `generate` that generates permutations using Heap's Algorithm.
       - If `n` (length of the array) is 1, push a copy of the current array (`arr`) to `results`.
       - Otherwise, recursively generate permutations by reducing `n`, swapping elements accordingly.
     - Start the generation process by calling `generate` with the length of the input string and its character array.
     - Convert each array in `results` back to a string and return the array of strings.

2. **No Repeats Checker (`isNoRepeat` function):**
   - **Purpose:** Check if a given string has no consecutive repeating characters.
   - **Process:**
     - Split the string into an array of characters.
     - Loop through the array and check if any character is the same as the next one.
     - Return `false` if a repeat is found; otherwise, return `true`.

3. **Main Logic:**
   - **Process:**
     - Generate all permutations of the input string using the `permutations` function.
     - Initialize a counter `ctr` to count valid permutations.
     - Loop through each permutation and check if it has no repeating consecutive characters using `isNoRepeat`.
     - If a permutation is valid, increment the counter `ctr`.
     - Print each valid permutation (for debugging purposes).
     - Print the final count of valid permutations.
     - Return the count of valid permutations.
