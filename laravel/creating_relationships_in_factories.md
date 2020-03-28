# Creating relationships in factories

If we want to create a relationship in factory, but with the ability to overwirte it later, we can do it like this
```php
$factory->define(Property::class, function (Faker $faker) {
    return [
        'title' => $faker->sentence(3),
        'slug' => $faker->slug,
        'status' => $faker->randomElement(['draft', 'published']),
        'description' => $faker->text(),
        'address' => $faker->address,
        'price' => $faker->randomNumber(2),
        'square_meter' => $faker->numberBetween(50, 150),
        'type' => $faker->randomElement(['house', 'apartment', 'room']),
        // laravel is smart enough to know that if value is not provided
        // it will need to create a user and assign the id
        'user_id' => factory(App\User::class),
    ];
});

// if we want to overwrite the relationship value
factory(Property::class)->create(['user_id' => 1]);
```
