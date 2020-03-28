# Loop through a class

If you want to make it possible to loop through a class in PHP, you just need to make it implement the IteratorAggregate interface and define a single "getIterator" method which describes what to iterate over
```php
class CustomCollection implements IteratorAggregate
{
    public $dontInclude;
    public $theseProperties;
    public $whenLooping;

    public $items;

    public function __construct($items)
    {
        $this->items = $items;
    }

    public function getIterator()
    {
        return new ArrayIterator($this->items);
    }
}

// By default when you loop over a class instance, it will iterate over
// the public props. But since we're implementing the ItteratorAggregate interface,
// it'll only loop over what we tell it to inside the getIterator() method
foreach (new CustomCollection(['foo', 'bar']) as $key => $value) {
    dump("Loop item $key: $value");
}

// Result:
// Loop item 0: foo
// Loop item 1: bar
```
