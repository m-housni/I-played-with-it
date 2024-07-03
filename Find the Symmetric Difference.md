# Find the Symmetric Difference
The mathematical term symmetric difference (△ or ⊕) of two sets is the set of elements which are in either of the two sets but not in both. For example, for sets A = {1, 2, 3} and B = {2, 3, 4}, A △ B = {1, 4}.

Symmetric difference is a binary operation, which means it operates on only two elements. So to evaluate an expression involving symmetric differences among three elements (A △ B △ C), you must complete one operation at a time. Thus, for sets A and B above, and C = {2, 3}, A △ B △ C = (A △ B) △ C = {1, 4} △ {2, 3} = {1, 2, 3, 4}.

Create a function that takes two or more arrays and returns an array of their symmetric difference. The returned array must contain only unique values (no duplicates).

# Solution O(n2)

``` javascript
function symdiff2( a1 , a2 ) {
    let res = [];
    for(let i = 0; i < a1.length; i++) {
        if(a2.indexOf(a1[i]) === -1) {
            res.push(a1[i]);
        }
    }
    for(let i = 0; i < a2.length; i++) {
        if(a1.indexOf(a2[i]) === -1) {
            res.push(a2[i]);
        }
    }
    let resWithNoDupLicates = new Set()
    for(let i = 0; i < res.length; i++) {
        resWithNoDupLicates.add(res[i]);
    }
    
    return Array.from(resWithNoDupLicates);

}

function symdiff(...args) {
    return args.reduce(symdiff)
}

sym([1, 2, 3], [5, 2, 1, 4]);
```
