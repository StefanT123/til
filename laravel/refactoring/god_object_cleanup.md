# God object cleanup

## User class is growing as we implement new methods check if the methods fit under some term

So instead of this:
```php
class User extends Authenticatable
{
    public function favoritesCount()
    {
        return 15;
    }

    public function completionsCount()
    {
        return 20;
    }

    public function experience()
    {
        return 1234;
    }
}
```

We can see that these are all stats, so we can add method `stats()`
```php
class User extends Authenticatable
{
    protected function stats()
    {
        return new Stats($this);
    }
}

class Stats
{
    protected $user;

    public function __construct(User $user)
    {
        $this->user = $user;
    }

    public function favorites()
    {
        return $this->user->favorites()->count();
    }

    public function completions()
    {
        return $this->user->completions()->count();
    }

    public function expirience()
    {
        return $this->user->expirience()->count();
    }
}
```

---

## Use traits

Instead of adding many methods in some class like this:
```php
class User extends Authenticatable
{
    public function completions()
    {
        // fetch completions
    }

    protected function complete()
    {
        // reference relationship to complete item
    }

    protected function uncomplete()
    {
        // reference relationship to uncomplete item
    }

    protected function completed()
    {
        // check if item is completed
    }

    protected function startConversation(Conversation $conversation)
    {
        // create a new thread for the current user
    }

    protected function replyTo(Conversation $conversation, Reply $reply)
    {
        // have the user reply to a conversation with the given reply
    }
}
```

We can use traits:
```php
class User extends Model
{
    use Completable;
    use ParticipatesInForum;
}

trait Completable
{
    public function completions()
    {
        // fetch completions
    }

    protected function complete()
    {
        // reference relationship to complete item
    }

    protected function uncomplete()
    {
        // reference relationship to uncomplete item
    }

    protected function completed()
    {
        // check if item is completed
    }
}

trait ParticipatesInForum
{
    protected function startConversation(Conversation $conversation)
    {
        // create a new thread for the current user
    }

    protected function replyTo(Conversation $conversation, Reply $reply)
    {
        // have the user reply to a conversation with the given reply
    }
}
```

---

## Extracting value objects

If you find multiple pieces of behavior that surround a single primitive or value, consider a value object
here we have a hint, the prefix "revenue" is repeating
```php
class Performace extends Model
{
    public function revenue()
    {
        return $this->revenue; // in cents 9000 (90 dollars)
    }

    public function revenueInDollars()
    {
        return $this->revenue() / 100; // 90
    }

    public function revenueAsCurrency()
    {
        return money_format('$%i', $this->revenueInDollars()); // $90.00
    }
}
```

So we can extract a value object
```php
class Performance extends Model
{
    // custom accessor that eloquent uses
    // when you access revenue field, laravel will
    // pipe the value through there
    // that means that when we are accessing the revenue property
    // we are getting an instance of the Revenue class
    // check https://laravel.com/docs/5.6/eloquent-mutators
    public function getRevenueAttribute($revenue)
    {
        return new Revenue($revenue);
    }
}

// value object
class Revenue
{
    private $revenue;

    public function __construct($revenue)
    {
        $this->revenue = $revenue;
    }

    public function inDollars()
    {
        return $this->revenue / 100; // 90
    }

    public function asCurrency()
    {
        return money_format('$%i', $this->inDollars()); // $90.00
    }

    // function that handles
    // if we try to refference this object as a string
    // what should happen
    public function __toString()
    {
        // when we try to echo $performance->revenue
        return (string) $this->revenue;
    }
}
```
