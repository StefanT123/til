# Get only needed fields from relationship

```php
class User extends Model
{
    // ...

    public function teams()
    {
        return $this->belongsToMany(Team::class);
    }

    // ...
}

class Team extends Model
{
    // ...

    public function users()
    {
        return $this->belongsToMany(User::class);
    }

    // ...
}
```

`User` model has sensitive data or maybe your `User` model is huge and its a better approach to get only the data that you need, maybe you want the name and email only
```php
$team = Team::first();
$team->users()->select(['name', 'email'])->get();
```
Here you would see some eloquent exception, this is because the `User` model has a column name and `Team` model could have a column name too, we just need to be explicit with the table and the columns that we need:
```php
Team::users()->select(['users.name', 'users.email'])->get();
```
