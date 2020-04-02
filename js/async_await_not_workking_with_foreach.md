# `async/await` not working with `forEach()`

**INSTEAD USE for...of**
`forEach()` expects a synchronous function and won’t do anything with the return value. It just calls the function and on to the next. `for...of` will actually await on the result of the execution of the function.
```js
const example = async () => {
  const nums = [1,2,3];
  nums.forEach(async num => {
   const result = await returnNum(num);
   console.log(result);
  });
  console.log('after forEach');
}

const returnNum = x => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(x);
    }, 500);
  });
}

example().then(() =>{
  console.log('done');
});
/*
    The result:
    after forEach
    done
    1
    2
    3
*/

const example = async () => {
  const nums = [1,2,3];
  for (const num of nums) {
   const result = await returnNum(num);
   console.log(result);
  }
  console.log('after forEach');
}

const returnNum = x => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(x);
    }, 500);
  });
}

example().then(() => {
  console.log('done');
})
/*
    The result:
    1
    2
    3
    after foreach
    done
*/
```
