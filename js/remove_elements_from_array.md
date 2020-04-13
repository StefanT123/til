# Remove elements from array

This snippet returns a new array with n elements removed from the left
```js
const drop = (arr, n = 1) => arr.slice(n);

drop([1, 2, 3]); // [2,3]
drop([1, 2, 3], 2); // [3]
drop([1, 2, 3], 42); // []
```

This snippet returns a new array with n elements removed from the right
```js
const dropRight = (arr, n = 1) => arr.slice(0, -n);

dropRight([1, 2, 3]); // [1,2]
dropRight([1, 2, 3], 2); // [1]
dropRight([1, 2, 3], 42); // []
```

This snippet removes elements from an array until the passed function returns true
```js
const dropWhile = (arr, func) => {
  while (arr.length > 0 && !func(arr[0])) arr = arr.slice(1);
  return arr;
};

dropWhile([1, 2, 3, 4], n => n >= 3); // [3,4]
```
