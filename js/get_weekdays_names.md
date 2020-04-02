# Get weekdays names

```js
Array.from({length: 7}, (x, index) => (new Date(0, 0, index).toLocalseDateString('en-US', {weekday: 'long'})));
// ['Sunday', 'Monday', ... , 'Saturday']
```
