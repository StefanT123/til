# Factory callbacks

While using factories for seeding data, you can provide Factory Callback functions to perform some action after record is inserted
```php
$factory->afterCreating(App\User::class, function ($user, $faker) {
    $user->accounts()->save(factory(App\Account::class)->make());
});
```
