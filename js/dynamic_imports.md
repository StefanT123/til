# Dynamic imports

```js
const module = await import('./some-script.js');
```
```js
element.addEventListener('click', async () => {
    const module = await import('./some-script/click.js');
    module.clickEvent();
});
```
