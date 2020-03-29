# Execute a function after the script ends

Registers a callback to be executed after script execution finishes or `exit()` is called
```php
function shutdown($param)
{
    // This is our shutdown function, in
    // here we can do any last operations
    // before the script is complete.

    echo 'Script executed with success', PHP_EOL;
}

register_shutdown_function('shutdown', 'some param');
```
