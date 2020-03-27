# Normalizing

Instead of normalizing in the controller:
```php
class SubscriptionController
{
    public function update()
    {
        if (! $coupon = Coupon::havingCode($code)) {
            $code = null;
        } else {
            if (! $coupon->worksWithPlan($plan)) {
                $code = null;
            }
        }

        $this->user
             ->subscription()
             ->usingCoupon($coupon)
             ->swap($plan);
    }
}
```

We can extract a class and normalize it in there:
```php
class SubscriptionController
{
    public function update(Request $request)
    {
        $code = $request->coupon
        $plan = $request->plan;

        $coupon = Coupon::normalize($code)->against($plan);

        $this->user
             ->subscription()
             ->usingCoupon($coupon)
             ->swap($plan);
    }
}

class Coupon extends Eloquent
{
    public function normalize($code)
    {
        $coupon = static::where('code', $code)->first();

        return $coupon ?: new static;
    }

    public function against($plan)
    {
        if (! $this->worksWithPlan($plan)) {
            return false;
        }

        return $this->code;
    }

    public function worksWithPlan($plan)
    {
        //
    }
}
```
