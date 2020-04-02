# Generators


It allows a function to pause at a particular moment, and later we have the ability to resume it

yield - like a return statement, except we can resume it from the exact same point using the exact same set of state
```js
function* numbers() {
    console.log('begin');

    yield 1;
    yield 2;
    yield 3;
}

numbers(); // we can't call it like this

let iterator = numbers();
console.log(iterator.next()); // we see the log and the first yield
console.log(iterator.next()); // {value: 2, done: false}
console.log(iterator.next()); // {value: 3, done: false}
```

```js
function* range(start, end) {
    while (start <= end) {
        yield start;

        start++;
    }
}

let iterator = range(1, 5);
console.log(iterator.next()); // {value: 1, done: false}
console.log(iterator.next()); // {value: 2, done: false}
console.log(iterator.next()); // {value: 3, done: false}
console.log(iterator.next()); // {value: 4, done: false}
console.log(iterator.next()); // {value: 5, done: false}
console.log(iterator.next()); // {value: undefined, done: true}

// for-of understands iterators
// and it will return the value instead of object
for (let i of iterator) {
    console.log(i);
}

// with SPREAD operator
console.log([...range(1, 5)]); // [1, 2, 3, 4, 5]
```
