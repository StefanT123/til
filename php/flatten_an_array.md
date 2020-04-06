# Flatten an array

```php
$arr = [1, 2, [3, [4]], 6];
$arr2 = [];

array_walk_recursive($arr, function ($value) use (&$arr2) {
    array_push($arr2, $value);
});

var_dump($arr2);
```
