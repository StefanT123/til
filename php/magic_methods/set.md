# Set

`__set()` is called whenever an undefined class variable is set

This is a little harder to use with good reason, however, and is more likely to confuse than help
```php
class MyTable {
    public $name;

    public function __construct($name) {
        $this->name = $name;
    }

    public function __set($var, $val) {
        GLOBAL $db;
        mysqli_query($db, "UPDATE {$this->name} SET $var = '$val';");
    }
}

$systemvars = new MyTable("systemvars");
$systemvars->adminEmail = 'telrev@somesite.net';
```
