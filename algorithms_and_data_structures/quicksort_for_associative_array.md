# Quicksort for associative array

```php
$array = [
    [
        'id' => 1,
        'rating' => 5,
        'reviewCreatedOnTime' => 1611579567,
    ],
    [
        'id' => 2,
        'rating' => 5,
        'reviewCreatedOnTime' => 1711559567,
    ],
    [
        'id' => 3,
        'rating' => 2,
        'reviewCreatedOnTime' => 1611578567,
    ],
    [
        'id' => 4,
        'rating' => 3,
        'reviewCreatedOnTime' => 1411579567,
    ],
    [
        'id' => 5,
        'rating' => 4,
        'reviewCreatedOnTime' => 1611579867,
    ],
];

function quicksort($array) {
    $count = count($array);

    if ($count < 2) {
        return $array;
    }

    $pivot = $array[$count - 1];
    $arrRight = [];
    $arrLeft = [];

    for ($i = 0; $i < $count - 1; $i++) {
        if ($array[$i]['rating'] < $pivot['rating']) {
            $arrLeft[] = $array[$i];
        } elseif ($array[$i]['rating'] === $pivot['rating']) {
            if ($array[$i]['reviewCreatedOnTime'] < $pivot['reviewCreatedOnTime']) {
                $arrLeft[] = $array[$i];
            } else {
                $arrRight[] = $array[$i];
            }
        } else {
            $arrRight[] = $array[$i];
        }
    }

    return array_merge(quicksort($arrRight), [$pivot], quicksort($arrLeft));
}

print_r(quicksort($reviews));
```
