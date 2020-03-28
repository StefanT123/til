# Calling the relationship by method vs calling it by property

When we are referencing a relationship in our model and we are calling it with property, we are going to get a full collection of related models
```php
class User extends Authenticatable
{
    // [...]

    public function follows()
    {
        return $this->belongToMany(User::class, 'follows', 'user_id', 'following_user_id');
    }

    public function timeline()
    {
        // this will create a collection of all users that our user is following
        // and the it will get their id
        $friends = $this->follows->pluck('id') ;

        return Tweet::whereIn('user_id', $friends)
            ->orWhere('user_id', $this->id)
            ->latest()
            ->get();
    }
}
```

When we are referencing a relationship in our model and we are calling it with method, we are going to get only the specified field (id), and not a full collection of users
```php
class User extends Authenticatable
{
    // [...]

    public function follows()
    {
        return $this->belongToMany(User::class, 'follows', 'user_id', 'following_user_id');
    }

    public function timeline()
    {
        // this will only get the ids of the users
        // this is much better optimized
        $friends = $this->follows()->pluck('id') ;

        return Tweet::whereIn('user_id', $friends)
            ->orWhere('user_id', $this->id)
            ->latest()
            ->get();
    }
}
```
