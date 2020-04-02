# Load first existng view

We can even load an array of views and only the first existing will be actually loaded
```php
return view()->first(['custom.dashboard', 'dashboard'], $data);
```
