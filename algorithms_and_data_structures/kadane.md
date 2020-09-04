# Kadane's algorithm

Given an array of `n` numbers, calculate the maximum subarray sum, i.e., the largest possible sum of a sequence of consecutive values in the array.
```php
function kadane(array $arr) {
    $sum = -INF;
    $best = -INF;
    $arrLength = count($arr);

    for ($i = 0; $i < $arrLength; $i++) {
        $sum = max($arr[$i], $arr[$i] + $sum);
        $best = max($best, $sum);
    }

    return $best;
}
```
