# Domain events

### We should think if we should fire an event or use "use cases"
### With the events it's less obvious what we are doing, for this we might use the doc annotation (ex. @event, @fire)

If we have a lot of things that we need to do in our controller:
```php
class UsersController extends Controller
{
    public function store()
    {
        // Register a user
        $user = new User;
        $user->name = 'Name';
        $user->email = 'asd@ads.com';
        $user->password = bcrypt('pass');
        $user->save();

        // Send them a welcome email
        Mail::send('emails.welcome', compact('user'), function ($message) use ($user) {
            $message->to($user->email)->subject('Welcome');
        }

        // Add to CampaignMonitor newsletter list
        $cm = new CampaignMonitor;
        $cm->addToList('users');

        // Schedule a follow-up email

        // Update yout stats, payments
    }
}
```

Instead we can use the events:
```php
/**
 * @fires App\Events\UserRegistered
 */
class UsersController extends Controller
{
    public function store()
    {
        User::register([
            'name' => 'Name',
            'email' => 'asd@asd.com',
            'password' => bcrypt('pass')
        ]);
    }
}

// App\User
class User
{
    // [...]

    public static function register($attributes)
    {
        $user = statc::create($attributes);

        event(new UserRegistered($user)); // laravel event

        return $user;
    }
}

// App\Events\UserRegistered
class UserRegistered extends Event
{
    public $user;

    function __construct(User $user)
    {
        $this->user = $user;
    }
}

// App\Listeners\SendWelcomeEmail
class SendWelcomeEmail
{
    public function handle(UserRegistered $event)
    {
        var_dump("send welcome email to {$event->user->email}") ;
    }
}

// App\Listeners\AddUserToNewsletter
class AddUserToNewsletter
{
    public function handle(UserRegistered $event)
    {
        var_dump("add {$event->user->email} to newsletter") ;
    }
}
```
