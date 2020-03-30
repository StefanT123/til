# Destruct

PHP calls destructors as soon as objects are no longer available, and the destructor function takes no parameters

We should call `parent::__destruct()` after the local code for the destruction so that you are not destroying variables before using it
```php
class MyClass
{
    public $name = 'MyClass';

    public function __destruct() {
        echo "{$this->name} is no more...\n";

        parent::__destruct();
    }
}
```
