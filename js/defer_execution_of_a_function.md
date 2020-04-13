# Defer execution of a function

This snippet delays the execution of a function until the current call stack is cleared
```js
const defer = (fn, ...args) => setTimeout(fn, 1, ...args);

defer(console.log, 'a'), console.log('b'); // logs 'b' then 'a'
```
