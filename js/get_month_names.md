# Get month names

```js
// instead of long, we can type narrow, short, 2-digit
Array.from({length: 12}, (x, index) => (new Date(0, index).toLocaleDateString('en-US', {month: 'long'})));
// ['January', 'February', ... , 'December']
```
