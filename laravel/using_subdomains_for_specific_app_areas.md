# Using subdomains for specific app areas

Consider using subdomains for your app areas and also splitting routes in files.
1. Put your domains in your "hosts" file
2. All route groups with respective domains
3. Session domain
4. php artisan serve --port=80
```php
# config/app.php
'domain' => env('APP_DOMAIN', 'app.test');
'dashboard_domain' => env('APP_DASHBOARD_DOMAIN', 'dashboard.app.test');

# .env
SESSION_DOMAIN=.app.test

# app/Providers/RouteServiceProvider.php
protected function mapWebRoutes()
{
    Route::middleware('web')
        ->domain(config('app.domain')) # -> NOTE THIS
        ->namesapce($this->namespace)
        ->group(base_path('routes/web.php'));
}

protected function mapDashboardRoutes() # -> Call this from the map method
{
    Route::middleware('web')
        ->name('dashboard.')
        ->domain(config('app.dashboard_domain'))
        ->namesapce("$this->namespace\\Dashboard")
        ->group(base_path('routes/dashboard.php'));
}
```
