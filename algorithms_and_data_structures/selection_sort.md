# Selection sort

Complexity of selection sort is `O(n^2)`. Note that technically the number of items we compare keeps becoming smaller, but this does not mean anything in terms of the Big O conventions for complexity.
```js
const selectionSort = (originalList) => {
  //we first copy the array to avoid modifying the original array, since objects are passed by reference in JS
  const list = [...originalList]
  const len = list.length
  for (let i = 0; i < len; i++) {
    let min = i
    for (let j = i + 1; j < len; j++) {
      if (list[min] > list[j]) {
        min = j
      }
    }
    if (min !== i) {
      // a new minimum is found. Swap that with the current element
      ;[list[i], list[min]] = [list[min], list[i]]
    }
  }
  return list
}

const listOfNumbers = [1, 6, 3, 4, 5]
console.log(selectionSort(listOfNumbers)) //[1,3,4,5,6]
```
