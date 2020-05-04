# Tagged template literals

Tagged Template literals allow you to have more control over parsing the template literals to a string, by adding a custom tag to the template literals. Tag is simply a parser function which gets array of all the strings and values interpreted by the string template. The tag function is expected to return the final string.

In following example, our custom tag — highlight, interprets the values for template literal and also wraps the interpreted values in the result string with a element, for highlighting.
```js
function highlight(strings, ...values) {
  let results = '';
  strings.forEach((str, i) => {
    result += str;
    if (values[i]) {
      result += `<mark>${values[i]}</mark>`;
    }
  });

  return result;
}

const author = 'Henry Avery';
const statement = 'I am a man of fortune & I must seek my fortune';
const quote = highligh`${author} once said, ${statement}`;
// <mark>Henry Avery</mark> once said, <mark>I am a man of fortune & I must seek my fortune</mark>
```
