# Find the length of strng in bytes

Convert a given string to a `Blob` `Object` and find its `size`
```js
const byteSize = str => new Blob([str]).size;
byteSize('😀'); // 4
byteSize('Hello World'); // 11
```
