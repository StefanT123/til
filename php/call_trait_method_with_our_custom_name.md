# Call trait method with our custom name

We can call any trait method inside our class with the name we have provided
```php
trait MyTrait
{
    public function foo()
    {
        var_dump('Hello from trait.');
    }
}

class SomeClass
{
    use MyTrait {
        foo as anotherFoo;
    }
}

(new SomeClass)->anotherFoo(); // Hello from trait.
```
