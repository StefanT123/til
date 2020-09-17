# Group Route::resource() into one statement

If you have a lot of `Route::resource()` statements in your routes, you can group them into one array.
```php
// Instead of
Route::resource('photos', 'PhotoController');
Route::resource('posts', 'PostController');
Route::resource('users', 'UserController');

// You can do one array
Route::resource([
    'photos' => 'PhotoController',
    'posts' => 'PostController',
    'users' => 'UserController',
]);
```
