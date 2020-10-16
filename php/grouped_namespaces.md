# Grouped namespaces

If we have to import two or more classes from the same namespace, we can group them together on the same line.
```php
// Before
use App\User;
use App\Team;
use App\Subscription;

// After
use App\{User, Team, Subscription};
```
