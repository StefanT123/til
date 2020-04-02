# Bitwise left shift

This operator shifts the first operand the specified number of bits to the left. Excess bits shifted off to the left are discarded. Zero bits are shifted in from the right

Bitwise shifting any number x to the left by y bits yields x * 2 ** y
```js
1 << 3 // outputs 8 (basicaly it means 1 * (2^3))
10 << 6 // outputs 650 (10 * (2^6))
```
