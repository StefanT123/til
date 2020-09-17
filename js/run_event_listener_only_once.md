# Run event listener only once

Automatically remove an event listener after it has executed.
```js
el.addEventListener('click', console.log, {
    once: true
});
```
Removing event listeners, assuming they're not needed anymore, with `{once: true}` will help performance.
