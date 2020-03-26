# Cheatsheet for belongsToMany relationship methods

Mini cheatsheet to shed some light on the differences between the various belongsToMany relationship methods (save, delete, attach, detach & sync)
```php
// attach() creates the record in the pivot table.
// The model/ID passed must already exist in your database.
// Accepts a single ID, array of IDs, an Eloquent model or even a collection of models
$post->tags()->attach(Tag::all()); // Fine
$post->tags()->attach(Tag::all()->pluck('id')); // Fine
$post->tags()->attach(Tag::first()); // Fine
$post->tags()->attach(Tag::first()->id); // Fine
$post->tags()->attach(new Tag(['name' => 'A New Tag'])); // Nope

// save() will save OR create the model AND create the pivot row
$post->tags()->save(new Tag(['name' => 'A New Tag'])); // Fine

// detach() is the inverse of attach in that it will only delete the pivot
$post->tags()->detach(1);

// delete() will delete the actual tag itself on top of the pivot row
$post->tags()->delete(1);

// sync() will only attach if the pivot row does not yet exists
// Same rules as attach().
// Also accepts a second param to delete pivot rows not passed in as the first param
$post->tags()->sync([1, 2], false); // create pivot rows with tag_id 1 and tag_id 2
$post->tags()->sync([2], true); // create pivot rows with tag_id 2 and delete the rest
$post->tags()->sync(new Tag(['name' => 'A New Tag'])); // Nope
```
