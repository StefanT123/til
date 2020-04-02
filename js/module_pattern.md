# Module pattern (export func.)

Module pattern is a way of exposing some function or variable to the outer world. It's the same as ES6 export func. or CommonJS module.exports

It uses IIFE that returns object to expose something. If something is not returned, it won't be exposed

**EVERYTHING PUBLICLY EXPOSED CAN BE CHANGED FROM THE OUTSIDE. THIS IS ONE OF THE BIGGEST MODULE PATTERN DRAWBACKS**

Use: Formatter.makeUppercase('some text');
     Formatter.writeToDOM(document.querySelector('#el'), 'This is some text')
```js
// Mocker for testing purposes
const documentMock = (() => ({
  querySelector: (selector) => ({
    innerHTML: null,
  }),
}))();

const Formatter = (function(doc) {
  const log = (message) => console.log(`[${Date.now()}] Logger: ${message}`);

  const makeUppercase = (text) => {
    log("Making uppercase");
    return text.toUpperCase();
  };

  const writeToDOM = (selector, message) => {
    doc.querySelector(selector).innerHTML = message;
  }

  return {
    makeUppercase,
    writeToDOM,
  }
})(document || documentMock);
```
