# Check from where some method has been called

```php
foreach (debug_backtrace() as $debug) {              
   echo "{$debug['file']} on line {$debug['line']} is calling function: {$debug['function']}<br>";
}
```
