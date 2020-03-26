# setRelation method won't run a DB query

This is usefull when we are testing.
If we have a relationship defined, and we don't want a DB query to be runned we can just call the setRelation() method.
```php
/** @test */
public function some_test_function()
{
    $user = factory(User::class)->create();
    $article = factory(Article::class)->create(['user_id' => $user->id]);

    // will run DB query
    $user->article;

    // will NOT run DB query
    $user->setRelation('article', $article);
}
```
