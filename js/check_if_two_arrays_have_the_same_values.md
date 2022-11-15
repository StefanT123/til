# Check if two arrays have the same values

This is only valid if the arrays contain primitive values.
```js
const checkIfArraysHaveSameValues = (array1, array2) => {
  const uniques = [...new Set(array1.concat(array2))];
  return uniques.length === array1.length // or uniques.length === array2.length;
}
```
