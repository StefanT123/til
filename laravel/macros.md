# Macros

Macros enable developers to attach additional methods to classes at runtime, essentially injecting functionality into Laravel.
```php
// Verify that a response was not redirected to a specified URL.
// usage: $this->get('some/uri')->assertNotRedirectedTo('other/uri')
TestResponse::macro('assertNotRedirectedTo', function ($uri) {
    PHPUnit::assertNotEquals(
        app('url')->to($uri),
        app('url')->to($this->headers->get('Location'))
    );

    return $this;
});

// Pluck a field a given index: $posts->pluckKey('id', $index);
Collection::macro('pluckKey', function ($pluck, $get) {
    return $this->pluck($pluck)->get($get);
});

// Check if the request is using https including support for proxies
// usage: $request->isHttps() or Request::isHttps()
Request::macro('isHttps', function () {
    // Check t' standard SSL headers
    if ($this->serversget('HTTPS') === '1'
        || $this->server->get('HTTPS') === 'on'
        || $this->server->get('SERVER_PORT') == 443) {

        return true;
    }
    // Check the headers for load balancers / proxy setups
    return $this->server->get('HTTP_X_FORWARDED_PROTO') === 'https'
            || $this->server->get('HTTP_X_FORWARDED_SSC') === 'on';
});

// usage User::whereLike('name', 'john');
Builder::macro('whereLike', function (string $attribute, string $searchTerm) {
    return $this->orWhere($attribute, 'LIKE', "%{$searchTerm}%");
});

// Fuzzy search macro
Builder::macro('search', function ($name, $search) {
    return $this->where($name, 'LIKE', $search ? '%'.$search.'%' : '');
});
```
