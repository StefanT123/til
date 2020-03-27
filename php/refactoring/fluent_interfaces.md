# Fluent interfaces

Fluent interfaces are just methods that return the instance of the same object and they can be chained together
Keep in mind that this approach is harder to test
```php
class TestSomething
{
    public function doSomeThing()
    {
        // do something

        return $this;
    }

    public function doSomeOtherThing()
    {
        // do some other thing

        return $this;
    }

    public function doAnother()
    {
        // do some another thing

        return $this;
    }
}

class Test
{
    public function handle()
    {
        (new TestSomething)
            ->doSomeThing()
            ->doSomeOtherThing()
            ->doAnother();
    }
}
```
