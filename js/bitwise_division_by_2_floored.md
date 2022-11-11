# Bitwise division by 2 floored (right shift)

This operator shifts the first operand the specified number of bits to the right. Excess bits shifted off to the right are discarded. Copies of the leftmost bit are shifted in from the left. Since the new leftmost bit has the same value as the previous leftmost bit, the sign bit (the leftmost bit) does not change. Hence the name "sign-propagating".

```js
9 >> 1 // outputs 4 (when the second number is 1, it means Math.floor(9 / 2))
5 >> 1 = 2
6 >> 1 = 3
7 >> 1 = 3
```
