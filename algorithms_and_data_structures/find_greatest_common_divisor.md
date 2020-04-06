# Find greatest common divisor

```js
function GCD(num1, num2) {
    if (num1 === 0) {
        return num1;
    }

    if (num2 === 0) {
        return num2;
    }

    modulo = num1 % num2;

    return GCD(num2, modulo);
}
```
