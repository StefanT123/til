# Avoid deeply nested loops with eachSpread

Here's a trick for avoiding deeply nested loops with a little collection magic.. eachSpread'ing the result of a crossJoin
```php
// Old manual iteration method
foreach ($posts as $post) {
    foreach ($tags as $tag) {
        doSomethingWith($post)->and($tag);
    }
}

// The declarative way
$posts->crossJoin($tags)->eachSpread(function ($post, $tag) {
    doSomethingWith($post)->and($tag);
});
```
