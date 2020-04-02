# Sleep in async function

```js
const sleep = (ms) => (new Promise(resolve => setTimeout(resolve, ms)));
```
