# Decorator pattern

Stack on behaviour to an existing class dynamically
Useful when you want to preform some action somewhere, but somewhere not
Decorators exclude the need for creating different classes for doing basicaly the same thing, with only one or two functionalities more
They should all adhere to the same interface

**WITHOUT** decorator
```php
class BasicInspection
    {
        public function getCost()
        {
            return 19;
        }
    }

    class BasicInspectionAndOilChange
    {
        public function getCost()
        {
            return 19 + 19;
        }
    }

    class BasicInspectionAndOilChangeAndTireRotation
    {
        public function getCost()
        {
            return 19 + 19 + 10;
        }
    }

    echo (new BasicInspection)->getCost();
    echo (new BasicInspectionAndOilChange)->getCost();
    echo (new BasicInspectionAndOilChangeAndTireRotation)->getCost();
```

**WITH** decorator
```php
interface CarService
{
    public function getCost();

    public function getDescription();
}

class BasicInspection implements CarService
{
    public function getCost()
    {
        return 19;
    }

    public function getDescription()
    {
        return 'Basic Inspection';
    }
}

class OilChange implements CarService
{
    protected $carService;

    public function __construct(CarService $carService)
    {
        $this->carService = $carService;
    }

    public function getCost()
    {
        return 29 + $this->carService->getCost();
    }

    public function getDescription()
    {
        return $this->carService->getDescription() . 'and oil change';
    }
}

class TireRotation implements CarService
{
    protected $carService;

    public function __construct(CarService $carService)
    {
        $this->carService = $carService;
    }

    public function getCost()
    {
        return 15 + $this->carService->getCost();
    }

    public function getDescription()
    {
        return $this->carService->getDescription() . 'and tire rotation';
    }
}

echo (new TireRotation(new OilChange(new BasicInspection())))->getCost();

$service = new OilChange(new TireRotation(new BasicInspection));
echo $service->getDescription();
```
