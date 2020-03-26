# Magic methods on eloquent where clauses

You can use "magic" methods* on eloquent where clauses for a shorthand way of adding conditions - these take the shape of `YourModel::wherePascalCaseFieldName()`
```php
// This
User::where('name', 'John')->orWhere('email', 'john@example.com');

// ..can be this
User::whereNameOrEmail('John', 'john@example.com');

// ...
User::whereStatusAndTotalAndUseridOrPaid('shipped', 100, 20, 1);
```
