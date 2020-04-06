# Scroll to element

```js
const smoothScroll = element =>
  document.querySelector(element).scrollIntoView({
    behavior: 'smooth'
  });

smoothScroll('#fooBar'); // scrolls smoothly to the element with the id fooBar
smoothScroll('.fooBar'); // scrolls smoothly to the first element with a class of fooBar
```
