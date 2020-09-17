# Inline static caching (memoization)

Little inline caches for when a method is called multiple times within a request and don't want to "re-compute" that value.
```php
class Post extends Model
{
    public function commentCount()
    {
        static $cache;

        return $cache ?: $cache = $this->comment->count;
    }
}
```
