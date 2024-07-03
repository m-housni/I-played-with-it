# Inventory Update

Compare and update the inventory stored in a 2D array against a second 2D array of a fresh delivery. Update the current existing inventory item quantities (in arr1). 

If an item cannot be found, add the new item and quantity into the inventory array. The returned inventory array should be in alphabetical order by item.

``` javascript
function updateInventory(arr1, arr2) {
    return arr1;
}

// Example inventory lists
var curInv = [
    [21, "Bowling Ball"],
    [2, "Dirty Sock"],
    [1, "Hair Pin"],
    [5, "Microphone"]
];

var newInv = [
    [2, "Hair Pin"],
    [3, "Half-Eaten Apple"],
    [67, "Bowling Ball"],
    [7, "Toothpaste"]
];

updateInventory(curInv, newInv);
```

# Solution O(n^2 + mn)

``` javascript
function updateInventory(arr1, arr2) {
    let keysArr1 = arr1.map(item => item[0]) 
    let valuesArr1 = arr1.map(item => item[1]) 

    // O(mxn)
    for ( let i = 0; i < arr2.length; i++ ) { 
        let idx = valuesArr1.indexOf(arr2[i][1])
        if( idx !== -1 ) {
            arr1[idx][0] += arr2[i][0]
        } else {
            arr1.push(arr2[i])
        }
    }

    valuesArr1 = arr1.map(item => item[1]); 
    let sortedValuesArr1 = arr1.map(item => item[1]).sort() // O(nlogn)
    let result = []
    for(let i = 0; i < arr1.length; i++) {
        let idx = valuesArr1.indexOf(sortedValuesArr1[i])
        result.push(arr1[idx])
    }
    return result
}

// Example inventory lists
var curInv = [
    [21, "Bowling Ball"],
    [2, "Dirty Sock"],
    [1, "Hair Pin"],
    [5, "Microphone"]
];

var newInv = [
    [2, "Hair Pin"],
    [3, "Half-Eaten Apple"],
    [67, "Bowling Ball"],
    [7, "Toothpaste"]
];

updateInventory(curInv, newInv);
```

# Analysis

Let's analyze the time complexity of the provided `updateInventory` function step by step:

```javascript
function updateInventory(arr1, arr2) {
    let keysArr1 = arr1.map(item => item[0]);
    let valuesArr1 = arr1.map(item => item[1]);

    for (let i = 0; i < arr2.length; i++) {
        let idx = valuesArr1.indexOf(arr2[i][1]);
        if (idx !== -1) {
            arr1[idx][0] += arr2[i][0];
        } else {
            arr1.push(arr2[i]);
        }
    }

    valuesArr1 = arr1.map(item => item[1]);
    let sortedValuesArr1 = arr1.map(item => item[1]).sort();
    let result = [];
    for (let i = 0; i < arr1.length; i++) {
        let idx = valuesArr1.indexOf(sortedValuesArr1[i]);
        result.push(arr1[idx]);
    }
    return result;
}
```

### Step-by-Step Time Complexity Analysis

1. **Mapping to `keysArr1` and `valuesArr1`**:
    ```javascript
    let keysArr1 = arr1.map(item => item[0]);
    let valuesArr1 = arr1.map(item => item[1]);
    ```
    - Both `map` operations iterate through `arr1`, which has a complexity of O(n), where `n` is the length of `arr1`.
    - Combined, this step has a complexity of O(n).

2. **Loop through `arr2` and update `arr1`**:
    ```javascript
    for (let i = 0; i < arr2.length; i++) {
        let idx = valuesArr1.indexOf(arr2[i][1]);
        if (idx !== -1) {
            arr1[idx][0] += arr2[i][0];
        } else {
            arr1.push(arr2[i]);
        }
    }
    ```
    - The loop runs `m` times, where `m` is the length of `arr2`.
    - Inside the loop, `valuesArr1.indexOf(arr2[i][1])` has a complexity of O(n) in the worst case.
    - The `push` operation is amortized O(1).
    - The overall complexity for this loop is O(m) * O(n) = O(mn).

3. **Re-mapping `valuesArr1`**:
    ```javascript
    valuesArr1 = arr1.map(item => item[1]);
    ```
    - This `map` operation iterates through `arr1`, which has a complexity of O(n).

4. **Mapping and sorting to `sortedValuesArr1`**:
    ```javascript
    let sortedValuesArr1 = arr1.map(item => item[1]).sort();
    ```
    - The `map` operation is O(n).
    - The `sort` operation, in the average case, is O(n log n).
    - Combined, this step has a complexity of O(n) + O(n log n) = O(n log n).

5. **Loop through `arr1` and build `result`**:
    ```javascript
    let result = [];
    for (let i = 0; i < arr1.length; i++) {
        let idx = valuesArr1.indexOf(sortedValuesArr1[i]);
        result.push(arr1[idx]);
    }
    ```
    - The loop runs `n` times.
    - Inside the loop, `valuesArr1.indexOf(sortedValuesArr1[i])` has a complexity of O(n) in the worst case.
    - The `push` operation is O(1).
    - The overall complexity for this loop is O(n) * O(n) = O(n^2).

### Total Time Complexity

Combining the complexities of each step:
1. Mapping to `keysArr1` and `valuesArr1`: O(n)
2. Loop through `arr2` and update `arr1`: O(mn)
3. Re-mapping `valuesArr1`: O(n)
4. Mapping and sorting to `sortedValuesArr1`: O(n log n)
5. Loop through `arr1` and build `result`: O(n^2)

The dominant term in the total complexity is the one with the highest growth rate, which is O(mn) and O(n^2).

Therefore, the total time complexity of the `updateInventory` function is:
\[ O(n^2 + mn) \]

In the worst case, if `m` and `n` are of similar magnitude, the time complexity can be approximated to:
\[ O(n^2) \]

### Conclusion

The overall time complexity of the `updateInventory` function is O(n^2 + mn), where `n` is the length of `arr1` and `m` is the length of `arr2`. This complexity is primarily dominated by the quadratic term O(n^2) and the product term O(mn).

