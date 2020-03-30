# Get

`__get()` allows you to specify what to do if an unknown class variable is called

Laravel very much depends on this
```php
class Dog {
    public $name;
    public $dogTag;

    public function __get($var) {
        print "Attempted to retrieve $var and failed...\n";
    }
}

$poppy = new Dog();
print $poppy->age;
```
