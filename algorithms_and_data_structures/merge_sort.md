# Merge sort

Notice how in `_mergeArrays()` we initialize a resulting array `c` that we fill with the values of the 2 arrays `a` and `b` we pass to the function, ordered by value. Calling `shift()` on an array will remove the first item in the array, returning it, so we pass it to `c.push()` to add it to the `c` array.

The complexity of this algorithm is `O(n log(n))`, which makes it very efficient.
```js
const _mergeArrays = (a, b) => {
  const c = []

  while (a.length && b.length) {
    c.push(a[0] > b[0] ? b.shift() : a.shift())
  }

  //if we still have values, let's add them at the end of `c`
  while (a.length) {
    c.push(a.shift())
  }
  while (b.length) {
    c.push(b.shift())
  }

  return c
}

const mergeSort = (a) => {
  if (a.length < 2) return a
  const middle = Math.floor(a.length / 2)
  const a_l = a.slice(0, middle)
  const a_r = a.slice(middle, a.length)
  const sorted_l = mergeSort(a_l)
  const sorted_r = mergeSort(a_r)
  return _mergeArrays(sorted_l, sorted_r)
}
```
