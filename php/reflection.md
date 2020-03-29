# Reflection

Reflection is designed to reverse engineer various parts of PHP, including classes, functions, and extensions. By "reverse engineer" it means that it gives you all sorts of information that otherwise you would need to try to dig out yourself. There are three primary uses for reflection:
  + You have encoded scripts you need to interact with.
  + The PHP manual isn't wholly up to date and you are unable to/don't want to read the source code.
  + You're just curious how something works and would rather not read someone else's PHP source code.

Reflection itself is handled through various classes, the root of which is the Reflection class. There's also ReflectionClass, ReflectionExtension, ReflectionException, ReflectionFunction, ReflectionMethod, ReflectionObject, ReflectionParameter, and ReflectionProperty, for looking at various parts of your script

There are many other functions available in the ReflectionClass class – check out the online PHP manual for more information

The @@ lines tell us where individual items were actually defined in the source code, which is great for jumping straight to something that interests you
```php
class MyParent {
    public function foo($bar) {
        // do stuff
    }
}

class MyChild extends MyParent {
    public $val;

    private function bar(myparent &$baz) {
        // do stuff
    }

    public function __construct($val) {
        $this->val = $val;
    }
}

$child = new MyChild('hello world');
$child->foo('test');

$reflect = new ReflectionClass('MyChild');
echo $reflect;
```

---

The output is detailed information on all our functions, neatly formatted
```php
class MyParent {
    public function foo($bar) {
        // do stuff
    }
}

class MyChild extends MyParent {
    public $val;

    private function bar(myparent &$baz) {
        // do stuff
    }

    public function __construct($val) {
        $this->val = $val;
    }
}

$reflect = new ReflectionClass('MyChild');

echo "\nPrinting all methods in the 'MyChild' class:\n";
echo "============================================\n";

foreach($reflect->getMethods() as $reflectmethod) {
    echo "  {$reflectmethod->getName()}()\n";
    echo "  ", str_repeat("-", strlen($reflectmethod->getName()) + 2), "\n";

    foreach($reflectmethod->getParameters() as $num => $param) {
        echo "    Param $num: \$", $param->getName(), "\n";
        echo "      Passed by reference: ", (int)$param->isPassedByReference(), "\n";
        echo "      Can be null: ", (int)$param->allowsNull(), "\n";

        echo "      Class type: ";
        if ($param->getClass()) {
            echo $param->getClass()->getName();
        } else {
            echo "N/A";
        }
        echo "\n\n";
    }
}
```
