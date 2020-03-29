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

---

If you need fine control over iteration through your object, we can use `Iterator` interface
A class that implements Iterator needs the following functions:
  1. `rewind()` - reset to the beginning of the collection
  2. `key()` - get the current key
  3. `current()` - get the value of current key
  4. `next()` - move to the next item in the collection
  5. `valid()` - returns whether there are more values to be read in the collection
```php
class Factor implements Iterator {
    private $currpos = 0;
    private $max;

    private function doFactor($val) {
        if ($val <= 1) return 1;

        return $val * $this->doFactor($val - 1);
    }

    public function key() {
        return $this->currpos;
    }

    public function current() {
        if ($this->currpos == 0) return 0;
        return $this->dofactor($this->currpos);
    }

    public function next() {
        ++$this->currpos;
    }

    public function rewind() {
        $this->currpos = 0;
    }

    public function valid() {
        if ($this->currpos <= $this->max) {
            return true;
        } else {
            return false;
        }
    }

    public function __construct($maxval) {
        $this->max = $maxval;
    }
}

// caling the object as iterator
$myfactor = new Factor(6);

foreach($myfactor as $key => $val) {
    echo "$key = $val\n";
}
```
