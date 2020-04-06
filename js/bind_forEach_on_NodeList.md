# Bind `forEach()` on `NodeList`

```js
if (! Object.getOwnPropertyDescriptor(NodeList.prototype, 'forEach')) {
    Object.defineProperty(NodeList.prototype, 'forEach', Object.getOwnPropertyDescriptor(Array.prototype, 'forEach'));
}
```
