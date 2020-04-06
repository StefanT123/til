# Fibonacci with math

```js
// 0(1) time complexity
function fibonacci(n) {
    return Math.round(
        (Math.pow((1 + Math.sqrt(5)) / 2, n) -
        Math.pow(-2 / (1 + Math.sqrt(5)), n)) /
        Math.sqrt(5)
    );
}

fibonacci(50);
```
