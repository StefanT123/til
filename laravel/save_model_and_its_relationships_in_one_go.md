# Save model and its relationships in one go

You can save a model and its corresponding relationships using the `push()` method.
```php
class User extends Model
{
    public function phone()
    {
        return $this->hasOne('App\Phone');
    }
}
$user = User::first();
$user->name = "Peter";
$user->phone->number = '1234567890';
$user->push(); // This will update both user and phone record in DB
```
