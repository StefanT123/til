# Emulate `async/await` with generator

Using `async/await`:
```js
const getData = async () => {
  const cfg = await readConfig();
  const authDetails = extractAuthDetails(cfg);
  const token = await fetchAuthToken(authDetails);
  const data = await secureFetch(DATA_URL, token);

  return data;
};
```

Before we had async/await, we could do something like this using generators:
```js
const getData = asyncDo(function*() {
  const cfg = yield readConfig();
  const authDetails = extractAuthDetails(cfg);
  const token = yield fetchAuthToken(authDetails);
  const data = yield secureFetch(DATA_URL, token);

  return data;
});

const promiseForData = getData();

const asyncDo = (runTasks) => (...args) => {
  // We expect runTasks() to be a generator function,
  // like, for example, getData(). We first run it to
  // get a generator object.
  const generator = runTasks(...args);
  // Next, we create a recursive function that resolves
  // promises yielded by the generator function.
  const resolve = (next) => {
    // In any recursive function, we need to check to
    // see if we're done. Here we check the `done`
    // attribute returned from the generator result.
    if (next.done) return Promise.resolve(next.value);
    // We assume that `next.value` is always a promise.
    // If we haven't finished yet, then we grab the
    // value, and pass it back to the generator
    // using .next().
    return next.value.then(data => resolve(generator.next(data)));
  }

  // We kick the whole process off by calling resolve().
  return resolve(generator.next());
};
```

This is neat. But perhaps not so useful. Most of us won’t need to emulate `async/await`. But, that said, perhaps you use Babel (or similar) to make your code work with older browsers. If that’s the case, transpiler will use generators like this to make `async/await` work for you. And, because generators are so low-level, we can tinker with this yield pattern in ways we can’t with `.next()`. This allows authors to create interesting libraries that go beyond async/await.
