# Sleep and wakeup

There is one special feature with saving objects, though, and that is the fact that when `serialize()` and `unserialize()` are called, they will look for a `__sleep()` and `__wakeup()` function on the object they are working with respectively. These functions, which you have to provide yourself if you want them to do anything, allow you to properly keep an object working during its hibernation period (when it is just a string of data)

For example, when `__sleep()` is called, a logging object should save and close the file it was writing to, and when `__wakeup()` is called the object should reopen the file and carry on writing. Although `__wakeup()` need not return any value, `__sleep()` must return an array of the values you wish to have saved. If no `__sleep()` function is present, PHP will automatically save all variables, but you can mimic this behaviour in code by using the `get_object_vars()` function

If you find yourself needing to save objects, keep `__sleep()` and `__wakeup()` in mind - together they allow you to keep objects fully working across pages
```php
class logger {
    private function __sleep() {
        // do stuff here
        return array_keys(get_object_vars($this)); // get_object_vars() takes an object as its only parameter, and returns an array of all the variables and their values in the object

        // You need to pass the variables to save back as the values in the array, so you should use the array_keys() function on the return value of get_object_vars()
    }

    private function __wakeup() {
        $this->openAndStart();
    }

    private function saveAndExit() {
        // ...[snip]...
    }
}
