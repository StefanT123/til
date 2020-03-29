# Array functions

```php
array_diff(arr1, arrays) // returns a new array containing all the values of $arr1 that do not exist in $arr2
array_intersect(arr1, arrays) // returns a new array containing all the values of $arr1 that do exist in $arr2
array_merge(arr1, arrays) // combines the two arrays
array_unique(arg, flags) // removes the duplicate values from the array

array_filter(arg, callback, use_keys) // filter elements through a function you specify. If the function returns true, the item makes it into the array that is returned, otherwise it is not
/*
    EXAMPLE:
    function endswithy($value) {
        return (substr($value, -1) == 'y'); // will return all the people that dont have y as the last letter
    }

    $people = array("Johnny", "Timmy", "Bobby", "Sam", "Tammy", "Danny", "Joe");
    $withy = array_filter($people, "endswithy");
    var_dump($withy);
 */

extract(&arg, extract_type, prefix) // converts elements in an array into variables in their own right ( check for the values of the second param )
/*
    EXAMPLE:
    $Wales = 'Swansea';
    $capitalcities['England'] = 'London';
    $capitalcities['Scotland'] = 'Edinburgh';
    $capitalcities['Wales'] = 'Cardiff';
    extract($capitalcities);
    print $Wales;

    After calling extract, the "England", "Scotland", and "Wales" keys become variables in their own right ($England, $Scotland, and $Wales), with their values set to "London", "Edinburgh", and "Cardiff" respectively. By default, extract() will overwrite any existing variables, meaning that $Wales's original value of "Swansea" will be overwritten with "Cardiff".
 */

in_array(needle, haystack, strict) // check if some value exists in array
array_shift(&stack) // takes an array as its only parameter, and returns the value from the front of the array while also removing it from the array
array_pop(&stack) // takes an array as its only parameter, and returns the value from the end of the array while also removing it from the array
array_unshift(&stack, vars) // place an element into an array at the start
array_push(&stack, vars) // place an element into an array at the end
array_flip(arg) // exchanges all the keys in that array with their matching values, returning the new, flipped array

array_keys(arg, search_value, strict) // returns an array of all the keys in an array
array_values(arg) // returns an array of all the values in an array

shuffle(&arg) // takes the entire array and randomises the position of the elements in there ( One major drawback to using shuffle() is that it mangles your array keys )
array_rand(arg, num_req) // takes an array to read from, then returns one random key from inside there

range(low, high, step) // generate number in given range and put them in array

reset(&arg) // rewinds its array parameter's cursor to the first element, then returns the value of that element
end(&arg) // set the array cursor to the last element, and returns that value
next(&arg) // move the cursor pointer forward
prev(&arg) // move the cursor pointer backward

$myarray['foo'] = "bar";
print "This is from an array: {$myarray['foo']}\n"; // passing arrays in string

serialize(var) // converts an array, given as its only parameter, into a normal string that you can save in a file, pass in a URL, etc.
unserialize(variable_representation, allowed_classes) // it takes a serialize()d string and converts it back to an array
```
