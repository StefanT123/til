# Spliting tasks into steps (sort of chain of responsibility)

If we have a class that has many smaller tasks that it needs to do:
```php
class Thing
{
    public function handle()
    {
        // doThis
        // doThat
        // runSomething
        // eraseSomething
        // addSomething
    }
}
```

We can instead extract each step into it's own class and then filter through an array of these bite-sized chunks and trigger them
If we have differenet dependencies for different classes, we should use Laravel `app()` helper to resolve them properly
```php
class Thing
{
    public function handle()
    {
        $tasks = [
            DoThis::class,
            DoThat::class,
            AddFooToBar::class,
            RunSomething::class
        ];

        foreach ($tasks as $task) {
            (new Task)->handle();
        }
    }
}

// we can make them adhere to some interface
class DoThis
{
    public function handle()
    {

    }
}

class DoThat
{
    public function handle()
    {

    }
}

class AddSomething
{
    public function handle()
    {

    }
}

class RunSomething
{
    public function handle()
    {

    }
}
```
