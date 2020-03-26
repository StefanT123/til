# Bulk filling model attributes

Use the fill() method to assign attributes to an eloquent model in bulk. this also allows method chaining in the same block to help your code flow a little smoother.

Instead of:
```php
// Assigning properties one by one
$user->first_name = 'John';
$user->last_name = 'Doe';
$user->active = true;
$user->save();
```

We can do this:
```php
// bulk aissining with fill()
$attributes = [
    'first_name' => 'John',
    'last_name' => 'Doe',
    'active' => true
];
$user->fill($attributes)->save();
```
