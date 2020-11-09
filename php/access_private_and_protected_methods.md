# Access private and protected methods

```php
namespace Tests\Support\Concerns;

use ReflectionClass;

trait InteractsWithInaccessibleMethods
{
    public function invokeInaccessibleMethod(&$object, string $method, array $params = [])
    {
        try {
            $reflectionClass = new ReflectionClass(get_class($object));
            $reflectionMethod = $reflectionClass->getMethod($method);
        } catch (\Exception $e) {
            return null;
        }

        $reflectionMethod->setAccessible(true);

        return $reflectionMethod->invokeArgs($object, $params);
    }
}
```
