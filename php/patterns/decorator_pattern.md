# Decorator pattern

Stack on behaviour to an existing class dynamically
Useful when you want to preform some action somewhere, but somewhere not
Decorators exclude the need for creating different classes for doing basicaly the same thing, with only one or two functionalities more
They should all adhere to the same interface
```php
class TutorialController extends Controller
{
    public function store()
    {
        // $tutorial = new PublishesTutorial;
        $tutorial = new TweetsTutorial(new PublishesTutorial); // decorating

        $tutorial->publish();
    }
}

interface PublishesTutorial
{
    public function publish();
}

class PublishesTutorial implements PublishesTutorial
{
    public function publish()
    {
        // var_dump('saving the tutorial to the db and publishing it');
    }
}

class TweetsTutorial implements PublishesTutorial
{
    protected $tutorial;

    public function __construct(PublishesTutorial $tutorial)
    {
        $this->tutorial = $tutorial;
    }

    public function publish()
    {
        $tutorial = $this->tutorial->publish();

        // var_dump('tweet the tutorial');
    }
}
```
