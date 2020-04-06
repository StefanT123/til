# Check if number is prime

```js
function isPrime(number) {
    // if is divisible by 2,
    // and is not 2, it's composite
    if (number % 2 === 0) {
        return number === 2;
    }

    let sqrtNumber = Math.floor(Math.sqrt(number));

    for (let i = 3; i <= sqrtNumber; i += 2) {
        if (number % i === 0) {
            return false;
        }
    }

    return true;
}
```
