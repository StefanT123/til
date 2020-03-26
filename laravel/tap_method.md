# Tap method

The tap() function allows you to perform some action on/with a variable whilst returning the original value within the same block of code.
```php
// The old way of storing in a varibale, performing the action
// and eventually returning that variable
$user = User::first();
if ($user->name == 'Some Name') {
    $user->doThis();
} else {
    $user->doThat();
}
$user->save();

return $user

// VS using the tap magic
return tap(User::first(), function ($user) {
    if ($user->name === 'Some Name') {
        $user->doThis();
    } else {
        $user->doThat();
    }
    $user->save();
});

// Supports chaining as well (returns $user but calls save separately)
return tap(User::first())->save();
```
