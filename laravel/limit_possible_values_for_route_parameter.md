# Limit posible values for route parameter

When registering routes, you may limit the possible values for a route parameter. In this way you may change your response based on a valid parameter, having an expressive route and not a Query string parameter.
```php
Route::get('stores/{store}/orders/{type?}')
    ->uses('StoreOrderController@byType')
    ->name('stores.orders.by-type.index')
    ->where('type', 'new|fulfilling|pickup|history');
```
