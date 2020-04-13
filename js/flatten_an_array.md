# Flatten an array

```js
const arrayToFlatten = [[1,2,3], [4,5,6], [7,8,9]];
const flattenedArray = [].concat(...arrayToFlatten);

// with recursion
function flatten(arr) {
  var result = []
  arr.forEach(function(element) {
    if (! Array.isArray(element)) {
      result.push(element)
    } else {
      result = result.concat(flatten(element))
    }
  })
  return result
}
flatten([1, [2], [3, [[4]]]]);
```

```js
const flatten = arr => [].concat(...arr.map(v => (Array.isArray(v) ? flatten(v) : v)));

flatten([1, [2], [[3], 4], 5]); // [1,2,3,4,5]
```

This snippet flattens an array up to a specified depth using recursion
```js
const flatten = (arr, depth = 1) =>
  arr.reduce((a, v) => a.concat(depth > 1 && Array.isArray(v) ? flatten(v, depth - 1) : v), []);

flatten([1, [2], 3, 4]); // [1, 2, 3, 4]
flatten([1, [2, [3, [4, 5], 6], 7], 8], 2); // [1, 2, 3, [4, 5], 6, 7, 8]
```
