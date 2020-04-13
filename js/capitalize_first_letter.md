# Capitialize first letter

```js
const capitalize = ([first, ...rest]) =>
  first.toUpperCase() + rest.join('');

capitalize('fooBar'); // 'FooBar'
capitalize('fooBar', true); // 'Foobar'
```
