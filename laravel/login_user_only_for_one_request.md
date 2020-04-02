# Login user ony for one request

You can login with user only for ONE REQUEST, using method `Auth::once()`. No sessions or cookies will be utilized, which means this method may be helpful when building a stateless API
```php
if (Auth::once($credentials)) {
    //
}
```
