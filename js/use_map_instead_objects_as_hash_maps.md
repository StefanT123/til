# Use `map` instead `object` as Hash Map

`Map` is a built-in data structure that was made for exactly the purpose to be Hash Map

+ Maps can have any type of value as a key: objects, functions, or primitives
```js
const map = new Map();
const myFunction = () => console.log('I am a useful function.');
const myNumber = 666;
const myObject = {
  name: 'plainObjectValue',
  otherKey: 'otherValue'
};
map.set(myFunction, 'function as a key');
map.set(myNumber, 'number as a key');
map.set(myObject, 'object as a key');

console.log(map.get(myFunction)); // function as a key
console.log(map.get(myNumber)); // number as a key
console.log(map.get(myObject)); // object as a key
```

+ While a Map provides a size property, the size of a plain object has to be determined the hard way. Determining the size of a Map is possible in O(1) time, while it takes O(n) steps for a plain object.
```js
const map = new Map();
map.set('someKey1', 1);
map.set('someKey2', 1);
...
map.set('someKey100', 1);

console.log(map.size) // 100, Runtime: O(1)
```

+ Maps are optimized for frequent additions and removals of entries. Moreover, the number of entries of a Map can be retrieved in constant time, while the number of entries of a plain object must be counted, which takes O(n) time.

+ Objects must be iterated by getting the keys and iterating over them. On the other hand, a Map is iterable, which means it can be iterated directly.
```js
const map = new Map();
map.set('someKey1', 1);
map.set('someKey2', 2);
map.set('someKey3', 3);

for (let [key, value] of map) {
  console.log(`${key} = ${value}`);
}
// someKey1 = 1
// someKey2 = 2
// someKey3 = 3
```

+ Before ECMAScript 2015, the keys of an object are not guaranteed to be in any specific order. Iterating over a Map guarantees that the keys appear in the order of insertion.
