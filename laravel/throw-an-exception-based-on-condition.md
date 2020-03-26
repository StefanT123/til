# Throw an exception based on condition

If we need to throw an exception based on some condition:
```php
if ($condition) {
    throw new Exception('Something went wrong.');
}
```

We can shrink that code in one-liner with `throw_if` and `throw_unless`:
```php
throw_if($condition, new Exception('Something went wrong.'));

// Another way of achieving same thing
throw_if($condition, Exception::class, 'Something went wrong.');

// The inverse
thorw_unless($condition, Exception::class, 'The oposite went wrong');
```
