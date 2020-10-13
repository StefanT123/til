# Quicksort

```php
$toBeSorted = [-2, -6, 8, 2, 54, 1, 3, 9, -54, 3];

function quicksort($array) {
    $length = count($array);

    if (count($array) < 2) {
        return $array;
    }

    $pivot = $array[$length - 1];
    $arrRight = [];
    $arrLeft = [];

    for ($i = 0; $i < $length - 1; $i++) {
        if ($array[$i] < $pivot) {
            array_push($arrLeft, $array[$i]);
        } else {
            array_push($arrRight, $array[$i]);
        }
    }

    return array_merge(quicksort($arrLeft), [$pivot], quicksort($arrRight));
}

print_r(quicksort($toBeSorted));
```

---

```js
// Swaps two items in an array, changing the original array
var swap = function(array, firstIndex, secondIndex) {
    var temp = array[firstIndex];
    array[firstIndex] = array[secondIndex];
    array[secondIndex] = temp;
};

var partition = function(array, p, r) {
    var q = p;

    // Compare array[j] with array[r], for j = p, p+1,...r-1
    // maintaining that:
    // array[p..q-1] are values known to be <= to array[r]
    // array[q..j-1] are values known to be > array[r]
    // array[j..r-1] haven't been compared with array[r]
    // If array[j] > array[r], just increment j.
    // If array[j] <= array[r], swap array[j] with array[q],
    // increment q, and increment j.
    for (var j = p; j < r; j++) {
        if (array[j] <= array[r]) {
            swap(array, j, q);
            q++;
        }
    }

    // Once all elements in array[p..r-1]
    //  have been compared with array[r],
    //  swap array[r] with array[q], and return q.
    swap(array, r, q);
    return q;
};

var quickSort = function(array, p, r) {
    if (p < r) {
        var pivot = partition(array, p, r);
        quickSort(array, pivot + 1, r);
        quickSort(array, p, pivot - 1);
    }
};

// Another way of doing it
function quickSort(arr, length = arr.length - 1, start = 0) {

    if (arr.length < 2) return arr // base case

    const pivot = arr[arr.length - 1]; //pivot value
    const left = [ ];
    const right = [ ];

    while (start < length) {
        if (arr[start] < pivot) left.push(arr[start])
        else right.push(arr[start])
        start++
    }
    return [...quickSort(left), pivot, ...quickSort(right)];
}
console.log(quickSort([4, 9, 2, 6, 8, 10, 3, 1, 7, 5]))
// [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```
