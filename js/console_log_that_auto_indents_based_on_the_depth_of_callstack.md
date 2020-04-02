# Console.log that auto-indents based on the depth of the call stack

```js
function log(message) {
    console.log(' '.repeat(new Error().stack.match(/\n/g).length - 2) + message);
}
```
