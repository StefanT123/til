# Clone array of objects

```js
const cards = [{cardId: 'card1'}, {cardId: 'card2'}];

// This will not work!!! It will clone the array but not
// the objects in the array. They will have the same reference
// in the two arrays!
const cloneThatDontWork = [...cards];

// Have to do this instead. This will clone the objects and
// put them in a new array
const cloneThatWorks = cards.map(element => ({...element}));
```
