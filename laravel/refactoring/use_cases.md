# Use cases (in laravel these are called jobs)

### Do this workflow for the very important and complicated things in your system that have many operations
### Don't unit test it, it's hard for testing

Instead of mudding our controller with many operations:
```php
class PurchasesController extends Controller
{
    public function store()
    {
        // different
        // operations
        // for purchasing
        // something


        return redirect('/');
    }
}
```

We can use laravel jobs:

```php
class PurchasesController extends Controller
{
    public function store()
    {
        dispatch(new PurchaseSomething());

        return redirect('/');
    }
}

// use jobs (php artisan make:job PurchaseSomething)
class PurchaseSomething extends Job
{
    public function handle()
    {
        $this->preparePurchase()
            ->sendEmail();
    }

    protected function preparePurchase()
    {
        var_dump('preparing the purchase');

        return $this;
    }

    protected function sendEmail()
    {
        var_dump('sending email');

        return $this;
    }
}
```

