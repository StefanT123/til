# redirectTo as method

We can use redirectTo not only as variable, but also as a method in which we can apply some custom logic:
```php
public function redirectTo()
{
    if (auth()->user()->isAdmin()) {
        return '/admin';
    }

    return '/';
}
```
