# pipe method

Laravels Collection 'pipe' operation provides a nice interface for extracting out a series of operations into named functions that we pipe the collection through.
```php
/*
    Here's a pipeline which is doing the following steps:
    1. Grouping products by catefory
    2. Grabbing the first catefory with 2+ products
    3. Reducing set down to products more expensive than 100
    4. sorting products from cheapest to most expensive
 */
$filtered = $products->groupBy('category')
                        ->firstWhere(function ($categoryGroup) {
                            return count($categoryGroup) > 1;
                        })
                        ->where(function ($product) {
                            return $product['price'] > 100;
                        })->sortBy('price');

/*******/

function multipleProducts($collection)
{
    return $collection->first(function ($categoryGroup) {
        return count($categoryGroup) > 1;
    });
}

function expensive($collection)
{
    return $collection->filter(function ($product) {
        return $product['price'] > 100;
    })->sortBy('price');
}

// Using the pipe() method and passing our own custom callables can simplify it
// down to something like this
$filtered = $products->groupBy('category')
                        ->pipe('multipleProducts')
                        ->pipe('expensive');
```
