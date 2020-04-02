# Wildcard subdomains

You can create route group by dynamic subdomain name, and pass its value to every route
```php
Route::domain('{username}.workspace.com')->group(function () {
    Route::get('user/{id}', function ($username, $id) {
        //
    });
});
```
