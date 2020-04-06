# Factorial

```js
function factorial(n) {
    // base case (must have)
    if (n === 0) {
        return 1;
    }

    return n * factorial(n - 1);
};
```
