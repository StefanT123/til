# Pivot renaming in `belongsToMany` relationship

if you dislike using `->pivot` when calling intermediate table in `belongsToMany` relationship with extra fields, you can rename it! Instead of `$user->pivot->some_field`, you can rename "pivot" to "privilege", and call it `$user->privilege->some_field`.
```php
class User extends Model
{
    [...]

    public function roles()
    {
        return $this->belongsToMany(Role::class)
            ->as('privilege')
            ->withPivot('team_leader');
    }
}

// then
$users = User::with('roles')->get();
foreach ($users as $user) {
    // instead of
    if ($user->pivot->team_leader) { /*...*/ }
    // we can do
    if ($user->privilege->team_leader) { /*...*/ }
}
```
