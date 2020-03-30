# Clone

Sometimes it is important to only work on copies of objects - you might not want to affect the state of the original. To do this, we use the built-in keyword "clone", which performs a complete copy of the object

Internally, the clone keyword copies all the variables from the first object to a new object, then calls a magic function `__clone()` for the class it is copying. You can override `__clone()` if you want, thereby giving you the flexibility to perform extra actions when a variable is copied - you can think of it as a constructor for copied object
```php
class MyClass
{
    public $name = 'MyClass';

    public function __clone() {
        $this->name .= '++';
    }
}
```
