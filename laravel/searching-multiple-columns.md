# Searching multiple columns

In laravel we can make macro for searching model by using multiple columns.

Using eloquent we can do this:
```php
User::query()
   ->where('name', 'LIKE', "%{$searchTerm}%")
   ->orWhere('email', 'LIKE', "%{$searchTerm}%")
   ->get();
```

Instead we can build macro for searching in multiple columns:
```php
Builder::macro('search', function ($attributes, string $searchTerm) {
    $this->where(function (Builder $query) use ($attributes, $searchTerm) {
        foreach (array_wrap($attributes) as $attribute) {
            $query->orWhere($attribute, 'LIKE', "%{$searchTerm}%");
        }
    });

    return $this;
});
```

Now we can do this:
```php
// searching a single column
User::whereLike('name', $searchTerm)->get();

// searching multiple columns in one go
User::whereLike(['name', 'email'], $searchTerm)->get();
```

If we want a support for relations (ex. `category.name`):
```php
Builder::macro('search', function ($attributes, string $searchTerm) {
    $this->where(function (Builder $query) use ($attributes, $searchTerm) {
        foreach (array_wrap($attributes) as $attribute) {
            $query->when(
                str_contains($attribute, '.'),
                function (Builder $query) use ($attribute, $searchTerm) {
                    [$relationName, $relationAttribute] = explode('.', $attribute);

                    $query->orWhereHas($relationName, function (Builder $query) use ($relationAttribute, $searchTerm) {
                        $query->where($relationAttribute, 'LIKE', "%{$searchTerm}%");
                    });
                },
                function (Builder $query) use ($attribute, $searchTerm) {
                    $query->orWhere($attribute, 'LIKE', "%{$searchTerm}%");
                }
            );
        }
    });

    return $this;
});
```

With this macro, we can search like this:
```php
Post::whereLike(['name', 'description', 'category.name'], $searchTerm)->get();
```

We can also allow for wildcard searches (ex. `%jon`, `john%`):
```php
Builder::macro('search', function ($attributes, $terms) {
    $this->where(function (Builder $query) use ($attributes, $terms) {
        foreach (array_wrap($attributes) as $attribute) {
            foreach (array_wrap($terms) as $term) {
                /*** allow arbitrary patterns by not forcing % wildcard chars around the term(s) ***/
                $query->orWhere($attribute, 'LIKE', $term);
            }
        }
    });

    return $this;
});
```

With this macro we can search like this:
```php
User::search('name', ['john%', 'jon%', 'jone%']);
```
