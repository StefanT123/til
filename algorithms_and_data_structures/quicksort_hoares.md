# Quicksort with Hoare's partitioning scheme

```js
/**
 * Hoares quicksort, this quicksort is optimimzed for
 * speed and memory efficiency.
 *
 * @example https://itnext.io/a-sort-of-quick-guide-to-quicksort-and-hoares-partitioning-scheme-in-javascript-7792112c6d1
 *
 * @param  {Array} arr
 * @param  {Number} left
 * @param  {Array} right
 *
 * @return {Array}
 */
function quicksort(arr, left = 0, right = arr.length - 1) {
    if (left >= right) return;

    // we choose the pivot to be middle element
    // because if the array is already sorted it
    // won't do extra work

    // make sure that the pivot will be halfway between the left
    // and right pointers
    const pivot = arr[Math.floor((left + right) / 2)];

    // returned index is the pivot element
    const index = partition(arr, left, right, pivot);

    quicksort(arr, left, index - 1);
    quicksort(arr, index, right);

    return arr;
}

/**
 * Partition the array so that the values
 * bigger than the pivot are on the left,
 * and the values smaller than the pivot
 * are on the right.
 *
 * @param  {Array} arr
 * @param  {Integer} left
 * @param  {Integer} right
 * @param  {Integer} pivot
 *
 * @return {Integer}
 */
function partition(arr, left, right, pivot) {
    // loop unitl left pointer is not past right pointer
    while (left <= right) {
        while (arr[left] < pivot) {
            left++;
        }

        while (arr[right] > pivot) {
            right--;
        }

        // check if the left pointer is still to the left
        // of the right pointer, then switch the elements
        if (left <= right) {
            [arr[left], arr[right]] = [arr[right], arr[left]];
            left++;
            right--;
        }
    }

    // because everything is swapped we don't
    // know where our pivot point is in the
    // array, and the while loop breaks when
    // the left pointer comes next to the pivot
    // meaning that this is where the left sub-array
    // ends and the right one begins
    return left;
}
```
