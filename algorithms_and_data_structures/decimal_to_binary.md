# Decimal to binary

```js
function decToBin(num){
    if(num >= 1){
        return decToBin(Math.floor(num/2)) + (num % 2);
    }
    // we return a string with leading 0
    // so the function will concatenate the
    // output of the function and return the
    // correct result i.e 1 = 01
    // !!!! 0 = 0, not 00!!!!
    return '0';
}
```
