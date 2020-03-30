# toString

`__toString()` allows you to set a string value for the object that will be used if the object is ever used as a string
```php
class Cat {
    public function __toString() {
        return "This is a cat\n";
    }
}

$toby = new Cat;
echo $toby;
```
