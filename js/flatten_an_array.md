# Flatten an array

```js
const arrayToFlatten = [[1,2,3], [4,5,6], [7,8,9]];
const flattenedArray = [].concat(...arrayToFlatten);

// with recursion
function flatten(arr) {
  var result = []
  arr.forEach(function(element) {
    if (!Array.isArray(element)) {
      result.push(element)
    } else {
      result = result.concat(flatten(element))
    }
  })
  return result
}
flatten([1, [2], [3, [[4]]]]);
```
