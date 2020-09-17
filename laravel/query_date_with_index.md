# Query date with index

Using `whereDate()` in Laravel is easy, but because it uses the MySQL `date` function, it can't use an index for that column. If you want to use an index, use comparison (>= today, < tomorrow) or between instead. You can simplify that using a model query scope:
```php
use \Carbon\Carbon;

// Using MySQL `date()` does NOT use an index
User::whereDate('created_at', '=', Carbon::today())->get();

// Using `between` instead of `date()` does use an index
public function scopeDate($q, $column = 'created_at', $date = null)
{
    $date = $date ? Carbon::parse($date) : Carbon::today();

    $q->whereBetween($column, [
        $date->startOfDat()->toDateTimeString(),
        $date->endOfDat()->toDateTimeString()
    ]);
}

User::date('created_at', Carbon::today())->get();
```
