# With statement

Did you know, JavaScript has a `with` statement block? `with` is actually a keyword in JS. The syntax to write a `with` block is as follows
```js
with (object) {
   statement
   statement
   ...
}
```

`with` adds all the properties of the `_object_` passed, in the scope chain used for evaluating the statements.
```js
const person = {
  firstname: 'Name',
  lastname: 'Last',
  age: 26,
};

with (person) {
  console.log(`${firstname} ${lastname} is ${age} years old`);
}
```
