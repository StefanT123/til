# Strategy pattern

Instead of putting multiple if statements in our method:
```php
class SubscriptionsController
{
    public function store()
    {
        if ($request->filed) {
            // do this
        }

        if ($request->plan == 'forever') {
            // do that
        }

        // Sign up the user, but do they want a..
        // 1. Forum account
        // 2. Regular subscription
        // 3. Team member acces
        // 4. forever account
    }
}
```

We can use unique strategy how you can accomplish particular goal
1. Identify a point of flexibility
    1. Forum account
    2. Regular subscription
    3. Team member acces
    4. forever account
2. Extract each strategy into its own class
3. Ensure that each of those strategies adheres to a common contract/interface
4. Determine the proper strategy, and let it handle the task
```php
interface Logger
{
    public function log($data);
}

class LogToFile implements Logger
{
    public function log()
    {
        var_dump('log to file');
    }
}

class LogToDatabase implements Logger
{
    public function log()
    {
        var_dump('log to db');
    }
}

class LogToXWebService implements Logger
{
    public function log()
    {
        var_dump('log to a Saas site');
    }
}

class App
{
    public function log($data, Logger $logger = null)
    {
        // set a default
        $logger = $logger ?: new LogToFile;

        $logger->log($data);
    }
}

$app = new App();
$app->log('Some info here', new LogToXWebService);
```
