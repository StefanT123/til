# Merge arrays

We can merge arrays with `array_merge` or with `+`, but there's a difference between these two. The merging with `array_merge` will override existing keys, while merging with `+` will not. In other words: when a key exists in the first array, `+` will not merge an item with the same key from another array into the first one.
```php
$first = [
    'a',
    'b',
];

$second = [
    'c',
];
```

With `+`:
```php
$first + $second;

// ['a', 'b']
```

With `array_merge`:
```php
array_merge($first, $second);

// ['a', 'b', 'c']
```

What's happening here is that `array_merge` will override existing keys, while `+` will not. In other words: when a key exists in the first array, `+` will not merge an item with the same key from another array into the first one.

In our example, both arrays actually had numerical keys, like so:
```php
$first = [
    0 => 'a',
    1 => 'b',
];

$second = [
    0 => 'c',
];
```

Which explains why `$first + $second` doesn't add 'c' as an element: there already is an item with index 0 in the original.
