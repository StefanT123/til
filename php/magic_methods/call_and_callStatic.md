# Call and callStatic

The `__call()` magic function is to class functions what `__get()` is to class variables - if you call `meow()` on an object of class dog, PHP will fail to find the function and check whether you have defined a `__call()` function. If so, your `__call()` is used, with the name of the function you tried to call and the parameters you passed being passed in as parameters one and two respectively

Laravel very much depends on this
```php
class Dog {
    public function bark() {
        print "Woof!\n";
    }

    public function __call($function, $args) {
        $args = implode(', ', $args);
        print "Call to $function() with args '$args' failed!\n";
    }
}

$poppy = new Dog;
$poppy->meow("foo", "bar", "baz");
```

`__callStatic` behaves in exactly the same way but responds to undefined static method calls instead

Laravel very much depends on this
```php
class Dog {
    public function bark() {
        print "Woof!\n";
    }

    public static function __callStaic($function, $args) {
        $args = implode(', ', $args);
        print "Call to $function() with args '$args' failed!\n";
    }
}
Dog::meow("foo", "bar", "baz");
```
