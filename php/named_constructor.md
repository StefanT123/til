# Named constructor (static factory methods)

Named constructors can add clarity to your code. With the following example, the constructor params may not be obvious without actually digging into the source. A named constructor allow us to sidestep any doubt during setup
```php
class Product
{
    // The constructor can become private in this case
    private function __construct($category, $price = null)
    {
        $this->category = $category;
        $this->price = $price;
    }

    public static function withCategoryAndPrice($category, $price)
    {
        return new static($category, $price);
    }
}

$product  = Product::withCategoryAndPrice('clothes', 50);
```
