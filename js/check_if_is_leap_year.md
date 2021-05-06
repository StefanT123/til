# Check if the year is leap year

```js
function isLeapYear(year) {
    return new Date(year, 1, 29).getDate() === 29;
}
```
