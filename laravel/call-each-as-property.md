# Call "each" as a property instead of a method

If you're looping through a collection and performing a simple operation, you can call "each" as a property instead of a method.
```php
$posts = Post::all();

// This is shorter version
$posts->each->update(['active' => 1]);

// ..of this
$posts->each(function ($post) {
    $post->update(['active' => 1]);
});
```
