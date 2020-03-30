# Template method

The sign that we need the template method is that you copy and paste a lot of code from one class to another, and then we modify some bits and pieces of code

We extract bunch of this code to an abstract class and the specific differences are put in to sub classes

**WITHOUT** template method
```php
class TurkeySub
{
    public function make()
    {
        return $this
                ->layBread()
                ->addLetuce()
                ->addTurkey()
                ->addSauces();
    }

    public function layBread()
    {
        var_dump('laying down bread');

        return $this;
    }

    public function addLetuce()
    {
        var_dump('add some letuce');

        return $this;
    }

    public function addTurkey()
    {
        var_dump('add some turkey');

        return $this;
    }

    public function addSauces()
    {
        var_dump('add sauces');

        return $this;
    }
}

// call the class function
(new TurkeySub)->make();

class VeggieSub
{
    public function make()
    {
        return $this
                ->layBread()
                ->addLetuce()
                ->addVeggies()
                ->addSauces();
    }

    public function layBread()
    {
        var_dump('laying down bread');

        return $this;
    }

    public function addLetuce()
    {
        var_dump('add some letuce');

        return $this;
    }

    public function addVeggies()
    {
        var_dump('add some veggies');

        return $this;
    }

    public function addSauces()
    {
        var_dump('add sauces');

        return $this;
    }
}

// call the class function
(new VeggieSub)->make();
```

**WITH** template method
```php
abstract class Sub
{
    public function make()
    {
        return $this
                ->layBread()
                ->addLetuce()
                ->addPrimaryToppings()
                ->addSauces();
    }

    protected function layBread()
    {
        var_dump('laying down bread');

        return $this;
    }

    protected function addLetuce()
    {
        var_dump('add some letuce');

        return $this;
    }

    protected function addSauces()
    {
        var_dump('add sauces');

        return $this;
    }

    abstract protected function addPrimaryToppings();
}

class TurkeySub extends Sub
{
    public function addPrimaryToppings()
    {
        var_dump('add some turkey');

        return $this;
    }
}

class VeggieSub extends Sub
{
    public function addPrimaryToppings()
    {
        var_dump('add some veggies');

        return $this;
    }
}
```
