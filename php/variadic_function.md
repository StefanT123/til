# Variadic function

These are functions that are specifically designed to take any number of parameters
To make a parameter variadic, just add ... before it. Your variadic parameter must be the final parameter in your function to avoid confusion. When the function is called, PHP automatically converts sets your variadic parameter to be an array of all the values that were provided
```php
function sum_numbers(...$numbers) {
    $result = 0;

        foreach ($numbers as $number) {
            $result += $number;
        }

    return $result;
}

print sum_numbers(1, 2, 3, 4, 5);

// using array as parameter to a variadic function
// if you find you’re making common use of this you should probably rethink your approach!
print sum_numbers(...[1, 2, 3, 4, 5]);
```
