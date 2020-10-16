# goto keyword

This is one of the ways we can write recursion in PHP. Say we have a function, we want the first few lines to always be executed, and then we want to recursively execute the rest of the function. We can either extract everything but the first few lines to a new, recursive function. Or we can be lazy and use the goto feature.
```php
function installJob(): bool
{
    $job = $this->service->installInBackground();

    beginning:

    if ($job->status() === 'installed') {
        return true;
    }

    sleep(3);

    $job = $this->service->updateStatus();

    goto beginning;
}
```
Another thing we can do with this syntax is to conditionally skip parts of the code. Not sure I can think of a good real-world use case for that, but it's worth mentioning.
