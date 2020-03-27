# Policies

Instead of doing checks in our controller, we can make a policy class

Instead of this:
```php
class TeamMembersController extends Controller
{
    public function store()
    {
        // if you are not signed in, no
        if (auth()->guest()) {
            abort(403, 'You are not signed in');
        }

        // if you are not the owner of the team, no
        if ($team->owner_id != auth()->id()) {
            abort(403, 'Not owner');
        }

        // if the team is maxed out, no
        if ($team->isMaxedOut()) {
            abort(403, 'Maxed out');
        }

        return 'Add the user to the team';
    }
}
```

We can write it like this:
```php
class TeamMembersController extends Controller
{
    public function store()
    {
        (new AddTeamMemberPolicy($team))->allows();

        return 'Add the user to the team';
    }
}

class Team
{
    public function isMaxedOut()
    {
        return false;
    }

    public function isOwnedBy(User $user)
    {
        return $this->owner_id == $user->id;
    }
}

class TeamMemberPolicy
{
    protected $team;

    public function __construct(Team $team)
    {
        $this->team = $team;
    }

    public function allows()
    {
        if (auth()->guest()) {
            abort(403, 'You are not signed in');
        }

        if ($team->isOwnedBy(auth()->user())) {
            abort(403, 'Not owner');
        }

        if ($team->isMaxedOut()) {
            abort(403, 'Maxed out');
        }
    }
}
```
