# Default parameter can be a value or function

```js
function apply(cost, discount = .10) {
    return cost - (cost * discount);
}

function apply(cost, discount = defaultDiscountRate()) {
    return cost - (cost * discount);
}
```
