# Mix and match blade directives

Did you know you can mix and match Blade directives? Once you realize @laravelphp's Blade directives just compile down to raw PHP, all sorts of things are possible!
```php
// there is no @elseisset, like @elseAuth or @elseGuest
@isset($success) ?>
    <h2>Success</h2>
<?php
// No problem, just use a plain @else
@else ?>
    <h2>Failure</h2>
<?php
@endisset
```
