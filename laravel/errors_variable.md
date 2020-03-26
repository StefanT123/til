# Errors variable

Laravel's $errors variable enables you to simplify these things as well and can already be leveraged to really cut down extraneous keystrokes.
```php
// before
@if ($errors->has('email'))
    <span>{{ $errors->first('email') }}</span>
@endif
// after
{ !! $errors->first('email', '<span>:message</span>') !! }
```
