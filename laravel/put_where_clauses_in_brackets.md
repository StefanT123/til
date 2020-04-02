# Put where clauses in brackets

If we want to find the posts where the `user_id` is 1 `AND` where year of creation is 2018 `OR` update year is 2018, so the SQL query for this would be: `SELECT * FROM 'posts' where 'user_id' = 1 AND (year('created_at') = 2018 OR year('updated_at') = 2018)` - notice the brackets after the `AND`

In eloquent we can do that by passing the callback function in the where clause
```php
Post::where('user_id', 1)
    ->where(function ($query) {
        $query->whereYear('created_at', 2018)
            ->orWhere('updated_at', 2018);
    })
    ->get();
```
