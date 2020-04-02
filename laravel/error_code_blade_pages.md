# Error code blade pages

If we want to create a specific error page for some HTTP code, like 500 - just create a blade file
with this code as filename, in `resources/views/errors/500.blade.php`, or
`403.blade.php` etc, and it will automatically be loaded in case of that error code.
