# Observer

Basic event-listeners system
```php
// publisher
interface Subject
{
    public function attach($observable);
    public function detach($observer);
    public function notify();
}

// subscriber
interface Observer
{
    public function handle();
}

class Login implements Subject
{
    protected $observers = [];

    public function attach($observable)
    {
        if (is_array($observable)) {
            return $this->attachObservers($observable);
        }

        $this->observers[] = $observable;
    }

    protected function attachObservers($observable)
    {
        foreach ($observable as $observer) {
            if (! $observer instanceof Observer) {
                throw new Exception;
            }

            $this->attach($observer);
        }
    }

    public function detach($index)
    {
        unset($this->observers[$index]);
    }

    public function notify()
    {
        foreach ($this->observers as $observer) {
            $observer->handle();
        }
    }

    public function fire()
    {
        //preform the login
        $this->notify();
    }
}

class LogHandler implements Observer
{
    public function handle()
    {
        var_dump('log something');
    }
}

class EmailNotifier implements Observer
{
    public function handle()
    {
        var_dump('fire off an email');
    }
}

class LoginReporter implements Observer
{
    public function handle()
    {
        var_dump('do some form of reporting');
    }
}

$login = new Login;

$login->attach([
    new LogHandler,
    new EmailNotifier,
    new LoginReporter
]);

$login->fire();
```
