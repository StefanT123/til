# Invoke

The `__invoke()` method is called when a script tries to call an object as a function
```php
class CallableClass
{
    public function __invoke($x)
    {
        var_dump($x);
    }
}
$obj = new CallableClass;
$obj(5); // int(5)
var_dump(is_callable($obj)); // true
```
