# Tap into collection at any point without affecting the original collection

You can "tap" into the results at any point during a set of collection operations without affecting the main collection.
```php
$products->where('price', 100)
    ->tap(function ($productsThatCost100) {
        // Do something with the current collection results
        // without affecting the rest of the pipeline
        dump($productsThatCost100);
    })
    ->where('color', 'blue')
    ->tap(function ($blueProductsThatCost100) {
        // Jump in and out at any point to get different sets of data
        dump($blueProductsThatCost100);
    });
```
