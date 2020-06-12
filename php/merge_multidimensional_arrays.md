# Merge multidimensional arrays

If we want to merge multidimensional arrays we can still use `array_merge` instead of `array_merge_recursive`
```php
$first = [
    'level 1' => [
        'level 2' => 'original'
    ]
];

$second = [
    'level 1' => [
        'level 2' => 'override'
    ]
];

array_merge($first, $second);

// [
//     'level 1' => [
//         'level 2' => 'override'
//     ]
// ]
```
