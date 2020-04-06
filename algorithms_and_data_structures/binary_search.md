# Binary search

**ARRAY MUST BE SORTED**

Pseudocode:
1. Let min = 0 and max = n-1.
2. Compute guess as the average of max and min, rounded down (so that it is an integer).
3. If array[guess] equals target, then stop. You found it! Return guess.
4. If the guess was too low, that is, array[guess] < target, then set min = guess + 1.
5. Otherwise, the guess was too high. Set max = guess - 1.
6. Go back to step 2.
```js
function binarySearch(array, targetValue) {
    let min = 0;
    let max = array.length - 1;
    let guess;
    while(max >= min) {
        guess = (min + max) >> 1; // divide by 2 without reminder (floor)
        if (array[guess] === targetValue) {
            return guess;
        }

        if (array[guess] < targetValue) {
            min = guess + 1;
        } else {
            max = guess - 1;
        }
    }
    return -1;
};
```
