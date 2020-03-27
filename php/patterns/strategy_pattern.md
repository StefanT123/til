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
class SubscriptionsController implements RegisterUserInterface
{
    public function handle()
    {
        $this->getRegistrationStrategy($request)->handle();
    }

    protected function getRegistrationStrategy(Request $request)
    {
        if ($request->plan == 'forever') {
            return new RegistersLifetimeMember;
        }

        if ($request->invitation) {
            return new RegistersTeamMember;
        }

        return new RegistersSubscriber;
    }
}

class RegistersForumUser implements RegisterUserInterface
{
    public function handle()
    {

    }
}

class RegistersSubscriber implements RegisterUserInterface
{
    public function handle()
    {

    }
}

class RegistersTeamMember implements RegisterUserInterface
{
    public function handle()
    {

    }
}

class RegistersLifetimeMember implements RegisterUserInterface
{
    public function handle()
    {

    }
}

interface RegisterUserInterface
{
    public function handle();
}
```
