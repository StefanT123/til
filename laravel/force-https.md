# Force HTTPS

If you want to force HTTPS in your project, do it in `AppServiceProvider` file's `boot()` method
```php
class AppServiceProvider extends ServiceProvider
{
    /**
     * Register any application services.
     *
     * @return void
     */
    public function register()
    {
        if (env('APP_ENV') === 'production') {
            $this->app['url']->forceScheme('https');
        }
    }
}
```
