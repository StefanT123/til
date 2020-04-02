# Partition an array

```js
Array.prototype.partition = function (predicate) {
    const results = [[], []];

    this.forEach((item, index) => {
        results[predicate(item, index) ? 0 : 1].push(item);
    });

    return results;
}

const [evens, odds] = [1, 2, 3, 4, 5, 6, 7, 8].partition(n => n % 2 === 0);
```
