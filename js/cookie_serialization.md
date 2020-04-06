# Cookie serialization

This snippet can be used to serialize a cookie name-value pair into a Set-Cookie header string.
```js
const serializeCookie = (name, val) => `${encodeURIComponent(name)}=${encodeURIComponent(val)}`;

serializeCookie('foo', 'bar'); // 'foo=bar'
```
