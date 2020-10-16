# The `+` operator for merging arrays

I was taught to use `array_merge()` when I want to merge arrays. However, I find myself reaching out for the + operator more often, because it doesn't allow overriding keys.
```php
$trusted = [
    'name' => 'Jeff',
    'user_id' => 5,
];

$untrusted = [
    'user_id' => 1,
];

$trusted + $untrusted;
=> [
     "name" => "Jeff",
     "user_id" => 5,
   ]

array_merge($trusted, $untrusted);
=> [
     "name" => "Jeff",
     "user_id" => 1,
   ]
```
