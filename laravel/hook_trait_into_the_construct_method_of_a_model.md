# Hook trait into the construct() method of a model from a trait

Laravel allows you to hook into the `__construct()` method of a model from a trait by implementing the initialize{TraitName} method.

NOTE: **YOUR TRAIT CAN’T OVERRIDE ANY VALUES ALREADY SPECIFIED ON THE MODEL**
```php
// 1. create a trai with initialize(TraitName) method
trait Membership
{
    public function initializeMembership()
    {
        // we can access instance properties

        $this->casts = array_merge([
            'membership_started_at' => 'datetime'
        ], $this->casts);
    }
}

// 2. Use the trai on your model
class User extends Eloquent
{
    use Membership;

    protected $casts = [
        'age' => 'int'
    ];
}
```
