# Fallback when no other route is matched

If you want to specify additional logic for not-found routes, instead of just throwing default 404 page, you may create a special Route for that, at the very end of your Routes file
```php
Route::group(['middleware' => ['auth'], 'prefix' => 'admin', 'as' =>'admin.'], function () {
    Route::get('/home', 'HomeController@index');
    Route::resource('tasks', 'Admin\TasksController');
});

// Some more routes....

Route::fallback(function() {
    return 'Hm, why did you land here somehow?';
});
```
