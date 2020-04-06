# Fibonacci

```js
// 0(N) time complexity
function fib(a, b, n) {
    if (n) {
        return fib(b, a + b, n - 1);
    }

    return a;
}

fib(0, 1, 50);
```
