# Find the Symmetric Difference
The mathematical term symmetric difference (△ or ⊕) of two sets is the set of elements which are in either of the two sets but not in both. For example, for sets A = {1, 2, 3} and B = {2, 3, 4}, A △ B = {1, 4}.

Symmetric difference is a binary operation, which means it operates on only two elements. So to evaluate an expression involving symmetric differences among three elements (A △ B △ C), you must complete one operation at a time. Thus, for sets A and B above, and C = {2, 3}, A △ B △ C = (A △ B) △ C = {1, 4} △ {2, 3} = {1, 2, 3, 4}.

Create a function that takes two or more arrays and returns an array of their symmetric difference. The returned array must contain only unique values (no duplicates).

# Solution O(kxn2)

``` javascript
function symdiff2( a1 , a2 ) {
    let res = [];
    // O(n2)
    for(let i = 0; i < a1.length; i++) {
        if(a2.indexOf(a1[i]) === -1) {
            res.push(a1[i]);
        }
    }
    // O(n2)
    for(let i = 0; i < a2.length; i++) {
        if(a1.indexOf(a2[i]) === -1) {
            res.push(a2[i]);
        }
    }

    // O(n)
    let resWithNoDuplicates = new Set()
    for(let i = 0; i < res.length; i++) {
        resWithNoDuplicates.add(res[i]);
    }
    
    return Array.from(resWithNoDuplicates);

}

function sym(...args) {
    return args.reduce(symdiff2)
}
```

# Analysis

To analyze the time complexity of the given functions `symdiff2` and `sym`, we will break down the complexity of each part of the code and then combine them to get the overall complexity.

### Function `symdiff2`

```javascript
function symdiff2(a1, a2) {
    let res = [];

    // O(n2)
    for(let i = 0; i < a1.length; i++) {
        if(a2.indexOf(a1[i]) === -1) {
            res.push(a1[i]);
        }
    }

    // O(n2)
    for(let i = 0; i < a2.length; i++) {
        if(a1.indexOf(a2[i]) === -1) {
            res.push(a2[i]);
        }
    }

    // O(n)
    let resWithNoDuplicates = new Set();
    for(let i = 0; i < res.length; i++) {
        resWithNoDuplicates.add(res[i]);
    }

    return Array.from(resWithNoDuplicates);
}
```

### Analysis of `symdiff2`

1. **First loop**:
   ```javascript
   for(let i = 0; i < a1.length; i++) {
       if(a2.indexOf(a1[i]) === -1) {
           res.push(a1[i]);
       }
   }
   ```
   - This loop runs `a1.length` times.
   - Inside the loop, `a2.indexOf(a1[i])` has a complexity of O(n2) in the worst case.
   - Combined, this part has a complexity of O(n1 * n2).

2. **Second loop**:
   ```javascript
   for(let i = 0; i < a2.length; i++) {
       if(a1.indexOf(a2[i]) === -1) {
           res.push(a2[i]);
       }
   }
   ```
   - This loop runs `a2.length` times.
   - Inside the loop, `a1.indexOf(a2[i])` has a complexity of O(n1) in the worst case.
   - Combined, this part also has a complexity of O(n1 * n2).

3. **Removing duplicates using a `Set`**:
   ```javascript
   let resWithNoDuplicates = new Set();
   for(let i = 0; i < res.length; i++) {
       resWithNoDuplicates.add(res[i]);
   }
   ```
   - This loop runs `res.length` times.
   - Adding to a `Set` is O(1) on average.
   - Combined, this part has a complexity of O(n), where `n` is the length of `res`.

### Overall Time Complexity of `symdiff2`

Combining all parts, the time complexity of `symdiff2` is:
\[ O(n1 * n2) + O(n1 * n2) + O(n) \]
Since `O(n1 * n2)` dominates, the overall time complexity of `symdiff2` is:
\[ O(n1 * n2) \]

### Function `sym`

```javascript
function sym(...args) {
    return args.reduce(symdiff2);
}
```

### Analysis of `sym`

- The `reduce` method applies the `symdiff2` function cumulatively to the elements of `args`.
- If `args` has `k` arrays, `symdiff2` will be called `k-1` times.
- Each call to `symdiff2` has a complexity of O(n1 * n2).

In the worst case, where each pair of arrays has the maximum length, the total complexity would be:

### Overall Time Complexity of `sym`

Let the lengths of the arrays be approximately equal, `n1 = n2 = n`. Therefore, the time complexity is approximately:
\[ O(k \cdot n^2) \]

### Conclusion

The overall time complexity of the `sym` function, which calls `symdiff2` multiple times, is:
\[ O(k \cdot n^2) \]
where `k` is the number of arrays and `n` is the average length of the arrays. This complexity indicates that the function scales quadratically with the size of the input arrays and linearly with the number of arrays.
