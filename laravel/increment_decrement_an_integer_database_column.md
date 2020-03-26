# Increment/decrement an integer database column

We can increment/decrement an integer database column in laravel by calling the increment/decrement methods directly on the model and passing through a field name.
```php
// behind the scenes it runs update model set field_name = field_name + 1
$model->increment('field_name');

// Before:
$post = Post::first();
$post->comments_count++;
$post->save();

// After:
Post::first()->increment('comments_count');

// Or
Post::first()->decrement('comments_count');

// Also accepts a second argument for how much to increment by
Post::first()->increment('comments_count', 5);
```
