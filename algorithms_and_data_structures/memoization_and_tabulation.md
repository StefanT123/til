# Memoization and tabulation

Returns the memoized (cached) function.

Create an empty cache by instantiating a new Map object. Return a function which takes a single argument to be supplied to the memoized function by first checking if the function's output for that specific input value is already cached, or store and return it if not. The function keyword must be used in order to allow the memoized function to have its this context changed if necessary. Allow access to the cache by setting it as a property on the returned function.
```js
const memoize = fn => {
  const cache = new Map();
  const cached = function(val) {
    return cache.has(val) ? cache.get(val) : cache.set(val, fn.call(this, val)) && cache.get(val);
  };
  cached.cache = cache;
  return cached;
};

// See the `anagrams` snippet.
const anagramsCached = memoize(anagrams);
anagramsCached('javascript'); // takes a long time
anagramsCached('javascript'); // returns virtually instantly since it's now cached
console.log(anagramsCached.cache); // The cached anagrams map
```

TOP-DOWN APPROACH
memoization fibbonaci function:
```js
memFib(n) {
    if (mem[n] is undefined)
        if (n < 2) result = n
        else result = memFib(n-2) + memFib(n-1)
        mem[n] = result
    return mem[n]
}
```

BOTTOM-UP APPROACH ↑
tabulation fibbonaci function:
```js
tabFib(n) {
    mem[0] = 0
    mem[1] = 1
    for i = 2...n
        mem[i] = mem[i-2] + mem[i-1]
    return mem[n]
}
```

Should I use tabulation or memoization?
If the original problem requires all subproblems to be solved,
tabulation usually outperformes memoization by a constant factor.
This is because tabulation has no overhead for recursion and can use a preallocated array rather than a hash map.

If only some of the subproblems needs to be solved for the original problem to be solved,
then memoization is preferrable since the subproblems are solved lazily, i.e. precisely the computations needed are carried out.
