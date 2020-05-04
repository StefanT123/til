# Comma operator

JavaScript has a comma operator. It allows us to write multiple expressions separated by comma in a single line and return the result of last expression
```js
let result = expression1, expression2,... expressionN
```

Sometimes it helps when writing multiple statements in a single line
```js
function getNextValue() {
    return counter++, console.log(counter), counter
}
```

or writing short lamda functions
```js
const getSquare = x => (console.log (x), x * x)
```
