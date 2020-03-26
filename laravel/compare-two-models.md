# Compare two models

We can compare two laravel models with:
```php
$user->is(auth()->user());
```

Or the inverse:
```php
$user->isNot(auth()->user());
```
