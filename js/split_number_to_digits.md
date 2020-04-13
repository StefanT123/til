# Split number to digits

```js
const digitize = n => [...`${n}`].map(i => parseInt(i));

digitize(431); // [4, 3, 1]
```
