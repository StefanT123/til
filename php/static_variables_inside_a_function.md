# Static variables inside the body of a function

Class properties being declared as `static` is nothing new. But did you know that we can declare static variables inside the body of a function?
```php
function surprise()
{
    static $alreadySurprised;

    if ($alreadySurprised) {
        return;
    }

    // This line of code will be reached only the first time the function is being called

    $alreadySurprised = true;
}
```
Consider that we call the `surprise()` method from several different places in our app. The line that's commented out would be executed just once for the lifetime of the request (in HTTP context) / script execution (in CLI context)

If that function was a class method, it would behave the exact same way as it’s being declared as a static property on the class level. Ie. if we use it inside a non-static method, and we call that method on two different instances of the class, PHP will use the same variable for both. So the only thing we get by declaring it inside the body of the function rather than the class itself, is that only the current function will have access to the variable. So yeah, most probably that's not a good use case for them.

The interesting part however is we can use static variables inside regular functions as well (outside classes). And what’s more fascinating for me is that they work inside closures, too. I remember the first time I saw this feature, it was used exactly inside a closure. The default Laravel `UserFactory` file used to ship with that in the past. They needed it so the `bcrypt` function is called only once even if you seed thousands of records.

I also find this feature very useful when I want to lazy load a database query, and to make sure it's not called more than once per request. Sure, there are other ways to achieve the same thing, but I like this approach because it’s short and clean.
