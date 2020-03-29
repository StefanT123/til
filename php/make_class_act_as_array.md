# Make class act like array

SPL allows us to make our objects act like arrays in certain situations
To do this, we need to implement the `ArrayAccess` interface and its four functions: `offsetSet()`, `offsetGet()`, `offsetExists()`, and `offsetUnset()`
```php
class FileArray implements ArrayAccess {
    function offsetExists($offset) {
        return file_exists($offset);
    }

    function offsetGet($offset) {
        return file_get_contents($offset);
    }

    function offsetSet($offset, $value) {
        return file_put_contents($offset, $value);
    }

    function offsetUnset($offset) {
        return unlink($offset);
    }
}

// then we can use it like an array
$myarr = new FileArray();
$myarr["somefile.txt"] = "This is a test.";
echo $myarr["somefile.txt"];
$myarr["otherfile.txt"] = $myarr["somefile.txt"];

if (isset($myarr["somefile.txt"])) {
    unset($myarr["somefile.txt"]);
}
```
